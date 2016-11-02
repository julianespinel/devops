# MongoDB

### Make a Backup

1. `mongodump --gzip --archive=stockreader_dump.gz --db stockreaderdb`
1. `du -hs stockreader_dump.gz`

### Restore a backup

1. `gzip -d stockreader_dump.gz`
1. `mongorestore --archive=stockreader_dump --db stockreaderdb`
