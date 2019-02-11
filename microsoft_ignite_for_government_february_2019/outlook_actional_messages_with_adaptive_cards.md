# Outlook extensibility with Adaptive Cards

- if you learn how to build Adaptive Cards, that learning is applicable to Teams and other stuff

"Actionable Messages": it's how you make the 5 seconds a user spends reading your email count

So, kinda like, an email that lets you "do the job the email wants you to do" right from within the context of the email.
  - for example, instead of getting an email with a link to click, you click it and go to that website and do the job you needed to do, and then close that web page; instead, you do it all from within the context of that message
  
I like this guy's message: "No, it's not climbing mount everest to have a user do that, but we certainly can do better and reduce friction". This really is about reducing context switching

"Actionable Messages = productive email"

"effortless task completion right from outlook"


This is all pretty new to GCC. They don't have a lot of folks out there doing this on GCC b/c it's so new


## How Actionable Messages work

safe and secure end-to-end

1. you register with MS to be allowed to send Actionable Messages
2. you implement dkim and spf to prove your identity as a sender
3. your service sends an actionable message; O365 sits in between your service and OWA/Outlook; outlook then sends the task actions back out through O365 and to your service; your service then returns a response, including an updated card; goes through )365 again back to OWA / Outlook


Actionable Messages are different from Adaptive Cards; AM is the entire process; AC is the thing that basically represents the payload


## Built with Adaptive Cards


- just introduced in mid 2018
- simple yet flexible card design format
- used by outlook, teams, windows, cortana skills, Bot Framework, and more
- why adaptive cards and not HTML?... native rendering, automatically adapt to host ux; purely declarative, no code (OMG like Flex!)

Shows an example of an adaptive card for trello

They've done the work to build scaffolding around this to make it easy to build adaptive cards

They even have a designer app! OMG this is amazing. it's in preview mode: http://acdesignerstaging.azurewebsites.net  WTF is this geocities or some shit

You can then even submit a test email with the designer thing, so you can see it end to end


WHOA: they have a ServiceNow integration (I think)... it's listed on the slide.

GitHub one, dealing with bugs and commits and such

When users click a submit button, apparently there is a "donut" spinner type deal to let the user know something is going on


## What's next for actionable messages?

- outlook for mac, outlook mobile; coming first half of 2019 with outlook for ios


## What to think about:

- do you have time sensitive internal business processes?
- (and a few other things he talked about but which I didn't take notes on)
- consider actionable messages


## Resources:
- he has a slide with a bunch of resources, number of these including an end to end actionable message scenario step by step is on github

