```SQL

CREATE KEYSPACE "SeetiTel" with replication=('class':'SimpleStrategy', 'replication_factor':1);

USE "SeetiTel";

DROP TABLE IF EXISTS whistle;

CREATE TABLE IF NOT EXISTS whistle(
  id uuid,
  dummy int,
  created timestamp,
  type int,
  encrypted boolean,
  value text,
  PRIMARY KEY (dummy, created)
)
WITH CLUSTERING ORDER BY (created DESC);

```
