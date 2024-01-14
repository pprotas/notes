---
id: set-cover-problem
aliases:
  - Set cover problem
tags: []
---

# Set cover problem

The set cover problem involves finding the smallest subset of [[sets]] that together contain all elements in a universal set. In other words, it's about selecting the fewest groups from a collection where each group contains certain elements, so that all items are included at least once. It is an example of a problem that can be [[algorithms#Approximation algorithms|approximated]] by a [[algorithms#Greedy algorithms|greedy algorithm]].

That is a mouthful, so let's look at an example. Let's say that you have the following collection of sets:

| Radio station | Cities                            |
| ------------- | --------------------------------- |
| Kone          | Leeuwarden, Groningen             |
| Ktwo          | Amsterdam, Rotterdam, Utrecht     |
| Kthree        | Den Haag, Eindhoven               |
| Kfour         | Groningen, Maastricht, Leeuwarden |
| Kfive         | Amsterdam, Rotterdam              |

Each radio station is a set that contain elements from the universal set (the set with all cities). The set cover tries to find the smallest subset of sets (radio stations) that contain all elements in the universal set (cover every city at least once).

## Ideal algorithm

1. List every possible subset of sets (radio stations)
2. From these, pick the subset with the smallest set that covers all elements in the universal set (pick the subset with the smallest number of stations that cover all cities)

For each of the $n$ elements in the universal set, you have two choices: either include or exclude it in a subset.The [[big-o|complexity]] of this approach is $O(2^n)$, because there are $2^n$ possible subsets. This is a very slow algorithm.

## Approximate algorithm

There is a greedy algorithm that can approximate the solution pretty well:

1. Pick the subset that covers the most elements that have not been covered yet.
2. Repeat until all elements hav been covered.

This algorithm is $O(n^2)$ because it has to iterate over every element for every set. This is much faster than the ideal algorithm, but it does not always find the optimal solution. Despite this, it is widely used due to its simplicty and relatively good performance in many cases.

### Example implementation

Here is an example implementation of the approximate algorithm in [[python|Python]], using the radio station scenario:

```python
# the cities that still are not covered by the cover set yet
# we start off with our universal set
cities_needed = set(
    [
        "Leeuwarden",
        "Groningen",
        "Amsterdam",
        "Rotterdam",
        "Utrecht",
        "Den Haag",
        "Eindhoven",
        "Maastricht",
    ]
)

# each station is subset of the universal set
stations = {
    "kone": set(["Leeuwarden", "Groningen"]),
    "ktwo": set(["Amsterdam", "Rotterdam", "Utrecht"]),
    "kthree": set(["Den Haag", "Eindhoven"]),
    "kfour": set(["Groningen", "Maastricht", "Leeuwarden"]),
    "kfive": set(["Amsterdam", "Rotterdam"]),
}

# starts out empty, but over time we fill the cover set with stations
cover_set = set()

# while we are not covering every city
while cities_needed:
    best_station = None
    cities_covered = set()

    # get the station name and the corresponding cities
    for station, cities in stations.items():
        # check which cities that we still need are covered by this station using a set intersection
        covered = cities_needed & cities

        # if this station covers more cities than the current best_station, it becomes the new best_station
        # otherwise we just move on to the next station to see if it is better
        if len(covered) > len(cities_covered):
            best_station = station
            # the cities covered by this station, excluding the cities we already cover by other stations
            cities_covered = covered

    # we don't need to cover cities that we already cover in this iteration
    cities_needed -= cities_covered
    # since this station covers the cities we need, we add it to the cover set
    cover_set.add(best_station)

# at the end, the cover set will contain a subset of stations that cover the enitre universal set
print(cover_set)
```
