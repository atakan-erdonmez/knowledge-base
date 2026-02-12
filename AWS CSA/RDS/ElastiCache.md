It is a managed Redis or Memcached
- Reduces load off of a DB for read intensive workload
- AWS takes care of it, OS maintenance, patching, optimization etc
- *Using it required heavy application code changes*

- Applications queries ElastiCache, if not available, get from RDS and store in ElastiCache.
- Cache must have an invalidation strategy to make sure only the most current data is used in there, which makes it hard to set up

It can be used for session data, in user -> multiple sessions and apps

## Patterns
- **Lazy Loading**: all the read data is cached, data can become stale in cache
- **Write Through:** Adds or update data in the cache when written to a DB (no stale data)
- **Session Store:** store temporary session data in a cache (using TTL features)


Important ports
- PostgreSQL: 5432
- MySQL: 3306
- Oracle RDS: 1521
- MSSQL Server: 1433
- MariaDB: 3306 (same as MySQL)
- Aurora: 5432 (if PostgreSQL compatible) or 3306 (if MySQL compatible)