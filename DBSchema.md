```SQL

CREATE KEYSPACE SeetiTel with replication=('class':'SimpleStrategy', 'replication_factor':1);

CREATE TABLE IF NOT EXISTS whistle(
  id uuid PRIMARY KEY,
  created timestamp,
  type int,
  encrypted bool,
  value text
);

```
