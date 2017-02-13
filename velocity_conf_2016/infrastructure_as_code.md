Kief Morris, thoughtworks
infrastrucuture-as-code.com

Belief / myth: the longer you take to make a change, the more effective / safe the change will be
- it's the process-bureaucrat vs. cowboys thing

Configuration management: apply tools of software engineering to infrastructure management

All your stuff can be rebuilt, repeatably

All your stuff is disposable. Don't have to be as precious about them

Everything is consistent... decrease the amount of variation in the system
  - and variation is codified in software
  
Pipelines to manage changes

- validate changes to definitions and promote them across environments

Continuous Change Management

- small frequent changes, fast feedback
- operational quality and compliance validated **for every change**
- Effort focused on the delivery process

Configuration synchronization

- have configuration agents continuously re-apply the current definitions
- makes issues immediately visible
- ensures automation is always working, relevant, and correct

Server templates

- start with OS installation image
- use that image as base of a Template
= use the template to build multiple servers

- tradeoff between using a stock AMI and then applying all configs to a server vs. putting those configs in a template 
- harder if there is a lot of variation that leads to many server templates
- with a template, you have to keep it updated