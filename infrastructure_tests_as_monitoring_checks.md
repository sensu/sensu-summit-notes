## Infrastructure Tests as Monitoring Checks

Notes from an afternoon discussion at the 2017 Sensu Summit. 

### Attendees: 

- Ben Abrams (HPE)
- Jeff Barrows (GE)
- Tim Smith (Chef)
- Andre Niemann (Becon) 
- Garrett Honeycutt (LearnPuppet)
- Mercedes Coyle (Sensu)
- Justin Kolberg (Sensu) 
- James Phillips (Sensu)
- Caleb Hailey (Sensu) 

### Notes: 

- Certain infrastructure testing best practices are important in the context of reusing 
  them as monitoring checks; e.g.:
  - As a general best practice, functional tests are better than doing things like checking for the existence of files on disk
  - Functional tests should do things like check if services are running and responding to requests
  - Functional tests are even better if they are doing things like validating service responses
  - The things you want to be true (via an infrastructure test) upon a successful 
    configuration management run, are very similar to the things you want to monitor on an ongoing basis
- Sean Porter gave a talk at PuppetConf 2016 demonstrating this workflow using ServerSpec tests with Puppet
  - Video: https://youtu.be/AbRA-bqqOrg 
  - Slides: https://speakerdeck.com/portertech/watching-the-puppet-show 
- Paul Czarkowski (IBM) made mention of using Sensu for actual compliance testing using InSpec and Sensu
  - Slides: http://tech.paulcz.net/sensu-at-bluebox-sensuconf-2017/#/ 
  - Paul shared a link to their InSpec plugin in the Sensu Community Slack, here: https://github.com/blueboxgroup/ursula-monitoring/blob/master/sensu/plugins/check-inspec.rb
- There is a Sensu Plugin for ServerSpec: https://github.com/sensu-plugins/sensu-plugins-serverspec 
  - In reviewing the plugin it looks like it may be RSpec under hood
  - This plugin may "just work" with InSpec with some testing


