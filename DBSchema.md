```SQL

CREATE KEYSPACE SeetiTel with replication=('class':'SimpleStrategy', 'replication_factor':1);

CREATE TABLE whistles(
  id int PRIMARY KEY,
  created int,
  type text,
  encrypted int,
  value text
);

```
