# TODO List for v2 Release

- Infrastructure upgrade
  - [x] create v2 branch
  - [x] Remove obsolete/unused projects (alternative runtimes, monodevelop, sharpdevelop integration, vs2010)
  - [x] Remove VS2013 integration and moved it to a separate github repo: [https://github.com/techtalk/SpecFlow.VisualStudio](https://github.com/techtalk/SpecFlow.VisualStudio)
  - [x] Upgrade all projects to .NET 4.5 and VS2013
  - [x] Replace lib references with NuGet wherever it was possible
  - [x] Upgrade "generateall" command to support new MsBuild infrastructure [Pull Request #411](https://github.com/techtalk/SpecFlow/pull/411)
  - [ ] Cleanup NuGet package generation (eliminate SpecFlowBinPackage)
  - [ ] Remove SpecFlow.Reporting from the main repo
  - [ ] Integrate Gherkin3
  - [x] Renew CI build infrastructure
  - [x] Enable build for Pull Requests
  - [ ] Review pending Pull Requests to `master`

- Features
  - [ ] Support for ordering hooks
  - [ ] Assist table helpers should use `[StepArgumentTransformation]` extensions

- To be decided
  - [ ] `[Binding]` attribute should not be necessary
