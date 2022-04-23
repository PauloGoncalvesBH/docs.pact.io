---
title: Why we're getting rid of Pact Broker tags
author: Beth Skurrie
authorURL: http://twitter.com/bethesque
tags: [features, tags, branches, deployments, releases]
keywords: [features, tags, branches, deployments, releases]
date: 2021-07-04
draft: false
hide_table_of_contents: true
---

:::info tl&semi;dr

Tags that represent branches and environments are being replaced with first class support for branches, environments, deployments and releases.

:::

"Tags" in the Pact Broker are simple string values that belong to application version resources (aka. "pacticipant versions") that are generally used to track the git branches and environments associated with an application version. They allow us to identify specific versions when testing backwards compatability and introducing new features, and when determining if an application is safe to deploy. Tags have the advantage of being flexible and generic enough to support any development workflow.

Tags have their disadvantages though. They are similar enough to Docker tags that users expect them to work the same way, but different enough that pages of documentation need to be written to explain how to use them. The main problem with tags though, is that no semantic information that can be inferred from them - that is, it's impossible for the Broker to know whether a tag represents a git branch, an environment, or something else entirely.

<!--truncate-->

This pushes the burden of interpreting Pact Broker data and messages onto the user. For example, which message makes more sense - "There is no verified pact between version 6f6ca2f73 of Foo and the latest version of Bar with tag prod (no such version exists)" or "There is no verified pact between version 6f6ca2f73 of Foo and the production version of Bar, as Bar has not been deployed to production yet."

While we used the argument of "tags allow any workflow to be supported in the Broker in a non-opinionated way", it turns out that 99% of the times people use tags, they either represent branches or deployment environments. So, after 8 years of avoiding it, we have finally added first class support for branches, environments, deployments and releases, and now, we wish we'd done it years ago! 

So what are the changes?

1. When pacts and verification results are published, instead of "tagging with the branch name", we now set the more obviously named "branch" property for the application version. 
2. The pacticipant resource now has a configurable "main branch" property.
3. Instead of "tagging with the environment name" when an application version is deployed or released, we use the `record-deployment` or `record-release` commands provided by the Pact Broker CLI.

Not only does explicit branch and environment support allow the Broker to show much more meaningful and user friendly messages, it also makes Pact simpler to configure, and makes it easier to set up a CI/CD workflow that would previously have required a much more advanced understanding of the Broker.

Let's go through a list of the features that we've been able to add, enhance or simplify since the branch and environment support was added.

* can-i-deploy and verification configuration for integrations involving mobile applications is now the same as any other application
* Support for sensible defaults and simplification of pact selection when verifying
* Deploying a consumer version with a changed but already supported pact has become easier
* Addition of "next steps" to Pact CLI output

## can-i-deploy and verification configuration for integrations involving mobile applications is now the same as any other application

  When a server based application is deployed to an instance, the previously deployed version is removed from that environment, and no longer needs to be supported. When an application like a mobile app or code library is released, the previously released versions are still available, and still need to be supported for a time at least. Tags were unable to infer the difference between the two, meaning that when a user was using can-i-deploy or configuring pact verification, they had to be aware of whether they needed to specify "all versions with tag prod" or "the latest version with tag prod". The can-i-deploy variations especially were much more complicated for applications that integrated to a mobile application.

  The new `record-deployment` and `record-release` commands model these differences correctly, so the Broker always knows exactly which application version or versions are currently in an environment. This means that no matter whether an application is deployed or released, everyone can use `can-i-deploy` with the new `--to-environment ENVIRONMENT` option the same way, and can use the new `{ deployedOrReleased: true }` consumer version selector for pact verification.

## Support for sensible defaults and simplification of pact selection when verifying

  Previously, the documentation for pact verification has stated "verify the pacts from the main branch of your consumers and each of the deployment environments", followed by examples of what the selectors for those pacts could look like. It was impossible to code the Broker to return a "no configuration required" set of sensible default pacts however, as the tags did not allow the Broker to identify which pacts those were. With the addition of branch and environment support, the recommended selectors of `{ mainBranch: true }` and `{ deployedOrReleased: true }` can be set as the defaults, and we can now document the exact way to configure pact verification, rather than showing an example of what it might look like.

## Deploying a consumer version with a changed but already supported pact has become easier

  The workflow for getting a verification result for a changed pact from the latest version of its provider is well documented and supported. Obtaining verification results from the currently deployed versions of the providers requires an advanced understanding of the Pact Broker however. These "missing verifications" (which might well be successful, if they were actually run) mean that the deployment of the changed consumer must wait always for the deployment of the provider version that *was* the latest when the pact changed, even if the existing production version of the provider might already support the change.

  Knowing which versions of a provider application are currently deployed allows us to support a much smarter webhook, with the new event `contract_content_published_requiring_verification`. This webhook triggers a build for each of the deployed provider versions, as well as the latest main branch, when any of those provider versions is detected to be missing a verification for the published content. This logic has the additional side effect of stopping some unnecessary duplicate builds that are currently being triggered when tags are added to existing contract content.

## Addition of "next steps" to Pact CLI output

  We all like tools that help us use them better. The addition of branches and environment support allows the Broker to detect how far along a user is in getting a Pact supported CI/CD workflow set up (eg. have they set up any environments, have they recorded any deployments). The output from the new contract and verification publishing APIs now includes "next steps", which tell a user what technical tasks need to be completed next to achieve a fully Pact supported workflow.

As time goes on, explicit branch and environment support will continue to help us make Pact easier and better to use. Death to tags! Long live branches and environments!

## Why migrate?

If you already have your CI/CD workflow set up to use tags, you may wonder what benefits there are to migrating. The main reason to migrate is that tags are hard for new users to understand, and even if your current team is experienced with Pact, there will always be new users coming into the organization/team. Another good reason is that while tags will continue to be supported, future Pact Broker features will be built for deployed/released versions rather than tags.

## How do I migrate from tags to branches and environments?

You can read the docs for branches [here](/pact_broker/branches) and learn how to migrate from branch tags to real branches [here](/pact_broker/branches#migrating-from-tags-to-branches).

You can read the docs for releases and deployments [here](/pact_broker/recording_deployments_and_releases) and learn how to migrate from environment tags to recording deployments and releases [here](/pact_broker/recording_deployments_and_releases#migration-steps)


