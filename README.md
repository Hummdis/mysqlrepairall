# MySQL Repair All

### Version 2.2.0

## Why such a large script?

This script takes into consideration many different things that could happen.  Since the intent of this script is to be run in a screen, it provides minimal output to the TTY, but logs all other activity in `/var/log/mysql_db_repair.log`.    The goal is to be as hands-off as possible to ensure that the process can just run.  Therefore, arguments can be passed to it to make it customizable to a particular need.

=======
## What's the point?

The point of this script is to allow a consistent and safe way for MySQL/MariaDB databases to be backed up and repaired on servers running either MySQL or MariaDB.  While there are many different ways to do this, the main goal is consistency in the process.

## Why such a large script?

This script takes into consideration many different things that could happen.  Since the intent of this script is to be run in a screen, it provides minimal output to the TTY, but logs all other activity in `/var/log/mysql_db_repair.log`.    The goal is to be as hands-off as possible to ensure that the process can just run.  Therefore, arguments can be passed to it to make it customizable to a particular need.

## How do I run it?

The easiest and fastest way is this:

    curl -sL https://raw.githubusercontent.com/Hummdis/mysqlrepairall/master/mysqlrepairall | bash -

Passing arguments:

    curl -sL https://raw.githubusercontent.com/Hummdis/mysqlrepairall/master/mysqlrepairall | bash - [args]

One advantage of the above methods is that no file will be downloaded to the machine you're working on, so you'll make sure that the GitHub version is always the version being run.  If, however, you want to download the file to run it, then you'll want this method:

    wget -a /var/log/mysql_db_repair.log -O /usr/bin/mysqlrepairall https://raw.githubusercontent.com/Hummdis/mysqlrepairall/master/mysqlrepairall && chmod +x /usr/bin/mysqlrepairall && /usr/bin/mysqlrepairall

You may also specify options to skip certain tasks:

```Usage: mysqlrepairall [ OPTIONS ]

    [ OPTIONS ]
	-b	,	--skip-backup
		Skip running the backup process. Use only if you've performed a manual
		export of the database(s) yourself.

	-l	,	--skip-live
		Skip running the live repair process.

	-o	,	--skip-offline	
		Skip running the offline repair process.
	
	-O	,	--skip-optimize
		Skip the InnoDB optimization process.  Useful if it seems to hang up
		some systems.
	
	-m	,	--skip-mysql
		Skip trying to stop MySQL/MariaDB and just run the offline tests.
		This also means that the backups can't be done with mysqldump, so the
		whole $SQL_DIR (/var/lib/mysql is the default) is backed up using TAR
		to Root's home directory.

	-h	,	--help
		Display this help text.
```

=======
## License
This work is licensed under the Creative Commons Attribution-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-sa/4.0/.
