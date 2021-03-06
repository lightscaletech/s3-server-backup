# s3-server-backup
A tool to setup with CRON on a server to back it up to Amazon S3. This is designed to be run everyday and will create nightly and weekly backups with an option of how many of each too retain. It works by creating a temparary archive in `/tmp` then copys that to S3 and deletes the left overs.

## Disclaimer
The Software is provided "AS IS" and "WITH ALL FAULTS," without warranty of any kind, including without limitation the warranties of merchantability, fitness for a particular purpose and non-infringement. The Licensor makes no warranty that the Software is free of defects or is suitable for any particular purpose. In no event shall the Licensor be responsible for loss or damages arising from the installation or use of the Software, including but not limited to any indirect, punitive, special, incidental or consequential damages of any character including, without limitation, damages for loss of goodwill, work stoppage, computer failure or malfunction, or any and all other commercial damages or losses. The entire risk as to the quality and performance of the Software is borne by you. Should the Software prove defective, you and not the Licensor assume the entire cost of any service and repair.

## Requirements
* Python 2
* minio

## Database support
Currently this script can only dump one database each run. Going forward this may need to change for me right now this is acceptable.

It support different DBMSs:
* MySQL (mysqldump)
* Postgres (pg_dump)

NOTE: The database user used for postgres needs to support password login for this to work. This can be configured in `/etc/postgresql/{PG_VERSION}/main/pg_hba.conf` on most distrobutions.

## Usage

### Configuration
To configure this please update the config module. The options within this file are fairly self explanatary.

### Via Shell

To simply run a backup all you need to do is run:

```
./backup.py
```

### Via Cron

To setup cron you need to run `backup.py` at a certain time. A typical setup here is to run it at some time overnight every day.

To edit your cron jobs run the following. Think about the user that this is run under. Do they have the permissions to access the files and database that you want to backup. They also need to be able to write to the temp directory specified in the config file.

```
crontab -e
```

Then insert and tweek the following:

```
12 2 * * * /path/to/backup.py
```

© 2017 LIGHTSCALE TECH LTD ALL RIGHTS RESERVED
