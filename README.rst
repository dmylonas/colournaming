===============
colornaming.net
===============

This is the code for the colornaming.net website and experiment.


Testing
=======

A local instance of the app can be launched using Docker Compose::

    docker-compose build
    docker-compose up -d postgres
    docker-compose run --rm web initdb
    docker-compose run --rm web import_centroids English en /path/to/dataset_en.csv
    docker-compose up web

Under Linux the app can now be accessed at `localhost:5000 <http://localhost:5000>`_.
If you're using docker-machine (e.g. on OS X) then run ``docker-machine ip`` to
get the machine IP address and browse to port 5000 on that address.

The database can be reinitialized by running::

    docker-compose run --rm web dropdb
    docker-compose run --rm web initdb

Additional dataset can be added by running e.g.::

    docker-compose run --rm web import_centroids /path/to/dataset_fr.csv Francais fr

To stop the test instance run::

    docker-compose down


Translation
===========

To add a new language, from the project root run::

    pybabel init -i messages.pot -d colournaming/translations -l [language code]

This will create a new messages file at ``colournaming/translations/[language
code]/LC_MESSAGES/messages.po`` to complete.

When a message file is completed or updated the messages must be compiled::

    pybabel compile -d colournaming/translations

To include new strings in the translation files run::

    pybabel update -i messages.pot -d colournaming/translations

See the `Flask-Babel <https://pythonhosted.org/Flask-Babel/>`_ website for
more information on adding translations.  Check the pages in
`colournaming/templates` for an example of how to use translated text.
