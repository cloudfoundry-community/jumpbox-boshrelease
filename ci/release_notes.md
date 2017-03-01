## Bug Fixes

- The ~/.repo file is no longer constantly updated by the `watcher`
  script. It is only updated when the contents change. This works
  around issues when performing tar-based-backups that take longer
  than 5 minutes, as the watcher script would update the modification/
  creation time of files underneath tar, causing it to error.

##### cf
Bumped cf to v6.25.0

##### vim
Updated vim to v8.0.0386
