# Advent of Code 2021 in Excel

## [Day 1](https://adventofcode.com/2021/day/1)
### Part 1

| Data | IsLarger | RESULT |
|------|---------:|-------:|
| 199  |          |        |
| 200  |        1 |      7 |
| 208  |        1 |        |
| 210  |        1 |        |
| 200  |        0 |        |
| 207  |        1 |        |
| 240  |        1 |        |
| 269  |        1 |        |
| 260  |        0 |        |
| 263  |        1 |        |

**Steps:**

1. check if the current value is larget then the previous value
```
IF(A1<A2, 1, 0)
```

2. sums all the TRUE values
```
SUM(B2:B2000)
```

### Part 2

| Data | WindowSum | IsLarger | RESULT |
|------|----------:|---------:|--------|
| 149  |       477 |        1 |      5 |
| 163  |       488 |        1 |        |
| 165  |       504 |        1 |        |
| 160  |       523 |        1 |        |
| 179  |       549 |        1 |        |
| 184  |       569 |        1 |        |
| 186  |       592 |        1 |        |
| 199  |       616 |        1 |        |
| 207  |       628 |        1 |        |
| 210  |       633 |        1 |        |

**Steps:**

1. safely sums the sliding window of three elements
```
IF(ISTEXT(A3), 
    "", 
    SUM(A1:A3)
)
```
The `SUM(A1:A3)` sums the sliding window of three elements
The `IF(ISTEXT(A3)` part displays empty cell in case of no input

2. do the same as *Part 1* but with empty input handeling
```
IF(ISTEXT(B3), 
    "", 
    INT(B2<B3)
)
```

3. sums all the TRUE values
```
SUM(C1:C2000)
```

## [Day 2](https://adventofcode.com/2021/day/2)
### Part 1

| Data      | Command | By |  X |  Y | LAST X | LAST Y | RESULT |
|-----------|---------|----|:--:|:--:|--------|--------|--------|
| -         | -       | 0  |  0 |  0 | 15     | 10     | 150    |
| forward 5 | forward | 5  |  5 |  0 |        |        |        |
| down 5    | down    | 5  |  5 |  5 |        |        |        |
| forward 8 | forward | 8  | 13 |  5 |        |        |        |
| up 3      | up      | 3  | 13 |  2 |        |        |        |
| down 8    | down    | 8  | 13 | 10 |        |        |        |
| forward 2 | forward | 2  | 15 | 10 |        |        |        |

**Steps:**

1. split string by space and take the first part
```
LEFT(A3, FIND(" ", A3) - 1)
```

2. split string by space and take the second part
```
RIGHT(A3, LEN(A3) - FIND(" ", A3))
```

3. increment the previous X coordinate if the command is "forward"
```
IF(B3 = "forward", D2+C3, D2)
```

4. increment the previous Y value in case of "down" and decrement in case of "up"
```
IF(B3 = "down",E2+C3,
IF(B3 = "up",  E2-C3,
               E2))
```
   
5. find the last value of X   
```
LET(X, FILTER(D:D, D:D <> ""), INDEX(X, COUNTA(X)))
```

6. find the last value of Y
```
LET(Y, FILTER(E:E, E:E <> ""), INDEX(Y, COUNTA(Y)))
```

7. get the result
```
F2 * G2
```

### Part 2

| Data      | Command | By |  X |  Y | Aim | LAST X | LAST Y | RESULT |
|-----------|---------|----|:--:|:--:|:---:|--------|--------|--------|
| -         | -       | 0  |  0 |  0 |  0  | 15     | 60     | 900    |
| forward 5 | forward | 5  |  5 |  0 |  0  |        |        |        |
| down 5    | down    | 5  |  5 |  0 |  5  |        |        |        |
| forward 8 | forward | 8  | 13 | 40 |  5  |        |        |        |
| up 3      | up      | 3  | 13 | 40 |  2  |        |        |        |
| down 8    | down    | 8  | 13 | 40 |  10 |        |        |        |
| forward 2 | forward | 2  | 15 | 60 |  10 |        |        |        |

**Steps:**

1. split string by space and take the first part with empty string handeling
```
IF(NOT(ISTEXT(A3)), 
    "", 
    LEFT(A3, FIND(" ", A3) - 1)
)
```

2. split string by space and take the second part with empty string handeling
```
IF(NOT(ISTEXT(A3)), 
    "", 
    RIGHT(A3, LEN(A3) - FIND(" ", A3)))
```

3. increment the previous X coordinate if the command is "forward"
```
IF(B3 = "", "", 
    IF(B3 = "forward", D2 + C3, D2)
)
```

4. increment the previous Y coordinate if the command is "forward" in the AIM direction
```
IF(B3 = "", "", 
    IF(B3 = "forward", E2 + C3 *  F2, E2)
)
```

5. increment the previous AIM value in case of "down" and decrement in case of "up"
```
IF(B3 = "", "", 
  IF(B3 = "down", F2 + C3,
  IF(B3 = "up",   F2 - C3,
                F2))
)
``` 

6. find the last value of X
```
LET(X, FILTER(D:D, D:D <> ""), 
    INDEX(X, COUNTA(X))
)
```

7. find the last value of Y
```
LET(Y, FILTER(E:E, E:E <> ""), 
    INDEX(Y, COUNTA(Y))
)
```

8. get the result
```
G2 * H2
```

## [Day 3](https://adventofcode.com/2021/day/3)
### Part 1

| Data  |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   | bin   |        dec |
|-------|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|---|-------|-----------:|
| 00100 |   | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |   | 10110 |         22 |
| 11110 |   | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |   | 01001 |          9 |
| 10110 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |       |            |
| 10111 |   | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |   |       | **RESULT** |
| 10101 |   | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |   |       |        198 |
| 01111 |   | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |   |       |            |
| 00111 |   | 1 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |   |       |            |
| 11100 |   | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |   |       |            |
| 10000 |   | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |   |       |            |

The columns C:O represent 13 possible bits of the input. Each number from the data column is split into bits and placed into rows 5 downwards.
The region C1:O1 represents the number with the most common bits, the thumber in C2:O2 least common bits.

**Steps:**

1. take a the nth bit of a binary number
```
INT(RIGHT(LEFT($A2#, COLUMN(A:A)), 1))
```
The `COLUMN(A:A)` indicates the "n"-th bit of the number
The `$A2#` represents a range from A2 downwards until an empty cell is reached

2. calucalte the most common nth bit 
```
LET(occurences, COUNTIF(C5#, C5#), 
    most_common, MAX(occurences), 
    INDEX(C5#, MATCH(most_common, occurences, 0))
)
```
The `COUNTIF(C5#, C5#)` calculates occurances for each number in range
  - ex. {"1", "2", "3", "1", "1"} returns {3, 1, 1, 3} 
  
3. calulcate the least common nth bit
```
LET(occurences, COUNTIF(C5#, C5#), 
    least_common, MIN(occurences), 
    INDEX(C5#, MATCH(least_common, occurences, 0))
)
```

4. join the most common bits into a value GAMMA
```
LEFT(CONCAT(C2:O2), LEN(A2))
```

5. join the least common bits into a value EPSILON
```
LEFT(CONCAT(C3:O3), LEN(A3))
```

6. convert the GAMMA value from binary to decimal
```
BIN2DEC(RIGHT(LEFT(R2, LEN(R2) - 8), 8)) * 2^8 + BIN2DEC(RIGHT(R2, 8))
```

7. convert the EPSILON value from binary to decimal
```
BIN2DEC(RIGHT(LEFT(R3, LEN(R3) - 8), 8)) * 2^8 + BIN2DEC(RIGHT(R3, 8))
```
  - note: `BIN2DEC` does not support more then 10 digits, therefore we split the value into chunks of 8 and then merge them back together


### Part 2
This part has been separated into two Worksheets containing very similar formulas
but differing in the calculation of common value according to rules
| Data  |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |  Data |   |   |        | bin   | dec | **RESULT** |
|-------|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|:-----:|:-:|---|--------|-------|-----|------------|
| 00100 | 1 | 11110 | 0 | 10110 | 1 | 10110 | 1 | 10110 | 1 | 10111 | 1 | 10111 | 1 | 10111 | 1 | 10111 | 1 | 10111 | 1 | 10111 | 1 | 10111 | 1 | 10111 | 1 |   | oxygen | 10111 | 23  | 73094      |
| 11110 |   | 10110 |   | 10111 |   | 10111 |   | 10111 |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |
| 10110 |   | 10111 |   | 10101 |   | 10101 |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |
| 10111 | 0 | 10101 | 1 | 10000 | 1 |       | 1 |       | 0 |       | 1 |       | 1 |       | 1 |       | 1 |       | 1 |       | 1 |       | 1 |       | 1 |   |        |       |     |            |
| 10101 | 1 | 11100 | 0 |       | 1 |       | 1 |       | 1 |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |
| 01111 | 1 | 10000 | 0 |       | 1 |       | 0 |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |
| 00111 | 1 | 11001 | 0 |       | 0 |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |
| 11100 | 1 |       | 1 |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |
| 10000 | 0 |       | 0 |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |       |   |   |        |       |     |            |

Each iteration is divided into the 2 columns.
The nth-bit is extracted from the Data column an placed from the 4th row downwards.
From these bits the most-common/least-common bit is calculated.
The next iteration is calculated by filtering the previous input on the nth-bit matching the calculated common bit.

**Steps:**

1. take a the nth bit of a binary number
```
INT(RIGHT(LEFT(A2#, COLUMN(A:A)), 1))
```

2. calculate the most common bit according to the rules
```
LET(occurences, TRANSPOSE(COUNTIF(B5#, {0, 1})),
    common, IF(INDEX(occurences, 1) = INDEX(occurences, 2), 
                1, 
                INT(INDEX(occurences, 1) < INDEX(occurences, 2))
    ),
    IFNA(INDEX(B5#, MATCH(common, B5#, 0)), B5)
)
```
The `TRANSPOSE(COUNTIF(B5#, {0, 1}))` counts the occurences of 0 and 1
The `IF(INDEX(...` calculates the most common value according to the rules
The `IFNA(INDEX(B5#, MATCH(common, B5#, 0)), B5)` displays the correct value from the available bits
	
3. join the most common bits into a value GAMMA
```
LEFT(CONCAT(B2,D2,F2,H2,J2,L2,N2,P2,R2,T2,V2,X2,Z2), LEN(A2))
```

4. allow conversion of binary numbers up to 16 bits
```
IF(LEN(AC2) <= 8, BIN2DEC(AC2),
                  BIN2DEC(RIGHT(LEFT(AC2, LEN(AC2) - 8), 8)) * 2^8 + BIN2DEC(RIGHT(AC2, 8))
)
``` 

5. calculate result
```
AD2 * 'Part2-CO2'!AD2
```

## Day 4
### Part1 & Part 2

|   NUMBERS   |       |   | Example    |   |       |      BOARD 1     |    |    |    |    |   |       |      BOARD 2     |    |    |    |    |
|:-----------:|-------|:-:|------------|:-:|-------|:----------------:|:--:|:--:|:--:|:--:|:-:|-------|:----------------:|:--:|:--:|:--:|:--:|
| 7,4,9,5,... |       |   |            |   |       | 22 13 17 11  0   |    |    |    |    |   |       |  3 15    0  2 22 |    |    |    |    |
|             |       |   |            |   |       |  8  2   23  4 24 |    |    |    |    |   |       |  9 18 13 17    5 |    |    |    |    |
|    SPLIT    | ALIGN |   |   RESULT   |   |       | 21  9 14 16    7 |    |    |    |    |   |       | 19  8  7   25 23 |    |    |    |    |
|      7      |       |   | 4512       |   |       |  6 10    3 18  5 |    |    |    |    |   |       | 20 11 10 24  4   |    |    |    |    |
|      4      |       |   |            |   |       |  1 12 20 15 19   |    |    |    |    |   |       | 14 21 16 12  6   |    |    |    |    |
|      9      |       |   | SUM        |   |       |                  |    |    |    |    |   |       |                  |    |    |    |    |
|      5      |       |   | 188        |   | FALSE |        22        | 13 | 17 | 11 |  0 |   | FALSE |         3        | 15 |  0 |  2 | 22 |
|      11     |       |   | NUM_CALLED |   | FALSE |         8        |  2 | 23 |  4 | 24 |   | FALSE |         9        | 18 | 13 | 17 |  5 |
|      17     |       |   |         24 |   | FALSE |        21        |  9 | 14 | 16 |  7 |   | FALSE |        19        |  8 |  7 | 25 | 23 |
|      23     |       |   | TURN       |   |       |         6        | 10 |  3 | 18 |  5 |   |       |        20        | 11 | 10 | 24 |  4 |
|      2      |       |   | 12         |   |       |         1        | 12 | 20 | 15 | 19 |   |       |        14        | 21 | 16 | 12 |  6 |
|      0      |       |   | GAME_WON   |   |       |                  |    |    |    |    |   |       |                  |    |    |    |    |
|      14     | 7     |   | 3          |   | FALSE |        22        | 13 | 17 | 11 |  0 |   | FALSE |         3        | 15 |  0 |  2 | 22 |
|      21     |       |   |            |   | FALSE |         8        |  2 | 23 |  4 | 24 |   | FALSE |         9        | 18 | 13 | 17 |  5 |
|      24     |       |   | WIN_ORDER  |   | FALSE |        21        |  9 | 14 | 16 | xx |   | FALSE |        19        |  8 | xx | 25 | 23 |
|      10     |       |   | 92         |   |       |         6        | 10 |  3 | 18 |  5 |   |       |        20        | 11 | 10 | 24 |  4 |
|      16     |       |   | 98         |   |       |         1        | 12 | 20 | 15 | 19 |   |       |        14        | 21 | 16 | 12 |  6 |
|      13     |       |   | 80         |   |       |                  |    |    |    |    |   |       |                  |    |    |    |    |
|      6	  | 4     |	  |			   |   | FALSE |        22	      | 13 | 17 | 11 |  0 |	  | FALSE |	       3         | 15 |  0 |  2 | 22 |


The sequence of called numbers is split into the first column from A5 downwards.
The sequence is then alligned in column `B` with the boards dimensions. (each number is offset by n cells from the previous one)
Each game board is placed into n-th column (plus offset).
For each game the respective regions (columns `F:K`, `M:R`, ...) handle the play logic.

First. the board is split into `G2:K12`. 
Each game iteration creates a new board that marks the chosen value as "xx".
The values on the left of the table check if the rows or columns are striked-out and the first boolean checks if either condition is true.
From these the WIN_ORDER is calculated, scanning for the value TRUE in columns `F,M,...`

The part1 chooses the MIN and the part2 chooses the MAX storing the winning board in the GAME_WON cell.
From the WIN_ORDER cell we calculate the TURN, NUM_CALLED and SUM easily giving us the RESULT.

**Steps:**

1. split the sequence of called numbers
```
TRIM(MID(SUBSTITUTE(TRIM($A$2), ",", REPT(" ", 99)), ROW(1:1) * 99 - 98, 99))
```
  - `SUBSTITUTE(TRIM($A$2), ",", REPT(" ", 99))` replaces the delieter with 99 spaces which renders only the first value in the cell.
  - `MID(..., ROW(1:1) * 99 - 98, 99)` takes the n-th element.

2. align the sequence with the table by displaying the value only each 6th cell
```
LET(index, (ROW(A1)-1)/6,
    IF(MOD(index, 1) = 0,
        INDIRECT(ADDRESS(5+INT(index)*6, COLUMN(A:A))),
        "")
)
``` 

3. safely copy the correct board into this cell
```
LET(data, $D$1, row, 4 + COLUMN(A:A) - INT(COLUMN(A:A)/7) - 1,
           board, INDIRECT(data & "!A"& row &":A"&(row+4)),
           IF(board=0, "", board))
```

4. split the board into (x,y)-th cell
```
LET(cell, INDIRECT(ADDRESS(ROW(2:2), COLUMN($G$1) + INT((COLUMN(A1) - 1) / 7) * 7)),
          IFERROR(TRIM(MID(SUBSTITUTE(SUBSTITUTE(TRIM(cell), "  ", " "), " ", REPT(" ", 999)), MOD(COLUMN(A:A), 7) * 999 - 998, 999)), ""))
```

5. copy cell from the previous iteration and strike out this cell if called out
```
IF($B14 = "", "", IF(G8:K12 = $B14, "xx", G8:K12))
```

6. calculate if won in columns
```
OR(AND(G14:G18 = "xx"), AND(H14:H18 = "xx"), AND(I14:I18 = "xx"), AND(J14:J18 = "xx"), AND(K14:K18 = "xx"))
```

7. calculate if won in rows
```
OR(AND(G14:K14 = "xx"), AND(G15:K15 = "xx"), AND(G16:K16 = "xx"), AND(G17:K17 = "xx"), AND(G18:K18 = "xx"))
```

8. calculate if the board won
```
OR(F15:F16)
```

9. for each board (row) find the soonest turn that board won
```
LET(col_index,ADDRESS(1,6+(ROW(1:1)-1)*7,4),
    col_letter, SUBSTITUTE(col_index,1,""),
    col, INDIRECT(col_letter & ":" & col_letter),
    IFNA(MATCH(TRUE,col,0), ""))
```
  - `ADDRESS(1,6+(ROW(1:1)-1)*7,4)` calulates the column of the board
  - `SUBSTITUTE(col_index,1,"")` obtains the column letter from the address (F1 -> F)
  - `INDIRECT(col_letter & ":" & col_letter)` creates a full column referece (F -> F:F)
  - `MATCH(TRUE,col,0)` returns the index of the first TRUE
  
 10. first the smallest / largest value in the WIN_ORDER
 ```
 MATCH(MIN(D17:D696), D17:D696, 0)
     -- or --
 MATCH(MAX(D17:D696), D17:D696, 0)
 ```
 
 11. calculate the finished turn
 ```
 (INDEX(D17:D696, D14) - 8) / 6
 ```
 
 12. find the last called out number
 ```
 INDIRECT(ADDRESS(INDEX(D17:D696, D14), 2))
 ```
 
 13. obtain the sum of the unstriked cells in the winning board
 ```
 LET(top_left, ADDRESS(INDEX(D17:D696, D14), 6+(D14-1)*7+1),
     winning_board, OFFSET(INDIRECT(top_left), 0, 0, 5, 5),
     SUM(IFERROR(INT(winning_board), 0)))
```
  - `OFFSET(INDIRECT(top_left), 0, 0, 5, 5)` returns the array containig the range `G8:K12`
  - `SUM(IFERROR(INT(winning_board), 0)))` convert all values to numbers and filter the errors, then sum
  
 14. calculate result
 ```
 D8*D10
 ```
 
 ## Day 5
 ### Part 1
 
| DATA       | X1 | Y1 | X2 | Y2 |   | X1 | Y1 | X2 | Y2 |   |  HORI |  VERT | VALID |   | X1 | Y1 | X2 | Y2 |   | X1 | Y1 | X2 | Y2 |   | 5 |   |   |   |   |   |   |   |   |   |   |
|------------|:--:|:--:|:--:|:--:|:-:|:--:|:--:|:--:|:--:|---|:-----:|:-----:|:-----:|:-:|:--:|:--:|:--:|:--:|:-:|:--:|:--:|:--:|:--:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0,9 -> 5,9 |  0 |  9 |  5 |  9 |   |  0 |  9 |  5 |  9 |   | FALSE | TRUE  | TRUE  |   |  2 |  1 |  2 |  2 |   |  0 |  9 |  5 |  9 |   | . | . | . | . | . | . | . | 1 | . | . | . |
| 8,0 -> 0,8 |  8 |  0 |  0 |  8 |   |  0 |  0 |  8 |  8 |   | FALSE | FALSE | FALSE |   |  7 |  0 |  7 |  4 |   |  3 |  4 |  9 |  4 |   | . | . | 1 | . | . | . | . | 1 | . | . | . |
| 9,4 -> 3,4 |  9 |  4 |  3 |  4 |   |  3 |  4 |  9 |  4 |   | FALSE | TRUE  | TRUE  |   |    |    |    |    |   |  0 |  9 |  2 |  9 |   | . | . | 1 | . | . | . | . | 1 | . | . | . |
| 2,2 -> 2,1 |  2 |  2 |  2 |  1 |   |  2 |  1 |  2 |  2 |   | TRUE  | FALSE | TRUE  |   |    |    |    |    |   |  1 |  4 |  3 |  4 |   | . | . | . | . | . | . | . | 1 | . | . | . |
| 7,0 -> 7,4 |  7 |  0 |  7 |  4 |   |  7 |  0 |  7 |  4 |   | TRUE  | FALSE | TRUE  |   |    |    |    |    |   |    |    |    |    |   | . | 1 | 1 | 2 | 1 | 1 | 1 | 2 | 1 | 1 | . |
| 6,4 -> 2,0 |  6 |  4 |  2 |  0 |   |  2 |  4 |  6 |  0 |   | FALSE | FALSE | FALSE |   |    |    |    |    |   |    |    |    |    |   | . | . | . | . | . | . | . | . | . | . | . |
| 0,9 -> 2,9 |  0 |  9 |  2 |  9 |   |  0 |  9 |  2 |  9 |   | FALSE | TRUE  | TRUE  |   |    |    |    |    |   |    |    |    |    |   | . | . | . | . | . | . | . | . | . | . | . |
| 3,4 -> 1,4 |  3 |  4 |  1 |  4 |   |  1 |  4 |  3 |  4 |   | FALSE | TRUE  | TRUE  |   |    |    |    |    |   |    |    |    |    |   | . | . | . | . | . | . | . | . | . | . | . |
| 0,0 -> 8,8 |  0 |  0 |  8 |  8 |   |  0 |  0 |  8 |  8 |   | FALSE | FALSE | FALSE |   |    |    |    |    |   |    |    |    |    |   | . | . | . | . | . | . | . | . | . | . | . |
| 5,5 -> 8,2 |  5 |  5 |  8 |  2 |   |  5 |  5 |  8 |  2 |   | FALSE | FALSE | FALSE |   |    |    |    |    |   |    |    |    |    |   | 2 | 2 | 2 | 1 | 1 | 1 | . | . | . | . | . |
|            |    |    |    |    |   |    |    |    |    |   |       |       |       |   |    |    |    |    |   |    |    |    |    |   | . | . | . | . | . | . | . | . | . | . | . |

The input us loaded into the first column and split into the following four.
The coordinates get reordered so they ascned on the X axis.
The K:L columns check if the line is a HORIZONTAL or VERTICAL line.
The columns P:S filter the data into only the HORIZONTAL lines.
The columns U:X filter the data into only the VERTICAL lines.
The area Z2:AJ12 calculates the state visually.
Z1 contains the result.

**Steps:**

1. split input into four parts
```
INT(LEFT(A2#, FIND(",",A2#) - 1))
	-- and --
LET(start, FIND(",", A2#) + 1,
           INT(MID(A2#, start, FIND(" -> ", A2#) - start)))
	-- and --
LET(start,FIND(" -> ", A2#) + 4,
           INT(RIGHT(A2#, LEN(A2#) - FIND(",", A2#, start))))
```

2. swap the input if xs are smaller or the x are equal and ys are smaller
```
xs:      IF(B2#<=D2#,B2#,D2#)
ys:      IF(B2#<>D2#,C2#, IF(C2#<=E2#,C2#,E2#))
``` 

3. check if HORIZONTAL `G2#=I2#`
4. check if VERTICAL `H2#=J2#`

5. filter the HORIZONTAL lines
```
LET(hor_index, FILTER(ROW($G$2#), $G$2#=$I$2#), 
	INDEX(G:G, hor_index))
```

6. filter the VERTICAL lines
```
LET(ver_index, FILTER(ROW($H$2#), $H$2#=$J$2#), 
	INDEX(G:G, ver_index))
```

7. calculate the intersection for each cell
```
LET(y, ROW(1:1)-1,
    x, COLUMN(A:A)-1,
    horizontal_intersects,
        LET(match,AGGREGATE(15,3,($P$2#=x)/($P$2#=x)*ROW($P$2#),ROW($P$2#)-1),
            SUM(IF(ISERROR(match), 0, LET(
                indexes, FILTER(match,ISNUMBER(match)),
                left, INDEX($Q$2#, indexes-1),
                right, INDEX($S$2#, indexes-1),
                IF(left <= y, IF(y <= right, 1, 0), 0))))),
    vertical_intersects,
        LET(match,AGGREGATE(15,3,($V$2#=y)/($V$2#=y)*ROW($V$2#),ROW($V$2#)-1),
            SUM(IF(ISERROR(match), 0, LET(
                indexes, FILTER(match,ISNUMBER(match)),
                left, INDEX($U$2#, indexes-1),
                right, INDEX($W$2#, indexes-1),
                IF(left <= x, IF(x <= right, 1, 0), 0))))),
   intersects, SUM(horizontal_intersects, vertical_intersects),
   IF(intersects=0, ".", intersects))
```
  - first calculate the cell's (x, y) coordinates
  - calculate the intersections with HORIZONTAL lines
	```
	LET(match,AGGREGATE(15,3,($P$2#=x)/($P$2#=x)*ROW($P$2#),ROW($P$2#)-1),
            SUM(IF(ISERROR(match), 0, LET(
                indexes, FILTER(match,ISNUMBER(match)),
                left, INDEX($Q$2#, indexes-1),
                right, INDEX($S$2#, indexes-1),
                IF(left <= y, IF(y <= right, 1, 0), 0))))),
	```
	  - `AGGREGATE(15,3,($P$2#=x)/($P$2#=x)*ROW($P$2#),ROW($P$2#)-1)` returns all indexes matching condition (= x)
	  - `FILTER(match,ISNUMBER(match))` returns only the indexes, without the errors
	  - `INDEX($Q$2#, indexes-1)` get the Y1
	  - `INDEX($S$2#, indexes-1)` get the Y2
	  - `IF(left <= x, IF(x <= right, 1, 0), 0)))))` return 1 if the point is intersected
	  - `SUM(IF(ISERROR(match), 0, ...` sum the matched intersects and replace erros with 0

8. do the same for VERTICAL lines

9. sum the intersections
```
SUM(horizontal_intersects, vertical_intersects)
```

10. get the result
```
LET(range, Z2:ARU635,
           values, IF(ISTEXT(range), 0, range),
           SUM(IF(values>1, 1, 0)))
```

### Part2

| DATA       | X1 | Y1 | X2 | Y2 |   | X1 | Y1 | X2 | Y2 |   |  HORI |  VERT |  LDIA |  RDIA | VALID |   |     |     |   |     |   | 12 |   |     |     |     |     |     |     |     |     |     |   |   |   |
|------------|:--:|:--:|:--:|:--:|:-:|:--:|:--:|:--:|:--:|---|:-----:|:-----:|:-----:|:-----:|:-----:|:-:|:---:|:---:|:-:|:---:|:-:|:--:|:-:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:-:|:-:|:-:|
| 0,9 -> 5,9 |  0 |  9 |  5 |  9 |   |  0 |  9 |  5 |  9 |   | TRUE  | FALSE | FALSE | FALSE | TRUE  |   | 0,9 | 0,9 | 2 | 0,9 | 2 |  2 |   | 0,9 | 1,9 | 2,9 | 3,9 | 4,9 | 5,9 |     |     |     |   |   |   |
| 8,0 -> 0,8 |  8 |  0 |  0 |  8 |   |  0 |  8 |  8 |  0 |   | FALSE | FALSE | FALSE | TRUE  | TRUE  |   | 1,9 | 1,9 | 2 | 1,9 | 2 |  2 |   | 0,8 | 1,7 | 2,6 | 3,5 | 4,4 | 5,3 | 6,2 | 7,1 | 8,0 |   |   |   |
| 9,4 -> 3,4 |  9 |  4 |  3 |  4 |   |  3 |  4 |  9 |  4 |   | TRUE  | FALSE | FALSE | FALSE | TRUE  |   | 2,9 | 2,9 | 2 | 2,9 | 2 |  2 |   | 3,4 | 4,4 | 5,4 | 6,4 | 7,4 | 8,4 | 9,4 |     |     |   |   |   |
| 2,2 -> 2,1 |  2 |  2 |  2 |  1 |   |  2 |  1 |  2 |  2 |   | FALSE | TRUE  | FALSE | FALSE | TRUE  |   | 3,9 | 3,9 | 1 | 3,9 | 1 |  3 |   | 2,1 | 2,2 |     |     |     |     |     |     |     |   |   |   |
| 7,0 -> 7,4 |  7 |  0 |  7 |  4 |   |  7 |  0 |  7 |  4 |   | FALSE | TRUE  | FALSE | FALSE | TRUE  |   | 4,9 | 4,9 | 1 | 4,9 | 1 |  2 |   | 7,0 | 7,1 | 7,2 | 7,3 | 7,4 |     |     |     |     |   |   |   |
| 6,4 -> 2,0 |  6 |  4 |  2 |  0 |   |  2 |  0 |  6 |  4 |   | FALSE | FALSE | TRUE  | FALSE | TRUE  |   | 5,9 | 5,9 | 1 | 5,9 | 1 |  2 |   | 2,0 | 3,1 | 4,2 | 5,3 | 6,4 |     |     |     |     |   |   |   |
| 0,9 -> 2,9 |  0 |  9 |  2 |  9 |   |  0 |  9 |  2 |  9 |   | TRUE  | FALSE | FALSE | FALSE | TRUE  |   |     | 0,8 | 1 | 0,8 | 1 |  2 |   | 0,9 | 1,9 | 2,9 |     |     |     |     |     |     |   |   |   |
| 3,4 -> 1,4 |  3 |  4 |  1 |  4 |   |  1 |  4 |  3 |  4 |   | TRUE  | FALSE | FALSE | FALSE | TRUE  |   |     | 1,7 | 1 | 1,7 | 1 |  3 |   | 1,4 | 2,4 | 3,4 |     |     |     |     |     |     |   |   |   |
| 0,0 -> 8,8 |  0 |  0 |  8 |  8 |   |  0 |  0 |  8 |  8 |   | FALSE | FALSE | TRUE  | FALSE | TRUE  |   |     | 2,6 | 1 | 2,6 | 1 |  2 |   | 0,0 | 1,1 | 2,2 | 3,3 | 4,4 | 5,5 | 6,6 | 7,7 | 8,8 |   |   |   |
| 5,5 -> 8,2 |  5 |  5 |  8 |  2 |   |  5 |  5 |  8 |  2 |   | FALSE | FALSE | FALSE | TRUE  | TRUE  |   |     | 3,5 | 1 | 3,5 | 1 |  2 |   | 5,5 | 6,4 | 7,3 | 8,2 |     |     |     |     |     |   |   |   |

Same as in the Part1 the input get parsed and reordered.
Now, we calculate HORIZONTAL, VERTICAL, LEFT DIAGONAL and RIGHT DIAGONAL.
For each line we generate all its points from the column Y onwards.
Then we flatten the 2D array into the column R.
We remove the whitespace in the column S.
Then we calculate the occurances for each point.
The columns U:V contain only unique points.
Lastly we filter the values with more then one intersect and calculate the result.

**Steps:**

1. - 4. same as Step1
5. check if LEFT DIAGONAL `(I2# - G2#) = (J2# - H2#)`
6. check if RIGHT DIAGONAL `(I2# - G2#) = -(J2# - H2#)`
7. generate points for each line
```
IF(L2=TRUE,TRANSPOSE((G2+SEQUENCE(I2-G2+1)-1)&","&H2),
IF(M2=TRUE,TRANSPOSE(G2&","&(H2+SEQUENCE(J2-H2+1)-1)),
IF(N2=TRUE,TRANSPOSE((G2+SEQUENCE(I2-G2+1)-1)&","&(H2+SEQUENCE(J2-H2+1)-1)),
IF(O2=TRUE,TRANSPOSE((G2+SEQUENCE(I2-G2+1)-1)&","&(H2+(-1)*SEQUENCE(H2-J2+1)+1)),
""
))))
```

8. flatten the 2D array into a 1D array
```
LET(range, $Y$2:$AR$19,
    value, LET(columns,COLUMNS(range),
               row_, ROUNDUP(ROW(A1)/columns, 0),
			   col_, MOD(ROW(A1)-1, columns)+1,
			   INDEX(range, row_, col_)),
    IF(ISERROR(value), "", IF(value=0, "", value)))
```
  - `ROUNDUP(ROW(A1)/columns, 0)` divide the index by the number of columns, making the inceremnt every n times.
  - `MOD(ROW(A1)-1, columns)+1` roll over the counter when reaching the end of a column
  

9. remove whitespace from the 1D array
```
FILTER(R2:R1048576, R2:R1048576<>"")
```

10. count the occurences
```
COUNTIF(S2#, S2#)
```

11. filter the unique values
```
UNIQUE(S2:T54, 0)
```

12. filter the points with more then 2 intersections
```
LET(cols,INDEX(U2#, 0, 2),
    FILTER(cols, cols>1))
```

13. calculate the result
```
COUNT(W2#)
```