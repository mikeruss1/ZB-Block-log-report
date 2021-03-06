This is a simple PHP program which should sit in the site root. It reads the `killed_log.csv` produced by ZB Block, prints any blocks that are not on the excluded list, and keeps totals for the day. After processing the input file, it is renamed to `copykilledlog.csv`. It does not need to be run each day. It will produce reports on each day present on the input file. Processing starts from the last record processed previously. It can also be run more than once each day, totals are updated as necessary.

A MySQL DB keeps summary totals by day. The record types on the DB are:

- 2. Totals for the day for each excluded block type.
- 3. Total blocks for each day.
- 4. Block types that do not require listing.
- 5. The last record number processed from the log.

There was originally going to be a type 1, blocks requiring further analysis, but I decided the risks of keeping such info on a DB were too high.

The PHP code and the MySQL import can be downloaded. I have set up the type 4 blocks which I use; You can change them as you wish. There is also a type 5 with the record number set to zero.
The only thing you must change is the include on line 7. This should contain something like:

```PHP
$db = mysqli_connect("host address", "hostname", "password");
mysqli_select_db($db, "DB name");
```

Modify to meet your needs.

There is an option to email summary results. This depends on setting the "Why" field of the type 5 record to your email address. Obviously modify the content as needed.

To test it you should just upload the PHP file to the root of the server and add the include. Check the logs are in `/zbblock/vault`, create the DB, and run the program.
