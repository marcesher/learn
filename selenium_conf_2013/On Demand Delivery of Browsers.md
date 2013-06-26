# Problems

 - most web products need cross browser, cross platform testing
 - channel based browsers update frequently
 - products need to catch up quickly
 - products may need compat with older browser releases
 - need to react quicklky to new browser / platform combinations


# Goals
 - explore an option for scalable borwser-based testing
 - what if we could have tests get browser updates on demand
 - browsers as configuration
   - think parameterized testing, but with browsers as params
 - test with latest version in a channel
 - test with older versions
 - reproducibility
   - easily reproduce an issue  / test run on a specific browser version
 - scalability

# Problems not meant to cover

 - Build and test infrastructure, continuous integration

# Possibilities

 ## use VMs preconfigured with browsers of interest

  - Pros
    - easy to replicate and scale
    - clean configurations can be built
    - save older configs and checkout when needed

  Works great if you have ability to
   - maintain VMs for each browser build
   - have full ocntrol over machine farm technoogy


 ## Use external services like Sauce
  - Pros
    - easy to use, no local machine farm needed
    - local machine time freed for otehr uses
    - good option when building home grown testing farm is not an option or is too expensive

  - Concerns
    - some test requirements could be hard to externalize
    - round trip overhead
    - cost

 ## Install a browser during testing

  - Pros
    - no need to have pre installed browsers
    - no need to preconfigure machines
    - can be fit itno existing CI systems

  - Concerns
    - couuld 'pollute' machine
    - install overhead each time test cycle runs


# Installing browsers during testing

 - where will browsers come from?
   - vendor sites?
     - what if site isn't available?

   - internal repository?

 - How will browsers be installed?
 - How will a build ask for a particular browser version?
 - Will these on-demand browsers interfere with locally installed browsers?
   - not an issue for clean test machines, just dev machines


## Browsers in internal repository

Maven!

  - used nexus as repo manager
  - GroupID = repo branch
  - ArtifactID = browser channel
  - Version - build number of browser
  - Classifier - OS / type (e.g., installer)

  - shows example of what firefox release V18.0 for windows would be

    - browsers.release:firefox-release-win:18.0

### Adding a new browser version

  - download latest version
  - zip it up
  - mvn deploy
  - deploy additional artifacts (installers, driver execs)
  - all ov the above automated via shell scripts
  - takes a few minutes for a new browser version ( + download time)

### How do builds ask for browsers?

  - use installer library code
    - knows how to set up various browsers
  - Example
    - maven plugin written around installer code
    - browsers are configuration elements in plugin

  - Similar with Ant, same installer wrapped up in a task
  - Binary location passed along to selenium
  - each tool can provide its own way to specify browsers
  - these browser config elements translate into the identifier from the nexus repo

### Installing browsers

  - see his slides

### "Releasing" new browser versions

  - see his slides
  - they can't just release a new browser version automatically
  - need to "qualify" or "certify" it, then make sure it's supported by selenium, update tools
  - eventually users update their tools
  - new browsers put into "staging" configuration first, then to "release", etc