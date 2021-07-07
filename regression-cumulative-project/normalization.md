# Normalization

Machine learning algorithms combining different data (values of an entity, e.g. engin types, manufacturer, fuel consumption) of one entity so that entities (cars) becoming comparable. However, the value of the data differs vastly, hence the impact of some values are much bigger than others.

## Example

Lets say we want to make a recommendation system for movies. In this case the entity is one movie and the data we have for one movie is: Release Year, Producing budget, Genre.

Lets say our favorite movie was made in 2005 and the used budget for the movie was 1,000,000$ and is inside the action genre. Now the algorithm needs to check which other movie is very close to this one. It is doing that by calculating the distance of nearby neighbors. However, since the scale of our axises is vastly different the impact of budget will always be bigger. 

Lets say in our database are following movies:
movie 1: produced in 1955 with a budget of 1,000,000$ 
movie 2: produced in 2005 with a budget of 1,000,050$

If we calculate the euclidean distance for these to movies to our favorite movie both will have the same distance, however in reality it makes a huge different if a movie was produced 50 years ago, but only a little difference if the budget was 50$ higher. Therefore, the data needs to be normalized. 

## Ways to normalize

The two ways to normalize datasets are either min-max-normalization or Z-Score Normalization

### Min-Max Normalization

The min-max-normalization (mmn) is one of the most common normalizations. In easy terms, the minimum of the data gets transformed to 0, while every maximum gets transformed to 1. Hence all data will be between 0 and 1. However, the significant downside is that outliers, are not handled well and they vastly influence the model (squishing).

<img src="https://www.oreilly.com/library/view/regression-analysis-with/9781788627306/assets/ffb3ac78-fd6f-4340-aa92-cde8ae0322d6.png">
Source: https://www.oreilly.com/library/view/regression-analysis-with/9781788627306/6bb0d820-6200-4bfe-aa91-e7b7ffa2a9c1.xhtml

### Z-Score Normalization

The Z-Score normalization avoids the outlier issue of the mmn.

<img src="https://miro.medium.com/max/500/1*13XKCXQc7eabfZbRzkvGvA.gif">
source: https://medium.com/@TheDataGyan/day-8-data-transformation-skewness-normalization-and-much-more-4c144d370e55

If a value is equal to the mean, it will be transformed to 0, if the value is bigger it becomes positive, and if it is smaller it become negative.

- value = mean -> 0
- value > mean -> positive
- value < mean -> negative

However, the essential downside is that not all datasets will be scaled to the exact same scale. Hence, the impact of one dataset, might be bigger over the others 


# Resources
https://www.codecademy.com/articles/normalization
https://medium.com/@TheDataGyan/day-8-data-transformation-skewness-normalization-and-much-more-4c144d370e55
https://www.oreilly.com/library/view/regression-analysis-with/9781788627306/6bb0d820-6200-4bfe-aa91-e7b7ffa2a9c1.xhtml
