

# Microsoft Ignite for Government -- February 2019

**Monday morning notes**

  - Check out VS Code "Live Share"
    - I tried this out later... really easy to get set up, and it uses a secure shared tunnel to communicate
    - you can share with up to 5 people at a time
    - Could be a great solution for remote pairing, which we've been looking for since our previous go-to solution got acquired by Slack and then went away

**Microsoft Teams** -- [My notes](teams.md)

Key Takeaways:

- Fastest growing service ever
- Don't try to plan all the things in a teams rollout
- Pilot pilot pilot; eat your dogfood; start small, do proofs of concept, learn and adapt
- Bot integration coming soon to government version of Teams
- This does look like a suitable replacement for our use of Mattermost; but I would not want to move to it until we have approval and proofs-of-concept for bot integration... our CFPBot has become too important to our everyday use of chat to give it up
- People not used to using a chat tool like Teams are going to have to get used to managing notifications and otherwise taming it to make it useful
- Lots of potential here even for opening Teams up to external partners

**Graph API** -- [My notes](graph_api.md)

Key Takeaways:

- Incredibly powerful; relatively simple to use the APIs
- Good stuff in here that is "me" / "personalization" focused
- Tons of Office 365 functionality is exposed via APIs
- A good API Explorer, along with endpoints to use for testing

**Chatbots and AI** -- [My notes](chatbots_and_ai.md)

Key Takeaways:

- This was **not** an introductory Bots / Chat presentation; for example, our usage of CFPBot (based on Hubot) is absolutely NOT an AI bot; it's brute force scripts that mostly just orchestrates APIs
- This talk on bots was about conversational bots, using artificial intelligence style tools for taking bots to the next level, especially with natural language processing (NLP)
- Talking about the value of bots is really hard; you kinda have to see "the art of the possible" to really get it
- Don't be afraid of this stuff... there are tons of tools out there for building these things, it's not rocket science
- Focus on building bot-stye tools for the most common things you do; don't get bogged down in trying to rebuild / build all-the-things using a bot. Go for the "big rocks"

**Outlook Actionable Messages with Adaptive Cards** -- [My notes](outlook_actionable_messages_with_adaptive_cards.md)

Key Takeaways:

- This "Actionable Message" technology could be really, really useful for "processy" type things that we do
- Please let's remember that this technology exists! 
- Also, third party systems are building these things already; ServiceNow, for example
- Time savings from staying in email to perform simlple tasks can really add up when you consider the time saved in context switching between "get an email, click a link, do a thing in the browser, close the browser tab, go back to email". No, it's not earth shattering one at a time, but consider the cumulative effect for hundreds or thousands of people over the months and years
- The tooling for building these actionable messages is **really slick**; there isn't a ton of programming that goes into these things; most of the work is happening on the backend of the services anyway... these actionable messages just provide an easy to build UI on top of those services that keep people in email for these tasks and use Office365 as the conduit through which all the communications pass, which keeps it safe and secure and within compliance boundaries

**Modern Intranets with Sharepoint** -- [My notes](modern_intranets_with_sharepoint.md)

Key Takeaways:

- The entire first 1/3rd of this presentation was basically: take a user-centered approach to building an intranet, and that means prioritizing user research and UX; Jess would've probably liked this presentation
- Lots of emphasis on Intranets being important for helping people get their jobs done
- Lots of emphasis on Intranets being highly personalized, about "Me me me"
- Also lots of emphasis on governance, with a few seemingly really helpful links for learning more about her (the presenter's) advice here
- Sharepoint seems like a pretty darn good tool for building an Intranet that adheres to the principles she's espousing (personal: I do remember that our intranet at booz allen was built on top of sharepoint, and it was pretty darn good, highly personalized, highly functional, easy to use, and attractive)
  - This was another case of where seeing the demos was really high-impact for me, again in the spirit of "art of the possible"
- Final point: Intranets are never done; you gotta commit to continuously improving them and investing in them

**Kubernetes in Azure** -- [My notes](kubernetes_in_azure.md)

Key Takeaways:

- Really great session on the purpose of both containers and container orchestration tools such as Kubernetes, though I'd say that much of what he described as benefits of kubernetes could be said of any other orchestration engine such as Swarm, DC/OS, or even AWS ECS / Fargate
  - go get his slides for the "why containers?" and "why orchestration engine?" parts... it's good

- I loved the phrase "Life-and-reshape" as a type of migration in between "lift-and-shift" and "refactor"
  - lift-and-reshape is essentially what we're doing with at least a few of our things in our internal hosting environment, such as the intranet and presumably complaint analytics
  - lift-and-reshape is basically: containerize the app without changing much if any of the code; use managed services such as databases and search services for those types of dependencies

- If you're running containers at any kind of scale -- where scale can be either performance-related or just management-related (i.e. a non-trivial number of containerized apps) -- then you really do what an orchestration engine to take the most advantage of containers and to sanely operationalize them

**Accessibility in Office products** -- [My notes](accessibility_in_office_products.md)

Key Takeaways:

- WOW. A mind-blowing session. I am so friggin impressed with the accessibility features built into modern office products; note: office 2016+
- Accessibility is baked into their products; it's not a paid-for, bolted-on feature
- accessibility audit in Word looks super useful
- the translation tools built into powerpoint look super useful
- They have a Helpdesk that you can use, **for free**, so that your IT department doesn't need to be experts in all this stuff