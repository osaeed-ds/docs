!!! warning "Astra Cli is not released yet. It is in active developement "

Astra CLI provides a command line interface in a terminal to operate Datastax Astra. The goal is to offer access to any feature without accessing the user interface.

## Getting Started

### 1. Installation

**📘 1a Prequisites**

On your machine you will need the following components

- A bash shell ([Bourne Again SHell](https://www.gnu.org/software/bash/))
- The folowing commands `untar`, `unzip`, `curl`
- A Java JRE or JDK version 8+ installed

You will also need an Astra token. As such, make sure you completed those 2 steps before

- Create an [Astra account](https://astra.dev/3B7HcYo)
- Generate an [Astra Token](/docs/pages/astra/create-token/)

**✅ 1b Installation**

To install or reinstall the CLI use the following command. Previous installations will be cleaned but configuration will NOT be lost. The cli is installed in `~/.astra/cli` folder whereas your configuration is saved in `~/.astrarc` file. 

```
curl -Ls "https://dtsx.io/get-astra-cli" | bash
```

You can notice that the installation script also check the pre-requisites. It will download expected archive and update your bash profile to have `astra` in your path.

??? abstract "🖥️ Installation script output"

    ```
       █████╗ ███████╗████████╗██████╗  █████╗     ███████╗██╗  ██╗███████╗██╗     ██╗
      ██╔══██╗██╔════╝╚══██╔══╝██╔══██╗██╔══██╗    ██╔════╝██║  ██║██╔════╝██║     ██║  
      ███████║███████╗   ██║   ██████╔╝███████║    ███████╗███████║█████╗  ██║     ██║ 
      ██╔══██║╚════██║   ██║   ██╔══██╗██╔══██║    ╚════██║██╔══██║██╔══╝  ██║     ██║
      ██║  ██║███████║   ██║   ██║  ██║██║  ██║    ███████║██║  ██║███████╗███████╗███████╗
      ╚═╝  ╚═╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝    ╚══════╝╚═╝  ╚═╝╚══════╝╚══════╝╚══════╝
    
    Installing Astra Cli 0.1.alpha3, please wait...      

    Checking prerequisites:
    [OK] - Ready to install.
    [OK] - unzip command is available
    [OK] - zip command is available
    [OK] - curl command is available

    Preparing directories:
    [OK] - Created /Users/cedricklunven/.astra/tmp
    [OK] - Created /Users/cedricklunven/.astra/cli
    [OK] - Created /Users/cedricklunven/.astra/scb

    Downloading archive:
    ######################################################################## 100.0%
    [OK] - File downloaded
    [OK] - Integrity of the archive checked

    Extracting and installation:
    [OK] - Extraction is successful
    [OK] - File moved to /Users/cedricklunven/.astra/cli
    [OK] - Installation cleaned up
    [OK] - Installation Successful

    Open A NEW TERMINAL and run: astra setup

    You can close this window.
    ```

### 2. Setup

!!! info "After installing, make sure to open a new terminal to have `astra` in the `PATH`."

**✅ 2a - Run Setup**

Before issuing commands to init to initialize the configuration file `~/.astrarc`. To to so run the following command. You will be asked to provide your token (AstraCS:...). It will be saved and reuse for your commands.

```
astra setup
```

???+ abstract "🖥️ `astra setup` command output"

    ```
    +-------------------------------+
    +-     Astra CLI SETUP         -+
    +-------------------------------+

    Welcome to Astra Cli. We will guide you to start.

    [Astra Setup]
    To use the cli you need to:
    • Create an Astra account on : https://astra.datastax.com
    • Create an Authentication token following: https://dtsx.io/create-astra-token

    [Cli Setup]
    You will be asked to enter your token, it will be saved locally in ~/.astrarc

    • Enter your token (starting with AstraCS) : 
     AstraCS:lorem_ipsum
    ```

- Copy paste the value of your token and press enter.

???+ abstract "🖥️ `astra setup` command output"

    ```
    [What's NEXT ?]
    You are all set.(configuration is stored in ~/.astrarc) You can now:
      • Use any command, 'astra help' will get you the list
      • Try with 'astra db list'
      • Enter interactive mode using 'astra'

    Happy Coding !
    ```

**✅ 2b - Setup validation**

You are all set. The configuration (mainly your token) is stored in file `~/.astrarc`.

- Display current version of the cli, validating setup is complete.

```
astra --version
```

???+ abstract "🖥️ Sample output" 

    `0.1.alpha4`

You created a default configuration pointing to your organization. If you want to work with multiple organizations look at `Config Management` chapter below.

- After setup you have 1 configuration automaticall set as default. You can have more than one configuration is you work with multiple organizations for instance. To know more about multi-organizations configuration check chapter `5.1`.

```bash
astra config list
```

???+ abstract "🖥️ Sample output" 

    ```
    +-----------------------------------------+
    | configuration                           |
    +-----------------------------------------+
    | default (cedrick.lunven@datastax.com)   |
    | cedrick.lunven@datastax.com             |
    +-----------------------------------------+
    ```

### 3. Get Help

The solution provides extensive documentation for any command. It also provides som bash autocompletion, use the `TAB` key twice to get a list of propositions.

**✅ 3a - Autocompletion**

```
astra <TAB> <TAB>
```

???+ abstract "🖥️ Sample output" 

    ```
    --no-color  config      db          help        role        setup       shell       user  
    ```

**✅ 3b - Documentation**

Groups of command will get you the different command avalable.

- Display main help

```
astra help
```

???+ abstract "🖥️ Sample output" 

    ```
    usage: astra <command> [ <args> ]

    Commands are:
        help     View help for any command
        setup    Initialize configuration file
        shell    Interactive mode (default if no command provided)
        config   Manage configuration file
        db       Manage databases
        role     Manage roles (RBAC)
        user     Manage users

    See 'astra help <command>' for more information on a specific command.
    ```

- Display help for command group `astra db`

```
astra help db
```

???+ abstract "🖥️ Sample output" 

    ```
    NAME
            astra db - Manage databases

    SYNOPSIS
            astra db { cqlsh | create | create-keyspace | delete | dsbulk | get |
                    list } [--] [ --token <AUTH_TOKEN> ]
                    [ --config-file <CONFIG_FILE> ] [ --no-color ]
                    [ {-v | --verbose} ] [ {-conf | --config} <CONFIG_SECTION> ]
                    [ --log <LOG_FILE> ] [ {-o | --output} <FORMAT> ] [cmd-options]
                    <cmd-args>

            Where command-specific options [cmd-options] are:
                cqlsh: [ --debug ] [ {-f | --file} <FILE> ] [ {-k | --keyspace} <KEYSPACE> ]
                        [ --version ] [ {-e | --execute} <STATEMENT> ] [ --encoding <ENCODING> ]
                create: [ {-k | --keyspace} <KEYSPACE> ] [ --if-not-exist ] [ {-r | --region} <DB_REGION> ]
                create-keyspace: {-k | --keyspace} <KEYSPACE> [ --if-not-exist ]
                delete:
                dsbulk:
                get:
                list:

            Where command-specific arguments <cmd-args> are:
                cqlsh: <DB>
                create: <DB_NAME>
                create-keyspace: <DB>
                delete: <DB>
                dsbulk: [ <dsbulkArguments>... ]
                get: <DB>
                list:

            See 'astra help db <command>' for more information on a specific command.
    ```

- Display help for unitary command `astra db list`

For unitary commands all options details are provided. 

```
astra help db list
```

???+ abstract "🖥️ Sample output" 

    ```
    NAME
            astra db list - Display the list of Databases in an organization

    SYNOPSIS
            astra db list [ {-conf | --config} <CONFIG_SECTION> ]
                    [ --config-file <CONFIG_FILE> ] [ --log <LOG_FILE> ]
                    [ --no-color ] [ {-o | --output} <FORMAT> ]
                    [ --token <AUTH_TOKEN> ] [ {-v | --verbose} ]

    OPTIONS
            -conf <CONFIG_SECTION>, --config <CONFIG_SECTION>
                Section in configuration file (default = ~/.astrarc)

            --config-file <CONFIG_FILE>
                Configuration file (default = ~/.astrarc)

            --log <LOG_FILE>
                Logs will go in the file plus on console

            --no-color
                Remove all colors in output

            -o <FORMAT>, --output <FORMAT>
                Output format, valid values are: human,json,csv

            --token <AUTH_TOKEN>
                Key to use authenticate each call.

            -v, --verbose
                Verbose mode with log in console
    ```

## Databases

### 1. List databases

**✅ 1a - list**

To get the list of non terminated database in your oganization use the command `list` in the group `db`.

```
astra db list
```

???+ abstract "🖥️ Sample output" 

    ```
    +---------------------+--------------------------------------+---------------------+----------------+
    | Name                | id                                   | Default Region      | Status         |
    +---------------------+--------------------------------------+---------------------+----------------+
    | mtg                 | dde308f5-a8b0-474d-afd6-81e5689e3e25 | eu-central-1        | ACTIVE         |
    | workshops           | 3ed83de7-d97f-4fb6-bf9f-82e9f7eafa23 | eu-west-1           | ACTIVE         |
    | sdk_tests           | 06a9675a-ca62-4cd0-9b94-aefaf395922b | us-east-1           | ACTIVE         |
    | test                | 7677a789-bd57-455d-ab2c-a3bdfa35ba68 | eu-central-1        | ACTIVE         |
    | demo                | 071d7059-d55b-4cdb-90c6-41c26da1a029 | us-east-1           | ACTIVE         |
    | ac201               | 48c7178c-58cb-4657-b3d2-8a9e3cc89461 | us-east-1           | ACTIVE         |
    +---------------------+--------------------------------------+---------------------+----------------+
    ```

**✅ 1b - Get Help**

To get help on a command always prefix with `astra help XXX`

```
astra help db list
```

???+ abstract "🖥️ Sample output" 

    ```
    NAME
            astra db list - Display the list of Databases in an organization

    SYNOPSIS
            astra db list [ {-conf | --config} <CONFIG_SECTION> ]
                    [ --config-file <CONFIG_FILE> ] [ --log <LOG_FILE> ]
                    [ --no-color ] [ {-o | --output} <FORMAT> ]
                    [ --token <AUTH_TOKEN> ] [ {-v | --verbose} ]

    OPTIONS
            -conf <CONFIG_SECTION>, --config <CONFIG_SECTION>
                Section in configuration file (default = ~/.astrarc)

            --config-file <CONFIG_FILE>
                Configuration file (default = ~/.astrarc)

            --log <LOG_FILE>
                Logs will go in the file plus on console

            --no-color
                Remove all colors in output

            -o <FORMAT>, --output <FORMAT>
                Output format, valid values are: human,json,csv

            --token <AUTH_TOKEN>
                Key to use authenticate each call.

            -v, --verbose
                Verbose mode with log in console
    ```            

**✅ 1c - Change output**

```
astra db list -o csv
```

??? abstract "🖥️ Sample output" 

    ```csv
    Name,id,Default Region,Status
    mtg,dde308f5-a8b0-474d-afd6-81e5689e3e25,eu-central-1,ACTIVE
    workshops,3ed83de7-d97f-4fb6-bf9f-82e9f7eafa23,eu-west-1,ACTIVE
    sdk_tests,06a9675a-ca62-4cd0-9b94-aefaf395922b,us-east-1,ACTIVE
    test,7677a789-bd57-455d-ab2c-a3bdfa35ba68,eu-central-1,ACTIVE
    demo,071d7059-d55b-4cdb-90c6-41c26da1a029,us-east-1,ACTIVE
    ac201,48c7178c-58cb-4657-b3d2-8a9e3cc89461,us-east-1,ACTIVE
    ```

```
astra db list -o json
```

??? abstract "🖥️ Sample output" 

    ```json
      {
        "code" : 0,
        "message" : "astra db list -o json",
        "data" : [ {
          "Status" : "ACTIVE",
          "Default Region" : "eu-central-1",
          "id" : "dde308f5-a8b0-474d-afd6-81e5689e3e25",
          "Name" : "mtg"
        }, {
          "Status" : "ACTIVE",
          "Default Region" : "eu-west-1",
          "id" : "3ed83de7-d97f-4fb6-bf9f-82e9f7eafa23",
          "Name" : "workshops"
        }, {
          "Status" : "ACTIVE",
          "Default Region" : "us-east-1",
          "id" : "06a9675a-ca62-4cd0-9b94-aefaf395922b",
          "Name" : "sdk_tests"
        }, {
          "Status" : "ACTIVE",
          "Default Region" : "eu-central-1",
          "id" : "7677a789-bd57-455d-ab2c-a3bdfa35ba68",
          "Name" : "test"
        }, {
          "Status" : "ACTIVE",
          "Default Region" : "us-east-1",
          "id" : "071d7059-d55b-4cdb-90c6-41c26da1a029",
          "Name" : "demo"
        }, {
          "Status" : "ACTIVE",
          "Default Region" : "us-east-1",
          "id" : "48c7178c-58cb-4657-b3d2-8a9e3cc89461",
          "Name" : "ac201"
        } ]
      }
    ```

### 2. Create database

**✅ 2a - Create Database** 

If not provided the region will be the default free region and the keyspace will be the database name but you can change then with `-r` and `-k` respectivitely.

```
astra db create demo
```

**✅ 2b - If not Exists** 

Database name does not ensure unicity (database id does) as such if you issue the command multiple times you will end up with multiple instances. To change this behaviour you can use `--if-not-exist`

```
astra db create demo -k ks2 --if-not-exist
```

**✅ 2c - Get help** 

Better doc the cli itself.

```
astra help db create
```

### 3. Resume database

In the free tier, after 23H of inactivity your database got hibernated. To wake up the db you can use the `resume command`

**✅ 2a - Resuming** 

Assuming you have an hibernating database.

```
astra db list
+---------------------+--------------------------------------+---------------------+----------------+
| Name                | id                                   | Default Region      | Status         |
+---------------------+--------------------------------------+---------------------+----------------+
| hemidactylus        | 643c6bb8-2336-4649-97d5-39c33491f5c1 | eu-central-1        | HIBERNATED     |
```


```
astra db resume hemidactylus
```

??? abstract "🖥️ Sample output" 

    ```
    +---------------------+--------------------------------------+---------------------+----------------+
    | Name                | id                                   | Default Region      | Status         |
    +---------------------+--------------------------------------+---------------------+----------------+
    | hemidactylus        | 643c6bb8-2336-4649-97d5-39c33491f5c1 | eu-central-1        | RESUMING       |
    +---------------------+--------------------------------------+---------------------+----------------+

    And after a few time
    +---------------------+--------------------------------------+---------------------+----------------+
    | Name                | id                                   | Default Region      | Status         |
    +---------------------+--------------------------------------+---------------------+----------------+
    | hemidactylus        | 643c6bb8-2336-4649-97d5-39c33491f5c1 | eu-central-1        | ACTIVE         |
    +---------------------+--------------------------------------+---------------------+----------------+
    ```

### 4. Get database details

To get information or details on an entity use the command `get`.

```
astra db get demo
```

In the output you specially see the list of keyspaces available and the different regions.

???+ abstract "🖥️ Sample output" 

    ```
    +------------------------+-----------------------------------------+
    | Attribute              | Value                                   |
    +------------------------+-----------------------------------------+
    | Name                   | demo                                    |
    | id                     | 071d7059-d55b-4cdb-90c6-41c26da1a029    |
    | Status                 | ACTIVE                                  |
    | Default Cloud Provider | AWS                                     |
    | Default Region         | us-east-1                               |
    | Default Keyspace       | demo                                    |
    | Creation Time          | 2022-07-26T15:41:18Z                    |
    |                        |                                         |
    | Keyspaces              | [0] demo                                |
    |                        |                                         |
    | Regions                | [0] us-east-1                           |
    +------------------------+-----------------------------------------+
    ```

To get the status of your db (`ACTIVE`, `HIBERNATED`, `RESUMING`) you can use the pip and `grep`

```
astra db get demo | grep Status
```

???+ abstract "🖥️ Sample output" 

    ```
    | Status                 | ACTIVE                                  |
    ```

### 5. Create keyspace

A keyspace is created when you create the database. Default CLI behaviour is to provide same values for keyspace
and database names. But you can define your own keyspace name with the flag `-k`.

**✅ 5a - Create new keyspace** 

To add a keyspace `ks2` to an existing database `demo` use the following. The option `--if-not-exist` is optional but could help you providing idempotent scripts.

```
astra db create-keyspace demo -k ks2
```

If the database is not found you will get a warning message and dedicated code returned. 

To see your new keyspace you can display your database details

```
astra db get demo
```


**✅ 5b - Get help** 

```
astra help db create-keyspace
```

### 6. Cqlsh

[Cqlsh](https://cassandra.apache.org/doc/latest/cassandra/tools/cqlsh.html) is a standalone shell to work with Apache Cassandra™. It is compliant with Astra but requires a few extra steps of configuration. The purpose of the CLI is to integrate with `cqlsh` and do the integration for you.

Astra Cli will **download**, **install**, **setup** and **wrap** `cqlsh` for you to interact with Astra.

**✅ 6a - Interactive mode** 

If no option are provided,  you enter `cqlsh` interactive mode

```
astra db cqlsh demo
```

??? abstract "🖥️ Sample output" 

    ```
    Cqlsh is starting please wait for connection establishment...
    Connected to cndb at 127.0.0.1:9042.
    [cqlsh 6.8.0 | Cassandra 4.0.0.6816 | CQL spec 3.4.5 | Native protocol v4]
    Use HELP for help.
    token@cqlsh>
    ```

**✅ 6b - Execute CQL** 

To execute CQL Statement with `cqlsh` use the flag `-e`.

```
astra db cqlsh demo -e "describe keyspaces;"
```

**✅ 5b - Execute CQL Files** 

To execute CQL Files with `cqlsh` use the flag `-f`. You could also use the CQL syntax SOURCE.

```
astra db cqlsh demo -f sample.cql
```

### 7. DSBulk

**✅ 7a - Setup** 

[Dsbulk](https://github.com/datastax/dsbulk) stands for Datastax bulk loader. It is a standalone program to load, unload and count data in an efficient way with Apache Cassandra™. It is compliant with Datastax Astra.

As for `Cqlsh` the cli will **download**, **install**, **setup** and **wrap** the dsbulk command for you. All options are available. To give you an idea let's tak a simple example.


- Make sure we have a db `demo` with a keyspace `demo`

```
astra db create demo
```

- Looking at a dataset of cities in the world. [cities.csv](https://raw.githubusercontent.com/awesome-astra/docs/main/docs/assets/cities.csv). We can show here the first lines of the 
file.

```
id,name,state_id,state_code,state_name,country_id,country_code,country_name,latitude,longitude,wikiDataId
52,Ashkāsham,3901,BDS,Badakhshan,1,AF,Afghanistan,36.68333000,71.53333000,Q4805192
68,Fayzabad,3901,BDS,Badakhshan,1,AF,Afghanistan,37.11664000,70.58002000,Q156558
...
```

- Let's create a table to store those values. Connect to CQHSH

```
astra db cqlsh demo -k demo
```

- Create the table 

```sql
CREATE TABLE cities_by_country (
 country_name text,
 name       text,
 id         int,
 state_id   text,
 state_code text,
 state_name text,
 country_id text,
 country_code text,
 latitude double,
 longitude double,
 wikiDataId text,
 PRIMARY KEY ((country_name), name)
);

describe table cities_by_country;

quit
```

**✅ 7b - Load Data** 

```
astra db dsbulk demo load \
  -url https://raw.githubusercontent.com/awesome-astra/docs/main/docs/assets/cities.csv \
  -k demo \
  -t cities_by_country \
  --schema.allowMissingFields true
```

The first time the line `DSBulk is starting please wait` can take a few seconds to appear. The reason is the cli is download `dsbulk` if not downloaded before.

???+ abstract "🖥️ Sample output" 

    ```
    DSBulk is starting please wait ...
    Username and password provided but auth provider not specified, inferring PlainTextAuthProvider
    A cloud secure connect bundle was provided: ignoring all explicit contact points.
    A cloud secure connect bundle was provided and selected operation performs writes: changing default consistency level to LOCAL_QUORUM.
    Operation directory: /Users/cedricklunven/Downloads/logs/LOAD_20220823-182343-074618
    Setting executor.maxPerSecond not set when connecting to DataStax Astra: applying a limit of 9,000 ops/second based on the number of coordinators (3).
    If your Astra database has higher limits, please define executor.maxPerSecond explicitly.
      total | failed | rows/s |  p50ms |  p99ms | p999ms | batches
    148,266 |      0 |  8,361 | 663.86 | 767.56 | 817.89 |   30.91
    Operation LOAD_20220823-182343-074618 completed successfully in 17 seconds.
    Last processed positions can be found in positions.txt
    ```

**✅ 7c - Count** 

Check than the data has been imported with cqlsh SH

```
astra db cqlsh demo -e "select * from demo.cities_by_country LIMIT 20;"
```

??? abstract "🖥️ Sample output" 

    ```
    Cqlsh is starting please wait for connection establishment...

    country_name | name                | country_code | country_id | id   | latitude | longitude | state_code | state_id | state_name          | wikidataid
    --------------+---------------------+--------------+------------+------+----------+-----------+------------+----------+---------------------+------------
      Bangladesh |             Azimpur |           BD |         19 | 8454 |  23.7298 |   90.3854 |         13 |      771 |      Dhaka District |       null
      Bangladesh |           Badarganj |           BD |         19 | 8455 | 25.67419 |  89.05377 |         55 |      759 |    Rangpur District |       null
      Bangladesh |            Bagerhat |           BD |         19 | 8456 |     22.4 |     89.75 |         27 |      811 |     Khulna District |       null
      Bangladesh |           Bandarban |           BD |         19 | 8457 |       22 |  92.33333 |          B |      803 | Chittagong Division |       null
      Bangladesh |          Baniachang |           BD |         19 | 8458 | 24.51863 |  91.35787 |         60 |      767 |     Sylhet District |       null
      Bangladesh |             Barguna |           BD |         19 | 8459 | 22.13333 |  90.13333 |         06 |      818 |    Barisal District |       null
      Bangladesh |             Barisal |           BD |         19 | 8460 |     22.8 |      90.5 |         06 |      818 |    Barisal District |       null
      Bangladesh |                Bera |           BD |         19 | 8462 | 24.07821 |  89.63262 |         54 |      813 |   Rajshahi District |       null
      Bangladesh |       Bhairab Bāzār |           BD |         19 | 8463 |  24.0524 |   90.9764 |         13 |      771 |      Dhaka District |       null
      Bangladesh |           Bherāmāra |           BD |         19 | 8464 | 24.02452 |  88.99234 |         27 |      811 |     Khulna District |       null
      Bangladesh |               Bhola |           BD |         19 | 8465 | 22.36667 |  90.81667 |         06 |      818 |    Barisal District |       null
      Bangladesh |           Bhāndāria |           BD |         19 | 8466 | 22.48898 |  90.06273 |         06 |      818 |    Barisal District |       null
      Bangladesh | Bhātpāra Abhaynagar |           BD |         19 | 8467 | 23.01472 |  89.43936 |         27 |      811 |     Khulna District |       null
      Bangladesh |           Bibir Hat |           BD |         19 | 8468 | 22.68347 |  91.79058 |          B |      803 | Chittagong Division |       null
      Bangladesh |               Bogra |           BD |         19 | 8469 | 24.78333 |     89.35 |         54 |      813 |   Rajshahi District |       null
      Bangladesh |        Brahmanbaria |           BD |         19 | 8470 | 23.98333 |  91.16667 |          B |      803 | Chittagong Division |       null
      Bangladesh |         Burhānuddin |           BD |         19 | 8471 | 22.49518 |  90.72391 |         06 |      818 |    Barisal District |       null
      Bangladesh |            Bājitpur |           BD |         19 | 8472 | 24.21623 |  90.95002 |         13 |      771 |      Dhaka District |       null
      Bangladesh |            Chandpur |           BD |         19 | 8474 |    23.25 |  90.83333 |          B |      803 | Chittagong Division |       null
      Bangladesh |    Chapai Nababganj |           BD |         19 | 8475 | 24.68333 |     88.25 |         54 |      813 |   Rajshahi District |       null
    ```

- Count with ds bulkd

```
astra db dsbulk demo count -k demo -t cities_by_country
```

???+ abstract "🖥️ Sample output" 

    ```
    DSBulk is starting please wait ...
    [INFO ] - RUNNING: /Users/cedricklunven/.astra/dsbulk-1.9.1/bin/dsbulk count -k demo -t cities_by_country -u token -p AstraCS:gdZaqzmFZszaBTOlLgeecuPs:edd25600df1c01506f5388340f138f277cece2c93cb70f4b5fa386490daa5d44 -b /Users/cedricklunven/.astra/scb/scb_071d7059-d55b-4cdb-90c6-41c26da1a029_us-east-1.zip
    Username and password provided but auth provider not specified, inferring PlainTextAuthProvider
    A cloud secure connect bundle was provided: ignoring all explicit contact points.
    Operation directory: /Users/cedricklunven/Downloads/logs/COUNT_20220823-182833-197954
      total | failed | rows/s |  p50ms |  p99ms | p999ms
    134,574 |      0 | 43,307 | 315.71 | 457.18 | 457.18
    ```

**✅ 7d - UnLoad Data** 

```
astra db dsbulk demo unload -k demo -t cities_by_country -url /tmp/unload
```

???+ abstract "🖥️ Sample output" 

    ```
    DSBulk is starting please wait ...
    Username and password provided but auth provider not specified, inferring PlainTextAuthProvider
    A cloud secure connect bundle was provided: ignoring all explicit contact points.
    Operation directory: /Users/cedricklunven/Downloads/logs/UNLOAD_20220823-183054-208353
      total | failed | rows/s |  p50ms |    p99ms |   p999ms
    134,574 |      0 | 14,103 | 927.51 | 1,853.88 | 1,853.88
    Operation UNLOAD_20220823-183054-208353 completed successfully in 9 seconds.
    ```

### 8. Download Secure bundle

**✅ 8a - Default values** 

Download the different secure bundles (one per region) with the pattern `scb_${dbid}-${dbregion}.zip` in the current folder.

```
mkdir db-demo
cd db-demo
astra db download-scb demo
ls
```

**✅ 8b - Download in target folder** 

Download the different secure bundles (one per region) with the pattern `scb_${dbid}-${dbregion}.zip` in the  folder provide with option `-d` (`--output-director`).

```
astra db download-scb demo -d /tmp
```

**✅ 8c - Download in target folder** 

Provide the target filename with `-f` (`--output-file`). It will work only if you have a SINGLE REGION for your database (or you will have to use the flag `-d`)

```
astra db download-scb demo -f /tmp/demo.zip
```

## User and Roles

### 1. List users

```
astra user list
```

??? abstract "🖥️ Sample output" 

    ```
    +--------------------------------------+-----------------------------+---------------------+
    | User Id                              | User Email                  | Status              |
    +--------------------------------------+-----------------------------+---------------------+
    | b665658a-ae6a-4f30-a740-2342a7fb469c | cedrick.lunven@datastax.com | active              |
    +--------------------------------------+-----------------------------+---------------------+
    ```

### 2. Invite User

```
astra user invite cedrick.lunven@gmail.com
```

Check the list of user and notice the new user invited.

```
astra user list
```

??? abstract "🖥️ Sample output" 

    ```
    +--------------------------------------+-----------------------------+---------------------+
    | User Id                              | User Email                  | Status              |
    +--------------------------------------+-----------------------------+---------------------+
    | 825bd3d3-82ae-404b-9aad-bbb4c53da315 | cedrick.lunven@gmail.com    | invited             |
    | b665658a-ae6a-4f30-a740-2342a7fb469c | cedrick.lunven@datastax.com | active              |
    +--------------------------------------+-----------------------------+---------------------+
    ```

### 3. Revoke User

```
astra user delete cedrick.lunven@gmail.com
```

??? abstract "🖥️ Sample output" 

    ```
    +--------------------------------------+-----------------------------+---------------------+
    | User Id                              | User Email                  | Status              |
    +--------------------------------------+-----------------------------+---------------------+
    | b665658a-ae6a-4f30-a740-2342a7fb469c | cedrick.lunven@datastax.com | active              |
    +--------------------------------------+-----------------------------+---------------------+
    ```


### 4. List roles

```
astra role list
```

### 6. Get role infos

```
astra role get "Database Administrator"
```

## Advanced Topics

### 1 Config Management

If you work with multiple organizations it could be useful to switch from configuration to another, one token to another. The Cli provides a configuration management solution to handle this use case.

**✅ 1a - List available configuration**

```
astra config list
```

**✅ 1b - Create a new section**

```
astra config create dev --token <token_of_org_2>
```

**✅ 1c - Use your section config anywhere**

You can use any organization anytime with `--config <onfig_name>`.

```
astra user list --config dev
```


**✅ 1d - Select a section as defaul**

- Change the current org

```
astra config use dev
```

- See your new list 

 ```
 astra config list
 ```

**✅ 1e - Delete a section**

You can delete any organization. If you delete the selected organization you will have to pick a new one.

- Delete you config
```
astra config delete dev
```

- See the new list

```
astra config list
```
