# Autonity Documentation

Documentation for the Autonity client.

[https://docs.autonity.io][1]

Documentation is generated using [Sphinx][2] and the [Read The Docs Sphinx Theme][3]

## Improving this documentation

We welcome contributions and improvements to this documentation. You can find our [Contributing Guidelines][4] here.

## Installation

You will need to clone the repository.

    git clone git@github.com:clearmatics/autonity-docs.git

Change into the `autonity-docs` directory

    cd autonity-docs

Than you will need `python` and `pip` for the installation:

    make install

## Generating HTML

Build the static html using the `Makefile` provided

    make html

The html is generated into `_build/html`.

## Viewing HTML

You can use any HTTP server to view the site in a browser. A simple way is

    make start

If you get an error like `/usr/bin/python: No module named SimpleHTTPServer` try this 

    python3 -m http.server

Than you can open the documentation in your browser `localhost:8000`

[1]: https://docs.autonity.io
[2]: http://www.sphinx-doc.org/en/master/
[3]: https://sphinx-rtd-theme.readthedocs.io/en/latest/
[4]: https://github.com/clearmatics/autonity-docs/blob/master/CONTRIBUTING.md