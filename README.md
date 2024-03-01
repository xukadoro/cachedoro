[![Build Status](https://travis-ci.org/msurdi/tcache.svg?branch=master)](https://travis-ci.org/msurdi/tcache)

tcache
======

tcache is a command line tool for caching directory trees or files. An example usecase would be
a build/continuous integration system where on each build application dependencies need to be
setup consuming considerable time and quite often depending on the network or external repositories
being available and not banning users for abuse.

Example use case
----------------

In the following example, the command `pip install -r requirements.txt` will be executed only
if one of the following conditions is true:

  - It is the first time you run the command, thus the _env_ directory doesn't exist yet
  - The contents of requirements.txt have changed since the last time the command was run and _env_ doesn't exist anymore, or -f is provided.
  - The cached version of _env_ is older than 1 day since the command was run and _env_ doesn't exist anymore, or -f is provided.


        $ tcache -p env -k $(md5 -q requirements.txt) -r 1d -- pip install -r requirements.txt --root=env


Here is a similar example, but for npm:

        
        $ tcache -p ./node_modules -k $(md5 -q package.json) -- npm install
       
        
By default cached directory trees are stored in $HOME/.tcache, this can be changed with the -c option.

Please, run `tcache --help` for further details and usage examples.
