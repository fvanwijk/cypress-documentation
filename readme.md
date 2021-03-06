# Cypress Documentation

The code for Cypress's Documentation, Guides, and API.

* https://docs.cypress.io

## Introduction

The documents in this repo are synchronized remotedly with Readme.io.

`readmeio-sync` provides this functionality. Aka this enables us to commit locally, use commit messages, and know when the hell and who the hell edited the docs!

It does somewhat complicate the process and is not quite as nice as editing `Github Wikis`, but it's still pretty great.

## Getting Started

https://github.com/mobify/readmeio-sync

## Contributing

To make changes to our documentation:

- Make changes **locally** here (in markdown) and then synchronize them **remotely**.

### Working Locally

```shell
npm install
```

You will need to login with your Readme.io credentials before working. You may see an error when trying to upload or clean that looks like this: `throw 'Error: Request failed! (Redirected to login...)'`

Login with your Cypress readme.io account credentials.

```shell
export README_EMAIL=<readmeio_account_email>
export README_PASSWORD=<readmeio_account_password>
```

```shell
# add a new command
npm run add-command <command-name>
# see what add-command will do without changing files
npm run add-command <command-name> -- --dry-run

# remove a command
npm run remove-command <command-name>
# see what remove-command will do without changing files
npm run remove-command <command-name> -- --dry-run
```

```shell
# modify local files
<hack hack hack>

# commit to github
git commit -am 'updated docs'

# deploy changes to readme.io
npm run upload

# clean out deleted files on readme.io
npm run clean
```

### Writing Docs

**Edits should NEVER be made from the Readme.io's web ui**


#### Links

Links are all handled through our [cypress.on](https://github.com/cypress-io/cypress-on) api.

To link to a page on Guides:
```md
[Installing and Running](https://on.cypress.io/guides/$slug)
```

To link to a page on API:
```md
[and](https://on.cypress.io/api/$slug)
```

#### Creating New Files

When creating new files, each file requires an excerpt and a slug **followed by a newline**:
```md
excerpt: Description at top of page
slug: slug-for-url


```

If you forget the newline, readmeio-sync's upload will not work because of how they are regexing the metadata.
