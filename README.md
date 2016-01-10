### `jdbcli>` a jdbc command-line interface

* [Overview](#overview)
* [Features](#features)
  * [Horizontal Output](#horizontal-output)
  * [Vertical Output](#vertical-output)
  * [History](#history)
  * [Non-Interactive Mode](#non-interactive-mode)
* [Setup](#setup)
  * [Requirements](#requirements)
  * [Install jdbcli](#install-jdbcli)
  * [Locate Driver](#locate-driver)
  * [Install Driver](#install-driver)
  * [Update PATH](#update-path-optional)
* [Running](#running)
* [License](#license)

### Overview

`jdbcli` is a jdbc command-line interface for interacting with databases. 
The goal is to mimic `mysql`, the MySQL command-line client as much as
possible. After years of working with MySQL, the project I was on migrated to
Oracle, and I soon grew to detest it. After a while, I realized that though I
prefer MySQL, a lot of my grievances stemmed from having to choose between the
bloated `SQLDeveloper` and the ugly `sqlplus`. When using MySQL, I
often have multiple `mysql` processes in terminal tabs, and I really enjoy
that way of working.

Hopefully `jdbcli` makes you forget, if only for a little while, that
you're connected to a non-MySQL database.

### Features

##### Horizontal Output

The standard output. Simply end your query with either `;` or `\g`
```
jdbcli> select id, name, city from team where id = 1234567890;
+------------+--------+--------------+
| ID         | NAME   | CITY         |
+------------+--------+--------------+
| 1234567890 | Flyers | Philadelphia |
+------------+--------+--------------+
1 row in set (0.03 sec)
```

##### Vertical Output

Increase readability when the output would be too wide in horizontal mode. End
you query with `\G`

```
jdbcli> select id, name, city from team where id = 1234567890 \G
*************************** 1. row ***************************
                     ID: 1234567890119
                   NAME: Flyers
                   CITY: Philadelphia
1 row in set (0.16 sec)
```

##### History

The provided [JLine](https://github.com/jline/jline2) library provides console input; it provides similar functionality to [BSD editline](http://thrysoee.dk/editline/) and [GNU readline](http://cnswww.cns.cwru.edu/php/chet/readline/rltop.html). Commands get
added to your history file, which is `~/.jdbcli_history` by default. The normal history functions are supported (e.g. up-arrow for previous command, searching).

##### Non-Interactive Mode

Execute SQL queries directly from the command-line; this is referred to as "non-interactive mode". To do so, use
either the `--execute` or `-e` argument. See below for an example:

```
$ jdbcli --config ~/etc/myconfig.properties --execute "select id, name, city from team where id = 1234567890"
+------------+--------+--------------+
| ID         | NAME   | CITY         |
+------------+--------+--------------+
| 1234567890 | Flyers | Philadelphia |
+------------+--------+--------------+
1 row in set (0.03 sec)
```

### Setup

##### Requirements

You need a Java Runtime Environment (JRE) >= 1.6 and a suitable JDBC driver for your database.

##### Install `jdbcli`

Follow the instructions below to install the latest release in `/usr/local`, but obviously install it wherever you see fit. 

```
$ wget https://github.com/artloder/jdbcli/archive/jdbcli-0.1.0.tar.gz
$ tar -xzf jdbcli-0.1.0.tar.gz
$ sudo mv jdbcli-0.1.0 /usr/local/
```

##### Locate Driver

In order to talk to your database of choice, you need to provide a database-specific JDBC library.
The below table includes links to download the JDBC library for common databases. Links may be outdated,
in which case just Google it.

| Database     | JDBC driver download |
| ------------ | -------------------- |
| Apache Derby | https://db.apache.org/derby/derby_downloads.html |
| Java DB      | (provided in JDK) |
| MySQL        | https://dev.mysql.com/downloads/connector/j/ |
| Oracle       | http://www.oracle.com/technetwork/database/features/jdbc/index.html |
| PostgreSQL   | https://jdbc.postgresql.org/download.html |
| SQL Server   | https://www.microsoft.com/en-US/download/details.aspx?id=11774 |
| SQLite       | https://bitbucket.org/xerial/sqlite-jdbc/downloads |

##### Install Driver

Place the downloaded driver in the previous step into the installation's `lib/` directory.
For instance, if you are using MySQL and downloaded the mysql-connector-java-5.1.38-bin.jar, you would do the following:

```
$ cp /path/to/file/mysql-connector-java-5.1.38-bin.jar /usr/local/jdbcli-0.1.0/lib/
```

##### Update PATH (optional)

You may also want to add the installed bin directory, `/usr/local/jdbcli-0.1.0/bin/`, to your `$PATH` to more easily run via `jdbcli` instead of `/usr/local/jdbcli-0.1.0/bin/jdbcli`. This is platform-dependent (e.g. update your `.bashrc` if you use the bash shell).

### Running

```
$ /usr/local/jdbcli-0.1.0/bin/jdbcli --version
```

### License

Released under the MIT License (see LICENSE.txt file). Third party license information in NOTICE.txt file.
