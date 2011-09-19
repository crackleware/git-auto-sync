## Instant automatic git-based efficient network file synchronizer

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

- start git-daemon for your repository, for example:

        $ git daemon --export-all --base-path=$(cd GIT_REPO_DIR/..; pwd) --reuseaddr --enable=receive-pack --detach

- git-auto-sync init:

        $ cd GIT_REPO_DIR
        $ git-auto-sync init myname-master git://mycollaboratorsdomain/syncbox ...

    - use --shallow switch to perform shallow repository cloning (if
      you don't need all the history) 

    - WARNING: "git-auto-sync init" will reset working tree to state
      of a remote peer's branch

#### Automatic synchronization:

    $ cd GIT_REPO_DIR; git-auto-sync run

Created, changed and deleted files will be replicated to other peers
automatically. In the case of conflict which can happen when two peers
change the same file at roughly the same time, both file versions are
preserved by automatic renaming (file -> file.branch1 and
file.branch2).

- use "git-auto-sync run --periodic" to force periodic synchronization
  together with instant on-change sync

If you don't have inotify-tools installed:

    $ cd GIT_REPO_DIR; git-auto-sync run_with_polling 60 # secs

#### Manual synchronization:

    $ cd GIT_REPO_DIR; git-auto-sync once

#### Tests

    $ cd tests; ./t2 test1 && ./t2 test2

### Todo

- better handling of failures

- when using inotify-tools for automatic detection of changes, support
  full directory hierarchy synchronization instead of top directory
  only

### Related

- rsync, unison, dropbox, ...
- https://github.com/kinkerl/persy - personal synchronization application - based on git

