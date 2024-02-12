---
layout: post
title:  "A practical introduction to DDD and OOD coming from standard Rails, part 3 : Service Objects"
short_title: "DDD, part 3: Service Objects"
datetime: 2024-02-11T20:00
excerpt: This series is intended for an audience that feels comfortable with the basics of Ruby and Rails and wants to learn how to add practical DDD and OOD principles to their toolkit to improve the quality of their code.
---
I wrote a piece in 2016 about use cases for Service Objects. It was salonfähig at that time to complain about ActiveRecord and move as much business logic as possible out to a Service layer. But I was never confident enough to publish it. Were Service Objects really a step in the right direction? 7 years later I am still not very convinced. I will try to list the pros and cons in this post and give my own personal synthesis.

## The case for Service Objects

Models and controllers tend to get fat. Fat is bad so let’s move business logic to this concept called Service Objects living in “app/services”. Let’s couple one Service Object to every controller action. For create, update and destroy we put most lifecycle logic in the Service Object instead of callback. For show and index we use finder/query objects that construct the queries we want. That seems to be the basic argument for Service Objects.

### Gitlab

[Gitlab](https://gitlab.com/gitlab-org/gitlab) uses [Service Objects](https://docs.gitlab.com/ee/development/reusing_abstractions.html#service-classes) extensively.

Gitlab demonstrates how to move from [callbacks to Service Object](https://docs.gitlab.com/ee/development/backend/ruby_style_guide.html#example-of-moving-from-a-callback-to-a-service) but then warns us it can “be hard to see the benefits of the […] approach”. It also advocates for not sticking to [CRUD](https://docs.gitlab.com/ee/development/reusing_abstractions.html#service-classes) in naming.

### Dave Copeland

Dave Copeland in his [book](https://sustainable-rails.com/) also argues extensively for Service Objects avoiding most logic on ActiveRecord. His naming conventions and nuances differ slightly from Gitlab.

## The case against Service Objects

### Basecamp

Rails originated from Basecamp and as far as I know from the [code](https://dev.37signals.com/series/code-i-like/), [tweets](https://twitter.com/dhh/status/272455453630406656?s=20&t=VztxGfN6ZoKQnksPlCBpVA) and [videos](https://www.youtube.com/watch?v=m1jOWu7woKM) they share they do not use Service Objects (extensively). They keep their ActiveRecords thin in terms of logic by delegating methods and auxiliary logic to simple models (e.g. PORO’s). They don’t mind large surface api’s ([no they don’t violate SRP](https://www.oreilly.com/library/view/working-effectively-with/0131177052/)) on their ActiveRecords. They use CurrentAttributes to have access to e.g. current_user and they make classes used for auxiliary logic in callbacks [Suppressible](https://gist.github.com/tomafro/054d7d1a7c40ade27405599289196a54). 

### The Sandi Metz crowd

Avid Grimm (co-teacher of Poodr) writes his thoughts well in this [article](https://avdi.codes/service-objects/).

### Eric Evans and Martin Fowler

Service(s) (Objects) originated from [Domain-Driven Design](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/ref=as_li_ss_tl?s=books&ie=UTF8&qid=1509374681&sr=1-1&keywords=domain+driven+design&linkCode=sl1&tag=thlafa-20&linkId=c80725c168a095a86c3c9f742ddd0446). But in the book they are defined much more narrowly then they are often used in Rails projects. The book still advocates to build mainly around domain models. Martin Fowler also expands on it in this [article](https://martinfowler.com/bliki/AnemicDomainModel.html).

## Synthesis

Service Objects are not well understood. A lot of advocates of them don’t always know what they were intended for or even where they originated from. They gained a lot of popularity in the Rails community when a lot of more mature codebases suffered from obese GOD models (2010-2015). Fat controllers and models became fat ill-defined service folders. Codebases without a strong tech leadership and vision (such as Gitlab or Copeland) saw these folders devolve into the Wild West of code repeating many mistakes Rails or even more generally OOD and DDD already solved. 

I have seen multiple codebases couple multiple Service Objects to one controller action or spanning webs of Service Objects calling Service Objects (Service Object hell?). Services with horrible naming, loose confusing bounds and atomic operations not wrapped in transactions. Bugs due to essential business logic coupled to a domain model being hidden in a Service Object not being called in another controller operating on the same domain model (how could the second author even spot this?).

Rails (/Basecamp) did not always offer clear alternative solutions staying within the DDD philosophy. But I feel that changed in recent years even though the information is not yet fully breaking through the clutter (Sturgeon’s law?).  

Service Objects still have their use if the domain and bounded context is not yet clear, if you are juggling many models (failing to appoint one as the root) or designing an infrastructure service (webhook, notification, etc). But don’t consider app/services an excuse to stop modelling, naming or designing your software well. They need just as much thought as doing Vanilla Rails but you can’t rely on any well known conventions, framework classes or guidelines to protect yourself.
