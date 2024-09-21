### Arithmetric operations

All possible
```
1+1
5-4
2*(1+3)
1/4^2
```

eg. Represent the following in R -> (6 x 130 + 21)^3 / 9
```
(6*130+21)**3 / 9
```

### Commenting
- we can add # in front of the text to comment it out, so R does not consider as part of the code and will ignore it when the code is run.
- syntax same as python
```
# commenting
```

### Functions
- Functions allow you to automate routine and repetitive tasks in a more efficient way than doing the task manually.
    - The syntax to run an R function is function(argument1, argument2, etc.).
    - eg. suppose a sequence of values are stored in an R object (a vector) called y: (67.25, 65.78, 70.14, 64.36, 66.67, 70.54).
    - Let’s consider the steps to store these values in a vector, and then round them to 1 decimal place.
        - We can name and define y in R.
        - Note that the _**<-**_ syntax assigns whatever value(s) are given on the **right-hand-side** to the R object given on the left-hand-side.
        - The _**function c()** _ is used to **combine value**s listed as its arguments.
        - we can use the code **_head(y,n=3)_** to display the first few elements.
        - Once the appropriate values are stored in y, we can use the function round() to round each of the values in y to specified number of decimal places.
            - The round() function expects two arguments, or inputs: the value(s) you wish to round, and the number of decimal places to which you wish to round.

eg. converting values from in to centimeter
```
y<-c(67.25, 65.78, 70.14, 64.36, 66.67, 70.54) 
y_cm<-y*2.54
round(y_cm,1) # rounding to 1 decimal place
head(y_cm,n=3) # im saying from the variable y_cm i want only 3 items returned
# if i wanted ALL items returned i could just write y_cm
```

### sample() function
-  can sample values at random in R using the sample() function.
-  The sample() function needs at least two arguments:
    - x which is the vector from which the sample will be taken
    - size = the sample size
```
sample(x=1:1200,size=10)

>>>  1016  360 1004  554  931   41  288  989  636  586
```
- By default, sampling is done without replacement (i.e., it is impossible to sample the same individual more than once)
    - all individuals represented in the R object x have the same chance of being selected
        - settings can be changed IF NEEDED
     
with**OUT** replacement
```
outcomes<-c("Head","Tail")

sample(outcomes,1) # simulates flipping a fair coin once
```
**WITH** replacenent

```
outcomes<-c("Head","Tail")

sample(outcomes,4,replace = TRUE) # simulates flipping a fair coin once
```
- you NEED to add replace = TRUE to sample() to allow values to be repeated

### Summarizing Repetition
-  can compute the relative frequency of a particular outcome or event or proportion of repetitions that outcome or event occurred
-  If we have the results of repetitions of an random experiment stored in a vector called **reps**
    - we can use the function sum() to count the number of times an outcome or event occurred, and **sum()/length()* *to compute the_ relative frequency of repetitions _in which the outcome or event occurred.
        - OR we can just use mean()
            -  would calculate the proportion of 1's in your 100 simulated dice rolls?
                - mean(rolls==1)

```
# save possible outcomes in an R vector (called "outcomes" here):
outcomes<-c("Head","Tail")

# simulate flipping fair coin 1000 times & saving results in vector called 'results'
results<-sample(outcomes,1000, replaconsider rolling a weighted six-sided die; one with sides still marked as 1, 2, 3, 4, 5, and 6, but one where the probability of rolling a 1 is 0.4, and all the other sides are equally likely. The following code simulates rolling this weighted six-sided die 5000 times and computing the relative frequencies of rolling a 2 based on the simulated results.ce=TRUE) 

# Display first 10 elements of vector of TRUEs and FALSEs that compares each result to heads
head(results=="Head",n=10)

# use sum function to count number of heads in 1000 simulated repetitions
sum(results=="Head") # results == "Head" is used to COMPARE values

# use mean function to compute relative frequency of heads in 1000 simulated repetitions
mean(results=="Head")
```

### Simulating more complex random experiments
- consider rolling a weighted six-sided die; one with sides still marked as 1, 2, 3, 4, 5, and 6, but one where the probability of rolling a 1 is 0.4, and all the other sides are equally likely.
- The following code simulates rolling this weighted six-sided die 5000 times and computing the relative frequencies of rolling a 2 based on the simulated results.
```
rolls<-sample(1:6,5000, prob=c(0.4,0.12,0.12,0.12,0.12,0.12),replace=TRUE)
mean(rolls==2)
```

- What if we were interested in event A=roll an even number
- To find the proportion of even numbers in the 5000 rolls, we could modify the logical expression in the above code to rolls==2|rolls==4|rolls==6.
- The | specifies **or** so this logical expression will be TRUE (or 1) if the result is an even number, and FALSE (or 0) otherwise. Give it a try.

- eg.
```
outcomes<-c('Head',"Tails","edge")

#prob
p_edgey<-0.00001
p_heady<-(1-0.00001)/2
p_taily<-p_heady

flips<-sample(outcomes,1000000,prob=c(p_taily,p_heady,p_heady),replace=TRUE)
sum(flips=="edge")
```

### Counting in R

- built in math functions in R

```
factorial(5) # factorials 
choose(5,2) # combination (Binomial Coefficient)
```

eg
```
#A SOLUTION
# (a)
# Number of possible rearrangements
factorial(6)
# Simulation of one repetition 
letters<-c("R", "A", "N", "D", "O", "M")
sample(letters, 6)

# (b)
# Number of possible rearrangements
6^6
# Simulation of one repetition 
sample(letters, 6, replace=TRUE)


# (c)
# Number of possible rearrangements
factorial(6)/factorial(3)
# could also use combination
choose(6,3)*factorial(3)
# Simulation of one repetition 
sample(letters, 3, replace=FALSE)
```
  




