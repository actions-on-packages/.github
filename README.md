# Getting started with Actions on packages 📦 🛳️ 

Get started with the secure way of publishing 🛳️ and consuming in workflows 📑 without any fear of actions code being tampered by bad actors, and re-tagging with breaking changes.

## How to get started with `Actions on packages`
- Actions on packages requires that you copy `release.yml` workflow from this repository. This workflow is responsible for packaging the action contents  📦 while creating new releases and publish them to a container registry 🛳️.

  - you can further extend the workflow by additionally adding build, minify steps and much more.  

- Install GH CLI extenstion for new release experience https://github.com/actions-on-packages/gh-action-release. This extension requires few additional metadata while creating new releases, below is the command FYI,

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
  ✓ Release created successfully with tag_name 'vdf'
  https://github.com/raju-dasupally/js-action/releases/tag/vdf

  Click on the link below to track the progress of package: raju-dasupally/js-action:vdf
  http://github.com/raju-dasupally/js-action/actions
```
- That's all that it takes in securing your workflows from malicious commits to actions by bad actors and re-tagging of releases with breaking changes 🎉 🚀 .
- And the rest, leave it to us on how the action packages are stored and retrieved securely 🥳
