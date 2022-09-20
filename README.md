# Getting started with Actions on packages 📦 🛳️ 

Get started with the secure way of publishing 🛳️ and consuming in workflows 📑 without any fear of actions code being tampered by bad actors, and re-tagging with breaking changes.

## What is Actions on packages? 
At the moment Github Actions are hosted on git(hub) repositories, which due to their mutable design (mutable histories, and tags) - do not make a great choice as packaging format. And, this lack of a immutable properties from a git repository opens it up to attacks from a packaging perspective

With Actions Packages, you can reference actions by their version and feel confident that you are using the exact version as specified when your workflow runs.

## How to get started with `Actions on packages`
- The feature flag `actions_on_packages` should be enabled for the action repo to start experiencing `Actions on packages` feature. Please leave a message in `#actions-on-packages` channel if you would like to experiment with `Actions on packages`, and we will enable the feature flag on your  repository.
- Actions on packages requires that you copy [release.yml](https://github.com/actions-on-packages/.github/blob/main/workflow-templates/release.yml) workflow from this repository. This workflow is responsible for packaging the action contents  📦 while creating new releases and publish them to a container registry 🛳️.

  - (Optional) you can further extend the workflow by additionally adding build, minify steps and much more.
  - (Optional) You can also input the `path` of the action contents that needs to published for the `package-action` action within the workflow, as below 
 
 ```
    uses: actions-on-packages/package-action@0.3.0
    with:
      path: <path of action contents>  // (optional)
  ```

- Install GH CLI extenstion for new release experience https://github.com/actions-on-packages/gh-action-release. Installation instructions are available on the cli extension repo.

  - This new release experience enforces the semantic versioning for action releases by auto-generating tag_name based the changetype (valid values are `major/minor/patch`) provided. This enforcement helps in tag immutability and avoids re-tagging of new releases with existing tag_name, and follows the widely popular [Semver](https://semver.org) guidelines for genrating release tags.
  
**Note:** If your previous releases, did not follow semver compliance for tagging, the next release through this experience parses the latest release tag and generates subsequent semver compliant tag, which means, if the latest release tag is v2, the next major release would be tagged as `3.0.0`, and if the release tag only contains chars like `release` the next major release would reset to `1.0.0`. 
  
-   This extension requires few additional metadata while creating new releases, below is the command FYI,

``` 
gh-action-release: Works with GitHub Actions Releases. 

USAGE:
	gh-action-release <command> [flags]
	
CORE COMMANDS:
	create:		creates action release

FLAGS
	-c, --changetype            change type of the release. Valid values are: major/minor/patch
  	-p, --prerelease            is this a pre-release? Valid values are: (y/n or true/false)
  	-n, --releasenotes          release notes of the release
  	-r, --repo                  repo to create release for
  	-t, --title                 title of the release
	--help                      Show help for create command
	
EXAMPLES:
	$ gh action-release create
	$ gh action-release create -r github/js-action -c minor -t "release title" -p n
	$ gh action-release create -r github/js-action -c minor -t "release title" -n "release notes" -p n
	$ gh action-release create --repo github/js-action --changetype minor --title "release title" --releasenotes "release notes" --prerelease n
```

- The create release command above returns the link of the release workflow run, visit the link to track progress of package publishing. A package with with repo name and a generated semver compliant tag would be published to GHCR, 

<img width="1400" alt="image" src="https://user-images.githubusercontent.com/13884596/190091843-d739d30e-1406-451a-a00d-98c09a4b74d5.png">

- That's all that it takes in securing your workflows from malicious commits to actions by bad actors and re-tagging of releases with breaking changes 🎉 🚀 .
- And the rest, leave it to us on how the action packages are stored and retrieved securely 🥳
- The action package consumption experience in workflows remains the same, as we internally make sure to retrieve the action packages seamlessly. 
