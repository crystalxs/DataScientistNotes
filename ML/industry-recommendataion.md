# Recommendation System

> A system that predict the "rating" or "preference" that a **user** would give to an **item**.

Application that involve predicting user responses t options. 

- **Netflix** offers users recommendations of movies 
- **Amazon** offers related product suggestions 
- Recommending **YouTube** videos. 
- **Google News** offers personalized news articles 
- Pandora recommends songs 
- Quora recommends stories to users 
- OKCupid recommends people to date 

**Rating Prediction**

- Predict on a 5 star system 
- Predict a probability of click

## Components

- Users (request content) 
- Items (movies, news stories) 
- Context (device, location, time) 
- Interface (phone, tablet, computer) 

### Implicit v.s. Explicit Rating

* **Implicit:** make inferences from users' behavior.
  * eg. purchase history, browsing history, search pattern.
  * No negative feedback (positive-only data).
  * No level of preference.
  * More available, easier to get.
* **Explicit:** ask users to rate items.
  * Users are unwilling to provide responses.
  * Biased by the very fact that it comes from people willing to provide ratings.

### Format

#### Utility matrix

|       | item1 | item2 | item3 | ...  |
| ----- | ----- | ----- | ----- | ---- |
| USER1 |       |       |       |      |
| USER2 |       |       |       |      |
| USER3 |       |       |       |      |
| …     |       |       |       |      |



- Degree of preference that a user has for an item. Example: 1-5 scale ratings of movies 
- Very sparse (~1%) 

#### Tabular form

| user | item | score |
| ---- | ---- | ----- |
|      |      |       |
|      |      |       |



## Classification

![The principle behind collaborative and content-based filtering](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/ML/img/recommendation.png)

### Content-based systems

> Consists in matching up the attributes of a user profile with the attributes of a content object(item), in order to recommend to the **user** new interesting items.

- Based on content as opposed to user behavior.
- Common for recommending text based products.
- Items and users are described by a set of features.

#### Ingredients

* Item representation
* User representation
* Similarity metric

### Collaborative filtering

> Systems recommend items based on **similarity measures** between users and/or items. The items recommended to a user are those preferred by similar users. 

#### Memory based method

> Memorize utility matrix.

* Application of k-NN
* Slow

##### User-based

> Computes similarities between users.

* Need to add biases: some items are highly rated, some user rate lower.
* Time effect, global bias.

$$
\hat{y}_{ik} = \bar{y}_i + \frac{1}{\sum_{a \in U_k(i)}|w_{ia}|} \sum_{a \in U_k(i)} w_{ia}(y_{ak}-\bar{y}_a)
$$

where user $i$ and item $k$:

* $\bar{y}_i$ is the mean rating by the user $i$
* $w_{ia}$ is a similarity between users $i$ and $a$
* $U_k(i)$ are the users that have rated item $k$ that I closest to user $i$

##### Item-based

> Computes similarities between items based on **rating score**.

#### Model based method

> Fits a model.

* Each user is represented by a $K$-dimensional vector (embedding).
* Each item is represented by a $K$-dimensional vector.
* Dimensions are learned by optimizing a cost and cannot be interpret.
* Such like: word2vec, decomposition of a matrix.

$$
\hat{y}_{ij} = u_{i} * v_{j} \\
\hat{Y} = UV^T
$$

Where:

* $y_{ij}$ is the rating by the user $i$ to item $j$, where $i \in 1, …, n_u$ and $j \in 1, …, n_m$
* $u_i$ is user embedding, $U$ ($n_u \times K$) is user matrix
* $v_j$ is item embedding, V ($n_m \times K$) is item matrix

##### Learn model parameters

$$
min_{u_i,v_j} \frac{1}{N} \sum_{(i,j):r_{ij}=1} (y_{ij} - u_i v_j)^2
$$

