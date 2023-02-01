## Markdown Language
  
- Way of writing HTML content without having to deal with HTML code
- At the top of the page you'll notice a header section
  - this header section is defined by two sets of three dashes 
  - contains 
    - the title of our markdown report
    - the output format of our markdown report
- In the body of the document headers can be specified by adding hastags before the text
- Lists can be specified by adding a dash or asterisk before the text
- for more information on markdown formatting visit:
  https://www.markdownguide.org/basic-syntax/
- While we will be working with an R markdown document today you can also run code in an R script. To open an R script you can go to File > New File > R Script. 

NOTE: R scripts will end in ".R", while R markdowns will end in ".Rmd"

## Code chunks
  
- code chunks can be included in our markdown document with two sets of three tick marks
- you'll notice in the brackets we add in, `r`, which indicates we are running R code

Let's start with R by defining what is called a variable. We can run this chunk of code by clicking the play button in the corner of the code chunk:
  
```{r}
num <- 18
num
```

!!! info "output"

    ```
    [1] 18
    ```

What did we do:
  
  - assigned the value 18 to the word "num" 
  - assign value with  the "<-" operator
  - call the value of this variable with the word "num" 
  - NOTE: our variable appears in the environment window to the right.
  - NOTE: when we ran the code chunk our console window shrank! This is because our output is appearing below the code chunk. We can always reopen it by clicking on it!
  
## Variable Names

- variable names are case sensitive
- they can include any combination of:
  - lower-case letters
  - upper-case letters
  - underscores/periods/numbers (however, these cannot be the first character)
  
```{r}
second.number.2 <- 2
third_number_3 <- 3
fourthNumber4 <- 4
```

Whate did we do:

- we assigned three numbers 2,3,4 to the variables second.number.2, third_number_3,fourthNumber4
- all are valid variable names
- keep you variable names as short as possible to still convey what they represent
- just be consistent with your naming convention

## Variable Properties

- When we define variables we can treat that variable name as the value itself
- We can also add variable names together
- We can assign more than one value to a variable name

Let's try this out in code!

```{r}
# add 5 to num
num <- num + 5
num

# assign 20 to new num and add it to num
new_num <- 20
new_num + num

#create a variable with multiple values
combined <- c(3,4,6)
combined
```

!!! info "output"

    ```
    [1] 23
    
    [1] 43
    
    [1] 3 4 6
    ```

What did we do:

- First we added 5 to the variable `num`
- We assigned that num + 5 back to the variable `num` which overwrote the original value of 18! (now it's 23)
- we assigned a new variable `new_num` to the value 20 and then showed we can add the values of `new_num` and `num` together with just their names
- we then assigned multiple values to the variable `combined` by separating values by commas and enclosing them in `c()`
- this variable with multiple values is called a vector!


- You'll also note we add text inside our code block by putting a hashtag in front of it. This is called a comment and they are very useful in giving your code context. 
