# TCC-TESTS

CLI to run my graduation degree tests. I've implement two models for the minimal
common substring partition (MCSP) problem described by Blum e Raidl (2016) using
Google OR-Tools. As instances to problem this repository have a copy of the 
instances provided by Ferdous e Rahman (2013).

### Ortools

If you will use commercial solvers like CPLEX, you will have to compile it from
source as explained [here](https://developers.google.com/optimization/install/python/source_linux).
Otherwise you cant install it from pypi package.

```sh
pip install --upgrade ortools==9.6.2534
```

### Note

I'm unable to install ortools in my system after build it. A workaround is 
source the virtualenv in build folder.

```sh
source /path/to/or-tools-9.6/build/python/venv/bin/activate
```

## Installing dependencies

Dependencies can be installed with pip as follows.

```sh
pip install -r requirements.txt
```

## Google Settings

As this program uses google spreadsheets API you need to provide your own 
authentication credentials.

### Generating user secret file
To generate the client secret file from Google OAuth you can 
follow [this tutorial](https://developers.google.com/workspace/guides/configure-oauth-consent). 

### Add test user
Add your google account to test users in your google cloud project, so you will 
be able to give this program access to your spreadsheets. To do so, go to your 
project console > APIs & Services > OAuth consent screen > Test users > Add users.

## Dotenv

Before use it, rename or copy the dotenv file to .env and assign the variables 
the proper values.

## Options

Flags                                       | Description
---                                         | ---
-h, --help                                  | Show this help message and exit
-v, --version                               | Show program's version number and exit
--verbose                                   | Show debug messages
--local                                     | Don't send send the results to spreadsheets, just print it to stdout
--dry-run                                   | Don't run the tests, only log
--limit LIMIT                               | Time limit in milliseconds
-m, --models {cb,cs} [{cb,cs} ...]          | Defines which model should be used for resolve MCSP problem instances
-g, --group {1,2,3,real}                    | Defines which group of test cases should be used
-c, --cases [CASES ...]                     | Defines which instances should run for testing
-n, --num-executions NUM_EXECUTIONS         | Define how many times a instance should execute
-s, --solvers [{CPLEX,GUROBI,SCIP,CBC} ...] | Defines which solvers should be used
--heuristic {chrobak}                       | Set a heuristic to be used as warm start

## Example

In this case we are running with model Common Substring (-m cs) using instance 
113 (-c 113) from group 1 (-g 1), applying chrobak 
heuristic(--heuristic chrobak), using CPLEX as solver (-s CPLEX) and each 
instance will only run once (-n 1).

```sh
python tests_cli.py -m cs -g 1 -c 113 -n 1 -s CPLEX --heuristic chrobak
```
