
# Backup scripts for cron.daily

* Copy the files beginning with 9* to /etc/cron.daily
* Copy the symlink backup to /etc/cron.daily

## Configuration

The backup system is configured through /etc/default/backup

| Option | Value (Default) | Comment |
| --- | --- | --- |
| daily_backup_enable | "NO" | Activate the backup system with "YES" |
| daily_backup_logfile | "/var/log/backup-daily.log" | The logfile for the backup system |
| daily_backup_error_logfile | "/var/log/backup-error.log" | The error logfile for the backup system |
| **Borgbackup** |
| daily_backup_borg_enable | "NO" | Activate borg backup with "YES" |
| daily_backup_borg_backup_dir | "/mnt/borgbackup" | The borg repository's directory |
| daily_backup_borg_cache_dir | empty | Set to an existing directory to move borg backup's cache |
| daily_backup_borg_options | "-s" | borg backup command line options, e.g. "-v -p -s" |
| daily_backup_borg_include | "/etc /home /root /usr/local/etc /var/log" | Directories included in backup |
| daily_backup_borg_exclude | empty | Directories excluded from backup |
| daily_backup_borg_passphrase_source | "${HOME}/.borg_passphrase" | Path to the file with the passphrase for borg backup |
| **Git** |
| daily_backup_git_enable | "NO" | |
| daily_backup_git_compress | "YES" | |
| daily_backup_git_repository_dir | "/var/git" | |
| daily_backup_git_backup_dir | "/var/backups/git" | |
| daily_backup_git_keep_days | "-14days" | |
| **Grafana** |
| daily_backup_grafana_enable | "NO" | |
| daily_backup_grafana_compress | "YES" | |
| daily_backup_grafana_dir | "/var/db/grafana" | |
| daily_backup_grafana_db | "grafana.db" | |
| daily_backup_grafana_backup_dir | "/var/backups/grafana" | |
| daily_backup_grafana_keep_days | "-14days" | |
| **InfluxDB** |
| daily_backup_influxdb_enable | "NO" | |
| daily_backup_influxdb_compress | "YES" | |
| daily_backup_influxdb_backup_dir | "/var/backups/influxdb" | |
| daily_backup_influxdb_keep_days | "-14days" | |
| **MySQL** |
| daily_backup_mysql_enable | "NO" | |
| daily_backup_mysql_compress | "YES" | |
| daily_backup_mysql_backup_dir | "/var/backups/mysql" | |
| daily_backup_mysql_host | "localhost" | |
| daily_backup_mysql_user | "_backup_" | |
| daily_backup_mysql_password | "_backup_" | |
| daily_backup_mysql_replication | "NO" | |
| daily_backup_mysql_ignore_databases | "information_schema performance_schema sys" | |
| daily_backup_mysql_keep_days | "-14days" | |
| **PostgreSQL** |
| daily_backup_postgresql_enable | "NO" | |
| daily_backup_postgresql_compress | "YES" | |
| daily_backup_postgresql_backup_dir | "/var/backups/postgresql" | |
| daily_backup_postgresql_user | "_backup_" | |
| daily_backup_postgresql_password | "_backup_" | |
| daily_backup_postgresql_list | "SELECT datname FROM pg_database" | |
| daily_backup_postgresql_ignore_databases | "template0 template1" | |
| daily_backup_postgresql_keep_days | "-14days" | |
| **TiddlyWiki** |
| daily_backup_tiddlywiki_enable | "NO" | |
| daily_backup_tiddlywiki_compress | "YES" | |
| daily_backup_tiddlywiki_wiki_dir | "/var/tiddlywiki" | |
| daily_backup_tiddlywiki_backup_dir | "/var/backups/tiddlywiki" | |
| daily_backup_tiddlywiki_keep_days | "-14days" | |

### MySQL Setup

* Create a new user (e.g. _backup_)
** ```CREATE USER '_backup_'@'localhost' IDENTIFIED BY 'password';```
* Grant the required privileges to the user
** ```GRANT SELECT, RELOAD, SHOW DATABASES, LOCK TABLES, EVENT ON *.* TO '_backup_'@'localhost';```
** ```FLUSH PRIVILEGES;```
