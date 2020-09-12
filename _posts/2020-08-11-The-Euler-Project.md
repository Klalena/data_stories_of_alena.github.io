---
layout: post
title: The Euler Project
subtitle: Problems 4, 35, and 112
thumbnail-img: /assets/img/code.jpg
tags: [Project Euler]
---
<figure>
  <img style="float:left; margin-right: 20px;" src="/assets/img/euler_img.jpg" > 
  <figcaption>"Leonhard Euler" by John Baichtal is licensed under CC BY-NC-SA 2.0.</figcaption>
</figure>


{% include image.html file="image-name.jpg" description="This is an image." %}
In this post, I will explain how I solved three problems from [Project Euler](https://projecteuler.net/) using Python. Project Euler is a website that publishes computational problems, which often solved with computer programs.  The three problems I chose have a different level of difficulty as listed below: 

1. Problem 4: *Largest palindrome product* (Solved by < 500,000 people)
2. Problem 35: *Circular primes* ( Solved by < 100,000 people)
3. Problem 112: *Bouncy numbers*  (Solved by < 25,000 people)

# #4: Largest palindrome product

*A palindrome* is the number/word/phrase that can be read the same backward as forward. For example, 303  and 7557 are  palindromes. 

**Question**: Find the largest palindrome made from the product of two 3-digit numbers. 

###  Approach 

First, I created a function to check whether the number is palindrome or not. The function takes a  number and checks whether it is equivalent to the reversed number, in which case the function returns `True`  and `False`  otherwise. 

```python
def IsPalindrome(number):
    """
    The function checks whether the number is palindrome or not. 
    Input: 3-digit number
    Output: Boolean -- True when the number is palindrome. 
    """
    palindrome = True 
    number = str(number)
    if number != number[:: -1]: 
        palindrome = False 
    return palindrome
```

Next, I used nested for loop to get a product of two 3-digit numbers and checked whether it is a palindrome. If the product is a palindrome, it is added to the list of palindromes,  and the largest palindrome is printed. 

```python
import numpy as np 
def main():
    """
    Prints out the largest palindrome made from the product of two 3-digit numbers. 
    """ 
  	ls = np.arange(100, 1000, 1)
    palindromes = []
    for i in ls: 
        for j in ls:
            product = i*j
            if IsPalindrome(product):
                palindromes.append(product)

    print(f'The largest palindrome made from the product of two 3-digit numbers is {max(palindromes):,}.')
    
```

**Solution**: `The largest palindrome made from the product of two 3-digit numbers is 906,609.`

#  #35: Circular primes

*A circular prime* is a prime number for which the rotations of its digits are also prime numbers. For example, 199 is a circular number because 919 and 991 are also prime numbers. 

**Question**: How many circular primes are there below one million?

### Approach 

I started by creating a function to check whether the number is circular. This function takes a number and checks whether all its rotations are also prime numbers, in which case it returns  `True` and `False` otherwise. I used `sympy.isprime()` method (from`sympy` module) to check if the number is a prime  and list-like container `deque` ( `collections` library) to rotate the number. 

```python
import sympy
from collections import deque

def IsCircular(prime): 
    """
    The function checks whether the number is circular prime,
    which is a prime number where all the rotations of its digits
    are also prime numbers.

    Input: prime number
    Output: Boolean, where True means that the number is circular 
    """
    circular = True 
    prime = list(str(prime))
    d = deque()
    [d.append(x) for x in prime]
    for i in range(1, len(prime)):
        d.rotate(1)
        rotated_prime = int("".join(list(d)))
        if not sympy.isprime(rotated_prime):
            circular = False
    return circular
```

Instead of using `sympy.isprime` method, you can also create your own function that checks if the number is a prime. Below is a simple example of the `IsPrime` function. I would not recommend using it because it can slow down the program, which is why used `sympy` method.

```python
def IsPrime(number):
     prime = True
     for i in range(2, number): 
         if (number % i) == 0: 
             prime = False             
     return prime
```

Then, I iterated through the numbers from 2 to 1 000 000, checking whether a number is a circular prime number. If the number is a circular prime, it's appended to the list of `primes`. Lastly, the main function prints out the  number of circular primes below one million and the list of these primes.

```python
def main():
    """This program prints the number of circular primes below one million 
    and the list of these primes."""
    primes = []
    for i in range(2,1000000):
        if sympy.isprime(i) and IsCircular(i): 
            primes.append(i)
    print(f'The number of circular primes below one million is {len(primes)}. ')
    print(primes)
```



**Solution**: `The number of circular primes below one million is 55. `

`[2, 3, 5, 7, 11, 13, 17, 31, 37, 71, 73, 79, 97, 113, 131, 197, 199, 311, 337, 373, 719, 733, 919, 971, 991, 1193, 1931, 3119, 3779, 7793, 7937, 9311, 9377, 11939, 19391, 19937, 37199, 39119, 71993, 91193, 93719, 93911, 99371, 193939, 199933, 319993, 331999, 391939, 393919, 919393, 933199, 939193, 939391, 993319, 999331]`

Not so many...

# #112: Bouncy numbers

*A bouncy number* is a positive number that neither increasing nor decreasing (such as 12653). The definitions of increasing and decreasing number are presented in the description of this problem as follows: 

" Working from left-to-right if no digit is exceeded by the digit to its left it is called an increasing number; for example, 134468.

Similarly if no digit is exceeded by the digit to its right it is called a decreasing number; for example, 66420."

**Question**: Find the least number for which the proportion of bouncy numbers is exactly 99%.

### Approach 

I began by defining the functions to check whether the number is increasing, decreasing,  and bouncy. `IsIncreasing` and `IsDecreasing` functions input a number and check  whether the above-noted conditions are met, in which case the functions return `True` and `False` otherwise. 

```python
def IsIncreasing(num):
    """
    Input: number
    Output: Boolean -- True when the number is increasing
    """
    num = str(num)
    increasing = True 
    for i in range(len(num)-1):
        if int(num[i]) > int(num[i +1]):
            increasing = False 
    return increasing
 
def IsDecreasing(num):
    """
    Input: number
    Output: Boolean -- True when the number is decreasing
    """
    num = str(num)
    decreasing = True
    for i in range(len(num)-1):
        if int(num[i]) < int(num[i +1]):
            decreasing = False 
    return decreasing
```

`IsBouncy` function returns `True` if the number is neither increasing nor decreasing and `False` otherwise. 

```python
def IsBouncy(num):
    """
    Input: number
    Output: Boolean -- True when the number is bouncy
    """
    bouncy = True 
    if IsIncreasing(num) or IsDecreasing(num):
        bouncy = False
    return bouncy 
```

Having all the functions needed to solve this problem, it's time to write the program! I used a while loop to checks whether the number is bouncy or not, starting from 100 because there are no bouncy numbers below 100. Consequently, if the number is bouncy, it gets added to the list `bouncy_n` that keeps tracks of the bouncy number. While loop breaks when the proportion of bouncy numbers reaches 99%. Finally, following the loop, the `main` function prints the least number when the proportion first reaches 99%. 

```python
def main():
    """
    The function prints the least number for which the proportion of bouncy numbers is 0.99,
    where bouncy numbers are neither increasing nor decreasing numbers such as 155349.

    """
    number = 99
    bouncy_n  = 0
    while True:
        number += 1
        if IsBouncy(number):
            bouncy_n += 1
            proportion = (bouncy_n / number)
            if proportion == 0.99:
                print(f'The least number when the proportion of bouncy numbers is 99% is {number:,}')
                break
```

**Solution**: `The least number when the proportion of bouncy numbers is 99% is 1,587,000 `

Reference: https://projecteuler.net/archives

