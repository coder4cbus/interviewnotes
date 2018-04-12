## What's a "tuple"? What's a "triple"? What's the difference between a tuple and a set? 
  * A tuple is essentially an array where each index represents a category of some kind, such that you can reliably associate values at a certain index across tuples as being related to that category. 
  * Not sure what a triple is. I would suspect that tuple might be short hand for an array of two that carries this meaning, and a triple would be an array of three? 
  * The difference between a tuple and a set is that a set holds only unique values, but that both are array-like. A tuple does not have a restriction on duplicates.
## What is the average and worst-case time complexity of access, search, and insertion for common data structures? 
 * For each answer, briefly explain why.
 * Cover these data structures: array, queue, stack, singly-linked list, hash table, BST.

Array:
  - Arrays have linear access, because when you remove something you need to shift everything over. 
  - Search is constant time, since you can do array math to find any index. 
  - Array insertion can be constant if it doesn't matter where it goes, but if it does matter, it is linear since you will need to shift all the other items over. 

Queue
  - Access is constant for the element that is first in the queue, but would be linear otherwise. 
  - Search is linear since you would have to pull out and replace the elements
  - Insertion is constant since elements are just added to the end of the queue

Stack
  - Access is constant for the element at the top of the stack, linear otherwise
  - Search is linear since you would have to pop off items and push them back on
  - Insertion is constant since you just append items to the top of the stack

Singly-Linked List
  - Access is constant since you can just reroute nearby elements
  - Search is linear since you have to work through to find something
  - Insertion is constant since you can just add to the tail

Hash Table
  - Access is constant since you can simply remove a property
  - Search is constant since you have a key value relationship
  - Insertion is constant 

BST 
  - Access is at worst linear since you have to rebalance
  - Search is logrithmic 
  - Insertion is constant 

## When using git, what exactly do people mean when they talk about "the SHA-1"? 

  - I'm not sure of the answer to this, but I believe SHA-1 refers to the specific hashing function that generates unique commit references. 

## How is that related to how git works?

  - I'm not sure how this is related to how git works, it must be some kind of way to make sure to save unique commits but also have connections between hashes to indicate that they belong to the same branch. 

## Practically speaking, how does git rebase function compared to git merge? 
  - Git rebase is different from git merge in that git rebase actually rewrites the commit history of a branch, essentially going back in time to move all the commits from one branch onto the commits of another, and reset the top commit as if it had been committed after the other commits. Git merge does not rewrite the commit history, but simply merges two commits directly, preserving commit histories. 

## Present a quick overview of TDD.
 * What are the proposed benefits? How popular is it, really 
 * What are the arguments against it?

  TDD is the practice of writing your tests before you write the code. The proposed benefits are that it is easier to maintain clear modular code by forcing yourself to write success and fail cases and clear input/outputs for each function. Probably more popular in theory than in practice, and maybe not as useful when developing prototype from scratch, but for the second iteration maybe more so. 

  Arguments against it are that it slows you down, and could potentially create unnecessary work, because functions and their use can evolve, and so you might write a test for something, and then implement the code and realize that it should actually do something differnet, and so you have to then rewrite the test, whereas if you write the test after you would save yourself that wasted work. 
## Is JavaScript a functional language? What does it mean for a language to be "functional"? 

Although JavaScript is not strictly speaking a functional language because it also makes use of object oriented programming techniques, inheritance, and state, it nevertheless can be used as a functional programming language. It might be considered multi-paradigm. It is functional in the sense that you can use it imperatively, meaning that you can write code that does not make use of state or classes but rather is a serious of pure functions that pass around parameters and make changes to them. 


## Practically speaking, what's a "declarative" language? *
  * What's a popular example of one?
  A declarative language is one that describes the what without describing the how. It is a generally higher level language form which ignores implementation details. An example might be SQL query language. 
## Is JavaScript statically or dynamically typed? Is JavaScript strongly typed or loosely typed? What do those terms mean?
  - Javascript is loosely typed because it does not enforce value types, but rather employes type coercion when there is ambiguity. TypeScript came a long to change that and convert JavaScript into a strongly typed language. 

  - I am not sure what dynamically and statically typed languages are. 
## Give a brief analogy explaining how computer memory works to a beginning programmer.
  * (No more than a couple of paragraphs, max, please.)
  - Memory is a temporary storage space with values and references to those values that the computer has random access to. You can think of it like a bunch of items in a room and each one has a tag. If the tag to an item is removed, that item is now impossible to find, and eventually it will be automatically garbage collected. 

## Using official terminology, summarize how Promises work in JS. 
* Some terms to use: pending, fulfilled, rejected, resolve, reject, then, catch, all. 
* Cover how chaining/sequencing promises works.

- In JavaScript promises allow you to more elegantly handle asynchronous code by remembering and passing around an IOU for a particular asynchronous function. When an asynchronous function is executed, the promise is a type of object that has a status of pending until the action is finished. When the action is done it is considered fulfilled, and will be either rejected or resolved depending on if there is a failure or success. 

- Even though you don't know when the promise will be fulfilled, you can set up a scenario in a "then" which specifices what will happen when a promise resolves, and a "catch" when the promise is rejected. You can also collect promises and run a .all which executes something when all the promises resolve. You can also chain promises together in a sequence of thens. 

## What's an IIFE in JS? When would you use it? *
- Hint: IIFE is short for "Immediately Invoked Function Expression".

  - An IFFE is a function that is declared and invoked immediately after it is declared, meaning that it if you are only going to use it once you don't need to store the function itself in memory, just the result of the function.


## From memory, write the one-liner that determines if a given string is a palindrome. *


## From memory, write the one-liner that generates a random number between two given integers. *
Two lines, rather: Offer variants where the last number is excluded versus included in the range of possible output.

## From memory, write the short function to shuffle a deck of cards with complete randomness. *
Hint: You should know the Fisher-Yates shuffle. You shouldn't be deriving random shuffles on the fly, as it will slow you down when doing card-game type problems.

## From memory, write the shortest code snippet in JS for cloning an array. *
Hint: it's only about 8 characters long including punctuation.

## From memory, write a code snippet that binary-searches an array. *
## From memory, write code snippets for BFS and DFS of a BST. *
## From memory, write 3 code snippets that do: pre-order, in-order, and post-order traversal of a BST. *
## What does it mean for coding to be "idiomatic"? Give one example of idiomatic vs non-idiomatic coding in JavaScript. *
## There is overhead to sending a request to another machine over the network. Make a (simple) quantitative argument re why it's still often faster to fetch data from Redis vs not using it. *