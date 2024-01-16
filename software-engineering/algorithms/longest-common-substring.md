---
id: longest-common-substring
aliases:
  - Longest common substring
tags: []
---

# Longest common substring

The longest common substring problem described a situation where you want to find how similar two strings are based on the longest substring that both words have in common. As an example, the strings "fish" and "dishes" have the substring "ish" in common, which is their longest common substring with the length of 3. This is similar to the [[longest-common-subsequence|longest common subsequence]]. Solving this problem is useful in data de-duplication and plagiarism detection.

The [[algorithms|algorithm]] for this problem is often implemented using [[dynamic-programming|dynamic programming]], because the problem has [[optimal-substructure|optimal substructure]] and [[overlapping-subproblems|overlapping subproblems]]. The count of the longest common substring is calculated by looking at the previous count of the longest common substring, and the calculation of the longest common substring is repeated multiple times. This is how the algorithm works:

1. Create a table with one string as the rows and the other string as the columns.
2. Start at the first letter of the first string that you have not processed yet.
3. For each character of the second string, check if the character matches.
   1. If yes, look at the cell diagonally above and to the left of the current cell and increment it by 1.
   2. If no, set the current cell to 0.
4. Repeat from step 2 until every character of the first string is processed.
5. The maximum value in the table is the length of the longest common substring.

## Example implementation

This is how the algorithm for the longest common substring using dynamic programming would look like in [[python|Python]]:

```python
first = "fish"
second = "dishes"

# create a table like so
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# the extra row and column are necessary to account for the situation where you compare characters at the beginning of strings
table = [[0] * (len(first) + 1) for _ in range(len(second) + 1)]
for row in table:
    print(row)

# second is the rows, which we iterate over first
for i in range(1, len(second) + 1):
    # first is the columns, which we iterate over second
    for j in range(1, len(first) + 1):
        if second[i - 1] == first[j - 1]:
            # look diagonally to topleft, and increment it by 1 if it matches
            table[i][j] = table[i - 1][j - 1] + 1
        else:
            # otherwise there is no match so the current longest substring will be 0
            table[i][j] = 0

# prints the resulting table like so
# [0, 0, 0, 0, 0]
# [0, 0, 1, 0, 0]
# [0, 0, 0, 2, 0]
# [0, 0, 0, 0, 3]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 1, 0]
for row in table:
    print(row)

# print the biggest number in the table, which is the langest common substring
print(max(max(row) for row in table))  # prints 3
```
