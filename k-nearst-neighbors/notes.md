# K-nearest neighbors

Can be implemented as an algorithm, which will classify data points, so that they can be grouped together. 

In essence the algorithm needs to calculate the distance to all surrounding points and then see if the point rather belongs to class n or n+y, different distance formulas can be used, like the Euclidean Distance, Manhattan Distance and Hamming Distance. The most common used distance is the Euclidean Distance, which is the root of the sum of square differences.ö

<img src="../../pictures/Euclidean.PNG">

The three steps of the k algo

1. Normalize the data (more info can be found <a href="../normalization.md">here</a>)
2. Find the k nearest neighbors
3. Classify the new point based on those neighbors

## Step 1 normalize the data

it is important that all data points have the same impact on the model. Hence the data need to normalized, which means all values are brought to a number between 0 and 1. See the following python implementation. (more info can be found <a href="../normalization.md">here</a>)

```python
def min_max_normalize(lst):
  minimum = min(lst)
  maximum = max(lst)
  normalized = [(lst[i]-minimum)/(maximum-minimum) for i in range(len(lst))]
  return normalized
```

## Step 2 k-nearest Neighbors

to find the nearest neighbors the euclidean distance is calculated, see following equation:

<img src="https://www.tutorialexample.com/wp-content/uploads/2020/05/Euclidean-distance-in-tensorflow.png">
source: https://www.tutorialexample.com/calculate-euclidean-distance-in-tensorflow-a-step-guide-tensorflow-tutorial/

in code with multiple dimensions: 

```python
def distance(movie1, movie2):
  return (sum([(movie1[i]-movie2[i])**2 for i in range(len(movie1))]))**0.5
```

1. Calculate the nearest distance
2. sort them naturally from 0 to 1 e.g. in python `.sort()`
3. return th k-nearest neighbors

```python
def classify(unknown, dataset, k):
  distances = []
  for title in dataset:
    distance_to_point = distance(dataset[title], unknown)
    distances.append([distance_to_point, title])
    distances.sort()
  return distances[0:k]
```

### Step 3 classify the neighbors

For classifying the data  

```python
def classify(unknown, dataset, labels, k):
  distances = []
  #Looping through all points in the dataset
  for title in dataset:
    movie = dataset[title]
    distance_to_point = distance(movie, unknown)
    #Adding the distance and point associated with that distance
    distances.append([distance_to_point, title])
  distances.sort()
  #Taking only the k closest points
  neighbors = distances[0:k]
  num_good = 0
  num_bad = 0
  for neighbor in neighbors:
    title = neighbor[1]
    if labels[title] == 0:
      num_bad += 1
    elif labels[title] == 1:
      num_good += 1
  if num_good > num_bad:
    return 1
  else:
    return 0
```

sklearn implementation:

```python
from sklearn.neighbors import KNeighborsClassifier

classifier = KNeighborsClassifier(n_neighbors = 5)

classifier.fit(dataset, labels)

unknown_points = [
  [.45, .2, .5],
  [.25, .8, .9],
  [.1, .1, .9]
]

guesses = classifier.predict(unknown_points)
print(guesses)
```

### Optional Step 4 assert the classifier and alter the k value. 

Therefore data will need to be splitted in training and test set

```python
def find_validation_accuracy(training_set, training_labels, validation_set, validation_labels, k):
  num_correct = 0.0
  for movie in validation_set:
    guess = classify(validation_set[movie], training_set, training_labels, k)
    if guess == validation_labels[movie]:
      num_correct += 1
  return num_correct/len(validation_set)


print(find_validation_accuracy(training_set, training_labels, validation_set, validation_labels, 3))
```