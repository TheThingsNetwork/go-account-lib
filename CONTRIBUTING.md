# Contributing to The Things Network Stack

Thank you for your interest in building this thing together with us. We're really happy with our active community and are glad that you're a part of it. There are many ways to contribute to our project, but given the fact that you're on Github looking at the code for The Things Network Stack, you're probably here for one of the following reasons:

* **Requesting a new feature**: If you have a great idea or think some functionality is missing, we want to know! The only thing you have to do for that is to [create an issue](https://github.com/TheThingsNetwork/go-account-lib/issues) if it doesn't exist yet. Please give a detailed description of the functionality you would want, and why it would be nice to have it. Also let us know if you can help us build it.
* **Reporting an issue**: If you notice that a component of the Things Network Stack is not behaving as it should, there may be a bug in our systems. In this case you should [create an issue](https://github.com/TheThingsNetwork/go-account-lib/issues) if it doesn't exist yet. For really sensitive issues, you can [contact us directly](#security-issues).
* **Implementing a new feature or fixing a bug**: If you see an [open issue](https://github.com/TheThingsNetwork/go-account-lib/issues) that you would like to work on, let us know by commenting in the issue. 
* **Writing documentation**: If you see that our documentation is lacking or incorrect, it would be great if you could help us improve it. This will help users and fellow contributors understand better how to work with our stack, and will prevent making mistakes and introducing bugs. Our documentation is spread across a number of places. Code documentation obviously lives together with the code, and is therefore probably in this repository. More general documentation lives in [our `docs` repo](https://github.com/TheThingsNetwork/docs), that is published to our [official documentation pages](https://www.thethingsnetwork.org/docs).

If you'd like to contribute by writing code, you'll find [here](https://github.com/TheThingsNetwork/go-account-lib/README.md) how to set up your development environment. We also have some guidelines that describe how to make contributions that are consistent our way of working.

+ [Git branching workflow](#branching)
+ [Commit conventions](#commit)
+ [Coding conventions](#code)

## <a name="branching"></a>Branching

### Naming

All branches shall have one of these names.

- `master`: the default branch. This is a clean branch where reviewed, approved and CI passed pull requests are merged into. Merging to this branch is restricted to project maintainers
- `fix/#-short-name` or `fix/short-name`: refers to a fix, preferably with issue number. The short name describes the bug or issue
- `feature/#-short-name` or `feature/short-name`: (main) feature branch, preferably with issue number. The short name describes the feature
  - `feature/#-short-name-part`: a sub scope of the feature in a separate branch, that is intended to merge into the main feature branch before the main feature branch is merged into `master`
- `issue/#-short-name`: anything else that refers to an issue but is not clearly a fix nor a feature

### Scope

A fix, feature or issue branch should be **small and focused** and should be scoped to a **single specific task**. Do not combine new features and refactoring of existing code.

### Rebasing and Merging

Before feature branches are merged, they shall rebased on top of their target branch. Do not rebase a branch if others are still working on a derived branch.

Interactive rebase (git rebase -i) may be used to rewrite commit messages that do not follow these contribution guidelines

## <a name="commit"></a>Commit Messages

The first line of a commit message is the subject. The commit message may contain a body, separated from the subject by an empty line.

### Subject

The subject contains the concerning component or topic and a concise message in [the imperative mood](https://chris.beams.io/posts/git-commit/#imperative), starting with a capital. The subject may also contain references to issues or other resources.

The component or topic is typically a few characters long and should always be present. Component names are:

- `auth`: Authentication (incl Oauth)
- `app`: Applications management
- `gtw`: Gateways management
- `user`: User management
- `util`: utilities
- `ci`: CI instructions, e.g. Travis file
- `doc`: documentation
- `dev`: other non-functional development changes, e.g. Makefile, .gitignore, editor config
- `all`: changes affecting all code, e.g. primitive types

Changes that affect multiple components can be comma separated.

Good commit messages:
- `doc: doc update for application access `
- `auth,oauth: Fix TLS check`

Make sure that commits are scoped to something meaningful and could, potentially, be merged individually.

### Body

The body may contain a more detailed description of the commit, explaining what it changes and why. The "how" is less relevant, as this should be obvious from the diff.

## <a name="code"></a>Code

### Formatting

We want our code to be consistent across our projects, so we'll have to agree on a number of formatting rules. These rules should usually usually be applied by your editor. Make sure to install the [editorconfig](https://editorconfig.org) plugin for your editor.

Go code can be automatically formatted using the [`gofmt`](https://golang.org/cmd/gofmt/) tool. There are many editor plugins that call `gofmt` when you save your files.

#### General

We use **utf-8**, **LF** line endings, a **final newline** and we **trim whitespace** from the end of the line (except in Markdown).

#### Tabs vs Spaces

Many developers have strong opinions about using tabs vs spaces. We apply the following rules:

- All `.go` files are indented using **tabs**
- The `Makefile` and all `.make` files are indented using **tabs**
- All other files are indented using **two spaces**

#### Line length

- If a line is longer than 80 columns, try to find a "natural" break
- If a line is longer than 120 columns, insert a line break
- In very special cases, longer lines are tolerated

### Linting

We use [`golint`](github.com/golang/lint/golint) to lint `.go` files and [`eslint`](https://eslint.org) to lint `.js` and `.vue` files. These tools should automatically be installed when initializing your development environment.

### Variable naming

Variable names should be short and concise.

We follow the [official go guidelines](https://github.com/golang/go/wiki/CodeReviewComments#variable-names) and try to be consistent with Go standard library as much as possible, everything not defined in the tables below should follow Go standard library naming scheme.

#### Single-word entities

| entity               | name    | example type                                                  |
| :------------------: | :-----: | :-----------------------------------------------------------: |
| context              | ctx     | context.Context                                               |
| mutex                | mu      | sync.Mutex                                                    |
| configuration        | conf    | github.com/TheThingsNetwork/ttn/pkg/config.Config             |
| logger               | logger  | github.com/TheThingsNetwork/ttn/pkg/log.Logger                |
| message              | msg     | github.com/TheThingsNetwork/ttn/api/gateway.UplinkMessage     |
| status               | st      | github.com/TheThingsNetwork/ttn/api/gateway.Status            |
| server               | srv     | github.com/TheThingsNetwork/ttn/pkg/network-server.Server     |
| EUI                  | eui     | github.com/TheThingsNetwork/ttn/pkg/types.DevEUI              |
| ID                   | id      | string                                                        |
| counter              | cnt     | int                                                           |
| gateway              | gtw     |                                                               |
| application          | app     |                                                               |
| end device           | dev     |                                                               |
| user                 | user    |                                                               |

#### 2-word entities

In case both of the words have an implementation-specific meaning, the variable name is the combination of first letter of each word.

In case one of the words specifies the meaning of the variable in a specific language construct context, the variable name is the combination of abbrevations of the words.

But don't over do, the name should still have meaning, for example:

| entity        | name      | example type                                              |
| :-----------: | :-------: | :-------------------------------------------------------: |
| access key    | accessKey | github.com/TheThingsNetwork/go-account-lib/auth/accessKey |
| wait group    | wg        |                                                           |

#### Well-known variable names

These are the names of variables that occur often in the code. Be consistent in naming them, even when their
meaning is obvious from the context.

| entity                          | name    |
| :-----------------------------: | :-----: |
| gateway id                      | gtwID   |
| gateway EUI                     | gtwEUI  |
| application id                  | appID   |
| application EUI                 | appEUI  |
| device id                       | devID   |
| user id                         | userID  |

### Functions

Functions must have a clear role and name. As such they must be type scoped. They only do one thing
on one entity. Non entity-scoped function are allowed as long as they have a real purpose.

#### Naming

The name of the functions must indicate what they do on which type and consistent all around the
library.
 
- No shortened form of any entity nor actions.
- Start with one of the verb followed by the entity name.

#### Entity required functions

Every entity must have at least this four functions implemented, `Register`, `Edit`, `Delete`, `Get`.

| entity    | Register          | Edit          | Delete        | Get           |
| :-------: | :---------------: | :-----------: | :-----------: | :-----------: |
| User      | RegisterUser      | EditUser      | DeleteUser    | GetUser       |
| Gateway   | RegisterGateway   | EditGateway   | DeleteGateway | GetGateway    |

#### Entity Collection functions

If a collection of entity is made it also must implement functions, `List`, `Stream`.

| entity Collection     | List          | Stream            |
| :-------------------: | :-----------: | :---------------: |
| Users                 | ListUsers     | StreamUsers       |
| Gateway               | ListGateways  | StreamGateways    |

#### Entity attributes

When accessing an attributes of an entity a function should respect this format: `VerbEntityAttributeAction`.
Where the `Verb` is one of those `Edit`, `Delete`, `Get`

| entity    | attribute | Get                   | Edit                  |
| :-------: | :-------: | :-------------------: | :-------------------: |
| User      | Profile   | GetUserProfile        | EditUserProfile       |
| Gateway   | Altitude  | GetGatewayAltitude    | EditGatewayAltitude   |

## <a name="security-issues"></a>Security Issues

We do our utmost best to build secure systems, but we're human too, so we sometimes make mistakes. If you find any vulnerability in our systems, please contact us directly. We can be reached on Slack, by email and a number of other communication platforms.

- Johan Stokking - [keybase.io/johanstokking](https://keybase.io/johanstokking) `5D21A572255E61C6`
- Hylke Visser - [keybase.io/htdvisser](https://keybase.io/htdvisser) `A115FF80DC8A2270`
- Romeo Van Snick - [keybase.io/romeovs](https://keybase.io/romeovs) `FECE5D23EDDFFF1E`
- Eric Gourlaouen - [keybase.io/ericgo](https://keybase.io/ericgo) `BB6517CB9AA889B4`

Our email addresses follow the pattern `<firstname>@thethingsnetwork.org`.