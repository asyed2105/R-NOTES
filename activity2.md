### Vector operations in R
- can create vectors to store simulated values
- need to initalize first

```
x <- vector("numeric, lenght=10)
```
can initialize empty vectors too:
```
x <- NULL
```
can assign elements as follows:
```
x[1] <- 2 # assignment
x[1] # will display
```

### While loops in R
- syntax

```
while(condition){
  do statements
}
```

#### Examples
- Define a variable i and assign a value of 0 to it.
- Using a while loop, print the value of i then increase the value of i by 1 as long as i is less than 6.

```
i <- 0 # initialise
while (i < 6) {
  print(i)
  i <- i + 1 # increase
}
```

### For loops in R
- for loop used for iterating over a sequence
```
for(variable in sequence) {
  do statements
}
```

#### Example
- Create a vector called w consisting of a sequence of integers from 10 to 15.
- Using a for loop, iterate over the elements of the vector and print each element of the vector.

```
w <- 10:15 # consisting from int 10 to 15
len<-lenght(w) # are 6 elements in w
for (i in 1:len){
  print(w[i])
}
```

### Estimating event probabilites through simulation 
- Consider the probability of getting three heads in three fair coin tosses through simulation.
- We define the random experiment as consisting of three coin tosses (a repetition).
- The event is three heads.
<br>
  1. simulating one repetition of the experiment (i.e. tossing three coins): <br>
```
rep <- sample(c("Head","Tail"), size = 3, replace = TRUE)
```
  2. determining whether the event of interest occured (i.e. did we get three heads)? <br>
```
# The line below returns a 1 if the number of heads in each repetition is equal to 3
success <- if (sum(rep == "Head")==3) { 1 }  else { 0 }
```
  3. Repeating (i)-(ii) N times where N is the number of repetitions of the experiment. We store the simulated results in a vector. To do so, we will use a for loop.
```
N <- 500 # number of trials
sim <- NULL # Initialise a vector to store the result of each repetition

for(i in 1:N){ # Iterate over the # of repetition
  # Simulate a repetition of the random experiment
  rep <- sample(c("Head","Tail"), size = 3, replace = TRUE) 
  # Determine whether event of interest occurred
  success <- if (sum(rep == "Head")==3) { 1 }  else { 0 } 
  # Store result in a vector
  sim[i] <- success
}


```

### Code for simulating coin tossing 3 times
```
# SOLUTION
N <- 1000 # Set-up the number of repetitions
sim <- NULL # Initialise a vector to store the result of each repetition

for(i in 1:N){
  rep <- sample(c("Head","Tail"), size = 3, replace = TRUE)
  success <- if (sum(rep == "Tail")>=1) { 1 } else { 0 }
  sim[i] <- success
}

# Estimate probability of at least one Tail
mean(sim)
```
#### Justification for sum(rep == "Tail"):
rep == "Tail":

This comparison creates a logical vector where each element of rep (which stores the outcome of a coin flip) is compared to "Tail".
If the outcome is "Tail", the corresponding element in the logical vector is TRUE; otherwise, it is FALSE.
For example, if rep is c("Head", "Tail", "Tail"), then rep == "Tail" would return c(FALSE, TRUE, TRUE).
sum():

In R, logical TRUE values are treated as 1 and FALSE as 0 in numeric operations.
When you apply sum() to a logical vector, it counts the number of TRUE values (i.e., the number of times "Tail" appeared).
For example, sum(c(FALSE, TRUE, TRUE)) would return 2, because there are two TRUE values, indicating that two "Tails" appeared in the result.

### Conditionasl probabilities 
- Example
- Two dice are rolled. What is the probability that the first die is a 3 given that the product of the two dice is 12?
- Here we will simulate two dice rolls but only consider repetitions in which the product is 12.
- Hence we use a while loop to make sure that the number of repetitions in which the product of the dice is 12 (i.e. the number of repetitions that meet the condition) is equal to N

```
sim <- NULL # Initialise vector to store results
N <- 10000 # Number of repetitions
counter <- 0 # Here we keep a track of the number of repetitions where the product of the dice is 12

while(counter <= N){
  roll1 <- sample(c(1,2,3,4,5,6), size = 1) 
  roll2 <- sample(c(1,2,3,4,5,6), size = 1)
  # Below we verify if the product of the dice is 12
  if (roll1*roll2 == 12){
    # If it is equal to 12, we increase the counter by 1
    counter <- counter + 1
    if(roll1==3){
      # Then we record that the event of interest occurred
      success <- 1
    }else{
      success <- 0
    }
    sim[counter] <- success
  }
}

mean(sim) # relative frequency of first die being 3 in all repetitions where the product of the two dice was 12

```

#### Another Example
- Consider a bag which contains 2 <br>
 red balls and 2 <br>
 blue balls. We randomly draw 2 <br>
 balls without replacement from the bag (i.e. we do not place the ball back in the bag after drawing it). <br>

Let’s estimate the probability of drawing 2 <br>
 red balls if the first ball drawn is red using simulation (i.e., P(B|A) <br>
 where event A <br>
 = the first ball drawn is red, and event B <br>
 = both balls drawn are red)? <br>

```
ball <- c("red", "red",  "blue", "blue") 

sim <- NULL # Initialise vector to store simulated results
N <- 10000 # Number of repetitions of the experiment
counter <- 0 # Here we keep a track of the number of repetitions in which the first draw is a red ball 

while(counter <= N){
  # For each repetition we randomly draw two balls
  draw <- sample(ball, size = 2, replace = FALSE) 
  if (draw[1] == "red"){ # If the condition is met, we increase the counter by 1
    counter <- counter + 1 
    if(draw[2]=="red"){ # If the condition is met and the second ball is a red ball, then the event of interest occurred
      success <- 1
    } else {
      success <- 0
    }
    sim[counter] <- success
  }
}

mean(sim)
```
