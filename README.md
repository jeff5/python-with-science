# python-with-science (trinket version)

Introductory Python tutorial with a bias to science and maths.
The branch you are looking at has been modified for groups using
[Trinket](https://trinket.io/python-new)
a website that allows Python with turtle graphics to run anywhere on the web.

The version of Python at Trinket (at least, the free version) is limited.
The `turtle` module in particular
behaves differently from that in the Python 3 standard library.
This branch is under development to provide a trinket-friendly version.

## Building the project

Clone the project using `git`.
This project builds with Sphinx under Python 3.
Here's how it looks on Windows, using PowerShell (Posh).

### Getting started

A virtual environment is recommended
so that Sphinx is installed only for the project.
To get `virtualenv` use the command `pip install virtualenv`.

Navigate to the `doc` directory of the cloned project, then:
```
PS doc> virtualenv venv
Using base prefix '...
New python executable in ...\venv\Scripts\python.exe
Installing setuptools, pip, wheel...
done.
PS doc> .\venv\Scripts\activate
(venv) PS doc> pip install sphinx
Collecting sphinx
  Downloading ... (loads of stuff)
(venv) PS doc> pip install sphinx_rtd_theme
Collecting sphinx_rtd_theme
  Downloading ... (loads more stuff)
(venv) PS doc>
```


### Building to test

Navigate to the `doc` directory of the cloned project, if not there already.
If necessary, activate the virtual environment:
```
PS doc> .\venv\Scripts\activate
```
The `doc` directory of the project
contains a script `make.bat`that builds the project.
Sphinx is able to produce several output formats,
but the easiest one in which to browse is HTML.
It looks something like this:
```
(venv) PS doc> .\make html
Running Sphinx v1.8.4
loading translations [en]... done
making output directory...
building [mo]: targets for 0 po files that are out of date
building [html]: targets for 8 source files that are out of date
updating environment: 8 added, 0 changed, 0 removed
reading sources... [100%] spiral/spiral
looking for now-outdated files... none found
pickling environment... done
checking consistency... done
preparing documents... done
writing output... [100%] spiral/spiral
generating indices... genindex
writing additional pages... search
copying images... [100%] spiral\ammonite.png
copying static files... done
copying extra files... done
dumping search index in English (code: en) ... done
dumping object inventory... done
build succeeded.

The HTML pages are in build\html.

Build finished. The HTML pages are in build/html.
```
Then visiting `build/html/index.html` with a browser
allows one to view the documentation.
