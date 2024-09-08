Minerva relies on a database, and its configuration must be done by the SysAdmin.

We'll divide the database configuration steps.

Minerva DB schema is available at [this url](https://drive.paganosimone.com/s/dREMfOGRmTOHDkx) using `DB_Minerva_Sett2024` as password for accessing the file.
## 1. Create and configure the database server

Minerva uses *mysql* as database server. If you have an already existing MySQL database server with a proper backup solution and ACLs, you can use this. Otherwise, you can spin up a DB server using docker on a VM. 

A sample docker compose for this purpose might look similar to this:

```docker
version: '3.1'
services:
  db:
    image: mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpasswordhere
      MYSQL_DATABASE: sample
    ports:
      - "3306:3306"
  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    restart: always
    environment:
      PMA_HOST: db
    ports:
      - "8080:80"
```

This docker compose is useful if you want to give Minerva a try and you don't want to spin up a proper DB server. It uses phpMyAdmin in order to facilitate the DB management.

### 1.1 Create the Database

If you are using your own database server, make sure to adjust its configuration to the one shown in the following guide.

If you're using the provided docker compose, we prepared a how-to guide that will help you to create the database using phpMyAdmin. 

[Link to the guide.](https://scribehow.com/shared/Create_the_database_table_using_phpMyAdmin__0qoTGKuPSXuMTBS4QuX8aA)

After you finished creating the db table, proceed with this guide.


## 2. Populate the DB

Navigate to Minerva installation directory

```shell
cd /mnt/minerva
```

Where you'll find two files:

- `creadbserver.py`, that will automatically create the DB tables
- `creaautoritagiudiziarie.py`, that will add the autorities into the AutoritaGiudiziarie table.

We need to tune those two file.

### 2.1 Create the database tables

Open `creadbserver.py` using nano

```shell
nano creadbserver.py
```

The file content will be similar to this one

```python
import mysql.connector

# Connection to the MySQL server

conn = mysql.connector.connect(

host="10.10.10.100",

port="3306",

user="poleis",

password="Password100%New",

database="minerva_demo" # Replace with your desired database name

)

cursor = conn.cursor()

  

# Creazione della tabella AnagraficaPrivato se non esiste

cursor.execute('''

CREATE TABLE IF NOT EXISTS AnagraficaPrivato (


[...]
  

# Commit delle modifiche e chiusura della connessione

conn.commit()

conn.close()

  

print("Database e tabelle create con successo.")
```

You'll need to adjust the connection parameter at the beginning of the file. Press CTRL + X when ready to save.

After that run the script with the command

```shell
python creadbserver.py
```

If everything went correctly you'll receive this message from the terminal

```shell
Database e tabelle create con successo.
```

### 2.2 Populate the Authorities table

Open `creaautoritagiudiziarie.py` using nano

```shell
nano creaautoritagiudiziarie.py
```

The file will look similar to this

```python
import mysql.connector

  

# Credenziali di accesso al database

db_config = {

"host": "10.10.10.100",

"port": "3306",

"user": "poleis",

"password": "Password100%New",

"database": "minerva_demo"

}

  

# Lista di autorità giudiziarie da inserire

autorita_giudiziarie = [

"Corte di giustizia tributaria di I grado di Messina",

"Corte di giustizia tributaria di I grado di Catania",

"Corte di giustizia tributaria di II grado di Messina",

"Corte di giustizia tributaria di II grado di Catania",

"Corte di giustizia tributaria di II grado di Palermo",

"Tribunale di Messina",

"Tribunale di Catania",

"Giudice di pace di Messina",

"Giudice di pace di Catania",

"Giudice di pace di Giarre",

]


[...]


```

Modify the list of the Authorities, adding the one needed.

Save the file using CTRL + X, and run it 

```shell
python creaautoritagiudiziarie.py
```

You'll receive a message in case of a positive outcome.

## 3. Modify the app configuration

You finished the database configuration, you'll have to configure the database in the *minervaconf.py* file. Don't worry, we got you covered, [with this guide](/Minerva/Environment configuration/#2-configuring-the-database).

## Done!
Keep following [this guide](/Minerva/Environment configuration/#2-configuring-the-database) to end Minerva configuration.