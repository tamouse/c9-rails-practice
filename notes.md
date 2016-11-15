# notes about setting up a rails environment


## postgres doesn't do UTF8

[[https://wiki.postgresql.org/wiki/Adventures_in_PostgreSQL%2C_Episode_1][Adventures in PostgreSQL, Episode 1 - PostgreSQL wiki]]
describes a solution to the problem Cloud9 presents us with: a template1 definition 
with SQL_ASCII set instead of UNICODE.

Walking through the steps:

1. set `datallowconn` to true for `template0`
2. set `datistemplate` to false for `template1`
3. drop `template1`
4. create `template1` with the right encoding


So:

    sudo su - postgres
    psql
    update pg_database set datallowconn = TRUE where datname = 'template0';
    update pg_database set datistemplate = FALSE where datname = 'template1';
    drop database template1;
    create database template1 template = template0 encoding = 'UNICODE';
    \q

And Bob's yer nuncle



