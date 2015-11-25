Questions:

1. How painful is it to deploy our software?
1. How often to deploys either fail or require a roll-forward?
1. What's the time to go from code committed to code successfully running in production?
  - Note: this was precisely the idea behind Porchlight!
1. How could we determine our deploy frequency?
  - What are our options for doing this?
  - manually create a spreadsheet?
  - jenkins API?
  - record deploys in graphite or new relic or some other thing?
  - how are others doing this?
1. What percent of our unplanned outages / failures caused by 
  1. Changes from other departments, such as Systems Engineering?
  1. Our own busted software?
  1. Failures in middleware, databases, etc
1. How do these things differ across our platforms... cf.gov, FL, PDP, data, hmdaops, etc

Their metrics for measuring performance:

- Two throughput metrics: 
  1. deploy frequency
  1. deploy lead time (from commit to deploy)

- One stability metric:
  1. mean time to recover
    - time required to restore service when an incident occurs (unplanned outage, impairment, etc)

They did measure change fail rate -- % of changes that fail when rolled out -- and found that high-performing orgs have the lowest failure rates when they roll out changes while low-performing orgs have the highest change failure rates

However, change fail rate is not part of their performance construct... they don't say why. I do remember Gene & co. talking about this at velocity, though, and explaining that it wasn't a significant predictor of low vs high performing orgs

Love this paragraph:

>>>This year, we created two new theoretical models
 for how continuous delivery and 
lean management practices affect IT performance and organizational performance. 
As we had hoped and expected, these practices predict IT performance — and IT 
performance predicts organizational performance. The more you build quality into the 
system — through automation, reducing batch sizes and shortening cycle times — and 
the more effectively you manage your team’s workload and visualize work queues, 
defects and bottlenecks, the more you increase throughput and stability

Factors contributing to high performance:

1. comprehensive, fast, and reliable test and deployment automation
1. trunk-based development and continuous integration
1. app code and system config all in version control


And 2 new lean-focused measurements:

1. Ability of org to limit WIP and use those limits to drive process improvement
1. Visual displays for key quality and productivity metrics, current status of work, and ability to align these metrics with operational goals
  - Jeeesh.... that's a mouthful


And one from last year:

1. Use of monitoring tools to make business decisions


Architectural characteristics:

1. ability to test without an integrated environment
1. ability for devs to get comprehensive feedback from automated tests
1. ability to deploy an app independent of other services it depends on
1. use of microservices architecture

They see these characteristics in software designed for continuous delivery

### Organizational investment in devops

They looked at whether orgs planned to invest in devops tools, training and development, or have already done so.

Also, is devops a high priority in org

Even the intention to invest had an impact

Per John Kotter, _Leading Change_, establishing a sense of urgency is the first and most important steps required to create effective, lasting change

### Deployment pain

I'm just gonna copy/paste:

Common problems include:
- Changes that often result in failures and are difficult 
to diagnose and fix.
- Dev, test, and staging environments that are different from 
production environments, causing failures when builds are 
promoted across environments.
- Lots of manual work required to deploy.
- Lots of handoffs between teams, resulting in slow, 
inefficient deployments.
The countermeasures that should be implemented include:
  - Do smaller deployments more frequently (i.e., decrease batch sizes).
  - Automate more of the deployment steps.
  - Treat your infrastructure as code, using a standard configuration 
management tool.
  - Implement version control for all production artifacts.
  - Implement automated testing for code and environments.
  - Create common build mechanisms to build dev, test and 
production environments
