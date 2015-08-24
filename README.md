# opg-cron-formula
Saltstack formula for managing crontabs via pillar data

## Sample Pillar Data ##

```
cronjobs:
  enabled: True
  jobs:
    btrfsbalance:
      user: root
      hour: '4'
      minute: random
      daymonth: "'*'"
      month: "'*'"
      dayweek: "'*'"
      command: /sbin/btrfs fi balance start -dusage=10 /srv
    test:
      user: root
      hour: 2
      command: echo "this is a test job"
```

The `enabled` key can be set to `False` to remove jobs previously added when it was set to `True`. If there is no pillar data defined at all, `enabled` is treated as `False` but it will not delete any previously added jobs (since it has no `jobs` keys to work from).

Default values for the following are used when not supplied via pillar:

* Hour      (2am)
* Minute    (Random)
* Daymonth  (Every day of the month)
* Month     (Every month of the year)
* Dayweek   (Every day of the week)

The following pillar values MUST be specified as default values cannot be derived:

* User
* Command
