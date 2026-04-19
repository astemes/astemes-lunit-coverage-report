# LUnit Coverage Analysis

An add-on to [LUnit](https://github.com/astemes/astemes-lunit) that measures VI-level code coverage during test runs and reports the results in the LUnit UI or as a Cobertura XML report for continuous integration.
- **Measure** VI-level coverage for selected VIs
- **Reporting** In-IDE result view and/or Cobertura XML
- **Requires** LabVIEW, LUnit 2.0 or newer, debugging enabled on measured VIs
- **Install** throug VIPM (stable releases) or GitHub Releases (pre-release builds)

## Installation

Stable releases are distributed as VIPM packages and are installed like any other VI Package. Pre-release builds are generated for each tagged version and are available on the [Releases page](https://github.com/astemes/astemes-lunit-coverage-analysis/releases).

Since this is a standalone add-on to LUnit, LUnit must be installed first.

Once installed, the add-on is activated from the LUnit `Tools → Reporting…` menu.

## Configuration

Open the Reporting configuration dialog and click **Configure** to select which VIs to measure. The selection is saved as a text file named `coverage_include.txt`.

The location of `coverage_include.txt` is derived from the location of the test case classes and cannot be changed. This ensures the file can be found even when LUnit is invoked from the CLI outside the context of a project.

> **Note:** VIs must have **Debugging enabled** for coverage measurement to work. This is the most common cause of missing or zero coverage results.

## Result view

When enabled in the configuration dialog, a result view shows coverage as a percentage for each measured VI, laid out in the project tree. VIs can be opened by double-clicking them in the view.

## XML report (CI integration)

The add-on can generate a Cobertura XML report that can be consumed by most common CI systems (Jenkins, GitHub Actions, GitLab CI, and others that support the Cobertura format).

To produce the report from the [LUnit CLI](https://github.com/astemes/astemes-lunit-cli), the add-on must be installed on the CI runner. The coverage report is then passed as a custom report alongside any other reports you want to generate.

The example below generates both the native XML report and the coverage report into `c:\logs`:

```
LabVIEWCLI -OperationName LUnit -ProjectPath c:\tests -ReportPath c:\logs -CustomReports "XML Report,Coverage Report"
```

See the [LUnit CLI documentation](https://github.com/astemes/astemes-lunit-cli) for the full list of arguments.

## Background

Prior to LUnit 2.0, rudimentary coverage analysis was included in the framework itself. As of 2.0, these features have been migrated into this standalone project so that coverage analysis can evolve independently of the main framework. Functionality and usability were significantly improved in the process, and Cobertura XML output was added.
