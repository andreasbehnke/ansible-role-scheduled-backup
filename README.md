# Ansible Role: Run scheduled backup
Ansible role which configures a service which periodically backups source directories of remote hosts using rsync. Backup of ansible hosts in group ```scheduled_backup_source``` will be performed every ```backup_schedule.frequency_in_minutes``` automatically. A systemd timer is created on the server running backup.

For each host a backup log file is created in ```/var/lib/backup/[hostname].log```

## Groups
This rule supports a ansible group of hosts. All hosts that have files that need to be backed up go into the scheduled_backup_source group.

## Scheduled Backup Sources
The role [ansible-role-backup-source](https://github.com/andreasbehnke/ansible-role-backup-source) must be applied to every host participating as backup source.

Backup source can be any server in your network. This server should be in the ansible inventory group named by variable ```scheduled_backup_source_group_name``` which defaults to ```scheduled_backup_source```. Each backup source must provide the following variables:

```
scheduled_backup_sources:
    - path: "/path/to/files"
      rsync_opts: "-aRH --exclude='lost+found' ..."
      user: "username"
    - path: ...

    ...
```
