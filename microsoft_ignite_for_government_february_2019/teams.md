# Microsoft Teams

fastest growing business app in microsoft history

320+ thousand orgs using teams

1700 orgs with GCC

13 federal agencies, 87 state, 341 county agencies, 346 cities

Why teams?

- time savings compared to just using email to collaborate
- moving a lot of communication out of inbox into teams


Don't think of it as Teams killing outlook; think of it as outlook is becoming less valuable; conversations are being redirected from within outlook to within teams

he's said twice now that you can "find all the information about what's going on" within teams. WTF does that even mean? Third time: "easily find all the relevant information" but then he keeps saying "Group chat metaphor"

Important point: GCC (i.e. government cloud) is not a "feature"... it's a fundamentally different product than what you get with commercial cloud

Teams was released to GCC in July 2018

## Examples of Teams usage:


He's talking about how to roll out teams.... start with IT, eat your own dogfood; then find a coalition of the willing, perhaps people who've been clamoring for it or who are familiar with Slack and friends; project teams separated geographically

Huh... he has a quote up here about a team that replaced their scrum board with `Planner`


- Cross-agency collaboration. NOTE: for each licensed user, you can add 5 guests at no additional cost. Guest Access is through IT permissioning, including requiring MFA
- Live site / emergency incident response; mentions that stuff is documented in one place for review after
- New employee orientation

Note: the term "public team" means a team that anyone in the organization can join without asking for permission from the team owner


"Unified communications usage"

- not just chat, but also all the stuff in skype for business, but it can also replace skype for business; you can even turn on calling for just a subset of users

**He really encourages us to think about pilots; pilot first. Don't get caught up thinking you have to plan it all out perfectly before rolling it out; shoot for "small victory laps"**


## Advanced Usage of Teams

- interagency coordination; example of 42 federal, state, and local agencies coordinating on a thing
- emergency / diaster response
- juvenile rehabilitation and corrections; this example creates a team-per-juvenile where the parole officer is the team owner and the 5 free guests include parents/guardians, medical, vocational, nad educational professionals
- court case / legislative bill tracking; team per court case and channel per bill in the state legislature to centralize all meeting notes, drafts, evidence, etc


## Demo

- Teams is written for the web, and the windows and mac apps are built with electron wrapped around the web app
- a "Team" is just a group of people; you can belong to a bunch of teams
- Teams have channels
- Channels have conversations, files, Decisions, and other stuff (ok, the 'Decisions' Tab is just a custom tab)
- Every team has a general channel, and then you can add more


Thing I'm curious about: are Files in Teams integrated with OneDrive or whatevs? i.e. for searching
  - ultimately, this is just a file in sharepoint
  

Chat rooms are customizable to have not just the chat room, but also other tabs across the top

Dude in audience asks about controlling sprawl, says he's a member of 75 teams. HA fuck that noise

Interesting though: presenter says he uses "powershell for teams" to manage teams. 

They also have a tool called "Algebra" coming out for converting channels to teams, moving channels to a different team, and some other stuff I missed

Question from audience about creating teams based on org hierarchy

Presenter says "I wouldn't discourage you from that, but I wouldn't necesssarily start there". Says a good way to start is with a pilot based on "the real teams" that get the work done

He also says might be a good idea to start off without the bigwigs in the room; leave it to the worker bees

follow-up: can you have "sub teams"... presenter says: no, not yet. Look at "Private Channels" instead. They're also working on "shared channels" which lets multiple teams share a channel; should be available in gcc later this year. WAIT: did he says private channels aren't yet available in GCC?


OHHHHH... "chat is where most of the conversations happen in teams"... this is basically what we have now with private chats in Mattermost where you can add multiple people
  - me, editorializing to myself: I thought "most conversations happen in private chat" is a big anti-pattern; also doesn't jive with his whole "one place for all info" spiel from above, but whatever

https://aka.ms/T4GCC to learn more about teams in government clouds

Bots are not yet available in GCC; they're coming soon. The techniques and documentation are virtually identical to what's available in commercial so you can start learning it now. "Office Bot Framework". There are additional bot templates that are shipping in the next few months as well; employee surveys, FAQ with natural language access, etc


