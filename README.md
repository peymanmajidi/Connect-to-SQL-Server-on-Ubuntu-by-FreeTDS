# Connect to SQL-Server on Ubuntu by FreeTSD
How to connect to sql server on Ubuntu by FreeTDS

## install FreeTDS

sudo apt-get install wget

sudo apt-get install build-essential

sudo apt-get install libc6-dev

wget ftp://ftp.freetds.org/pub/freetds/stable/freetds-1.00.27.tar.gz

tar -xzf freetds-1.00.27.tar.gz

cd freetds-1.00.27

./configure --prefix=/usr/local --with-tdsver=7.3

make

make install

## install pyodbc
sudo -H pip3 install pyodbc
sudo apt install unixodbc-dev

# Add FreeTSD to pyodc drivers
sudo dpkg-reconfigure tdsodbc

## Test connection

tsql -H 192.168.2.75 -U 'sa' -P 'xxxxxxxxx' -p 1433

## main.py

import pyodbc

print("Connecting...")

cnxn = pyodbc.connect(driver = "{FreeTDS}", server = "192.168.2.75", database="SorterDB" , user="sa", password="server@1314", port = 1433)

print("Connected")

cursor = cnxn.cursor()

cursor.execute('SELECT * FROM [UsersTBL]')

for row in cursor:
    print('row = %r' % (row))


