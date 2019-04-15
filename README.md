# udm_import

Command line import tool for Univention Corporate Server (UCS).

Allows to create, modify and delete a list of UDM objects (users, group, settings, imap folder etc) read from a CSV file.

Requires UCS version 4.3 erratum 313 or higher.

# Usage

```bash
$ ./udm_import --help
Usage: udm_import [OPTIONS] UDM_MODULE ACTION FILENAME

  UDM_MODULE is the name of a UDM module like "users/user", "groups/group"
  etc. To see all possible values run "udm modules" on the command line.
  ACTION is one of "create", "modify", "remove".
  FILENAME is the CSV file to read.

Options:
  --help  Show this message and exit.
```

Examples:

```bash
$ ./udm_import users/user create example_users.csv
$ ./udm_import computers/windows modify example_computers.csv
$ ./udm_import groups/group remove example_groups.csv
```

# Installation

Install required Python libraries:
```bash
univention-install python-click python-magic
```

Download the udm_import script and make it executable:
```bash
$ wget https://raw.githubusercontent.com/univention/udm_import/master/udm_import
$ chmod +x udm_import
```

That's it. If you wish to use it without typing long paths, put it in a directory that is in your shells PATH:
```bash
mv udm_import /usr/local/sbin/
```

# File format
* The CSV file should be UTF-8 encoded.
* It is recommended to use the comma (`,`) as column sepratator.
* It is recommended to enclose each cell in double quotes.
* A header line is required.
* Each column header must be a UDM property name. Run `udm <module/name>` to see allowed values.
* When creating a `dn` column is not allowed.
* When modifying or deleting a `dn` column or a column with the unique identifier (e.g. `username` / `name`) must be present.

# Limitations
* Multivalue properties are not yet supported.
* Must be run as root on the DC master, as it doesn't accept LDAP credentials.

# Example files

* [users/user example CSV file](examples/users_user.csv)
* [groups/group example CSV file](examples/groups_group.csv)
* [computers/windows example CSV file](examples/computers_windows.csv)

# Problems
If you encounter a problem or wish to contribute, please create an issue in Github: https://github.com/univention/udm_import/issues
