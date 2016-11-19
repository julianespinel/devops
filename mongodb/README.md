# MongoDB

### Make a Backup

1. Make a compressed backup of a given database:<br>
   `mongodump --gzip --archive=<file-name>.gz --db <database-name>`
1. Check the size of the output file:<br>
   `du -hs <file-name>.gz`

### Restore a backup

1. Decompress the backup:<br>
   `gzip -d <file-name>.gz`
1. Restore the backup to a given database:<br>
   `mongorestore --archive=<file-name> --db <database-name>`
