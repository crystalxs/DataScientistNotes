# PostgreSQL

> Reference: <https://medium.com/@martinlasek/tutorial-how-to-use-postgresql-88cddc858d9f>

##Install

#### Requirement

Homebrew

```bash
brew install postgresql
initdb /usr/local/var/postgres
brew services start postgresql
```

## Create Database

```bash
createdb mydb;
psql mydb				# connect to mydb database
\l							# list databse in server
\q							# quit from server
```







