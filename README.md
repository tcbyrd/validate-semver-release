<h3 align="center">Validate Semver Release</h3>
<p align="center">A GitHub Action that validates GitHub Releases against semantic versioning rules<p>

## Usage

```workflow
# Triggered by new releases on GitHub
workflow "Publish a release" {
  on = "release"
  resolves = ["publish"]
}

# Run some checks against the new release
action "validate release" {
  uses = "JasonEtco/validate-semver-release@master"
}

# Publish the library to NPM if all is good!
action "Publish {
  uses = "actions/npm@master"
  args = "publish"
  needs = ["validate release"]
}
```

If your release is a valid prerelease, it'll store the prerelease tag in a `release-workflow-tag` file in the workspace.

One example usage is to use the contents of that file in later actions to pass a `--tag` flag to `npm publish`.
