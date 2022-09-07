# Sudoku Solver:

## Basic Working:

The working of the code works on **Backtracking** using **Recursion**. The main aim being able to fill in the empty spaces in the puzzle denoted by 0’s with values from 1-9 that fulfill the requirements to solve a sudoku. If no such value exists for a particular empty space the code backtracks to the previous position of 0 in the puzzle, resets its value back to 0 and tries other values until a result is reached. Once the last 0 is replaced by a value, the solution for that particular puzzle has been reached.

  

## Public Variables:

**solved_sudoku []**: is a list that stores the solved sudoku

**wrong_puzzle []**: stores a 9*9 list whose values are -1

  
## Functions in the code:

  

**chk_0(board)**
-

  

This function takes the sudoku puzzle as a parameter and returns the position of a ‘0’ if found. The position is returned as *row, col*. If there is not any 0’s to be found in the puzzle it will return **False**.


  

**box_chk(board, r, c, value_entered)**
-

  

This function checks if a value that is going to be entered into the puzzle along with its respective position *row, col* is valid in its 3*3 box and returns **True** if it is valid that is the same number does not exist in its square and returns **False** if it’s a duplicate number.

  

Each 3*3 box in the sudoku puzzle can be given a certain address:

**(row index position//3 , column index position//3)**

  

Example:

  

Parameters entered:

r = 5 (index position in the row)
c = 8 (index position in the column)

  

3*3 Address of value 6:

**(r//3 , c//3) = (5//3 , 8//3)**
=> **(1,2)**

  

In the sudoku puzzle this would be box number 6, as shown in the below table

  

| (0,0) | (0,1) | (0,2) |

Box:1 Box:2 Box:3

  

| (1,0) | (1,1) **| (1,2) |**

Box:4 Box:5 **Box:6**

  

| (2,0) | (2,1) | (2,2) |

Box:7 Box:8 Box:9

  

From this we can get the range of the row and column of the 3*3 box. After which we run the value through that range and check for a duplicate in the box.

  
**col_row_chk(board, r, c, value_entered)**
-

  

This function checks if a value that is going to be entered into the puzzle along with its respective position *row, col* is valid for its respective column and row. It returns **True** is both conditions for the row and the column are valid and **False** if either or both conditions is not valid.

It uses 2 different for-loops to loop through the different elements of its respective row and column.

  

**check(board)**
-

  

This function is responsible for the main working of the code.

It first checks if there are any 0’s in the puzzle using the *check_0()* function, if there are any 0’s it returns the position and assigns it to row and col respectively, else returns *True* if there are no 0’s left in the puzzle.

If there are 0’s left it runs a for loop from 1 to 9 to place values into the position. It then checks if the for-loop value, ‘v’ can be inserted into the board. To check its validity, it calls the *col_row_chk()* and *box_chk()* function and if they both return true then the value is assigned to the board.

It then calls the same function *check(board)* and checks if the puzzle is complete. If it is then it returns *True*

If after going through all the values from 1-9 and no value is valid for that position the code *backtracks* to the previous position where a ‘0’ was seen and resets its value to 0:

If there is no solution to the sudoku then it returns **False**.

  
**complete_check(board)**
-
  

This function checks if the entered puzzle is valid or not. It checks this by entering all the values of the puzzle through the *col_row_chk()* and *box_chk()* function. If both the functions return True for all the values of the puzzle and ignores all the instances of 0’s in the code, then the puzzle is valid and returns **True** else it returns **False**.

  
  
**sudoku_solver(sudoku)**
-
  

This function received the sudoku puzzle and prints the result of the puzzle. It first checks if the entered puzzle is valid by passing it through the *complete_check()* function. It then passes the puzzle through the *check()* function. If a solution is found it returns the solution through the as a numpy array called *solved_sudoku* else, it returns *wrong_puzzle*. And if the entered board is not valid it returns *wrong_puzzle*