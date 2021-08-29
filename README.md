# system-backup
A Linux backup system based on `rsync`, `cron`.

## One-time

```bash
rsync -aAXv --delete \
  --exclude-from rsync-excludes.txt \
  --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} \
  / /mnt/external-drive/$(date +%Y%m%d)
```

## Periodic

Add the following lines to your `/etc/crontab` file:

### Daily

```bash
00 12 * * * rsync -aAXv --delete --exclude-from rsync-excludes.txt --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"}  / /mnt/external-drive/daily
```

### Weekly (Friday)

```bash
00 12 * * 5 rsync -aAXv --delete --exclude-from rsync-excludes.txt --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"}  / /mnt/external-drive/weekly
```

### Monthly (first day)

```bash
00 12 1 * * rsync -aAXv --delete --exclude-from rsync-excludes.txt --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"}  / /mnt/external-drive/monthly
```
