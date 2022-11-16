# Getting started with Actions on packages 📦 🛳️ 

Get started with the secure way of publishing 🛳️ and consuming in workflows 📑 without any fear of actions code being tampered by bad actors, and re-tagging with breaking changes.

## What is Actions on packages? 
At the moment Github Actions are hosted on git(hub) repositories, which due to their mutable design (mutable histories, and tags) - do not make a great choice as packaging format. And, this lack of a immutable properties from a git repository opens it up to attacks from a packaging perspective

With Actions Packages, you can reference actions by their version and feel confident that you are using the exact version as specified when your workflow runs.

## How to get started with `Actions on packages`
- The feature flag `actions_on_packages` should be enabled for the action repo to start experiencing `Actions on packages` feature. Please leave a comment in the [discussion here](https://github.com/github/c2c-actions-nirvana/discussions/267) if you would like to try out Actions on packages or if you have any suggestions/feedback.
- Actions on packages requires that you copy [release.yml](https://github.com/actions-on-packages/.github/blob/main/workflow-templates/release.yml) workflow from this repository. This workflow is responsible for packaging the action contents  📦 while creating new releases and publish them to a container registry 🛳️.

  - (Optional) you can further extend the workflow by additionally adding build, minify steps and much more.
  - (Optional) You can also input the `path` of the action contents that needs to published for the `package-action` action within the workflow, as below 
 
 ```
    uses: actions-on-packages/package-action@0.4.1
    with:
      path: <path of action contents>  // (optional)
  ```

- After adding release.yml, action packages can be created and published to GHCR by following the normal release procedure either using Repo Releases GUI or CLI.
- The `gitTag` used for release creation should follow the guidlines of being semver compliant as mentioned in the release creation page. Refer below screenshot :

<img width="326" alt="Screenshot 2022-11-14 at 5 21 00 PM" src="https://user-images.githubusercontent.com/45332271/201653133-cc78d8b3-c2aa-4009-b190-e569d0814b72.png">



- Tags that strictly follow semantic versioning(`1.0.0` or `2.3.0`) or tags that have a prefix `v` along with semantic versioned tags(`v1.0.0` or `v2.3.0`) are acceptable.

- Packages cannot be re-published with existing package tags again.

- This release.yml is executed when a release is created either through GUI or CLI. Then the user has to track progress of package publishing from the workflow run of this release.yml

- That's all that it takes in securing your workflows from malicious commits to actions by bad actors and re-tagging of releases with breaking changes 🎉 🚀 .
- And the rest, leave it to us on how the action packages are stored and retrieved securely 🥳
- The action package consumption experience in workflows remains the same, as we internally make sure to retrieve the action packages seamlessly. 
