---
layout: post
title: The Euler Project
subtitle: Problems 4, 35, and 112
#cover-img: /assets/img/cover_pic_website.jpg
thumbnail-img: /assets/img/code.jpg
tags: [Euler]
---

In this post I will explain how I solved three problems from the [Project Euler](https://projecteuler.net/) using Python. Project Euler is  a website publishing computational problems that are solved with computer programs.  The three problems I chose have different level of difficulty as listed below: 

1. Problem 4: *Largest palindrome product*--  solved by < 500,000 people

2. Problem 35: *Circular primes* -- Solved by < 100,000 people

3. Problem 112: *Bouncy numbers*  --Solved by < 25,000 people

   

# #4: Largest palindrome product

*Palindrome* is the number/word/phrase that can be read the same backward as forward. For example, 303  and 7557 are  palindromes. 

<u>Problem<u> : 

Find the largest palindrome made from the product of two 3-digit numbers. 

## Approach 

First, I created a function to check whether the number is palindrome or not. The function takes a  number and checks whether this number is equivalent to the reversed number, in which case the functions returns `True`  and `False`  otherwise. 

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

Next, I used nested for loop to get a product of two 3-digit numbers and checked whether it is a palindrome. If the product is a palindrome, it is added to the list of palindromes and the largest palindrome is printed. 

```python
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

<u> Solution<u> : 

`The number of circular primes below one million is 55. `

# #35: Circular primes

