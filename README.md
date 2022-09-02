# Getting started with Actions on packages 📦 🛳️ 

Get started with the secure way of publishing 🛳️ and consuming in workflows 📑 without any fear of actions code being tampered by bad actors, and re-tagging with breaking changes.

## How to get started with `Actions on packages`
- Actions on packages requires that you copy [release.yml](https://github.com/actions-on-packages/.github/blob/main/workflow-templates/release.yml) workflow from this repository. This workflow is responsible for packaging the action contents  📦 while creating new releases and publish them to a container registry 🛳️.

  - (Optional) you can further extend the workflow by additionally adding build, minify steps and much more.
  - (Optional) You can also input the `path` of the action contents that needs to published for the `package-action` action within the workflow, as below 
 
 ```
    uses: package-action
    with:
      semver: <release-tag>
      path: <path of action contents>        
  ```

- Install GH CLI extenstion for new release experience https://github.com/actions-on-packages/gh-action-release. Installation instructions are available on the cli extension repo.

  - This new release experience enforces the semantic versioning for action releases by auto-generating tag_name based the changetype (valid values are `major/minor/patch`) provided. This enforcement helps in tag immutability and avoids re-tagging of new releases with existing tag_name, and follows the widely popular [Semver](https://semver.org) guidelines :g for genrating release tags.
  
  - If your previous releases, didnot follow semver compliance for tagging, the next release through this experience parses the latest release tag and generates subsequent semver compliant tag, which means, if the latest release tag is v2, the next major release would be tagged as `3.0.0`, and if the release tag only contains chars like `release` the next major release would reset to `1.0.0`. 
  
-   This extension requires few additional metadata while creating new releases, below is the command FYI,

```
gh action-release create --help

create action release

Usage:
  action-release create [flags]

Flags:
  -c, --changetype string     change type of the release
  -h, --help                  help for create
  -p, --prerelease            is this a pre-release?
  -n, --releasenotes string   release notes of the release
  -r, --repo string           repo to create release for
  -t, --title string          title of the release
```

for example,

```
gh action-release create --repo raju-dasupally/js-action --title v --releasenotes description --changetype major
? Is this a pre-release? No
? Submit?:   [Use arrows to move, type to filter]
> Publish release
  Save as draft
  Cancel
  
  Creating new release...
  ✓ Release created successfully with tag_name '2.0.0'
  https://github.com/raju-dasupally/js-action/releases/tag/2.0.0

  Click on the link below to track the progress of package: raju-dasupally/js-action:2.0.0
  http://github.com/raju-dasupally/js-action/actions
```
- The create release command above returns the link of the release workflow run, visit the link to track progress of package publishing. A package with name `raju-dasupally/js-action:200` would be creating as shown in below screenshot.

<img width="1088" alt="image" src="https://user-images.githubusercontent.com/13884596/188114491-3e943468-9b98-459e-bd89-2b856806d597.png">

- That's all that it takes in securing your workflows from malicious commits to actions by bad actors and re-tagging of releases with breaking changes 🎉 🚀 .
- And the rest, leave it to us on how the action packages are stored and retrieved securely 🥳
- The action package consumption experience remains the same, as we internally make sure to retrieve the action packages seamlessly. 
