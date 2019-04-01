# Gitbook

## Install

```shell
# requirement NodeJS v4.0.0 and above
node -v
npm install gitbook-cli -g
```

##Setup

```shell
gitbook serve # localhost:4000
gitbook build
gitbook build --gitbook=2.0.1
```

## `gitbook-cli` V.S. `gitbook`

`gitbook` is a command line tool (and Node.js library) for building beautiful books using GitHub/Git and Markdown (or AsciiDoc).

`gitbook-cli` is an utility to install and use multiple versions of GitBook on the same system. It will automatically install the required version of GitBook to build a book.

##Useful Command

```shell
gitbook help
gitbook --help # help for gitbook-cli
# list all version
gitbook ls
gitbook ls-remote
gitbook fetch <version>
gitbook update
gitbook uninstall <version>
gitbook build --log=debug
gitbook build --debug
```

##Directory Structure

A basic GitBook usually looks something like this:

```
.
├── book.json
├── README.md
├── SUMMARY.md
├── chapter-1/
|   ├── README.md
|   └── something.md
└── chapter-2/
    ├── README.md
    └── something.md
```

An overview of what each of these does:

| File          | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| `book.json`   | Stores [configuration](https://toolchain.gitbook.com/config.html) data (**optional**) |
| `README.md`   | Preface / Introduction for your book (**required**)          |
| `SUMMARY.md`  | Table of Contents (See [Pages](https://toolchain.gitbook.com/pages.html)) (**optional**) |
| `GLOSSARY.md` | Lexicon / List of terms to annotate (See [Glossary](https://toolchain.gitbook.com/lexicon.html)) (**optional**) |

##Ignoring files & folders

GitBook will read the `.gitignore`, `.bookignore` and `.ignore` files to get a list of files and folders to skip. The format inside those files, follows the same convention as `.gitignore`:

```
# This is a comment

# Ignore the file test.md
test.md

# Ignore everything in the directory "bin"
bin/*
```

### Project integration with subdirectory

For software projects, you can use a subdirectory (like `docs/`) to store the book for the project's documentation. You can configure the [`root` option](https://toolchain.gitbook.com/config.html) to indicate the folder where GitBook can find the book's files:

```
.
├── book.json
└── docs/
    ├── README.md
    └── SUMMARY.md
```

With `book.json` containing:

```
{
    "root": "./docs"
}
=======
Reference: https://toolchain.gitbook.com/setup.html

##### Requirements

Installing GitBook is easy and straightforward. Your system just needs to meet these two requirements:

- NodeJS (v4.0.0 and above is recommended)
- Windows, Linux, Unix, or Mac OS X

##### Install with NPM

The best way to install GitBook is via **NPM**. At the terminal prompt, simply run the following command to install GitBook:

```
$ npm install gitbook-cli -g
```

`gitbook-cli` is an utility to install and use multiple versions of GitBook on the same system. It will automatically install the required version of GitBook to build a book.

##### Create a book

GitBook can setup a boilerplate book:

```
$ gitbook init
```

If you wish to create the book into a new directory, you can do so by running `gitbook init ./directory`

Preview and serve your book using:

```
$ gitbook serve
```

Or build the static website using:

```
$ gitbook build
```

##### Install pre-releases

`gitbook-cli` makes it easy to download and install other versions of GitBook to test with your book:

```
$ gitbook fetch beta
```

Use `gitbook ls-remote` to list remote versions available for install.

##### Debugging

You can use the options `--log=debug` and `--debug` to get better error messages (with stack trace). For example:

```
$ gitbook build ./ --log=debug --debug
