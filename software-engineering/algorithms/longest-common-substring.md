---
id: longest-common-substring
aliases:
  - Longest common substring
tags: []
---

# Longest common substring

The longest common substring problem described a situation where you want to find how similar two strings are based on the longest substring that both words have in common. As an example, the strings "fish" and "dish" have the substring "ish" in common, which is their longest common substring with the length of 3. Solving this problem is useful in data de-duplication and plagiarism detection.

The [[algorithms|algorithm]] for this problem is often implemented using [[dynamic-programming|dynamic programming]], because the problem has [[optimal-substructure|optimal substructure]] and [[overlapping-subproblems|overlapping subproblems]]. The count of the longest common substring is calculated by looking at the previous count of the longest common substring, and the calculation of the previous count of the longest common substring is repeated multiple times. This is how the algorithm works:

1. Create a table with the first string as the rows and the second string as the columns.
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
second = "dish"

# create a table like so
# [0, 0, 0, 0]
# [0, 0, 0, 0]
# [0, 0, 0, 0]
# [0, 0, 0, 0]
table = [[0] * len(first) for _ in range(len(second))]

for i in range(len(first)):
    for j in range(len(second)):
        if first[i] == second[j]:
            table[i][j] = table[i - 1][j - 1] + 1
        else:
            table[i][j] = 0

# prints the resulting table like so
# [0, 0, 0, 0]
# [0, 1, 0, 0]
# [0, 0, 2, 0]
# [0, 0, 0, 3]
for row in table:
    print(row)

# prints the biggest number in the table, which is the longest common substring
print(max([j for sub in table for j in sub]))
```
