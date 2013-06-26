filipin.eu
zeljko@fillipin.eu

- missed the first 10 minutes of this talk

 walked in ...

 - They use RVM and Bundler which allows them to keep all their machines synchronized

 their "test automation framework" is all open

 - see his "qa-browsertests" git repo

 - mediawiki uses sauce labs
 - his browser has a saucelabs icon -- I need to see what that extension does

 - their jenkins is comlpetely open
   - wmf.ci.cloudbees.com
  - looks like their jenkins jobs use "templates"... I need to look into this more
   - "this job is created from template "browsertests""

 gerrit.mediawiki.org
   - all their code reviews are open

 they are all about transparency

 although MW is written in php, their tests are in ruby
  1. the php bindings suck
  1. when they hired zeljko, he knew ruby, so he went with what he knew

 they're still kinda new at browser automation
  - still selling test writing to the developers
  - "I don't want to insult anyone, but PHP developers aren't really test oriented" (unlike ruby, where you get burned if you don't write tests)

 connect jenkins to saucelabs
  - i think he said they just set an environment variable

