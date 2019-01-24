# Autonity Documentation

Documentation for the Autonity client using [Sphinx][1] and the [Read The Docs Sphinx Theme][2]

## Installation

You will need `python` and `pip` for the installation.

    pip install sphinx

Then you can clone the repository.

    git clone git@github.com/clearmatics/autonity-docs

Change into the `autonity-docs` directory

    cd autonity-docs

## Generating HTML

Build the static html using the `Makefile` provided

    make html

The html is generated into `_build/html`.

## Viewing HTML

You can use any HTTP server to view the site in a browser. A simple way is

    cd _build/html
    python -m SimpleHTTPServer

If you get an error like `/usr/bin/python: No module named SimpleHTTPServer` try this 

    python3 -m SimpleHTTPServer

[1]: http://www.sphinx-doc.org/en/master/
[2]: https://sphinx-rtd-theme.readthedocs.io/en/latest/
