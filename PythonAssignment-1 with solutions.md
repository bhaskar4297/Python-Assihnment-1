## Assignment Part-1
Q1. Why do we call Python as a general purpose and high-level programming language?
Ans because here we are writing everithing in human readable form.

Q2. Why is Python called a dynamically typed language?
Ans.It is dynamically typed language because we dont have to assign type of data(value) while writing the code. it is determined by compiler at time of excecution.

Q3. List some pros and cons of Python programming language?
Ans. Pros                                           cons :
     1. flexible                                    1.slower than other languages
     2. huge library                                2. Runtime errors
     3. connectivity with internet                  3. large memory consumption

Q4. In what all domains can we use Python?
Ans In todays time it is highly used and recoganised language in the world. As it is easy and convenient as compare to others
    Eg: Data science, AI, Machine learning, application development, game development, embedded systems

Q5. What are variable and how can we declare them?
Ans : variable are name assign to specific memory location. There is no such command to declare it.It is created by simply assigning the value to it.

Q6. How can we take an input from the user in Python?
ans : By using input() function

Q7. What is the default datatype of the value that has been taken as an input using input() function?
Ans : by default, input() fn returns string

Q8. What is type casting?
Ans: type casting is nothing but a conversion of variable from one type to another
eg: suppose we have to convert int() type to float() then,
    int_var = 5
    casted_int_var = float(int_var)
    print(casted_int_var) # o/p: 5.0


Q9. Can we take more than one input from the user using single input() function? If yes, how? If no, why?
Ans As far as i have studied i don't know. There might be some functions because python is vast.

Q10. What are keywords?
Ans: keywords are reserved words which is predefined in python. we cannot use it as a variable name.

Q11. Can we use keywords as a variable? Support your answer with reason.
Ans: No, because keywords have predefines meaning.

Q12. What is indentation? What's the use of indentaion in Python?
Ans: It is a spaces before any code. It is used in program to make it look good

Q13. How can we throw some output in Python?
Ans: by print() function

Q14. What are operators in Python?
And: Operators are special symbols which perform some arithmetic or logical operations
    Eg: Addition, substraction, comparision etc

Q15. What is difference between / and // operators?
And: / - it is used for float division operations
     // - it is used foe integer division operations

Q16. Write a code that gives following as an output.
```
iNeuroniNeuroniNeuroniNeuron
```
Ans: print("ineuron"*4)

Q17. Write a code to take a number as an input from the user and check if the number is odd or even.
Ans:
a = int(input("enter a no :"))
if (a % 2) == 0:
    print("it is even no")
else:
     print("it is odd no")

Q18. What are boolean operator?
Ans: which perform boolean operations
eg : true and false

Q19. What will the output of the following?
```
Ans:  1 or 0 ------ True
      0 and 0 ----- False
      True and False and True----false
      1 or 0 or 0-----True
```

Q20. What are conditional statements in Python?
Ans : it is used when condition is given in statement whether the first statement is true or not if it is false then it will go for else

Q21. What is use of 'if', 'elif' and 'else' keywords?
And: IF---It allows conditional excecution
     elif--if the previous conditions is not true, then elif condition is used.
     else---it is not mendatory to use this block but this is used at the end if all conditions are false to declare result,

Q22. Write a code to take the age of person as an input and if age >= 18 display "I can vote". If age is < 18 display "I can't vote".
Ans : 
age = int(input("enter your age:"))
if age>=18:
     print("i can vote")
else:
     print("i cannot vote")
    
Q23. Write a code that displays the sum of all the even numbers from the given list.
```
numbers = [12, 75, 150, 180, 145, 525, 50]
```
Ans i dont know

Q24. Write a code to take 3 numbers as an input from the user and display the greatest no as output.
Ans:
num1 = int(input("enter first num: "))
num2 = int(input("enter second num: "))
num3 = int(input("enter third num: "))

if (num1 >= num2) and (num1 >= num3) :
     greatest = num1
elif (num2 >= num1) and (num2 >= num3) :
     greatest = num2
else:
    greatest = num3

print("The greatest number is", greatest)

Q25. Write a program to display only those numbers from a list that satisfy the following conditions

- The number must be divisible by five

- If the number is greater than 150, then skip it and move to the next number

- If the number is greater than 500, then stop the loop
```
numbers = [12, 75, 150, 180, 145, 525, 50]
```
Ans : i dont know
