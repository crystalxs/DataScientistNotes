# Recommendation System

> a system that predict the "rating" or "preference" that a **user** would give to an **item**.

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

Classification

**Content-based systems:** consists in matching up the attributes of a user profile with the attributes of a content object(item), in order to recommend to the user new interesting items.

**Collaborative filtering:** systems recommend items based on similarity measures between users and/or items. The items recommended to a user are those preferred by similar users. 

**The recommendation problem** 

- Users (request content) 
- Items (movies, news stories) 
- Context (device, location, time) 
- Interface (phone, tablet, computer) 

**Users v.s. Items**

Utility matrix

- Degree of preference that a user has for an item. Example: 1-5 scale ratings of movies 
- Very sparse (~1%) 

Tabular form

