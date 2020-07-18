# Generate_series function in PostreSQL

`generate_series([start], [stop], [{optional}step/interval])` is one of the [set returning functions](https://www.postgresql.org/docs/current/functions-srf.html) functions that possibly return more than one row. Could be handy to generate test data for example.

```sql
create table scores (score int, update_date timestamp);

-- number field example
insert into scores (score) 
select g from generate_series(0,100) g(g);

-- timestamp field example
insert into scores (update_date) 
select g from generate_series(now(),now()+'1 day', '1 hour'::interval) g(g);

```

