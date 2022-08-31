---
layout: post
title:  "Interesting Leetcode Problems"
date:   2022-05-15 01:00:18 +0530
categories: engineering
---


I've been solving leetcode problems for the past several months and these are few of the interesting problems / algorithms I've encountered. 


## Binary Search Over Non-Sorted Array

I love Binary Search. It's a straight-forward, easy to understand, easy to implement algorithm & sometimes it can even be used on unsorted arrays. The idea is to apply it on the solution space. 

One way to understand is to imagine an array `x` as an input to a function `f(x)` which produces `y` and if you can deduce the range of `y` like `[10,71]`, you can then check for the right answer instead of solving `f(x)`directly. 

{% highlight python %}

Given: 
    solve(x) = y
    where x is an input unsorted array

Deduce: 
    range: 10 <= y <= 75 
    a O(N) or O(1) function: verify(y)

Now we can binary search over range of y 
and check if y is the correct answer or not.  

{% endhighlight %}

Checkout these questions which implements the above idea. 

1. Cutting Ribbons
2. Find Peak Element
3. Sell Diminishing-Valued Colored Balls
4. Sqrt of a number. 

## Backus–Naur form (BNF)  

Sadly I did not have a compiler design class a part of my Computer Science curriculum. [BNF](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) is often taught in those classes as a specification to describe syntax of a language. However, the same spec can be used for almost any problem which can be broken down into a set of rules. 

Let's look at a problem where BNF can be used. 

### [Build Binary Expression Tree From Infix Expression](https://leetcode.com/problems/build-binary-expression-tree-from-infix-expression/)

The question requires us to create a binary expression tree from an infix expression. 
The input to the question is an expression like `3+4*2-(4*12)` and we need a way to constuct a tree.

One way to solve it is evaluating the expression as a compiler would. 

For example this would a BNF form for an infix expresion. 

    '''
        Backus-Naur Form (BNF)
        
        digit := [0..9]
        bracket := digit | '(' expression ')'
        mult_div := bracket | bracket { ['/','*'] bracket }
        plus_min := mult_div | mult_div { ['+','-'] mult_div  }
        s := plus_min
    '''

Here's the solution.

{% highlight python %}

    def expTree(self, s: str) -> 'Node':        
        tokens = deque(list(s))
        
        def parsePlusMin():
            
            lhs = parseMultDiv()
            
            while tokens and tokens[0] in ['+','-']:
                
                op = tokens.popleft()
                rhs = parseMultDiv()
                lhs = Node(val=op,left=lhs,right=rhs)
            
            return lhs
        
        
        
        def parseMultDiv():
            
            lhs = parseBracket()
            
            while tokens and tokens[0] in ['*','/']:
                
                op = tokens.popleft()
                rhs = parseBracket()
                lhs = Node(val=op,left=lhs,right=rhs)
            
            return lhs
        
        
        def parseBracket():
            
            if tokens[0] == '(':
                
                tokens.popleft()
                node = parsePlusMin()
                tokens.popleft()
                return node
            
            else: 
                digit = tokens.popleft()
                return Node(val=digit)
            
        
        return parsePlusMin()

{% endhighlight %}


### Other Worthy Mentions

1. First Missing Positive Number
2. Median From Data Stream 
3. Valid Number (rule engine)
4. All Subarrays in O(N)