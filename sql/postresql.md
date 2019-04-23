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



## Role

PostgreSQL manages database access permissions using the concept of *roles*. A role can be thought of as either a database user, or a group of database users, depending on how the role is set up.

###Create Roles

```sql
CREATE ROLE name;
DROP ROLE name;
```

```bash
createuser name
dropuser name
```

A freshly initialized system always contains one predefined role, which is always a “superuser”, and by default (unless altered when running `initdb`) it will have the same name as the operating system user that initialized the database cluster. Customarily, this role will be named `postgres`. In order to create more roles you first have to connect as this initial role.

### List Roles

```sql
SELECT rolname FROM pg_roles;
\du		# under postgresql server
```



