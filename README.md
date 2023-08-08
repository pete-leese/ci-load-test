# goodnotes-tech-challenge

Setting Up CI Load Test Workflow with GitHub Actions

This project aims to establish an automated Continuous Integration (CI) load testing workflow using GitHub Actions, enhancing our development process's efficiency and ensuring the stability of our applications under varying levels of load. The workflow is triggered for each pull request to the default branch, automatically provisioning a multi-node Kubernetes cluster using KinD (Kubernetes in Docker) on the CI runner.

The KinD cluster is configured with an Ingress controller to manage incoming HTTP requests and two http-echo deployments serving distinct responses. The Ingress routing is set up to direct traffic based on hostnames to the respective deployments. Before progressing to the load testing step, the workflow verifies the health of the Ingress controller and deployments.

The load testing itself is executed in a separate job, simulating randomized traffic for the specified endpoints. The load test results, including request duration statistics, failure rates, and request throughput, are generated and saved as comments on the corresponding GitHub Pull Request, providing actionable insights into the system's performance impact introduced by code changes.

This comprehensive CI load testing setup empowers our team to detect and address potential performance bottlenecks early in the development cycle, ultimately contributing to the delivery of robust and high-quality software.
### Prerequisites and Development Best Practices

#### Using pre-commit for Code Quality and Formatting

To ensure consistent code quality and formatting in your repository, it's recommended to utilize `pre-commit` alongside other development tools like `commitizen`. `pre-commit` is a versatile framework that allows you to automatically run various checks and tasks on your code before it's committed, helping catch issues early and maintaining a high code standard.

Here's how `pre-commit` can benefit your development process:

1. **Code Formatting**: Enforce consistent code formatting across the repository, reducing unnecessary code style discussions and saving time during code reviews.

2. **Linting and Static Analysis**: Detect potential bugs, errors, and vulnerabilities in your codebase before they make their way into your commits.

3. **Documentation Checks**: Ensure that documentation remains up-to-date and accurate, reducing confusion for developers and users.

4. **Testing**: Automatically run tests before committing, preventing broken code from entering your codebase.

5. **Custom Hooks**: Define custom checks or tasks specific to your project's needs, tailoring the workflow to your team's preferences.

#### Integration with commitizen

While `pre-commit` focuses on maintaining code quality and formatting, `commitizen` enhances your version control history by promoting consistent commit messages. By combining the two tools, you achieve a comprehensive pre-commit workflow that addresses both code quality and version control practices.

`commitizen` encourages well-formatted commit messages following a conventional format, making it easier to understand changes and generate changelogs. When combined with `pre-commit`, you're ensured that not only is your codebase clean and formatted, but your commit history is also well-structured.

By adopting `pre-commit` and `commitizen` in your development workflow, you create a cohesive process that boosts code quality, simplifies collaboration, and streamlines the release process. When used in conjunction with the automated Kubernetes cluster provisioning and load testing in this GitHub Actions workflow, you establish a solid foundation for maintaining reliable and high-performing applications.

# Project Documentation: CI Load Test Workflow with GitHub Actions

## Overview

This project implements a robust Continuous Integration (CI) load testing workflow using GitHub Actions. The workflow is designed to ensure the stability and performance of your application by simulating realistic traffic scenarios and reporting load testing results on relevant pull requests.

## Workflow Configuration

The GitHub Actions workflow is divided into three logical sections:

### 1. Environment Setup (Setup-Environment Job)

This section is responsible for preparing the environment by installing necessary tools and setting up the Kubernetes cluster:

#### Environment Variables:

- **kind_version:** Version of KinD (Kubernetes in Docker).
- **kubectl_version:** Version of kubectl.
- **ingress_version:** Version of the Ingress controller.
- **cluster_name:** Name of the KinD cluster.
- **node_count:** Number of worker nodes in the cluster.
- **host:** Hostname for the HTTP requests.
- **bar_path:** Path for the '/bar' endpoint.
- **foo_path:** Path for the '/foo' endpoint.

### 2. Health Checks (Health-Checks Job)

This section ensures that the Kubernetes components are deployed and healthy before proceeding to load testing:

#### Dependencies:

- **Setup-Environment Job:** This job must complete successfully before executing the Health-Checks Job.

### 3. Load Testing (Perform-Load-Test Job)

This section performs the actual load testing and reports the results back to the pull request:

#### Dependencies:

- **Health-Checks Job:** This job must complete successfully before executing the Perform-Load-Test Job.

#### Environment Variables:

- **concurrent_requests:** Number of concurrent requests for load testing.
- **total_requests:** Total number of requests to be generated.
- **output_file:** Name of the file to save load testing results.

## Suggested Environment Variable Values

For an optimal load testing experience, consider using the following suggested values for environment variables:

- **kind_version:** 0.11.1
- **kubectl_version:** 1.27.4
- **ingress_version:** 1.8.1
- **cluster_name:** ci-load-test
- **node_count:** 2
- **host:** localhost
- **bar_path:** /bar
- **foo_path:** /foo
- **concurrent_requests:** 20
- **total_requests:** 500
- **output_file:** load_test_results.txt

## Load Testing Results

After each load test, the workflow will post a comment on the associated pull request with the load testing results. The comment will include key metrics such as node count, response times, and other relevant data, providing valuable insights into the application's performance under load.

## How to Use

To utilize this CI load testing workflow in your project, simply add the provided GitHub Actions workflow configuration to your repository. Customize the environment variables according to your application's needs, and GitHub Actions will automatically trigger the workflow on pull request events targeting the 'main' branch.

By implementing this workflow, you can ensure that your application remains resilient and responsive even under demanding traffic conditions, enabling you to deliver a high-quality user experience.

## Time Log
- 07/08/2023 - 17:00 - Setup Pre-commit / commitizen & Initial GitHub Workflows
- 07/08/2023 - 17:35 - Paused Challenge
- 08/08/2023 - 11:30 - Resumed Challenge
- 08/08/2023 - 12:00 - Further developed workflow to include dynamic kind-config.yaml file based on number of nodes, and condition check to determine if cluster already exists, initial ingress configuration & initial foobar deployment
- 08/08/2023 - 12:15 - Paused Challenge
- 08/08/2023 - 13:45 - Resumed Challenge
- 08/08/2023 - 14:10 - Reworked kind-conf to support deploy node-lables and required ingress configuration, added ingress service, network resources for foo & bar deployments
- 08/08/2023 - 14:30 - Paused Challenge
- 08/08/2023 - 17:00 - Added checks to validate ingress and pods are available
- 08/08/2023 - 17:30 - Paused Challenge
- 08/08/2023 - 19:50 - Updated Workflow to change event trigger when PR is created for testing purposes.
- 08/08/2023 - 20:30 - Created README Documentation
