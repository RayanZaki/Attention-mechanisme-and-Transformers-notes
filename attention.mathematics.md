# The Maths behind attention mechanisme:

## Similarity:

- In the [Attention Overview](./attention.mechanismes.md) , we talked about how models have "some meta information" on how words are similar, this is thanks to the **Similarity**.

- There are multiple measures for similarity

### Measure 1: Dot Product:

- The sum of the element-wise multiplication
- It measures the dot product between two words in the embedding space

### Measure 2: Cosine Similarity:

$$cos(\theta) = \frac{A.B}{\| A\|.\|B\|} $$

A: vector representing the first word

B: vector representing the second word 

$\theta$: angle between A and B 

- **Note:** if we use unit vecotors we see that they give the same result

- **Note:** The dot product is a the cosine similarity multiplied a scaler that represents the magnitude

- **Note:**  Cosine similirity is used when the magnited of the vectores are less relevant than the angle


### Measure 3: Scaled dot product:

$$scaledDotProduct(X, Y) = \frac{dot(X, Y)}{\sqrt{len(X, Y)}}$$
- Scaled dot products are used to reduce the large dot products produced by large vectors

- **This is the measure used by the attension mechanisme**


## Attention:

- To do the attention calculations, the similarity is calculated between each pair of words in a sentence

- for each pair, the similarity is then used to do a linear transformation of each word with respect to the other words using some **normalization**

## Normalization:

- Normalization means scaling down vectors to be unit vectors.

- In attention each sentence is multiplied by a normalized vector of similirities to make the transformation of a word.

$$

W_c = 
\begin{bmatrix}
x_1 \
x_2 \
\dots \
x_n 
\end{bmatrix} . \begin{bmatrix}
W_1 \\ W_2 \\ \vdots \\ W_n
\end{bmatrix}
$$

$$x_i = \frac{e^{s_i}}{\sum\limits_{j = 1}^{n}{e^{s_i}}}$$

$c$: current word index

$n$: size of a sentence

$s_i$: similarity of the $W_c$ word with respect to $W_i$

$W_i$: the vecor of the word at the $i^{th}$ position


## keys, Queries and values matrices (Q K V):

- As mentioned in the [Attention Overview](./attention.mechanismes.md), we use some **linear transformations** to create new embedding spaces from one parent embedding space.

- The Matrices $Q$, $K$ and $V$ helps us with this process

- The $Q$ aka query matrix is set to detect the low level features of a word and position it in the correct place inside of the cluster

- The $K$ aka Keys matrix is set to detect the high level features of a word and position it within the correct cluster

- The $V$ aka values matrix is set to do the final transoformation after repositioning the word into the correct place, meaning that it will optimize the search for the next word in a sentence 

### Keys and queries:

- In order to transform the embedding space, Two matrices $K$ and $Q$ are set as previously descibed.

- They work by multiplying the words by the matrices $Q$ and $K$.

- Similarity will then be calculated for the new transformed words instead of the previous ones

- the new dot product will be as follows:

$$

Dot(W_1, W_2) = W^{'}_1 . T. W^t_2
$$


$$
 T = Q .K^t
$$

with T is the transformation matrix

## Values:

- The Values matrix transforms the already trasnformed embedding by $K$ and $V$ ( we denote $E_1$)to a new embedding 

- As already mentionned it helps in creating a best embedding for finding the next word. ie, the embedding $E_1$ might only suit best for finding the best cluster to categorize the word but might not help in predicting the next word according to the context


> question:

- Why use 3 matrices for transformation instead of 1:

> Answer:

- Setting more matrices enables the model to detect more complex features while preserving the linearity of the embedded space


[Go back](./README.md)

[Overall overview of attention mechanisme](attention.mechanismes.md)

