# Dotfiles

My OS X dotfiles.


## How to install

The installation step requires the [XCode Command Line
Tools](https://developer.apple.com/downloads) and may overwrite existing
dotfiles in your HOME directory.

```bash
$ bash -c "$(curl -fsSL raw.github.com/pjeweb/dotfiles/master/bin/dotfiles)"
```

## How to update

You should run the update when:

* You make a change to `~/.dotfiles/git/gitconfig` (the only file that is
  copied rather than symlinked).
* You want to pull changes from the remote repository.
* You want to update Homebrew formulae and Node packages.

Run the dotfiles command:

```bash
$ dotfiles
```

Options:

<table>
    <tr>
        <td><code>-h</code>, <code>--help</code></td>
        <td>Help</td>
    </tr>
    <tr>
        <td><code>-l</code>, <code>--list</code></td>
        <td>List of additional applications to install</td>
    </tr>
    <tr>
        <td><code>--no-packages</code></td>
        <td>Suppress package updates</td>
    </tr>
    <tr>
        <td><code>--no-sync</code></td>
        <td>Suppress pulling from the remote repository</td>
    </tr>
</table>


## Features

### Custom OS X defaults

Custom OS X settings can be applied during the `dotfiles` process. They can
also be applied independently by running the following command:

```bash
$ osxdefaults
```

### Bootable backup-drive script

These dotfiles include a script that uses `rync` to incrementally back up your
data to an external, bootable clone of your computer's internal drive. First,
make sure that the value of `DST` in the `bin/backup` script matches the name
of your backup-drive. Then run the following command:

```bash
$ backup
```

For more information on how to setup your backup-drive, please read the
preparatory steps in this post on creating a [Mac OS X bootable backup
drive](http://nicolasgallagher.com/mac-osx-bootable-backup-drive-with-rsync/).

### Custom bash prompt

I use a custom bash prompt based on the Solarized color palette and influenced
by @gf3's and @cowboy's custom prompts. For best results, you should install
iTerm2 and import [Solarized
Dark.itermcolors](https://github.com/altercation/solarized/tree/master/iterm2-colors-solarized).

When your current working directory is a Git repository, the prompt will
display the checked-out branch's name (and failing that, the commit SHA that
HEAD is pointing to). The state of the working tree is reflected in the
following way:

<table>
    <tr>
        <td><code>+</code></td>
        <td>Uncommitted changes in the index</td>
    </tr>
    <tr>
        <td><code>!</code></td>
        <td>Unstaged changes</td>
    </tr>
    <tr>
        <td><code>?</code></td>
        <td>Untracked files</td>
    </tr>
    <tr>
        <td><code>$</code></td>
        <td>Stashed files</td>
    </tr>
</table>

Further details are in the `bash_prompt` file.

Screenshot:

![](http://i.imgur.com/DSJ1G.png)

### Local/private Bash configuration

Any private and custom Bash commands and configuration should be placed in a
`~/.bash_profile.local` file. This file will not be under version control or
committed to a public repository. If `~/.bash_profile.local` exists, it will be
sourced for inclusion in `bash_profile`.

Here is an example `~/.bash_profile.local`:

```bash
# PATH exports
PATH=$PATH:~/.gem/ruby/1.8/bin
export PATH

# Git credentials
# Not under version control to prevent people from
# accidentally committing with your details
GIT_AUTHOR_NAME="Nicolas Gallagher"
GIT_AUTHOR_EMAIL="nicolas@example.com"
GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
# Set the credentials (modifies ~/.gitconfig)
git config --global user.name "$GIT_AUTHOR_NAME"
git config --global user.email "$GIT_AUTHOR_EMAIL"

# Aliases
alias code="cd ~/Code"
```

N.B. Because the `git/gitconfig` file is copied to `~/.gitconfig`, any private
git configuration specified in `~/.bash_profile.local` will not be committed to
your dotfiles repository.