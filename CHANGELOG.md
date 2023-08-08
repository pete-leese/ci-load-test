## Unreleased

### Feature

- Included status badge in readme
- Generated changelog from Commitizen
- Included GitHub PR template
- Broke down workflow into seperate jobs & introduced script to upload into PR comment
- Updated workflow to change event trigger to on pr to facilitate testing inserting result output to PR comments
- Initial load testing script
- Added checks to validate ingress and http-echo pods are ready
- Further Workflow enhacements, dynamically create kind-config.yaml, initial deployment for http-echo
- Initial test of updated deployment workflow logic

### Fix

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
