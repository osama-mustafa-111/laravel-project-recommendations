
# Database Migrations
- Every change (major or minor) in database should be recorded as migration file
- Before adding new table migration file, you should use Schema has table check

    ```
    if (Schema::hasTable('users')) {
        // The "users" table exists...
    }
    ```



