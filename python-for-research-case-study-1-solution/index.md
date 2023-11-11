# Python for Research - HarvardX - Case Study 1 Solution

<!--more-->

## Introduction to Problem from HarvardX

> A cipher is a secret code for a language. In this case study, we will explore a cipher that is reported by contemporary Greek historians to have been used by Julius Caesar to send secret messages to generals during times of war.

### What is a Ceaser Cipher?
> The Caesar cipher shifts each letter of a message to another letter in the alphabet located a fixed distance from the original letter. If our encryption key were 1, we would shift `h` to the next letter `i`, `i` to the next letter `j`, and so on. If we reach the end of the alphabet, which for us is the space character, we simply loop back to a. To decode the message, we make a similar shift, except we move the same number of steps backwards in the alphabet.

So, we now know about our topic and what is a Ceaser Cipher. We should read the exercises and go on with solutions.

## Exercises

### Exercise 1

> In this exercise, we will define the alphabet used in the cipher.
> * The `string` library has been imported. Create a string called `alphabet` consisting of the space character `' '` followed by (concatenated with) the lowercase letters. Note that we’re only using the lowercase letters in this exercise.

```python
import string
# write your code here!
alphabet = " " + string.ascii_lowercase
```

The above code creates a string called `alphabet` as intended. 

#### What is the `string.ascii_lowercase` part and why does it work?

`string.ascii_lowercase` allows us to create a string that has English lowercase letters. There are also `string.ascii_letters`, which returns all English letters, and `string.ascii_uppercase`, which returns all letters in uppercase.

### Exercise 2

> In this exercise, we will define a dictionary that specifies the index of each character in `alphabet`. 
> * `alphabet` has already defined in the last exercise. Create a dictionary with keys consisting of the characters in `alphabet` and values consisting of the numbers from 0 to 26. Store this as `positions`.

```python
# write your code here!
positions = {}

for idx, letter in enumerate(alphabet):
  positions[letter] = idx
```

Works easily. However, how should we interpret this solution?

#### What is `enumerate()` and what does it do?

As you know, we need both indices and values, which leads to the question: How to do this in Python? And here comes the `enumerate()` built-in function. When `enumerate()` function returns too loopable (?) variables:

1. The index (place of the letter)
2. The value (letter)

### Exercise 3

For simplicity, I will skip Exercise 3. Since it asks us to encode a sentence and I want to generalize the problem, let's skip to Exercise 4, in which we have to create an encoder function. Just know that, later on, our will be encoded string is `message = "hi my name is caesar"`.

### Exercise 4

> In this exercise, we will define a function that encodes a message with any given encryption key.
> * `alphabet`, `position` and `message` remain defined from previous exercises. Define a function `encoding` that takes a message as input as well as an int encryption key `key` to encode a message with the Caesar cipher by shifting each letter in message by key positions. Your function should return a string consisting of these encoded letters. Use `encoding` to encode message using `key = 3` and save the result as `encoded_message`. Print `encoded_message`.

```python
# write your code here
def encoding(message, key):
  encoded_message = ""
  for i in message:
    new_letter = positions[i]+key
    if new_letter > 26:
      new_letter %= 27
    encoded_message += alphabet[new_letter]
  return encoded_message

print(encoded_message=encoding(message, key=3))
```

Observe that we had to take the modulus of `new_letter` if it increases more than 26. 

This problem has one more exercise; however, I won't be explaining it since the decoding process is just backward, negative, of the encoding.

