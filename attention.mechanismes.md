# The overview of attention mechanismes:

## Embeddings:

- They are the backbone of an LLM

- The embedings are bridges between the natural language and machine language

- Basically it means clustering the words with similar meaning in a high dimensional space

### Challenges of Embeddings:

- The embeddings can not pickup on words having different meanings 

> This is why **Attenstion** is created

## Attention:

- In order for the machine to differentiate between the meanings of a word, it has to relate it to the context the same way humans do

### Example:

_For the following examples, suppose our word space is a plane containing two clusters: [ fruits, technology ]_
#### Example 1:
> For the sentence: 
    please buy an apple and an orange.

- The word orange will help the model understand that we talk about the fruit and not the brand, so the word apple in the space of word moves closer to the fruits than to the technology area for exampl

#### Example 2:
> For the sentence: 
    apple unveiled the new phone.
- The word phone helps the model understand that we are talking about tech so it moves the word apple closer to the tech cluster

- The word orange will help the model understand that we talk about the fruit and not the brand, so the word apple in the space of word moves closer to the fruits than to the technology area for example

> A Question to ask:

**How do the model know that orange (resp. phone) is the relevant word to determine the context of the sentence and not the other works like buy (resp. unveil)?**

- This happens because words that are related to each other affect each other with higher intensity then the words that are not closely related. meaning there is some meta information that orange and apple are more related than the other words (it comes from the embedding space it self), hence even if all the words in a sentence try to pull the word **apple** towards them in the embedding space, they dont have the same effect as orange does, leading apple toward the fruits cluster.

> *The process of all words in a context pulling the new word towards them is called **Context pulls**

## Multi head attention:

- Up untill now attention mehanisms work very well,
but imagine a scenrio where the embedding space is not helpfull for the attention. ie. even after the attension happens, the model still cannot tell if the word belong to which cluster, since perhaps both cluster are near each other or the inital position of the word is in a spot where no matter what context it is at it moves towards the same direction.

> Example:

- imagine the follwing table represing a 2D embedding space:

x: denotes the word that the module confuses (apple)

C1: denotes the first cluster ( fruits )

C2: denotes the second cluster ( technology ) 

.: denotes ignored co-ordinates of the plane


| .| .| .|.|.|.|.|
|-|-|-|-|-|-|-|
|C1|.|C2|.|.|x|.|.
|.|.|.|.|.|.|.| 


or 


|C1| .| .|.|.|.|.|
|-|-|-|-|-|-|-|
|.|.|C2|.|.|.|.|.
|.|.|.|.|.|.|x| 

as you focus on the example you might notice other problems

- Therefore **Multi head attention** was invented
- Instead of using one embedding space, It creates multiple embedding spaces that keep the same clusters but spreads them in different ways to variate the possibilities and have a better understanding on how the attention is working accross all embeding spaces
- Each embedding space will have a score according how well it can differentiate between the clusters according to the specific word and context
= Next it will multply the embedding space by the score and do a wighted average of all the embeddings.

- Thaugh, the process of producing multiple embedding spaces might be costly and not easy.

- Fortunately, one easy way is to overcome that which is by using a single emedding space and modifying it to produce multiple ones using various techniques such as **Linear Transformations**.

## Linear Transformations

- linear transformations are basically matrix multiplications by specified matrices.

- They can Rotate, scale, shear or even do a compination of the latter
