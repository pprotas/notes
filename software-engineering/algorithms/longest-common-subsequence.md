---
id: longest-common-subsequence
aliases:
  - Longest common subsequence
tags: []
---

# Longest common subsequence

The longest common subsequence of two strings is the amount of letters that both words have in common. The longest common subsequence is useful in bioinformatics, where it is used to find similarities between two DNA sequences. For example, the strings "computer" and "boat" have the letters "o" and "t" in common in the same order, which makes their longest subsequence 2 letters long. Compare this to the [[longest-common-substring|longest common substring]], where it would only be 1 letter long due to the common substring "o". In a way, the longest common subsequence is a more lenient version of the longest common substring because it ignores the order of the letters.

The [[algorithms|algorithm]] for this problem is often implemented using [[dynamic-programming|dynamic programming]], because the problem has [[optimal-substructure|optimal substructure]] and [[overlapping-subproblems|overlapping subproblems]]. The count of the longest common subsequence is calculated by looking at the previously calculated longest common subsequence at each step, and the calculation of the longest common subsequence is repeated multiple times. This is how the algorithm works:

1. Create a table with the first string as the rows and the second string as the columns.
2. Start at the first letter of the first string that you have not processed yet.
3. For each character of the second string, check if the character matches.
   1. If yes, look at the cell diagonally above and to the left of the current cell and increment it by 1.
   2. If no, look at the cell to the left and to the top of the current cell. Pick the biggest one, this is the new value for your cell
4. Repeat from step 2 until every character of the first string is processed.
5. The maximum value in the table is the length of the longest common substring.

## Example implementation

This is how the algorithm for the longest common subsequence using dynamic programming would look like in [[python|Python]]:

```python
first = "computer"
second = "boat"

# create a table like so
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# the extra row and column are necessary to account for the situation where you compare characters at the beginning of strings
table = [[0] * (len(second) + 1) for _ in range(len(first) + 1)]

# second is the rows, which we iterate over first
for i in range(1, len(first) + 1):
    # first is the columns, which we iterate over second
    for j in range(1, len(second) + 1):
        if first[i - 1] == second[j - 1]:
            # look diagonally to topleft, and increment it by 1 if it matches
            table[i][j] = table[i - 1][j - 1] + 1
        else:
            # otherwise, pick either the cell above or the cell to the left, whichever is biggest
            table[i][j] = max(table[i - 1][j], table[i][j - 1])

# prints the resulting table like so
# [0, 0, 0, 0, 0]
# [0, 0, 0, 0, 0]
# [0, 0, 1, 1, 1]
# [0, 0, 1, 1, 1]
# [0, 0, 1, 1, 1]
# [0, 0, 1, 1, 1]
# [0, 0, 1, 1, 2]
# [0, 0, 1, 1, 2]
# [0, 0, 1, 1, 2]
for row in table:
    print(row)

# prints the last number in the table, which is the largest common subsequence
print(table[-1][-1])  # prints 2
```
