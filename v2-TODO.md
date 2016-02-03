# TODO List for v2 Release

- Infrastructure upgrade
  - [x] create v2 branch
  - [x] Remove obsolete/unused projects (alternative runtimes, monodevelop, sharpdevelop integration, vs2010)
  - [x] Remove VS2013 integration and moved it to a separate github repo: [https://github.com/techtalk/SpecFlow.VisualStudio](https://github.com/techtalk/SpecFlow.VisualStudio)
  - [x] Upgrade all projects to .NET 4.5 and VS2013
  - [x] Replace lib references with NuGet wherever it was possible
  - [x] Upgrade "generateall" command to support new MsBuild infrastructure [Pull Request #411](https://github.com/techtalk/SpecFlow/pull/411)
  - [x] Cleanup NuGet package generation (eliminate SpecFlowBinPackage)
  - [x] Integrate Gherkin3
  - [x] Renew CI build infrastructure
  - [x] Enable build for Pull Requests
  - [x] Enable beta nuget package generation on v2 branch builds
  - [x] Review pending Pull Requests to `master`

- Features
  - [x] Support for ordering hooks - [Pull Request #414](https://github.com/techtalk/SpecFlow/pull/414)
  - [ ] Assist table helpers should use `[StepArgumentTransformation]` extensions  - In progress (Darren)

- To be decided
  - [ ] [GitLink](https://github.com/catenalogic/gitlink) support (?)
  - [ ] Use `throw new PendingException()` instead of ScenarioContext.Pending()
  - [x] Should be able to inject ScenarioContext to binding classes
  - [ ] Should be able to inject ScenarioContext to hook methods as parameter
  - [ ] ScenarioContext.Embed -- embeds related files, images as assets?