

# Release

## Artefacts produced by the project

The project produces distributable Python package artefacts derived from the main codebase.

For each release, the following artefacts are generated:

-   **Python wheel package (.whl)**  
    Example:  
    `popcorn_meter-1.1.2-py3-none-any.whl`
    
-   **Source distribution (.tar.gz)**  
    Example:  
    `popcorn_meter-1.1.2.tar.gz`
    

In addition, GitHub automatically generates source code archives:

-   Source code (zip)
    
-   Source code (tar.gz)
    

The wheel package allows users to install the project directly using `pip`, while the source distribution allows manual builds or installations from source.

----------

## Release repositories

Project releases are distributed through **GitHub Releases** and **TestPyPI**.

GitHub is used to host versioned releases because it:

-   integrates directly with the source repository
    
-   automatically generates release notes
    
-   stores release artefacts
    
-   integrates with CI/CD pipelines
    

In addition, the Python package is published to **TestPyPI**, which is the testing environment for the Python Package Index. This allows verification that the package builds and installs correctly before a potential publication to the official PyPI repository.

The latest package release can be accessed at:

```
https://test.pypi.org/project/popcorn-meter/

```

----------

## Release automation

The release process is fully automated using **GitHub Actions**, **Poetry**, and **semantic-release**.

The deployment workflow is defined in:

```
.github/workflows/deploy.yml

```

A release is triggered automatically when:

-   changes are merged into the **main/master branch**
    
-   all CI tests pass successfully
    

The workflow performs the following steps:

1.  Checkout the repository
    
2.  Install dependencies using Poetry
    
3.  Determine the next semantic version
    
4.  Generate release notes automatically
    
5.  Create a GitHub release
    
6.  Build package artefacts
    
7.  Publish the package to TestPyPI
    

Version numbers are automatically determined by **semantic-release**, based on the commit messages.

----------

## Latest release

The most recent release (**version 1.1.2**) focused on stability improvements and infrastructure updates. The changes included:

-   fixing merge markers in `pyproject.toml` that were breaking `poetry install`
    
-   updating the project README and documentation
    
-   improving automated test coverage for key components
    
-   correcting CI workflow configuration
    
-   synchronizing deployment pipelines
    
-   updating project metadata and release configuration
    

These changes ensure that the packaging process, CI pipeline, and release workflow operate correctly.

----------

## Secrets and environment configuration

The release pipeline requires the following GitHub repository secrets:

Secret

Purpose

PYPI_USERNAME

Authentication username for PyPI/TestPyPI

PYPI_PASSWORD

PyPI API token

RELEASE_TOKEN

GitHub token used to create releases

These secrets are securely stored in GitHub and injected into the deployment workflow during execution.

----------

## License

The project is distributed under the **Apache License 2.0**.

This license was selected because it:

-   allows both academic and commercial use
    
-   permits modification and redistribution
    
-   provides an explicit patent grant
    
-   is widely adopted in open-source software projects
    

The same license applies to both the source code and the distributed artefacts.

----------

## Versioning schema

The project follows **Semantic Versioning (SemVer)** using the format:

```
MAJOR.MINOR.PATCH

```

Example:

```
1.1.2

```

Version numbers are incremented according to the type of change:

-   **MAJOR** – breaking changes
    
-   **MINOR** – backward-compatible new features
    
-   **PATCH** – bug fixes and small improvements
    

All generated artefacts share the same version number to maintain consistency.

----------

## Creating a new release

New releases are created automatically through the CI/CD pipeline:

1.  Developers implement changes in a feature branch
    
2.  The branch is merged into `develop` and then into `main/master`
    
3.  The CI pipeline executes tests
    
4.  If successful, **semantic-release**:
    

-   determines the next version
    
-   generates release notes
    
-   creates a GitHub release
    
-   uploads artefacts
    
-   publishes the package to TestPyPI
    

No manual tagging is required, as version tags are generated automatically by the release workflow.

