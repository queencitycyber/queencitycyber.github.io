# Getting msf running

msf = Metasploit Framework

The first thing we need to do to get up and running is start the  PostgreSQL database. This is the database that will store all our current working information and allow us to query the database to find different modules.

To start the database, run`service postgresql start`. It should exit cleanly.

![](/assets/start pql.png)

Then we need to create and initialize the database with `msfdb init.`![](/assets/init_db.png)

And finally start the Metasploit console by entering `msfconsole`

Make sure you're connect with `> db_status`

![](/assets/dbstatus.png)

# Getting msf running

msf = Metasploit Framework

The first thing we need to do to get up and running is start the  PostgreSQL database. This is the database that will store all our current working information and allow us to query the database to find different modules.

To start the database, run`service postgresql start`. It should exit cleanly.

![](/assets/start pql.png)

Then we need to create and initialize the database with `msfdb init.`![](/assets/init_db.png)

And finally start the Metasploit console by entering `msfconsole`

Make sure you're connect with `> db_status`

![](/assets/dbstatus.png)

