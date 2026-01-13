# Hard Fork Working Group Documentation

Repository for hard fork working group documentation.

This holds the source for the [cardanoupgrades.docs.intersectmbo](https://cardanoupgrades.docs.intersectmbo.org/) including polices/procedures the hard fork working group follows.

## Navigation

- [Cardano Upgrades Gitbook space](./gitbook/)
- [Hard fork Initiation Submission Policy](./gitbook/overview/hardfork-initation-submission-policy.md)
- [Past iterations of policies](./policies/past-iterations/)

## Contributing

### Updating Hard Fork Readiness Tracker

If you see that there is incorrect information on tooling readiness shown via [cardanoupgrades/intra-era-hard-fork-readiness](https://cardanoupgrades.docs.intersectmbo.org/proposed-intra-era-scope/intra-era-hard-fork-readiness).

Please create a pull request to update it!

#### Prerequisites

- [Node/NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- [Gitbook CLI](https://developer.gitbook.com/cli/quickstart)

#### 1. Fork the repository

From the [Intersectmbo/hf-wg-documentation page](https://github.com/IntersectMBO/hf-wg-documentation) create a fork of the repository.

#### 2. Clone the fork

Navigate to the directory where you want to work from.

Clone the fork, substitute your github username with `YOUR_USERNAME` in the below command.

```shell
git clone https://github.com/YOUR-USERNAME/hf-wg-documentation.git
```

#### 3. Create a branch

```shell
git checkout -b update-status-of-my-tool
```

#### 4. Setup Gitbook to run locally

Navigate into the directory.

```shell
cd hf-wg-documentation/gitbook
```

Install required gitbook plugins

```shell
gitbook install
```

#### 5. Run locally

Run and host the gitbook page locally.

```shell
gitbook serve
```

This can then be viewed via a web browser at `http://localhost:4000`.

#### 6. Make the new changes

In your favorite text editor navigate to to the readiness page.

This is how it can be done via VsCode.

```shell
code ./gitbook/proposed-intra-era-scope/intra-era-hard-fork-readiness.md
```

#### 7. Check changes

Confirming that the changes made within `./gitbook/proposed-intra-era-scope/intra-era-hard-fork-readiness.md` are impacting `http://localhost:4000` as expected.

#### 8. Add, Commit and Push changes to fork

If the changes/update is working, you can commit and push the changes to your fork.

Add changes to local.

```shell
git add .
```

Commit changes to local.

```shell
git commit -m "updated readiness page"
```

Push the changes to your fork.

```shell
git push
```

#### 9. Create pull request from fork back to source repository

From `https://github.com/IntersectMBO/hf-wg-documentation/compare`.

Ensure you select the `compare across forks`, to be able to see your fork.

Set `IntersectMBO/hf-wg-documentation` main branch as base and your fork's branch with the changes as the head.

Make sure you write a good pull request description.

#### 10. Review

Thank you for contributing.

[@Ryun1](https://github.com/Ryun1) or [@IntersectMatt](https://github.com/intersectmatt) will review the request and merge.
