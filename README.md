# action-docker-test

<p align="center">
  <!-- <a href="https://github.com/outoforbitdev/action-docker-test/discussions">
    <img alt="Join the community on GitHub Discussions" src="https://img.shields.io/badge/Join%20the%20community-on%20GitHub%20Discussions-blue">
  </a> -->
  <a href="https://github.com/outoforbitdev/action-docker-test/actions/workflows/test.yml">
    <img alt="Test states" src="https://img.shields.io/github/actions/workflow/status/outoforbitdev/action-docker-test/test.yml?label=Tests">
  </a>
  <a href="https://github.com/outoforbitdev/action-docker-test/actions/workflows/release.yml">
    <img alt="Release states" src="https://img.shields.io/github/actions/workflow/status/outoforbitdev/action-docker-test/release.yml?label=Release">
  </a>
  <a href="https://securityscorecards.dev/viewer/?uri=github.com/outoforbitdev/action-docker-test">
    <img alt="OpenSSF Scorecard" src="https://api.securityscorecards.dev/projects/github.com/outoforbitdev/action-docker-test/badge">
  </a>
  <a href="https://github.com/outoforbitdev/action-docker-test/releases/latest">
    <img alt="Latest release" src="https://img.shields.io/github/v/release/outoforbitdev/action-docker-test?logo=github">
  </a>
  <a href="https://github.com/outoforbitdev/action-docker-test/issues">
    <img alt="Open issues" src="https://img.shields.io/github/issues/outoforbitdev/action-docker-test?logo=github">
  </a>
</p>

GitHub Action for running a test script in a Docker container.

## Usage

### Inputs

- `tests-path`: Required.
  The path to the bash script that should be run in the container
- `dockerfile-path`: Optional.
  Path to the directory with the Dockerfile. Defaults to "."
- `build-command`: Optional.
  Full command to build the image. Defaults to "docker build"

### Outputs

- `success`: Whether the tests were successful

### Example

```yml
docker-test:
  runs-on: ubuntu-latest
  name: Docker Test
  outputs:
    success: ${{steps.dockertest.outputs.success}}
  steps:
    - name: Checkout
      uses: actions/checkout@v3
    - name: Docker Test
      uses: outoforbitdev/action-docker-test@v1.0.0
      id: dockertest
      with:
        tests-path: ./tests.sh
        build-command: "docker build --build-arg EXAMPLE_ARG='example'"
    - name: Output version
      run: echo "Latest version is ${{ steps.semanticrelease.outputs.version}}"
```
