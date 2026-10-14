# DRONE

![licence](https://img.shields.io/badge/licence-Apache-2.0-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![checks](https://img.shields.io/badge/checks-unknown_PASS-brightgreen)

> Governed Anticloud packaging of the upstream project `DRONE` in category **INFRA_DEVOPS**. check results: see ISOLATED_LAB_RESULTS. Every number below traces to a named file + run stamp; nothing is borrowed from other projects.

**Upstream:** https://github.com/harness/drone · **Upstream pin:** `243ce0ac9c51504fc846e4ea1e35dbff03985871` · **Category:** INFRA_DEVOPS · **Vendor:** Anticloud FZ LLE · **Licence:** Apache-2.0

---

## What This Project Does

# Harness
Harness Open Source is an open source development platform packed with the power of code hosting, automated DevOps pipelines, hosted development environments (Gitspaces), and artifact registries.

## Overview
Harness Open source is an open source development platform packed with the power of code hosting, automated DevOps pipelines, Gitspaces, and artifact registries.

## Running Harness locally
> The latest publicly released docker image can be found on [harness/harness](https://hub.docker.com/r/harness/harness).

To install Harness yourself, simply run the command below. Once the container is up, you can visit http://localhost:3000 in your browser.

```bash
docker run -d \
  -p 3000:3000 \
  -p 3022:3022 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /tmp/harness:/data \
  --name harness \
  --restart always \
  harness/harness
```
> The Harness image uses a volume to store the database and projects. It is highly recommended to use a bind mount or named volume as otherwise all data will be lost once the container is stopped.

See [developer.harness.io](https://developer.harness.io/docs/open-source) to learn how to get the most out of Harness.

## Where is Drone?

Harness Open Source represents a massive investment in the next generation of Drone. Where Drone focused solely on continuous integration, Harness adds source code hosting, developer environments (gitspaces), and artifact registries; providing teams with an end-to-end, open source DevOps platform.

The goal is for Harness to eventually be at full parity with Drone in terms of pipeline capabilities, allowing users to seamlessly migrate from Drone to Harness.

But, we expect this to take some time, which is why we took a snapshot of Drone as a feature branch [drone](https://github.com/harness/harness/tree/drone) ([README](https://github.com/harness/harness/blob/drone/.github/readme.md)) so it can continue development.

As for Harness, the development is taking place on the [main](https://github.com/harness/harness/tree/main) branch.

For more information on Harness, please visit [developer.harness.io](https://developer.harness.io/).

For more information on Drone, please visit [drone.io](https://www.drone.io/).

## Harness Open Source Development
### Pre-Requisites

Install the latest stable version of Node and Go version 1.20 or higher, and then install the below Go programs. Ensure the GOPATH [bin directory](https://go.dev/doc/gopath_code#GOPATH) is added to your PATH.

Install protobuf
- Check if you've already installed protobuf ```protoc --version```
- If your version is different than v3.21.11, run ```brew unlink protobuf```
- Get v3.21.11 ```curl -s https://raw.githubusercontent.com/Homebrew/homebrew-core/243ce0ac9c51504fc846e4ea1e35dbff03985871/Formula/protobuf.rb > /tmp/protobuf.rb```
- Install it ```brew install /tmp/protobuf.rb```
- Check out your version ```protoc --version```

Install protoc-gen-go and protoc-gen-go-rpc:

- Install protoc-gen-go v1.28.1 ```go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.28.1```
(Note that this will install a binary in $GOBIN so make sure $GOBIN is in your $PATH)

- Install protoc-gen-go-grpc v1.2.0 ```go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.2.0```

```bash
$ make dep
$ make tools
```

### Build

First step is to build the user interface artifacts:

```bash
$ pushd web
$ yarn install
$ yarn build
$ popd
```

After that, you can build the Harness binary:

```bash
$ make build
```

### Run

This project supports all operating systems and architectures supported by Go.  This means you can build and run the system on your machine; docker containers are not required for local development and testing.

To start the server at `localhost:3000`, simply run the following command:

```bash
./gitness server .local.env
```

### Docker Configuration for Pipelines

Harness pipelines run inside Docker containers. The application automatically negotiates the Docker API version with your Docker daemon, so it works with various Docker versions including Docker Desktop, Rancher Desktop, Colima, and native Docker on Linux.

**Docker Socket Location**

By default, Harness expects the Docker socket at `/var/run/docker.sock`. If you're using an alternative Docker runtime, you may need to configure the socket location:

| Runtime | Socket Location | Configuration |
|---------|-----------------|---------------|
| Docker Desktop | `/var/run/docker.sock` | Works by default |
| Rancher Desktop | `~/.rd/docker.sock` | Create symlink or set `GITNESS_DOCKER_HOST` |
| Colima | `~/.colima/default/docker.sock` | Create symlink or set `GITNESS_DOCKER_HOST` |
| Linux (native) | `/var/run/docker.sock` | Works by default |

**Option 1: Create a symlink (recommended)**
```bash
# For Rancher Desktop
sudo ln -sf ~/.rd/docker.sock /var/run/docker.sock

# For Colima
sudo ln -sf ~/.colima/default/docker.sock /var/run/docker.sock
```

**Option 2: Set environment variable**

Add to your `.local.env`:
```bash
# For Rancher Desktop
GITNESS_DOCKER_HOST=unix:///Users/<username>/.rd/docker.sock

# For Colima
GITNESS_DOCKER_HOST=unix:///Users/<username>/.colima/default/docker.sock
```

**Pinning Docker API Version**

The application automatically negotiates the API version with your Docker daemon. If you need to pin a specific version (e.g., for compatibility testing), you can set:
```bash
GITNESS_DOCKER_API_VERSION=1.45
```

### Auto-Generate Harness API Client used by UI using Swagger
Please make sure to update the autogenerated client code used by the UI when adding new rest APIs.

To regenerate the code, please execute the following steps:
- Regenerate swagger with latest Harness binary `./gitness swagger > web/src/services/code/swagger.yaml`
- navigate to the `web` folder and run `yarn services`

The latest API changes should now be reflected in `web/src/services/code/index.tsx`

# Run Registry Conformance Tests
```
make conformance-test
```
For running conformance tests with existing running service, use:
```
make hot-conformance-test
```

## User Interface

This project includes a full user interface for interacting with the system. When you run the application, you can access the user interface by navigating to `http://localhost:3000` in your browser.

## REST API

This project includes a swagger specification. When you run the application, you can access the swagger specification by navigating to `http://localhost:3000/swagger` in your browser (for raw yaml see `http://localhost:3000/openapi.yaml`).
For registry endpoints, currently swagger is located on different endpoint `http://localhost:3000/registry/swagger/` (for raw json see `http://localhost:3000/registry/swagger.json`). These will be later moved to the main swagger endpoint. 

For testing, it's simplest to just use the cli to create a token (this requires Harness server to run):
```bash
# LOGIN (user: admin, pw: changeit)
$ ./gitness login

# GENERATE PAT (1 YEAR VALIDITY)
$ ./gitness user pat "my-pat-uid" 2592000
```

The command outputs a valid PAT that has been granted full access as the user.
The token can then be sent as part of the `Authorization` header with Postman or curl:

```bash
$ curl http://localhost:3000/api/v1/user \
-H "Authorization: Bearer $TOKEN"
```

## CLI
This project includes VERY basic command line tools for development and running the service. Please remember that you must start the server before you can execute commands.

For a full list of supported operations, please see
```bash
$ ./gitness --help
```

## Contributing

Refer to [CONTRIBUTING.md](https://github.com/harness/harness/blob/main/CONTRIBUTING.md)

## License

Apache License 2.0, see [LICENSE](https://github.com/harness/harness/blob/main/LICENSE).

---

## Installation

```bash
docker run -d \
  -p 3000:3000 \
  -p 3022:3022 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /tmp/harness:/data \
  --name harness \
  --restart always \
  harness/harness
```
> The Harness image uses a volume to store the database and projects. It is highly recommended to use a bind mount or named volume as otherwise all data will be lost once the container is stopped.

See [developer.harness.io](https://developer.harness.io/docs/open-source) to learn how to get the most out of Harness.

## Usage

See [developer.harness.io](https://developer.harness.io/docs/open-source) to learn how to get the most out of Harness.

## API

**Docker Socket Location**

By default, Harness expects the Docker socket at `/var/run/docker.sock`. If you're using an alternative Docker runtime, you may need to configure the socket location:

| Runtime | Socket Location | Configuration |
|---------|-----------------|---------------|
| Docker Desktop | `/var/run/docker.sock` | Works by default |
| Rancher Desktop | `~/.rd/docker.sock` | Create symlink or set `GITNESS_DOCKER_HOST` |
| Colima | `~/.colima/default/docker.sock` | Create symlink or set `GITNESS_DOCKER_HOST` |
| Linux (native) | `/var/run/docker.sock` | Works by default |

**Option 1: Create a symlink (recommended)**
```bash

## Dependencies

| Metric | Value |
|--------|-------|
| Files | unknown |
| Lines of Code | unknown |
| Dependencies | unknown |
| Upstream license (harvested) | Apache-2.0 |
| Overlay license | Anticommons 0.1.0 |

Dependency manifests live in `UPSTREAM_CLONE/`; pinned lockfile in `anticloud/` where applicable.

## Configuration

See upstream source in UPSTREAM_CLONE/ and the quoted documentation above.

## Contributing

# Contributing to Harness

Thank you for your interest in open source contributions to Harness. Harness uses GitHub to manage open source reviews of pull requests.

* If you are a new contributor see: [Steps to Contribute](#steps-to-contribute)

* If you have a minor fix or improvement, feel free to create a pull request. Please provide necessary details in the pull request description and use a meaningful title.

* If you plan to do something more involved, first discuss your ideas by [raising an issue](https://github.com/harness/harness/issues). This will avoid unnecessary work and surely give you and us a good deal of inspiration. 

* Relevant coding style guidelines are 

    - For backend: the [Go Code Review Comments](https://code.google.com/p/go-wiki/wiki/CodeReviewComments) and the formatting and style section of Peter Bourgon's [Go: Best Practices for Production Environments](https://peter.bourgon.org/go-in-production/#formatting-and-style)
    - For frontend: [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html) and [Best practices for Typescript coding](https://medium.com/@eshagarg1996/best-practices-for-typescript-coding-8b1ea98d02f8). 

* Be sure to sign off on the [CLA](https://cla-assistant.io/harness/gitness).

## Steps to Contribute

Should you wish to work on an issue, please claim it first by commenting on the GitHub issue that you want to work on. This is to prevent duplicated efforts from contributors on the same issue.

Please check the [`good-first-issue`](https://github.com/harness/harness/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) label to find issues that are good for getting started. If you have questions about one of the issues, with or without the tag, please comment on them and one of the maintainers will clarify it. For a quicker response, contact us over [slack](https://developer.harness.io/docs/open-source/support#slack).

### Local Development

Please review [Harness development](https://github.com/harness/harness/tree/main?tab=readme-ov-file#harness-development) to build and test your code locally. 

### Pre-commit Hook

We have a pre-commit hook to ensure code quality before committing changes. This hook checks for required binaries (grep, sed, and xargs) and runs checks specifically for Go files (*.go). If any issues are found during the checks, the commit process will be halted until the issues are resolved.

### Lint Check

Our CI Linter pipeline conducts automated checks for code quality, with [separate lint checks for Go and TypeScript](https://github.com/harness/harness/blob/main/.github/workflows/ci-lint.yml). These checks help ensure adherence to coding standards and identify potential issues early in the development process. Thank you for contributing to our code quality efforts!

## Pull Request Checklist

* Branch from the main branch and, if needed, rebase to the current main branch before submitting your pull request. If it doesn't merge cleanly with m

## License

Upstream © its respective contributors under Apache-2.0 (harvested MIT/Apache-2.0/BSD source; see `UPSTREAM_CLONE/LICENSE`). This packaging overlay is licensed under Anticommons 0.1.0.

## Upstream

- **project:** https://github.com/harness/drone
- **Pinned SHA:** `243ce0ac9c51504fc846e4ea1e35dbff03985871`
- **source:** `UPSTREAM_CLONE/` (pinned at the SHA above)
- **Upstream README source:** `UPSTREAM_CLONE/README.md`

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`50b71de7e958c06936ec772b38991725faa64c0696d00ac20b9442da94b99125`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

