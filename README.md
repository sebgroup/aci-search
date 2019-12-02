---------------
About
---------------

ACI-search is a CLI tool for querying Cisco ACI APICs, via their API, displaying object relationships and certain object parameters.


---------------
Requirements
---------------

- Python 2.7

- ACI Cobra
Cobra SDK
https://cobra.readthedocs.io/en/latest/install.html

For database integration
- MariaDB or SQLite database abstracted with SQLAlchemy modules

Modules:
- pip2.7 install PyYAML
- pip2.7 install SQLAlchemy
- pip2.7 install SQLAlchemy-Utils

If you choose to use mysql:
- pip2.7 install mysql-connector-python

---------------
Setup
---------------

In Linux, set up a Python path to find the libraries included in the project, for example:
* "export PYTHONPATH=/home/user/github/"

In this example, "aci-search" project should be placed under /home/user/github/ directory.


You need a config file that includes the name of your APICs and (optionally) credentials. 
* See example file called "config.yaml.sample"
* Place config.yaml file under "aci-search/libraries" folder

Update aci-search.py script with your ACI fabric environment names in following line:
> parser.add_argument('env', nargs='?', choices=('fabric1_alias', 'fabric2_alias')

---------------
Session handling
---------------

* Session cookie file will be automatically created and placed under the current user's home directory
* Session cookie file is hidden and named ".ACI_(your environment name)"
* Session cookie for the script is automaticaly renewed if there is less than 5 minutes left before it expires. This can be configured under libraries/login.py 
* Session timer should be configured in APIC and have greater timeout value than the script. Configuration is found under Admin > AAA > Security Management > Web Token Timeout


---------------
Why Python 2.7?
---------------

We're dependent on ACI Cobra and Cisco has not yet released a Python 3.5 version of it.


---------------
Why ACI Cobra?
---------------

ACI Cobra takes care of:
- ACI object naming
- relations and some error detection
- abstracting the REST API calls and building Python objects from received JSON/XML data


---------------
Why database?
---------------

It's only required for storing and fetching ACI fault information gathered by ACI-search.
All other functionality is only directly querying APICs.


---------------
Additional notes
---------------

This code contains some functions that are not used with "aci-search" script and are intended for configuration. They are not called by "aci-search" but are left in as part of the original code base.