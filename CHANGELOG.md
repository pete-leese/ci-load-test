## Unreleased

### Feature

- Generated updated changelog
- Included status badge in readme
- Generated changelog from Commitizen
- Included GitHub PR template
- Broke down workflow into seperate jobs & introduced script to upload into PR comment
- Broke down workflow into seperate jobs & introduced script to upload into PR comment
- Updated workflow to change event trigger to on pr to facilitate testing inserting result output to PR comments
- Updated workflow to change event trigger to on pr to facilitate testing inserting result output to PR comments
- Initial load testing script
- Added checks to validate ingress and http-echo pods are ready
- Further Workflow enhacements, dynamically create kind-config.yaml, initial deployment for http-echo
- Initial test of updated deployment workflow logic

### Fix

- event trigger
- Updated readme to indicate challenge complete
- setting correct operator on loadtest  ouput file, ergo not overwriting the first load test results output
- Added comments to GitHub Actions workflow
- script refactor for PR comments
- Forgot to define fs const
- syntax issue in workflow code part 2
- syntax issue in workflow code
- Resolved issue with yaml indentation
- re-worked script for PR comments
- Adding missing GitHub token
- added additional InitConfigurtion to kind-configuration.yaml
- Updated readme to track timings
