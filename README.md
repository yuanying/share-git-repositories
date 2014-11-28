share-git-repositories
======================

Share local git repositories to global with "grack" and "vagrant share".

## Install

    $ git clone https://github.com/yuanying/share-git-repositories.git $SGR_ROOT

## How to Use

1.  Set local project root directory which contains git repositories.

        $ export GIT_PROJECT_ROOT=/git/repositories

2.  Boot vm and share.

        $ cd $SGR_ROOT
        $ vagrant up
        $ vagrant login
        $ vagrant share

