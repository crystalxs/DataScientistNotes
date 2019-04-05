# Gitbook

> https://toolchain.gitbook.com/

## Install

```shell
# requirement NodeJS v4.0.0 and above
node -v
npm install gitbook-cli -g
```

###`gitbook-cli` V.S. `gitbook`

`gitbook` is a command line tool (and Node.js library) for building beautiful books using GitHub/Git and Markdown (or AsciiDoc).

`gitbook-cli` is an utility to install and use multiple versions of GitBook on the same system. It will automatically install the required version of GitBook to build a book.

##Preview Book

```shell
gitbook serve # localhost:4000
gitbook build
gitbook build --gitbook=2.0.1
```

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

> More detail for config http://gitbook.zhangjikai.com/settings.html

##Ignoring files & folders

GitBook will read the `.gitignore`, `.bookignore` and `.ignore` files to get a list of files and folders to skip. The format inside those files, follows the same convention as `.gitignore`:

```
# This is a comment

# Ignore the file test.md
test.md

# Ignore everything in the directory "bin"
bin/*
```
