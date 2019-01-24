# Autonity Documentation

Documentation for the Autonity client.

[https://docs.autonity.io][1]

Documentation is generated using [Sphinx][2] and the [Read The Docs Sphinx Theme][3]

## Improving this documentation

We welcome contributions and improvements to this documentation. You can find our [Contributing Guidelines][4] here.

## Installation

You will need `python` and `pip` for the installation.

    pip install sphinx
    pip install sphinx_rtd_theme

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

[1]: https://docs.autonity.io
[2]: http://www.sphinx-doc.org/en/master/
[3]: https://sphinx-rtd-theme.readthedocs.io/en/latest/
[4]: https://github.com/clearmatics/autonity-docs/blob/master/CONTRIBUTING.md