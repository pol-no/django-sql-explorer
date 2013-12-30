Django SQL Explorer
==================

Django SQL Explorer is inspired by Stack Exchange's [Data Explorer](http://data.stackexchange.com/stackoverflow/queries) and is designed to make the flow of data between people in your company fast, simple, and confusion-free. Quickly write and share SQL queries in a clean, usable query builder, preview the results in the browser, share links to download CSV files, and keep the information flowing baby!

django-sql-explorer is MIT licensed, and pull requests are welcome!

![](http://www.untrod.com/django-sql-explorer/query2.jpg)

Install
=======

Requires Python 2.7.

This has been tested only with Django 1.6, however it should work back to 1.4. Please report an issue if you encounter problems on earlier versions of Django.

Install with pip from github:

    pip install django-sql-explorer

Add to your installed_apps:

    INSTALLED_APPS = (
      ...
      'explorer',
      ...
    )

Add the following to your urls.py (all Explorer URLs are restricted to staff only):

    url(r'^explorer/', include('explorer.urls')),

Run syncdb to create the tables (well...just one table really):
    
    python manage.py syncdb

Browse to https://yoursite/explorer/ and get exploring!


Dependencies
============

An effort has been made to require no packages other than Django. However a number of front-end dependencies do exist and are documented below. All front-end dependencies are served from CDNJS.com

Name | Version | License
--- | --- | ---
[Twitter Boostrap](http://getbootstrap.com/) | 3.0.3 | MIT
[jQuery](http://jquery.com/) | 2.0.3 | MIT
[Underscore](http://underscorejs.org/) | 1.5.2 | MIT
[Codemirror](http://codemirror.net/) | 3.19.0 | MIT
[floatThead](http://mkoryak.github.io/floatThead/)* | 1.2.0 | Creative Commons

_*Served locally because this is not available on cdnjs_

Factory Boy is needed if you'd like to run the tests, which can you do easily:

        python manage.py test


Settings
========

Setting | Description | Default
--------|-------------|--------
EXPLORER_SQL_BLACKLIST | Disallowed words in SQL queries to prevent destructive actions. | ('ALTER', 'RENAME ', 'DROP', 'TRUNCATE', 'INSERT INTO', 'UPDATE', 'REPLACE', 'DELETE')
EXPLORER_SQL_WHITELIST | These phrases are allowed, even though part of the phrase appears in the blacklist. | ('DROP FUNCTION', 'REPLACE FUNCTION', 'DROP VIEW', 'REPLACE VIEW', 'CREATED', 'DELETED')
EXPLORER_DEFAULT_ROWS | The number of rows to show by default in the preview pane. | 100
EXPLORER_SCHEMA_EXCLUDE_APPS | Don't show schema for these apps in /schema/. This is helpful to clear out cruft that users realistically won't want to refer to for reference. | ('',)  # No apps are excluded


Features
========

- SQL blacklist so destructive queries don't get executed (delete, drop, etc). This is not bulletproof and it's recommended that you instead configure a read-only database role, but when not possible the blacklist provides reasonable protection.
- Playground! Just want to get in and write some ad-hoc queries? Go nuts!
- Schema helper - /explorer/schema/ will dump a list of your Django apps' table and column names that you can refer to while writing queries.
- Reasonably good test coverage.
- Download multiple queries at once as a zip file through Django's admin interface.
