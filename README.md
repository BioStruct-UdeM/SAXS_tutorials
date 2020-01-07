## Description

Documentation for the [(bio-)SAXS instrument](https://biochimie.umontreal.ca/en/scientific-platforms-bmm/structural-biology/biosaxs/) of the [Structural Biology platform](https://biochimie.umontreal.ca/en/plateformes-scientifiques-bmm/biologie-structurale/) located in the [department of biochemistry and molecular medicine](https://biochimie.umontreal.ca/en) of the [Université de Montréal](https://umontreal.ca/en).

Tutorials and howtos are presented in this documentation, formatted using [MkDocs](https://www.mkdocs.org/), and the theme [Cinder](https://github.com/chrissimpkins/cinder).

To access the site: http://airen.bcm.umontreal.ca/biostruct/SAXS_tutorials/

![Screenshot of the front page](https://github.com/BioStruct-UdeM/SAXS_tutorials/raw/master/docs/img/screen_shots/site_front_page_screenshot.png)


## How to serve locally

First install the required Python distribution packages:

`pip install -r requirements.txt`

This will install the following (and associated requirements):

- MkDocs (`mkdocs`)
- MkDocs Cinder theme (`mkdocs-cinder`)
- Math extension for Python-Markdown (`python-markdown-math`)

Then serve the website lcoally with MkDocs:

`mkdocs serve`

By default, the documentation will be available in your browser at this address: http://127.0.0.1:8000/.


## How to deploy

First install the required Python distribution packages:

`pip install -r requirements.txt`

This will install the following (and associated requirements):

- MkDocs (`mkdocs`)
- MkDocs Cinder theme (`mkdocs-cinder`)
- Math extension for Python-Markdown (`python-markdown-math`)

Then build the website with MkDocs

`mkdocs build`

Finally, copy the static site files to the root folder of your webserver:

`cp -r site/* /path/to/server/root`

The site should then be available online. Make sure you adjust the `/path/to/server/root` to match the configuration of webserver.

More information [here](https://www.mkdocs.org/user-guide/deploying-your-docs/).
