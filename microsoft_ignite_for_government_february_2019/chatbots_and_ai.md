# Chatbots and AI

This guy doesn't work for MS; he's known for putting together useful infographics such as "visual guide to office 365 groups" and the "Periodic Table of Office 365"

some of this stuff isn't yet available for either GCC or azure govcloud (I don't know which)

## Why bots?

"Getting more value out of what you have"...

"show me ...."    "how do I .... "

Going after the high value information / tasks that people ask about on a regular basis

"I need to..."  -- this is where he thinks the big value is: Kicking off processes, workflows, etc

Don't go after every single need... go for the high value stuff

"A good FAQ bot is not good enough"


## Bot Architecture

- Understand: know how to translate english language requests into stuff
- Do: kick off the right thing based on what someone says
- Know: respond appropriately and conversationally about what you (the bot) just did or with the knowledge it found


- Bot Services
- Bot Framework

- LUIS: language understanding intelligence service
- QnAMaker: this is the knowledge / conversation aspect
- Coding: NodeJS or C#
- Other: Microsoft Flow... no-code solutions (not out yet in GCC, supposedly next few months)

Right now, Teams is the default home for azure-based bots

You can also drop bots into sharepoint, intranet, pretty much anything with a web api

this is an authenticated API; it can make graph calls, it knows who you are

## Demo

for asking the bot about time off, and then requesting time off. It's very conversational, with multiple back-and-forth for a single action. This is pretty slick

How this works under the hood:

QnAMaker: lets you plug in multiple ways to phrase a thing, with the response on the right. OK, this is basically like sorta advanced "ear dropping" like we have in our bot. The thing is that you can start with just a handful of phrases, and apparently its NLP stuff under the hood can then translate that into a pretty flexible thing, so it's not just "you add 5 things it should respond to and ti'll only respond to those 5 ways of phrasing that thing". OK, looks like "LUIS" is where all that magic happens. He says it's pretty easy to get started with this, but b/c of the trickiness of the english language, it can get a bit crazy; he's showing "entities" which are basically variables


He shows another demo for uploading an expense via chat; it uses Microsoft Flow in the background

And another demo on what looks like a sharepoint based intranet type deal with a "Help" bot type deal. the example here is in asking the bot to connect to a network printer; it prompts him with questions to find out what kind of printer he wants, helps him whittle down a printer to connect to. Now, this is rad: under the hood, this is all sending data to a servicenow ticket and sending the data to it, so there's a ticket created with history.

The thing you don't want to do is just to off and automate everything you can possibly do. Pick the important things first. Emphasizes that when you're an end user interacting with a bot, you're going to assume it can do everything

Try to make it like you're not replicating those really annoying phone trees... take advantage of natural language processing


## More use cases

probably the biggest hurdle right now, he says, is that people really don't understand how these things can be valuable

- HR, tech support, customer services
- ask the lean six sigma people... they know the business processes that could benefit from this
- knowledge management
- finance and accounting
- marketing (eg social media)
- Forms (he says this is  a really big one)
  - I'm thinking: PUA! man fuck our current pua process. 
  
He says you can use MS Flow in the background for simple forms, and "Power Apps" for more complex forms. Power Apps is tougher to integrate into the bot b/c it's not native (or something) but it is possible (I think)

He says consider a bot where you'd otherwise be using InfoPath and Sharepoint designer

see "The table of Azure Cognitive Services" (ai.jumpto365.com) for more of these types of services; LUIS and QnAMaker aren't the only ones





