# Sensu Community Plugins Pain Points

## Testing

- Some concern with determining the quality of plugins.
  - Current focus on integration testing as first step.
  - Regression testing across releases and platforms.
  - Interest in performance testing
- People loves when things work
  - Imperative that CM or monitoring is not broken,
  - Therefor for most plugin consumers it is important that they have the _confidence_ it works.

## Performance

-  Plugin installation is can be very slow.
  - Example: when using auto-scaling group and instances with 50 plugins by the time the new instance has converged the problem has fixed it's self
  - More and more plugins are using many / large dependencies
  - Could be better documentation for performance concerns and solutions. 
  - Possibly provide boilerplate code for embedding in debian package.
  - Possibly provide boilerplate code for using GemInABox, etc.
  - Boilerplate, boilerplate, and boilerplate...

## Windows

- Distinct lack of Windows plugins
  - How can we empower the community to contribute more Windows plugins
  - Majority of the current contributors and maintainers are not regularly administrating Windows environments
  - Could use more documentation? More windows boilerplate? scaffolding?

## Contributing

- Not immediately clear how to contribute new plugins.
  - Currently the process is buried in a `.github/PULL_REQUEST_TEMPLATE.md` file.
  - This could be helped with better documentation.
  - matt pls halp

## Best Practices

- Is there enough visibility on best practices for writing plugins?
  - Can some of this be documented in the skel repo

## Changelogs

- Having good changelogs is helpful for giving administrators confidence on what has changed
  - Helps mitigate the risk reward of upgrading a package
- @majormoses: [pagerduty plugin changelog](https://github.com/sensu-plugins/sensu-plugins-pagerduty/blob/master/CHANGELOG.md) is good example
  - Human readable changelog
  - Should always include a link to the diff
  - Include upgrade steps & any breaking changes
  - Helps with "upgrade evaluation"

## Updating

- Adding an `outdated` command to the CLI might be valuable
- Some use 50+ plugins and it would be nice to have a way to automate this process

## Sensu 2.0 Plugins

- Please god don't change the plugin format. Currently really easy for new developers get on board.
- No one wants it to become opinionated about what languages you use.
- If Ruby is not going to be available in 2.0 packaging; could affect 2.0  deployment.
  - Something we on the Sensu team will need to be mindful of moving forward.

## Testing Next Steps

- Look at DCOS plugin has good example of integrating testing
  - Limit the scope as much as possible
  - Tests should check output status, etc.
  - matt: adding something ^ like this to the skel repo would be helpful.
- Steps
  - phase one: improve integration
  - phase two: improve unit tests
- Start with most popular plugins(?)

## Miscellaneous

- PostgreSQL plugin needs an older version of Ruby
- People love that there is a plugin for almost everything
  - at least a starting point for most developers
- Sensu plugins skel repo; with information on getting started and what plugins should look like;
  - May need to be more discoverable(?)
- @amdprophet: likes integration testing
  - Regarding unit tests: mocking ffi calls is difficult.
  - A downside of integration testing is that it's hard to target every platform. eg. Windows & (impossible) AIX
  - It was suggested that we get linux testing story great first, and then worry about BSD, Windows, etc.
