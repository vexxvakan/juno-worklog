# Worklog Juno
## Juno

### Features and Enhancements

-   **Governance module wrapper:** Implemented a custom wrapper for the governance module’s gRPC queries to prevent a known panic when querying now removed proposal types.
   
- **Feemarket Integration**: Forked the x/feemarket from Skip after their deprecation notice. Adjusted it to fully integrate with Juno.

-   **Core improvements:** Various improvements were made while updating to **Cosmos SDK v0.53**. This modernized Juno’s module interactions, making it easier to extend functionality and integrate future features.
    
-   **Implemented Scalar UI & OpenAPI 3.0 and documentation generation:** Replaced the Swagger generation for Juno’s REST endpoints with OpenAPI 3.0 and Scalar as UI package. Available as of v30.0.0 on `<REST_ENDPOINT>:1317`
    
### Bug Fixes

-   **IBC vulnerability patch (ISA-2025-001):** Addressed and patched a critical IBC bug
-   **Governance query panic:** (Also covered by the gov module wrapper above) The root cause of a panic in gov queries was eliminated.
    
### Upgrades

-   **Cosmos SDK & CosmWasm upgrades:** Performed two major upgrades from Cosmos SDK v0.47 to v0.50 and finally **Cosmos SDK v0.53.0** and integrated **CosmWasm v2.0** (WasmVM 2.2+). Brings performance improvements, new features and security fixes from the SDK.
        
### Refactors and Cleanup

-   **Removal of deprecated modules:** Removed deprecated **MEV** module and the associated `x/builder` logic, as well as the unused ICS-08 **Wasm Light Client** implementation.
    
-   **Code modernization:** Refactored significant parts of the application to conform to the latest Cosmos SDK standards.
        
-   **Build and repository chores:** Simplified the **Makefile** and build pipeline – for example, introduced a “mise-en-place” script for version management and environment setup, and reorganized project layouts where needed.
    
### CI and Tooling

-   **Automated cross-repo release workflow:** Added a GitHub Actions workflow that bridges the main Juno repo with the new **juno-std** and **junojs** libraries. Now, when a new Juno version is released, the workflow automatically triggers a rebuild and publish process on all library repos. Get updated Juno bindings before a Juno blockchain upgrade happens so your contracts can be up-to-date on patch day.
    
-   **Enhanced linting and static analysis:** Upgraded **golangci-lint** to v2.1.6 and adjusted lint settings. The code was refactored to satisfy the new lint rules (fixing hundreds of warnings), which improves code quality and consistency.
    
-   **Continuous integration workflows:** Fixed and improved multiple GitHub workflow files. For example, pinned the Go version in the Docker build to avoid environment drift and ensured the test suites and build jobs run reliably on the updated Go version.
    
-   **Release process streamlining:** By integrating tools like **mise-en-place** and **auto-release** scripts, the team can cut a release with minimal manual steps. The changelog generation, version bump, artifact builds, and even drafting the GitHub release notes have been partially automated. This reduces the chance of human error during releases and allowed the quick succession of patch releases (like v28.0.1 and v28.0.2) to address issues faster.
    
## juno-std

### Features

-   **Introduction of Juno standard library:** Created the **juno-std** Rust crate to provide Juno-specific types and utilities when working in Rust and **CosmWasm smart contracts**. It assists contract developers with auto-generated Rust helpers for Juno’s protobuf-defined types and query interfaces.
    
### CI and Automation

-   **Automatic release workflow:** Setup GitHub Actions workflow to **auto-publish juno-std** to Rust’s package registry on every new Juno release. Smart contract developers can simply update their juno-std dependency to the new version right after a new Juno release, getting all updated types immediately.
        
## junojs

### Features

-   **JunoJS TypeScript SDK:** Created **junojs** – a JavaScript/TypeScript library for interacting with the Juno blockchain. Front-end and JS developers can now easily compose and broadcast Juno transactions or query on-chain data without needing to manually handle protobufs or low-level details. It greatly simplifies building web dApps on Juno.
        
-   **NPM distribution:** Published junojs as an NPM package under the `@buildonjuno` scope (`@buildonjuno/junojs`). Developers can install it via any package manager and get started quickly. The package is versioned in tandem with Juno’s releases. By using semantic versioning aligned to chain upgrades, it’s clear to developers which version of junojs to use for a given Juno network version.

### CI and Tooling
    
-   **Automatic release workflow:** Setup GitHub Actions workflow to **auto-publish junojs** to the NPM package registry on every new Juno release.
    
## Upcoming Work and Ideas

-   **Possibly fork Skip’s Connect (**Slinky**) oracle module:** Investigate integrating Skip’s deprecated oracle solution into Juno by forking and adapting it. This would provide Juno with a native price/oracle module for enhanced DeFi and other data capabilities. Comes with a serious maintainability commitment.
    
-   **Possibly replace Tokenfactory with a custom token creator:** Explore implementing a Juno-specific token issuance module to replace Osmosis’ Tokenfactory with more fine-grained control over token creation. Could also make it more flexible.
    
-   **Better endpoints for everything:** Improve node APIs by introducing more robust endpoints for example Websocket and gRPC state streaming, or even GraphQL endpoints. This would make it easier for applications to get real-time data and query the chain in more efficient ways than the current REST/gRPC flow.
    
-   **Add more module wrappers for custom functionality:** Following the pattern of the governance wrapper, create wrappers for other Cosmos SDK modules to customize Juno further. Examples: Bank improvements to let developers disable any token functionality on a fine-grained base (disable token transfers, IBC transfers, Freeze wallets and more on a per token basis).
    
-   **Modernize codebase and improve workflows to onboard new devs:** Continuously refactor and document the codebase to be more approachable. This includes improving developer documentation and streamlining the setup.
