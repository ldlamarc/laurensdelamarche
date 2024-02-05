---
layout: post
title: Vanilla Rails
short_title: Vanilla Rails
datetime: 2024-02-04T20:00
excerpt: An Ode to Vanilla Rails
---

## Introduction

Rails 1.0 was released in 2005. It took the world by storm and was soon adopted by many prominent companies still known
today: Shopify, Twitter, Github, Gitlab, Twitch, Kickstarter, Fiverr and Basecamp to name a few. With success comes disbelief and criticism. Well established communities such as the Java community
saw saw Ruby on Rails as threat dismissing it as a hype, not scalable or only for simple CRUD apps. Rails shin-kicking
marketing strategy might have propelled them forward but also left sour aftertaste in many communities who felt
targeted.

Some companies such as Shopify ignored the scepticism and their Rails stack today powers 10% of worldwide e-commerce
traffic. Other platforms such as Twitter reverted to other technologies blaming Ruby and Rails for their wrong
architectural choices (such as reinventing a queuing system in Ruby).

I was introduced to Rails at version 3. I was doing my Master in Computer Science and was used to writing in assembly,
C++, Java (NetBeans) and other options pushed upon us by various courses. Ruby (on Rails) hit me like a breath of fresh air. 
Our daunting school project was implemented in no time. Rails was fast, it was easy but most importantly it was a joy to program in.

During my career and free time I ventured into web technologies such as PHP (Drupal), Python (Django) and Elixir
(Phoenix). But none quite captured the magic of Rails.

## A bad workman always blames his tools

After my degree I started my career as a Rails engineer. Rails has many opinions and conventions for most common use cases. But webapps
being built on Rails are very diverse. Not every feature can be shoehorned into an ActiveRecord, ActionController or
view template as seen in the guides or tutorials. Engineers actually need to engineer when going beyond simple
tutorials. This is not a shortcoming of the framework but a choice. Rails is built on solid default conventions and you can't have sensible conventions for every use
case.

Every Rails developer at one point realises that it's called Ruby on Rails for a reason. Rails provides the tracks for
your Ruby train of code. Models don't need to be just ActiveModel or ActiveRecord, views can have their own objects, the controller can delegate to a service layer instead of a model layer. 
I as many was also tempted by movements trying to extend the
default vanilla conventions with extra conventions: decorators, form objects, interactors, service objects or even frameworks such as Trailblazer. 

And often these initiatives leave people feeling as if vanilla Rails is not the right choice. They feel every controller action
needs to be coupled to a service object, every model needs to be exposed to the view in a decorator, active records are left behind in favor
of plucking and raw SQL. But all these choices bump into all kinds of other challenges and problems once you use them enough 
or try to apply them too broadly showcasing why they are not default conventions but rather tools to be used wisely. 

Nowadays if I need to engineer a controller action that coordinates complex interactions between multiple records I am confident in using a Service Object. 
But I don't feel any guilt in sticking some methods on top of an ActiveRecord, introducing a helper to format some view, using a
callback to handle some lifecycle logic as they are often very solid default choices.

## Further reading

To understand how to engineer applications well without straying away too much from vanilla Rails consider learning from the creator of Rails himself or one of his 37signals engineers:

- [Writing software well](https://www.youtube.com/watch?v=H5i1gdwe1Ls)
- [Code I Like](https://dev.37signals.com/series/code-i-like/)


