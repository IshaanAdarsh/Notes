# SORTING:
- **Bubble Sort**:
```
for each person in a line:
    for each person before him:
        if he is smaller:
            swap them
```

- **Selection Sort**:
```
for all the people in the line:
    find the smallest person
    put him after the person we choose on previous step
        (if he is the first - just put him on the most left edge)
    remove him from the consideration
```

- **Insertion Sort**:
```
take the first person and put him on the first place
for all the rest of the people:
    compare each one with the people who are already in the line
    find his place moving those who are taller to the right
```

- **Merge Sort**:
```
while the number of people in a group bigger then 1:
    divide the group in halves
    do this process to the left half of people
    do this process to the right half of people
    combine two groups of people:
        if the next person in the first group is taller:
            put him in the next place of combined group
        else:
            put there the next person from another group
```

- **Quick Sort**:
```
take the first person as a model
for each person from the left edge and from the right edge:
    if someone from the left side is taller than the model
    and if someone from the right side is smaller than the model:
    swap them
continue doing this until the left side will meet the right side
move the model to the point where the left side met the right side
repeat the process for the left and right parts from the model
do this until there will be one person in each part
```

## Time and Space Complexity:
![comparison-of-sorting-algorithms-compare1-18082c14f960abf3](https://github.com/IshaanAdarsh/TIL/assets/100434702/43f24dd7-0d92-46a0-8e2f-fe872d33abdc)
