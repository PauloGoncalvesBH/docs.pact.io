---
title: pact_verifier_cli
custom_edit_url: https://github.com/pact-foundation/pact-reference/edit/master/rust/pact_verifier_cli/CHANGELOG.md
---
<!-- This file has been synced from the pact-foundation/pact-reference repository. Please do not edit it directly. The URL of the source file can be found in the custom_edit_url value above -->

## 0.9.9 - Bugfix Release

* 73ae0ef0 - fix: Upgrade reqwest to 0.11.10 to resolve #156 (Ronald Holshausen, Wed Apr 13 13:31:55 2022 +1000)
* 345b0011 - feat: support mock servers provided from plugins (Ronald Holshausen, Mon Mar 21 15:59:46 2022 +1100)
* f709528d - fix: rust/pact_verifier_cli/Dockerfile to reduce vulnerabilities (snyk-bot, Thu Mar 17 22:19:46 2022 +0000)

## 0.9.8 - Custom headers + Date-Time expression parser

* 79324802 - feat: add support for custom headers via the verifier CLI #182 (Ronald Holshausen, Mon Feb 28 15:22:47 2022 +1100)
* 74bd4531 - feat: add support for custom headers with the verifier FFI calls #182 (Ronald Holshausen, Mon Feb 28 13:58:46 2022 +1100)

## 0.9.7 - Bugfixes + added JSON report option

* 5ecf70a7 - feat: enable ANSI console output on Windows (Ronald Holshausen, Mon Jan 31 11:02:03 2022 +1100)
* d0fa29dc - feat: add json output to the verifier CLI (Ronald Holshausen, Fri Jan 28 15:21:17 2022 +1100)
* bf152233 - feat: Capture all the results from the verification process (Ronald Holshausen, Fri Jan 28 11:28:38 2022 +1100)
* 5f148cdd - feat: capture all the output from the verifier (Ronald Holshausen, Thu Jan 27 16:08:02 2022 +1100)
* f5aa34ea - Merge pull request #175 from pact-foundation/feat/fix-provider-timeout-value-validation (Ronald Holshausen, Thu Jan 27 13:41:56 2022 +1100)
* 0ef3fb98 - fix: provider request timeout should be > 16bit integers. Fixes https://github.com/pact-foundation/pact-js/issues/761 (Matt Fellows, Wed Jan 26 22:12:35 2022 +1100)

## 0.9.6 - Maintenance Release

* c2089645 - fix: log crate version must be fixed across all crates (including plugin driver) (Ronald Holshausen, Fri Jan 14 16:10:50 2022 +1100)

## 0.9.5 - Bugfix Release


## 0.9.5 - Bugfix Release

* c97f5d1a - fix: shutdown the tokio reactor correctly when there is an error (Ronald Holshausen, Wed Dec 15 16:28:37 2021 +1100)

## 0.9.4 - Bugfix Release

* 00a00461 - fix: add a small delay at the end of validation to allow async tasks to finish (Ronald Holshausen, Wed Dec 15 15:37:30 2021 +1100)

## 0.9.3 - Add metrics for provider verification

* f8042d6b - feat: add metrics event for provider verification (Ronald Holshausen, Tue Dec 14 17:29:44 2021 +1100)

## 0.9.2 - Bugfix Release


## 0.9.1 - Fix for branches and consumer version selectors

* df23ba3d - fix: allow multiple consumer version selectors (Matt Fellows, Mon Nov 15 14:28:04 2021 +1100)
* 0af18303 - fix: add missing provider-branch to verifier CLI (Ronald Holshausen, Mon Nov 8 11:40:05 2021 +1100)

## 0.9.0 - Pact V4 release


## 0.9.0-beta.0 - Pact Plugins Support

* 918e5beb - fix: update to latest models and plugin driver crates (Ronald Holshausen, Tue Oct 19 17:09:48 2021 +1100)

## 0.8.8 - support native TLS certs

* df715cd5 - feat: support native TLS. Fixes #144 (Matt Fellows, Mon Sep 20 13:00:33 2021 +1000)

## 0.8.7 - Bugfix Release


## 0.8.6 - Bugfix Release

* 0d5ec68a - feat: copied verfier_ffi crate to pact_ffi (Ronald Holshausen, Sat Jul 10 16:54:28 2021 +1000)
* a835e684 - feat: support message metadata in verifications (Matt Fellows, Sun Jul 4 21:02:35 2021 +1000)
* e8d6d844 - fix: pact_verifier_cli was printing the version from the FFI crate (Ronald Holshausen, Sat Jun 5 14:43:38 2021 +1000)
* 2f678213 - feat: initial prototype of a pact file verifier (Ronald Holshausen, Thu Jun 3 14:56:16 2021 +1000)

## 0.8.5 - V4 features + updated Tokio to 1.0

* 2ebeef9 - fix: pact_verifier_cli needs to use Tokio 0.2 (Ronald Holshausen, Tue Jan 5 16:24:29 2021 +1100)

## 0.8.4 - TLS support + FFI support

* 484b747 - fix: verify interaction was blocking the thread (Ronald Holshausen, Mon Jan 4 17:12:38 2021 +1100)
* 6cec6c7 - feat: allow https scheme and ability to disable ssl verification (Matt Fellows, Thu Dec 31 12:10:57 2020 +1100)

## 0.8.3 - Bugfix Release


## 0.8.2 - Support Pacts for Verification API


## 0.8.1 - arrayContains matcher + text/xml content type


## 0.8.0 - Supports verifying Message Pacts


## 0.7.1 - implemented provider state generator


## 0.7.0 - Updated XML Matching

* fe74376 - feat: implemented publishing provider tags with verification results #57 (Ronald Holshausen, Sun Mar 8 18:37:21 2020 +1100)
* 9f3ad74 - fix: docker build now requires libclang system library (Ronald Holshausen, Fri Sep 27 17:14:05 2019 +1000)

## 0.6.1 - Bugfix + Oniguruma crate for regex matching


## 0.6.0 - Publishing verification results

* 1110b47 - feat: implemented publishing verification results to the pact broker #44 (Ronald Holshausen, Sun Sep 22 13:53:27 2019 +1000)

## 0.5.1 - Use reqwest for better HTTP/S support, support headers with multiple values

* dac8ae1 - feat: support authentication when fetching pacts from a pact broker (Ronald Holshausen, Sun Aug 11 13:57:29 2019 +1000)
* e007763 - feat: support bearer tokens when fetching pacts from URLs (Ronald Holshausen, Sun Aug 11 13:21:17 2019 +1000)
* 0dd10e6 - fix: docker release script (Ronald Holshausen, Sat Jul 27 18:02:11 2019 +1000)

## 0.5.0 - Upgrade to non-blocking Hyper 0.12

* 3c33294 - fix: Only print errors in the CLI to STDERR #28 (Ronald Holshausen, Sun Apr 8 15:57:56 2018 +1000)
* 386ab52 - fix: corrected the release scripts to check for a version parameter (Ronald Holshausen, Sun Apr 8 13:44:57 2018 +1000)
* 9d24b7e - fix: corrected the docker build for the verifier cli #14 (Ronald Holshausen, Sun Apr 8 13:39:29 2018 +1000)
* 4b8fb64 - fix: verification CLI was reporting incorrect pact specification version (Ronald Holshausen, Sun Apr 8 13:12:45 2018 +1000)

## 0.4.0 - First V3 specification release


## 0.3.0 - Backported matching rules from V3 branch


## 0.2.0 - V2 specification implementation


## 0.1.0 - V1.1 specification implementation


## 0.0.0 - First Release
