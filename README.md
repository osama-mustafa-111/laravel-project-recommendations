
# Database Migrations
- Every (major or minor) change in the database should be recorded in migration file
- Before adding a migration file for a new table, you should use Schema hasTable() check

    ```
    if (Schema::hasTable('users')) {
        // The "users" table exists...
    }
    ```
- Before adding a migration file for a new column, you should use Schema hasColumn() check
  ```
    if (Schema::hasColumn('users', 'email')) {
        // The "users" table exists and has an "email" column...
    }
  ```
- You can run specific migration file with ``` --path ```
    ```
    php artisan migrate --path=/database/migrations/2025_04_01_create_users_table.php
    ```

# Naming Conventions
| What     | How      | Good     | Bad      |
|----------|----------|----------|----------|
| Variable   | camelCase      | $userDetails        | ~~$user_details~~   |
| method     | camelCase      | generatePDF         | ~~generate_PDF~~    |
| Model     | Singular      | User                  | ~~UsersF~~    |



