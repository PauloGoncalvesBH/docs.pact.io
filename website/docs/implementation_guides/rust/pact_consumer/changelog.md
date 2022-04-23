---
title: pact_consumer
custom_edit_url: https://github.com/pact-foundation/pact-reference/edit/master/rust/pact_consumer/CHANGELOG.md
---
<!-- This file has been synced from the pact-foundation/pact-reference repository. Please do not edit it directly. The URL of the source file can be found in the custom_edit_url value above -->

## 0.9.1 - Bugfix Release

* 73ae0ef0 - fix: Upgrade reqwest to 0.11.10 to resolve #156 (Ronald Holshausen, Wed Apr 13 13:31:55 2022 +1000)

## 0.9.0 - Supports mock servers from plugins

* 345b0011 - feat: support mock servers provided from plugins (Ronald Holshausen, Mon Mar 21 15:59:46 2022 +1100)

## 0.8.6 - Maintenance Release


## 0.8.5 - Bugfix Release

* c2089645 - fix: log crate version must be fixed across all crates (including plugin driver) (Ronald Holshausen, Fri Jan 14 16:10:50 2022 +1100)

## 0.8.4 - Maintenance Release


## 0.8.3 - Maintenance Release


## 0.8.2 - Maintenance Release

* cba3f08e - feat: add metrics events for Pact-Rust consumer tests (Ronald Holshausen, Tue Dec 14 16:20:40 2021 +1100)
* fc5be202 - fix: update to latest driver crate (Ronald Holshausen, Tue Nov 16 16:19:02 2021 +1100)

## 0.8.1 - Add plugin support to FFI functions


## 0.8.0 - Pact V4 release

* 75dd211c - feat: update readme with plugin example (Ronald Holshausen, Thu Oct 21 11:53:52 2021 +1100)
* be6c02b1 - feat: update readme with sync req/res message examples (Ronald Holshausen, Thu Oct 21 11:18:41 2021 +1100)
* e6610312 - feat: update readme with sync req/res message examples (Ronald Holshausen, Thu Oct 21 11:15:05 2021 +1100)
* 3b7aee5f - feat: update tests and docs with sync req/res message examples (Ronald Holshausen, Thu Oct 21 10:28:08 2021 +1100)
* 1427aa33 - feat: update tests and docs with message examples (Ronald Holshausen, Wed Oct 20 16:49:29 2021 +1100)

## 0.8.0-beta.3 - Bugfix Release

* df67b723 - fix: async message builder was not setting the pact plugin config correctly (Ronald Holshausen, Tue Oct 19 17:44:35 2021 +1100)
* 918e5beb - fix: update to latest models and plugin driver crates (Ronald Holshausen, Tue Oct 19 17:09:48 2021 +1100)

## 0.8.0-beta.2 - Support matching synchronous request/response messages


## 0.8.0-beta.1 - Support consumer tests with synchronous messages (Protobuf)

* d0bfb8a8 - feat: Support consumer tests with synchronous messages (Ronald Holshausen, Tue Oct 12 15:51:08 2021 +1100)
* 35ff0993 - feat: record the version of the lib that created the pact in the metadata (Ronald Holshausen, Tue Oct 12 14:52:43 2021 +1100)

## 0.8.0-beta.0 - Plugin support with consumer tests

* 9fd9e652 - feat: do no write empty comments + added consumer version to metadata (Ronald Holshausen, Thu Sep 30 17:40:56 2021 +1000)
* df715cd5 - feat: support native TLS. Fixes #144 (Matt Fellows, Mon Sep 20 13:00:33 2021 +1000)
* ee498dce - feat: consumer builders need to populate the interaction config from the plugins (Ronald Holshausen, Thu Sep 9 08:49:54 2021 +1000)
* 8bcd1c7e - fix: min/max type matchers must not apply the limits when cascading (Ronald Holshausen, Sun Aug 8 15:50:40 2021 +1000)
* 084ab46b - feat: Copied pact_mockserver_ffi to pact_ffi (Ronald Holshausen, Sat Jul 10 16:24:29 2021 +1000)
* be604cce - feat: add date-time matcher to consumer DSL (Ronald Holshausen, Wed Jun 2 15:19:06 2021 +1000)
* b4e26844 - fix: reqwest is dyn linked to openssl by default, which causes a SIGSEGV on alpine linux (Ronald Holshausen, Tue Jun 1 14:21:31 2021 +1000)

## 0.7.8 - Bugfixes + support native TLS certs

* df715cd5 - feat: support native TLS. Fixes #144 (Matt Fellows, Mon Sep 20 13:00:33 2021 +1000)
* 8bcd1c7e - fix: min/max type matchers must not apply the limits when cascading (Ronald Holshausen, Sun Aug 8 15:50:40 2021 +1000)

## 0.7.7 - Bugfix Release

* 084ab46b - feat: Copied pact_mockserver_ffi to pact_ffi (Ronald Holshausen, Sat Jul 10 16:24:29 2021 +1000)
* be604cce - feat: add date-time matcher to consumer DSL (Ronald Holshausen, Wed Jun 2 15:19:06 2021 +1000)
* b4e26844 - fix: reqwest is dyn linked to openssl by default, which causes a SIGSEGV on alpine linux (Ronald Holshausen, Tue Jun 1 14:21:31 2021 +1000)

## 0.7.6 - V4 features + DSL enhancements

* ffbcaf5 - feat: Added header_from_provider_state and path_from_provider_state (Rob Caiger, Mon May 24 13:54:16 2021 +0100)

## 0.7.5 - mock server metrics

* 5a529fd - feat: add ability of mock server to expose metrics #94 (Ronald Holshausen, Sun Mar 14 11:41:16 2021 +1100)

## 0.7.4 - Use a file system lock when merging pact files

* 9976e80 - feat: added read locks and a mutex guard to reading and writing pacts (Ronald Holshausen, Mon Feb 8 11:58:52 2021 +1100)

## 0.7.3 - Updated dependencies


## 0.7.2 - Upgrade Tokio to 1.0


## 0.7.1 - support generators associated with array contains matcher variants

* beb1c03 - fix: cleanup compiler warning (Ronald Holshausen, Thu Dec 31 14:41:09 2020 +1100)

## 0.7.0 - Update to latest matching and mock server crates

* 13976f5 - fix: failing pact_consumer build (Ronald Holshausen, Thu Oct 15 12:00:09 2020 +1100)
* 2fb0c6e - fix: fix the build after refactoring the pact write function (Ronald Holshausen, Wed Oct 14 11:07:57 2020 +1100)
* 29ba743 - feat: add a mock server config struct (Ronald Holshausen, Thu Sep 24 10:30:59 2020 +1000)

## 0.6.2 - Updated XML Matching


## 0.6.1 - Bugfix Release

* a45d0c3 - fix: FFI mismatch json should have the actual values as UTF-8 string not bytes #64 (Ronald Holshausen, Thu Apr 30 11:16:25 2020 +1000)
* 6ff9c33 - fix: ignore flakey test (Matt Fellows, Tue Mar 3 12:14:08 2020 +1100)

## 0.6.0 - Convert to async/await


## 0.5.3 - Bugfix Release

* 19e8ced - fix: cleanup env var and set tests to not run in parallel on CI #54 (Ronald Holshausen, Sat Dec 14 16:08:56 2019 +1100)
* b5474b4 - fix: set the path to the generated pact file #54 (Ronald Holshausen, Sat Dec 14 15:46:37 2019 +1100)
* d4dd39f - fix: repeat the test 3 times #54 (Ronald Holshausen, Sat Dec 14 15:30:01 2019 +1100)
* bc044be - fix: check the size of the merged pact file #54 (Ronald Holshausen, Sat Dec 14 15:25:33 2019 +1100)
* a660b87 - fix: correct pact merging to remove duplicates #54 (Ronald Holshausen, Sat Dec 14 15:06:30 2019 +1100)

## 0.5.2 - Fix dependency versions

* eef3d97 - feat: added some tests for publishing verification results to the pact broker #44 (Ronald Holshausen, Sun Sep 22 16:44:52 2019 +1000)
* 1110b47 - feat: implemented publishing verification results to the pact broker #44 (Ronald Holshausen, Sun Sep 22 13:53:27 2019 +1000)

## 0.5.1 - support headers with multiple values

* f0c0d07 - feat: support headers with multiple values (Ronald Holshausen, Sat Aug 10 17:01:10 2019 +1000)

## 0.5.0 - Upgrade to non-blocking Hyper 0.12

* 1e0c65b - fix: doc tests with Into trait fail to link with Rust beta 1.27.0 (Ronald Holshausen, Sun May 13 15:26:36 2018 +1000)
* a5588dc - feat: Allow the directory pacts are written to to be overriden in consumer tests #21 (Ronald Holshausen, Sun Apr 8 15:20:38 2018 +1000)

## 0.4.0 - First V3 specification release


## 0.3.1 - Converted OptionalBody::Present to take a Vec&lt;u8&;gt;


## 0.3.0 - Improved Consumer DSL


## 0.2.0 - V2 implementation


## 0.1.0 - V1.1 specification implementation


## 0.0.0 - First Release
