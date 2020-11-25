
# Backup scripts for cron.daily

Copy the files beginning with 9* to /etc/cron.daily
Copy the symlink backup to /etc/cron.daily

## Configuration

The backup system is configured through /etc/default/backup

| Option | Value (Default) | Comment |
| --- | --- | --- |
| daily_backup_enable | "NO" | Activate the backup system with "YES" |
| daily_backup_logfile | "/var/log/backup-daily.log" | The logfile for the backup system |
| daily_backup_error_logfile | "/var/log/backup-error.log" | The error logfile for the backup system |
| daily_backup_borg_enable | "NO" | Activate borg backup with "YES" |
| daily_backup_borg_backup_dir | "/mnt/borgbackup" | The borg repository's directory |
| daily_backup_borg_cache_dir | empty | Set to an existing directory to move borg backup's cache |
| daily_backup_borg_options | "-s" | borg backup command line options, e.g. "-v -p -s" |
| daily_backup_borg_include | "/etc /home /root /usr/local/etc /var/log" | Directories included in backup |
| daily_backup_borg_exclude | empty | Directories excluded from backup |
| daily_backup_borg_passphrase_source | "${HOME}/.borg_passphrase" | Path to the file with the passphrase for borg backup |

