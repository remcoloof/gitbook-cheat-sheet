# Granting access

### Granting permissions

The commands below can be used to grant a user access to the most used functions of a schema.

```sql
GRANT USAGE ON SCHEMA <schema> TO "<user>";
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA <schema> TO "<user>";
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA <schema> TO "<user>";
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA <schema> TO "<user>";
```

### Resources

* [https://tableplus.com/blog/2018/04/postgresql-how-to-grant-access-to-users.html](https://tableplus.com/blog/2018/04/postgresql-how-to-grant-access-to-users.html)
