---
layout: post
title: "Counting Streaks"
date: 2017-03-22
excerpt: "A ton of text to test readability."
tags: [sample post, readability, test]
comments: true
---

```python
from itertools import groupby

def len_iter(items):
    return sum(1 for _ in items)

def longest_streak(data):
    streak = max(len_iter(run) for val, run in groupby(data) if val)
    return streak

def count_streaks(data):
    for dist_group, runs in groupby(data):
        x = sum(1 for run in runs)
        print('Group:{}'.format(dist_group),
              'Count:{}'.format(x))
```


```python
data = [(1,1),(0,1),(1,0),(1,1),(1,1),(1,1),(1,1),(1,1),(0,1),(0,1),(0,1),(1,1)]
```


```python
count_streaks(data)
print('The longest streak in the data is: {}'.format(longest_streak(data)))
```

    Group:(1, 1) Count:1
    Group:(0, 1) Count:1
    Group:(1, 0) Count:1
    Group:(1, 1) Count:5
    Group:(0, 1) Count:3
    Group:(1, 1) Count:1
    The longest streak in the data is: 5
