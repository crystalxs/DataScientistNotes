# PostgREST

> Reference: <http://postgrest.org/en/v5.2/index.html>

## Install

```bash
brew install postgrest
```

## Run

###****.conf file

```bash
db-uri = "postgres://<role>:<role-password>@<host>:<port>/<database>"
db-schema = "<schema>"
db-anon-role = "<anon-role>"
```

Other option: <http://postgrest.org/en/v5.2/install.html#configuration>

```bash
postgrest ****.conf
#Listening on port 3000
#Attempting to connect to the database...
#Connection successful
curl http://localhost:3000/<table>
```

