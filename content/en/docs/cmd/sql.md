---
title: "sq sql"
description: "Execute DB-native SQL query or statement"
draft: false
images: []
menu:
  docs:
    parent: "cmd"
weight: 2100
toc: true
url: /docs/cmd/sql
---
When `sq`'s jq-like query language ([SLQ](/docs/concepts#slq)) isn't expressive enough,
you can use `sq sql` to execute DB-native SQL queries or statements.

```shell
$ sq sql 'SELECT * FROM actor WHERE actor_id < 5'
```

## Active source & schema

The `sql` command works very similarly to the root [`sq`](/docs/cmd/sq) command.
You can change the [active source](/docs/concepts#active-source) for the query using [`--src`](/docs/cmd/sq#override-active-source),
and change tha active [catalog/schema](/docs/concepts#schema--catalog) using [`--src.schema`](/docs/cmd/sq#override-active-schema).

Here's an example tying these together:

```shell
$ sq sql --src @sakila/pg12 --src.schema sakila.information_schema \
'select table_catalog, table_schema, table_name, table_type from tables'
table_catalog  table_schema          table_name                             table_type
sakila         pg_catalog            pg_statistic                           BASE TABLE
sakila         pg_catalog            pg_type                                BASE TABLE
sakila         public                actor                                  BASE TABLE
sakila         pg_catalog            pg_foreign_server                      BASE TABLE
sakila         pg_catalog            pg_authid                              BASE TABLE
sakila         pg_catalog            pg_shadow                              VIEW
sakila         pg_catalog            pg_statistic_ext_data                  BASE TABLE
[...]
```


## Reference

{{< readfile file="sql.help.txt" code="true" lang="text" >}}
