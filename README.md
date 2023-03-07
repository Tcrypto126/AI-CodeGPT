# CodeGPT

[![Lint and Testing](https://github.com/appleboy/CodeGPT/actions/workflows/testing.yml/badge.svg?branch=main)](https://github.com/appleboy/CodeGPT/actions/workflows/testing.yml)
[![codecov](https://codecov.io/gh/appleboy/CodeGPT/branch/main/graph/badge.svg)](https://codecov.io/gh/appleboy/CodeGPT)
[![Go Report Card](https://goreportcard.com/badge/github.com/appleboy/CodeGPT)](https://goreportcard.com/report/github.com/appleboy/CodeGPT)

![cover](./images/cover.png)

A CLI written in [Go](https://go.dev) language that writes git commit messages for you using ChatGPT AI (gpt-3.5-turbo model) and automatically installs a [git prepare-commit-msg hook](https://git-scm.com/docs/githooks).

## Installation

The pre-compiled binaries can be downloaded from [release page](https://github.com/appleboy/CodeGPT/releases).

On linux AMD64

```sh
wget -c https://github.com/appleboy/CodeGPT/releases/download/v0.0.4/CodeGPT-0.0.4-linux-amd64 -O codegpt
```

On macOS (Intel amd64)

```sh
wget -c https://github.com/appleboy/CodeGPT/releases/download/v0.0.4/CodeGPT-0.0.4-darwin-amd64 -O codegpt
```

On macOS (Apple arm64)

```sh
wget -c https://github.com/appleboy/CodeGPT/releases/download/v0.0.4/CodeGPT-0.0.4-darwin-arm64 -O codegpt
```

On Windows (AMD64)

```sh
wget -c https://github.com/appleboy/CodeGPT/releases/download/v0.0.4/CodeGPT-0.0.4-windows-amd64.exe -O codegpt.exe
```

Change the binary permissions to `755` and copy the binary to the system bin directory. Use the `codegpt` command as shown below.

```sh
$ codegpt version
version: v0.0.4 commit: 359a48a
```

## Setup

Please first create your OpenAI API Key. The [OpenAI Platform](https://platform.openai.com/account/api-keys) allows you to generate a new API Key.

![register](./images/register.png)

```sh
codegpt config set openai.api_key sk-xxxxxxx
```

This will create a `.codegpt.yaml` file in your home directory ($HOME/.config/codegpt/.codegpt.yaml).

## Usage

There are two methods for generating a commit message using the `codegpt` command. The first is CLI mode, and the second is Git Hook.

### CLI mode

You can call `codegpt` directly to generate a commit message for your staged changes:

```sh
git add <files...>
codegpt commit
```

The commit message is shown below.

```sh
Summarize the commit message use gpt-3.5-turbo model
We are trying to summarize a git diff
We are trying to summarize a title for pull request
================Commit Summary====================

Add OpenAI integration and CLI usage instructions

- Add download links for pre-compiled binaries for various platforms
- Add instructions for setting up OpenAI API key
- Add CLI usage instructions for generating commit messages with `codegpt`
- Add references to OpenAI Chat completions documentation and introducing ChatGPT and Whisper APIs

==================================================
Write the commit message to .git/COMMIT_EDITMSG file
```

or translate all git commit messages into a different language (`Traditional Chinese`, `Simplified Chinese` or `Japanese`)

```sh
codegpt commit --lang zh-tw
```

Consider the following outcome:

```sh
Summarize the commit message use gpt-3.5-turbo model
We are trying to summarize a git diff
We are trying to summarize a title for pull request
We are trying to translate a git commit message to Traditional Chineselanguage
================Commit Summary====================
增加發布頁面改進和CLI模式說明。

- 在發布頁面上增加了不同系統的預編譯二進制文件。
- 提供設置OpenAI API密鑰的說明。
- 提供使用CLI模式生成暫存更改的提交消息的說明。

==================================================
Write the commit message to .git/COMMIT_EDITMSG file
```

### Git hook

You can also use the prepare-commit-msg hook to integrate `codegpt` with Git. This allows you to use Git normally and edit the commit message before committing.

#### Install

You want to install the hook in the Git repository:

```sh
codegpt hook install
```

#### Uninstall

You want to remove the hook from the Git repository:

```sh
codegpt hook uninstall
```

Stage your files and commit after installation:

```sh
git add <files...>
git commit
```

`codegpt` will generate the commit message for you and pass it back to Git. Git will open it with the configured editor for you to review/edit it. Then, to commit, save and close the editor!

```sh
$ git commit
Summarize the commit message use gpt-3.5-turbo model
We are trying to summarize a git diff
We are trying to summarize a title for pull request
================Commit Summary====================

Improve user experience and documentation for OpenAI tools

- Add download links for pre-compiled binaries
- Include instructions for setting up OpenAI API key
- Add a CLI mode for generating commit messages
- Provide references for OpenAI Chat completions and ChatGPT/Whisper APIs

==================================================
Write the commit message to .git/COMMIT_EDITMSG file
[main 6a9e879] Improve user experience and documentation for OpenAI tools
 1 file changed, 56 insertions(+)
```

## Reference

* [OpenAI Chat completions documentation](https://platform.openai.com/docs/guides/chat).
* [Introducing ChatGPT and Whisper APIs](https://openai.com/blog/introducing-chatgpt-and-whisper-apis)
