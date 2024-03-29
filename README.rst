
CellML Specification
====================

This repository will be used by the CellML editors to develop the CellML specification (starting with the discontinued version 1.2)
The content has been reworked to include an informal guide embedded within the normative specification text (in version 2.0).

If things work correctly, changes in this repository will be reflected over at: https://cellml-specification.readthedocs.org/.
Any pull requests opened will also be built on read the docs.

Building the documentation locally
----------------------------------

The documentation can be built on your local machine with the following instructions.
Do take note that the following instructions are suitable for Unix-derived operating systems and may need modification for other operating systems.
Also, note that we require at least version 3.5 of Python to build the documentation.

First clone a local copy of the CellML specification repository::

  git clone https://github.com/cellml/cellml-specification.git

Next setup a virtual environment::

  virtualenv venv_specification

**Note:** make sure you are creating virtual environment using a suitable Python interpreter, if required use the ``-p`` flag to set the Python interpreter (for example ``virtualenv -p /absolute/path/to/python venv_specification``).

Then activate the virtual environment and instal the required packages::

  source venv_specification/bin/activate
  pip install -r cellml-specification/requirements.txt

That completes the environment setup required for building the documentation.
Once the environment is completed, the HTML form of the documentation can be built with the following commands::

  cd cellml-specification
  make html

The built documentation will be available at::

  /absolute/path/to/cellml-specification/build/html/index.html

Any good internet browser will be able to display the documentation (see also `Serving the documentation`_).

To build the documentation into a single page HTML document execute the following command::

  make singlehtml

The built documentation will be available at::

  /absolute/path/to/cellml-specification/build/singlehtml/index.html

Building PDFs
^^^^^^^^^^^^^

To build the PDF form of the documentation, simply execute the following command::

  make latexpdf

If this fails, please have a look at the following:

Creating the PDF form of the documentation requires that some or all of a tool like Windows/`MikTeX <https://miktex.org/>`_, Windows/`TeXlive <https://www.tug.org/texlive/>`_, Linux/`TeXlive <https://www.tug.org/texlive/>`_, and macOS/`MacTeX <https://tug.org/mactex/>`_ is available to the Sphinx build tool.

In addition, you'll need the following LaTeX packages: ``babel-greek``, ``capt-of``, ``cbfonts``, ``courier``, ``fncychap``, ``fontspec``, ``framed``, ``greek-fontenc``, ``helvetic``, ``latexmk``, ``needspace``, ``tabulary``, ``textgreek``, ``titlesec``, ``tocloft``, ``varwidth``, and ``wrapfig``.

In particular, check that you have ``latexmk`` available as this is required for creating the PDF form of the documentation.
Information on ``latexmk`` can be found at https://ctan.org/pkg/latexmk/.

You may also need to install the `"GNU FreeFont" fonts <https://www.gnu.org/software/freefont/>`_ ``FreeSans``, ``FreeSerif``, and ``FreeMono``.

Documentation builds
^^^^^^^^^^^^^^^^^^^^

There are two types of build that can be created from this codebase, they can be selected through the use of the environment variable ``CELLML_SPEC_BUILD``.

1. Normative only, set ``CELLML_SPEC_BUILD=Normative`` (default build).
2. Normative and informative specification combined, set ``CELLML_SPEC_BUILD=Full``

Serving the documentation
^^^^^^^^^^^^^^^^^^^^^^^^^

You can serve the documentation locally using a simple Python server.
Save the following text to a file named ``webserver.py`` (this file can be saved anywhere on your harddrive)::

  #!/usr/bin/env python

  import http.server
  import socketserver

  PORT = 8008
  Handler = http.server.SimpleHTTPRequestHandler

  with socketserver.TCPServer(("", PORT), Handler) as httpd:
      print("Serving at port", PORT)
      httpd.serve_forever()

To run the web server, use a terminal type application and change directory into::

  cd /absolute/path/to/cellml-specification/build/html/

then run the command::

  python /absolute/path/to/webserver.py

Now launch your internet browser and open the location::

  http://localhost:8008/

Building the documentation for cellml.org
-----------------------------------------

The documentation required for cellml.org can be built from this repository.
The documenation can be built by setting the variable `target_cellml_org` to `True` in the `conf.py` file and then building the documentation with the single html builder.
With `target_cellml_org = True` saved in the `conf.py` file the command::

  make singlehtml

will create a file `index.html` in the directory `build/singlehtml` relative to the root of the repository directory.
The contents of the `index.html` can be copied and pasted into cellml.org.
