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
    uses: actions-on-packages/package-action@0.4.2
    with:
      path: <path of action contents>  // (optional)
  ```

- After adding release.yml, action packages can be created and published to GHCR by following the normal release procedure either using Repo Releases GUI or CLI.
- The `gitTag` used for release creation should follow the guidlines of being semver compliant as mentioned in the release creation page. Refer below screenshot :

<img width="326" alt="Screenshot 2022-11-14 at 5 21 00 PM" src="https://user-images.githubusercontent.com/45332271/201653133-cc78d8b3-c2aa-4009-b190-e569d0814b72.png">



- Tags that strictly follow semantic versioning(`1.0.0` or `2.3.0`) or tags that have a prefix `v` along with semantic versioned tags(`v1.0.0` or `v2.3.0`) are acceptable.

- As the actions on packages are immutable, packages with existing semver tag once published, they cannot be republished.

- Release.yml workflow is triggered when a release is created either through releases GUI or CLI. The progress of package publishing can be tracked from the workflow run of the release.yml

- That's all that it takes in securing your workflows from malicious commits to actions by bad actors and re-tagging of releases with breaking changes 🎉 🚀 .
- And the rest, leave it to us on how the action packages are stored and retrieved securely 🥳
- The action package consumption experience in workflows remains the same, as we internally make sure to retrieve the action packages seamlessly. 

## How to migrate existing action releases to `Actions on packages`?
The new action releases will be automatically published as action packages as stated in the above section, for the existing action releases to be migrated as action packages, follow the steps below,

- The feature flag `actions_on_packages` should be enabled for the action repo to start experiencing `Actions on packages` feature. Please leave a comment in the [discussion here](https://github.com/github/c2c-actions-nirvana/discussions/267) if you would like to try out Actions on packages or if you have any suggestions/feedback.

- Install GitHub CLI extension for action releases migration, by running below command

    `gh extension install actions-on-packages/gh-action-release`

- For migrating a release of an existing action, run the below command

    `gh action-release migrate --repo <repo-name-with-owner>`

  and choose a release from the list of releases.
 
 - As the CLI utility will be creating action package(s) in your organisation, add `write:packages` to the CLI auth by running `gh auth refresh --scopes write:packages`

     Or if you would like to login with a PAT token, Create a PAT token with `write:packages` and `repo` full permissions and follow the screenshot below or you can 
     <img width="1013" alt="image" src="https://user-images.githubusercontent.com/13884596/207029122-ec685498-c54f-4b99-8126-05cc89ef7a80.png">
  
- The CLI extension will start migrating action release and ackowledges with resulting action package URL

For example, check out the below sample run 
![image](https://user-images.githubusercontent.com/13884596/207018328-6801c59e-a562-4216-a318-94e43370c4ba.png)
<img width="1225" alt="image" src="https://user-images.githubusercontent.com/13884596/207019455-43b2f166-21b8-41ca-8ebf-f4d64546e668.png">

## How to use `actions-packages` in workflows
The publishing workflow requires the actions repository to be added to the FF `actions_on_packages`, which also allows 100% of this action traffic to be routed to the actions-packages.

### Migrated releases
The migrated releases will continue to use the same referencing semantics, so there is no need to update the existing workflows.

### New releases
The new release or migrated release generates the `action-package` which can be found under the associated packages on the repository home page. Navigate to the action-package and you will find the usage snippet. See the screenshots below:
<img width="768" alt="image" src="https://user-images.githubusercontent.com/17195847/207063008-141b9c4d-795b-4a9d-860e-8c0fd76c74c7.png">
<img width="767" alt="image" src="https://user-images.githubusercontent.com/17195847/207068051-576ade19-78fe-4555-99bd-48215128e765.png">

### Splat versioning
🚀Good news🚀 Actions-Packages also supports the splat versioning hence the actions can be referenced using the sample semantics without having any additional tag maintained.

Say: The action author of `mycool\myawesome` just released a new version action version `v4.2.2`.
The splat referencing is shown as below:
```yml
- name: myawesome action
  uses: mycool/myawesome@v4

```
Now, no matter how many releases are created under the major version 4, `@v4` will always point to the latest released version.
