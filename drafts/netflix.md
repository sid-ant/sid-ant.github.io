
This post is my attempt to create a new series where I would discuss the direction of a product / feature at various tech companies.

Netflix recently announced that they will be putting several blockers to stop people from sharing their passwords. [1. CNBC Source](https://www.cnbc.com/2023/02/01/netflix-password-sharing-crackdown-faq-updates.html) [2 MarketWatch Source](https://www.marketwatch.com/story/heres-how-and-where-netflix-has-started-cracking-down-on-password-sharing-11675373633)

While I understand that it is within's Netflix interest to clamp down upon password sharing, I don't understand why would they design such a complicated mess to achieve their interests. 

# Proposed netflix's product design to stop password sharing

Netflix says that password sharing is allowed within a household. In the quest to increase their revenue numbers, Netflix set out to re-invent what it means to be in a household. According to them as household starts with the ip-address associated with primary account holder & all the members in the household must connect to that ip-address atleast once in 30 days. 

Sounds tricky enough? Well it doesn't stop there. To get around their own strict defination of a household, and to accomodate for edge-cases like vacations, family living separately etc. they have announced solutions like device verfication, paying for extra member etc. 

To me it looks like artifically manufacturing problems and then solving them via over-engineered approaches. I can't even fathom the amount of time, the product, engineering, marketing and finance teams would've spent on this. 

A feature where you have to track & characterize user logins based on ip-address, add & support an additional payment system for ad-hoc users & make estimations on lost vs gained revenue is alteast hunderds of jira tickets at Netflix's scale. 

So much of work for so little value. I still can't get over the fact, that the product team not only thought this was a good idea but also they imagined that their users would understand & accept such a complicated system. 

Are they forgetting that they are competiting with TVs & that does not require validating devices to watch gordon ramsay screaming at other chefs? TVs also don't make you question what it means to be a household in your culture.

# How I would've solved this problem? 

I like the KISS simple and especially when it comes to making changes to a product. Apple does it the best. 

I would've solved it by reducing Netflix's subscriptions plans to a single subscription plan. An affordable plan which only offers a single screen coupled with an discounted option to pay for additional screens. 

In this way for most people the Netflix would have become cheaper & that is excellent marketing! Also only families / friends who are in a actually in a household would be willing to pay more for additional screens. The defination of the household would be up to the people to decide.

# Why do I think this would work? 

Given the actions of Netflix, it is safe to make an assumption that they expected a net increase in revenue even with their user hostile solution. 

But what does it mean to have an increase in revenue? It doesn't happen magically! A real human being would need to take out their wallet, put in their credit card details and click pay. Who would these humans be? 

Let's try to figure it out. 

Assumptions

1. Plan Basic - 1 Screen - $10 - `SD` 
2. Plan Standard - 2 Screens - $15 - `>= HD` 
3. Plan Premium - 4 Screens - $20 - `>= HD` 

## Case 1 

- A friend take a premium plan which offers 4 screesn and shares them with 3 of their friends

Current Revenue: $20

Happy Case - All friends take the standard plan & the original friend downgrades to the standard plan. 

New Revenue: `$15 x 4` = $60 ( 200% increase in revenue ) 

Worst Case - None of the friends take the standard plan and the original friend downgrades to the basic plan. 

New Revenue: `$10 x 1` = $10 ( 100% loss in revenue)

## Case 2 

- A friend take a premium plan which offers 4 screesn and shares them with more than 3 of their friends

Say `Sam` pays for the Netflix premium plan which offers 4 screens. But since `Sam` is a really a good friend, he shares his password with 6 of his friends. `Rohit`,`Mark`,`Neha`,`Tess`,`Yuna` & `Rahul` all enjoy Netflix provided by `Sam`. In total we have 7 people watching Netflix off a plan which was originally meant to be shared among 4 people. 

This would only be possible if at any point in time, no more than 4 friends are watching Netflix. Thus it's not far to imagine that these viewers are not serious viewers of Netflix. If these people are not serious viewiers of Netflix then 