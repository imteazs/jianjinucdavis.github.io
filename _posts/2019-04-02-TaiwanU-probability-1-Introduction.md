---
layout: post
title: Learning Note - Introduction to Probability from Taiwan University
description: "What is the core of probability"
modified: 2019-04-02
comments: true
share: true
tags: [probability, learning_note]
---

Course Link: https://www.coursera.org/learn/prob1?
This is an excellent introductory course on probability. Unfortunately it is in Chinese.

Week 1 provides a high level overview of the terminologies that we'll use later in the course. It also established the logical links among different components. 

##### Difference between probability and statistics
- Probability: known probability model, what’s the probability of an event A occurs P(A)?
- Statistics: unknown probability model, find probability distribution from experiment
P(A) = p, A - event

##### Sets - terminologies

- Set, subset, universal set, empty set, Intersection, Union, Complement, Difference
- Disjoint describes that the intersection of the two sets are empty.
- Mutually exclusive describes that any two sets among a group of sets S1, S2, …, Sn are disjoint with each other. The intersection of any two sets among a group of sets are empty.

##### DeMorgan’s Law:

- The complement of the union of A and B is the same as the complement of A intersects the complement of B
- When proving two sides are equal for sets, we need to prove that the left side and the right set both contain each other. 

##### Experiments
- An Experiment contains procedure, model, observations, and outcome
- *Sample Space*: The set of all possible outcomes
- *Event* is the description of an experiment outcome.
- *Probability* describes the chance of an experiment outcome matches a certain event. Each event is a subset of a sample space of the experiment
- Event space: It is a set of sets. Each set is a possible combination of the outcomes. If S = {o1, o2, …, on} that has n outcomes, event space = {{null}, nC1 {Oi}, nC2 {Oi, Oi + 1}, …, {o1, o2, …, on}}

__Probability is a function of events. It is a mapping from an event in an event space to a number [0, 1]. It inputs an event, and output a number between [0, 1]. Sets are important because events are sets, and probability function has the input of events.__

The core of probability is that probability is a function that returns a number for the chance of its input event happening. 


##### sets in python

Sets in python 
* are unordered;
* contains only unique items;
* maybe modified if elements contained are immutable.


Operations and methods


~~~
empty_set = set([])
my_favorite_icecreams = set(['vanilla', 'coffee', 'chocolate', 'purple yam', 'pineapple', 'rockyroad'])
sids_favorite_icecreams = set(['chocolate', 'peanut butter', 'salted caramel', 'vanilla'])
~~~


~~~
# union
all_icecreams = my_favorite_icecreams.union(sids_favorite_icecreams)
all_icecreams2 = my_favorite_icecreams | sids_favorite_icecreams
print all_icecreams
print all_icecreams2
~~~


~~~
    set(['coffee', 'rockyroad', 'salted caramel', 'pineapple', 'vanilla', 'purple yam', 'peanut butter', 'chocolate'])
    set(['coffee', 'rockyroad', 'salted caramel', 'pineapple', 'vanilla', 'purple yam', 'peanut butter', 'chocolate'])
~~~


~~~
# set membership
print 'chocolate' in my_favorite_icecreams
print 'strawberry' in sids_favorite_icecreams
~~~

    True
    False



~~~
# subset
print my_favorite_icecreams.issubset(all_icecreams)
~~~

~~~
    True
~~~


~~~
# superset
print cissuperset(my_favorite_icecreams)
print my_favorite_icecreams.issuperset(all_icecreams)
~~~

~~~
    True
    False
~~~


~~~
# intersection: both a fav of sid and me
print my_favorite_icecreams.intersection(sids_favorite_icecreams)
print my_favorite_icecreams & sids_favorite_icecreams
~~~

~~~
    set(['vanilla', 'chocolate'])
    set(['vanilla', 'chocolate'])
~~~


~~~
# difference: sid's fav but not my fav
print sids_favorite_icecreams.difference(my_favorite_icecreams)
print sids_favorite_icecreams - my_favorite_icecreams
~~~

~~~
    set(['peanut butter', 'salted caramel'])
    set(['peanut butter', 'salted caramel'])
~~~


~~~
# XOR: either sid's fav or my fav
print sids_favorite_icecreams.symmetric_difference(my_favorite_icecreams)
~~~

~~~
    set(['coffee', 'rockyroad', 'salted caramel', 'pineapple', 'purple yam', 'peanut butter'])
~~~


~~~
# disjoint
print empty_set.isdisjoint(all_icecreams)
~~~

~~~
    True
~~~



