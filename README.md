Knowledge sources

1. https://medium.com/swlh/postgresql-replication-with-docker-c6a904becf77
2. https://youtu.be/OvSzLjkMmQo

Implimentation

1. Created the two saparate container master and slave for postgres replication refer docker-compose.yml.
   a. check a new folder called postgres-config.
   b. Added a new parameter in pg_hba.conf to allow replication user for all IP addresses ie, host replication all 0.0.0.0/0 trust.
   c. Updated the 3 parameters in postgresql.conf named wal_level = logical, max_replication_slots = 10, max_wal_senders = 10.
2. Updated Makefile according to the new container.
3. copy schema of outline db to replica database's container.
4. Run the following command for replication.

create user replicator with replication encypted password 'admin@123'
CREATE PUBLICATION my_publication FOR ALL TABLES;

CREATE SUBSCRIPTION my_subscription CONNECTION 'host=postgres-master port=5432 dbname=outline user=postgres password=Niks123' PUBLICATION my_publication;
