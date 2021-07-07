# Normalization

Machine learning algorithms combining different data (values of an entity, e.g. engin types, manufacturer, fuel consumption) of one entity so that entities (cars) becoming comparable. However, the value of the data differs vastly, hence the impact of some values are much bigger than others.

## Example

Lets say we want to make a recommendation system for movies. In this case the entity is one movie and the data we have for one movie is: Release Year, Producing budget, Genre.

Lets say our favorite movie was made in 2005 and the used budget for the movie was 1,000,000$ and is inside the action genre. Now the algorithm needs to check which other movie is very close to this one. It is doing that by calculating the distance of nearby neighbors. However, since the scale of our axises is vastly different the impact of budget will always be bigger. 

Lets say in our database are following movies:
movie 1: produced in 1955 with a budget of 1,000,000$ 
movie 2: produced in 2005 with a budget of 1,000,050$

If we calculate the euclidean distance for these to movies to our favorite movie both will have the same distance, however in reality it makes a huge different if a movie was produced 50 years ago, but only a little difference if the budget was 50$ higher. Therefore, the data needs to be normalized. 

