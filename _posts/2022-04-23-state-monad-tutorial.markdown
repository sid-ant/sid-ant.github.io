---
layout: post
title:  "State Monad Tutorial"
date:   2022-04-23 20:43:18 +0530
categories: jekyll update
---
 I've found Learn You A Haskell's explanation and even The State Monad: A Tutorial for the Confused? to be incomplete and making several key assumptions when explaining the state monad. Hopefully, this post should fill up those gaps. 
 
 As Brandon from The State Monad: A Tutorial for the Confused? rightly points out, the challenge in understanding State monad comes from understanding the following syntax.

{% highlight haskell %}
> newtype State s a = State { runState :: s -> (a, s) }
{% endhighlight %}

And this is where we start, or more accurately we start from `newtype` and `records` syntax. Let's take a simple example and start building on it.


### Example 1: 

As a refresher we start with a very simple newtype called Color.

{% highlight haskell %}
> newtype Color c = Color {getColor :: c}
{% endhighlight %}

Question: Given only this code snippet what can we do with it?  

Well, we can, 

1. Create a new Color type as `let x = Color "red"` 
2. Extract the red color out by using the accessory function as `let actualVal = getColor x` 

We notice that the type of Color constructor is

{% highlight haskell %}
> :t Color
Color :: c -> Color c
{% endhighlight %}

and the type of getColor is

{% highlight haskell %}
> :t getColor
getColor :: Color c -> c
{% endhighlight %}


### Example 2: 

A newtype with 2 type variables on the left side

{% highlight haskell %}
> newtype Couple a b = Couple {getter :: (a,b)}
{% endhighlight %}

Question: Couple takes 2 type variables on the left side, what does it mean? How can we create a couple type? 

To answer this, let's take a look a what is the type of Couple constructor?
 
{% highlight haskell %}
:t Couple
Couple :: (a, b) -> Couple a b
{% endhighlight %}

Couple constructor takes a `tuple` of values and then creates a `Couple` type. Thus we can do the following,

{% highlight haskell %}
> let y = Couple ("Electricity","Magnetism") 
{% endhighlight %}

getter y 
-- ("Electricity","Magnetism")

Wait what? Confused on why Couple take a tuple but not `Couple "Electricity" "Magnetism"` ? 
It's an easy mistake to make when looking at only the newtype syntax. Let's discover more and try to answer this. 

### Example 3: 

Multiple fields and records recap

{% highlight haskell %}
> data Family a b = Family {getFamily :: (a,b),getFirst :: a}
{% endhighlight %}

Once again we look at the type of Family constructor & we notice that to create Family we need

{% highlight haskell %}
:t Family
Family :: (a, b) -> a -> Family a b
{% endhighlight %}


If you are asking yourself why does `Family` constructor needs a tuple and also a value, it's okay. 
After reading countless tutorials on Monads it's easy to forget that records is just a sugar syntax. Let's look at Family constructor again without records.

{% highlight haskell %}
> data CleanFamily a b = CleanFamily (a,b) a
{% endhighlight %}

Aha, much cleaner. This tells us that, the number of type variables on the left has nothing to do with the actually usage of them. It's just telling us how many different types our constructor supports. The record syntax just provided us with helper functions. In the CleanFamily, we would've achieved the same functionality by writing those function functions by hand as

{% highlight haskell %}
> getCleanFamily :: CleanFamily a b -> (a,b) 
> getCleanFamily (a,b) _ = (a,b) 

> getFirst :: CleanFamily a b -> a 
> getFirst _ a  = a 
{% endhighlight %}

### Example 4: 

State Type Look alike without Records Syntax

{% highlight haskell %}
> newtype State s a = State { runState :: s -> (a, s) } 
> newtype Notebook page val = Notebook (page -> (val,page)) 
`Notebook` is very similar to State, except we don't have any accessory function like `runState`
{% endhighlight %}

Question: How do we create Notebook type? 

Looking at the type of Notebook tells us that, we need to pass a function which takes a page and return a tuple of val and page.

{% highlight haskell %}
> :t Notebook 
Notebook :: (page-> (val, page)) -> Notebook page val
{% endhighlight %}


So, we can create a Notebook type as

{% highlight haskell %}
> someFunc x = ("some default value",x+1)
let note = Notebook someFunc 
{% endhighlight %}


Note all we have done is wrap a function in the Notebook type. By very definition that is what Notebook type is. 

Now, how can we actually use the someFunc? Without the records type, we will have to create a custom function which takes Notebook and returns the function which is defined in it.

{% highlight haskell %}
> extractFunc :: Notebook page val -> ( page -> ( val, page ) ) 
extractFunc (Notebook fn) = fn 
{% endhighlight %}

Finally we can use the function as, `extractFunc note 2` which will produce the following result 

`("some default value",3)` 

Wrapping it all up Observe that we are actually doing exactly the same thing as we did with the `Notebook` type.

{% highlight haskell %}
> newtype State s a = State { runState :: s -> (a, s) }

:t State 
State :: (s -> (a, s)) -> State s a

:t runState 
runState :: State s a -> s -> (a, s)

let initialState = State $ \counter -> ("some default value",counter+1)
runState initialState 23 
--- ("some default value",24)
{% endhighlight %}


This concludes the Part 1. I hope you can now completely understand what does 
`newtype State s a = State { runState :: s -> (a, s) }` mean. 

Armed with this knowledge, let's explore how this is useful in the next Part.

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
