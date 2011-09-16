## Instant git-based automatic file synchronizer

### Requirements

- git
- inotify-tools (optional)

### Use

#### Setup:

- initializing new repository:

        $ mkdir -p GIT_REPO_DIR
        $ cd GIT_REPO_DIR
        $ git init
        $ git config user.name '...'
        $ git config user.email 'myself@domainM.com'

- git-auto-sync init:

        $ cd GIT_REPO_DIR
        $ git-auto-sync init myname-master git://mycollaboratorsdomain/syncbox ...

    - use --shallow switch to perform shallow repository cloning (if
      you don't need all the history).

- start git-daemon for your repository, for example:

        $ git daemon --export-all --base-path=$(cd GIT_REPO_DIR/..; pwd) --reuseaddr --enable=receive-pack --detach

#### Automatic synchronization:

    $ cd GIT_REPO_DIR; git-auto-sync run

If you change your files, changes will be replicated to other
collaborators automatically.

If you don't have inotify-tools installed:

    $ cd GIT_REPO_DIR; git-auto-sync run_with_polling 60 # secs

#### Manual synchronization:

    $ cd GIT_REPO_DIR; git-auto-sync once

### Todo

- full directory hierarchy synchronization instead of top directory only

### Related

- rsync, unison, dropbox, ...

