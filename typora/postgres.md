alter database database_name OWNER TO postgres;

create user postgres with password '123456';

alter user postgres superuser createrole createdb replication;

