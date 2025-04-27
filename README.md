
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
| Model     | Singular      | User                  | ~~Users~~    |


# Refactoring Tips
- Apply naming conventions correctly throughthout the project from the table above.
- Remove commented (unnecessary code) from methods.
- Apply Single Responsiblity Principle in classes (controllers, models, etc.) & methods.
- Extract private functions from controllers in trait or service if used in many classes.
- Apply meaningful names for functions & methods.
- DON'T write comment to explain your code if the code is clear & self-explantory.
- Apply database transaction in methods, if the method handle many operations.
- Handle logging carefully in your methods if error may occur.
- Apply DRY Principle (DON'T Repeat Yourself).
- Keep functions and methods small as possiple.
- Extract complex validation into FormRequest.
- Use Named Parameters in PHP 8.0 when calling function for readability and flexibility.
- Handle three files for .env in your project.
  - ``` .env.dev ```
  - ``` .env.beta ```
  - ``` .env.production ```  
- Align variables inside methods by the equal sign ```(=)``` to improve readability and maintain consistent structure.

   ```
       public function handleSomething()
       {
            $status             = ApInstitutionStatusEnum::values();
            $httpMethods        = HttpMethodsEnum::values();
            $apApiTypes         = ApApiTypes::values();
            $commissionTypes    = CommissionTypeEnum::values();
            $fieldsNames        = getKycFields(withoutApisFields: false);
       }
  ```
- Use Null-Safe Operator ```(?->)``` to access properties safely

  ```
         if ($user->kyc?->status == UserKycStatusEnum::NEED_TO_UPDATE) {
                $user->kyc->status = UserKycStatusEnum::PENDING;
            }
   ```
- Use ```Try-Catch``` block in cases like:
   - When handling external services or APIs
   - Database transactions
   - Custom error handling
- Avoid repeating if conditions in blade file and use custom blade directive
   ```
        Blade::if('closefund', function ($fund) {
            return $fund['type_of_investments'] === 'public_close_ended';
        });

    ```
   ```
        @closefund($fund)
   ```
- Avoid using magic numbers or hard coded values in your code, & use Const or Enum Value
  - Example for magic number:
    ```
        $chart[str()->limit($fund->name, 22)] = $this->charts($fund->id);
    ```
  - Best Practice
    ```
        const FUND_NAME_LIMIT = 22;
        $chart[str()->limit($fund->name, self::FUND_NAME_LIMIT)] = $this->charts($fund->id);
    ```
    
  
