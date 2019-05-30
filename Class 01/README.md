# Flex and Bison Tutorial

## Installation
**Mac:**

If you didn't install homebrew, do this following code:
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
If you installed homebrew, do those two commands in your terminal:
```bash
brew install flex # to install flex
brew install bison # to install bison
```
**Windows:**

Please find [this page](https://samskalicky.wordpress.com/2014/01/25/tutorial-setting-up-flex-bison-on-windows/) for the tutorial.

**Linux:**

Please find [this page](https://ccm.net/faq/30635-how-to-install-flex-and-bison-under-ubuntu) for the tutorial.

## Flex Scanner

## Bison Parser


## Exercise Questions
**Question 1:**

Design a regular expression for a language that accept all strings of lowercase letters containing the five english vowels (a,e,i,o,u) in order and each occurring exactly at once. For instance, a valid string is:
```
h a b e c i k o u m
```
and an invalid string is:
```
s a a a a b e
```
###### Answer:

**Question 2:**

Design a context-free grammar that accept this language:

![Q2](img/q2.png?raw=true "Optional Title")

###### Answer:

## Notes
1. If you plan to learn more, please see [this manual](http://web.iitd.ac.in/~sumeet/flex__bison.pdf).
2. Here is the [website](https://web.stanford.edu/class/archive/cs/cs103/cs103.1156/tools/cfg/) for testing the correctness of CFG.
