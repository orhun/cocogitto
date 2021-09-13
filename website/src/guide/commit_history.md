# Managing commit history

`cog` as several subcommands to examine and manipulate your commit history.

## Validate repository history compliance with the specification

Running `cog check` will check your commit history against the conventional commit specification :

```
❯ cog check
No errored commits
```

Let us create an invalid commit :
```shell script
git commit -m "Your Mother Was A Hamster, And Your Father Smelt Of Elderberries"
```

And check our commit history again :
```
❯ cog check
Error: ERROR - Your Mother Was A Hamster, And Your Father Smelt Of Elderberries - (c2bb56)
	cause: Missing commit type separator `:
```

Additionally, you can check your history, starting from the latest tag to HEAD using `from-latest-tag` flag.  
This is useful when your git repo started to use conventional commits from a certain point in history, and you
don't care about editing old commits.

## Rewrite non-compliant commits

Once you have spotted invalid commits you can quickly fix your commit history by running `cog edit`.
This will perform an automatic rebase and let you edit each malformed commit message with your `$EDITOR`
of choice.

**Example :**

`cog edit` will cycle to each malformed commit to rewrite their message : 

```
# Editing commit c2bb56b93821ff34282f322be4d2231f53b9ada8
# Replace this message with a conventional commit compliant one
# Save and exit to edit the next errored commit
Your Mother Was A Hamster, And Your Father Smelt Of Elderberries
```

⚠️ Beware that using `cog edit` will modify your commit history and change the commit SHA of edited commit
and their child.

## Conventional commits git log


`cog log` is like `git log` but it displays additional conventional commit information, such as commit scope,
commit type etc.


[![asciicast](https://asciinema.org/a/ssH4yRSlc28Rb9dHEDN7TowGe.svg)](https://asciinema.org/a/ssH4yRSlc28Rb9dHEDN7TowGe)

You can also filter the log content with the following flags (`cog log --help`) :

- `-B` : display breaking changes only
- `-t` : filter on commit type
- `-a` : filter on commit author
- `-s` : filter on commit scope
- `-e` : ignore errors

Those flag can be combined to achieve complex search in your commit history :

```shell script
cog log --author "Paul Delafosse" "Mike Lubinets" --type feat --scope cli --no-error
```
