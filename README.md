
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

# Coding Standards
- Keep spaces in ```if``` statements like the follwoing ```[PSR-12: Extended Coding Style]```
  ```
      if ($expr1) {
        // if body
      } elseif ($expr2) {
        // elseif body
      } else {
        // else body;
      }

  ```
- A ```for``` statement looks like the following. Note the placement of parentheses, spaces, and braces ```[PSR-12: Extended Coding Style]```.
  ```
  <?php

    for ($i = 0; $i < 10; $i++) {
        // for body
    }

  ```
- Each individual trait that is imported into a class MUST be included one-per-line and each inclusion MUST have its own use import statement ```[PSR-12: Extended Coding Style]```.

    ```
    class ClassName
    {
        use FirstTrait;
        use SecondTrait;
        use ThirdTrait;
    }
    ```
- Ternary operator must have at least one space around ```?``` and ```:``` characters ```[PSR-12: Extended Coding Style]```
    ```
    $variable = $foo ? 'foo' : 'bar';
    ```
    
# Refactoring Tips
- 💡 Always leave the code better than you found it. :)
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
- Prefer null coalescing (```??```) over verbose ternary checks for defaults
   - ❌ Before: ```$limit = isset($request->limit) ? $request->limit : 20;```
   - ✅ After: ```$limit = $request->limit ?? 20;```
- Take care of ```isset()``` vs ```!empty()```
  - ```isset()``` is faster, but less strict It allows ```''```, ```0```, ```false```, ```'0'```, ```[]```, etc.
  - ```!empty()``` is stricter, It returns false for: ```''``` (empty string), ```0```, ```null```, ```[]```, ```false```
- Use ```Log``` context effectively for better debugging
  - ❌ Bad: ```Log::error('Payment failed');```
  - ✅ Good:
  ```
    Log::error('Payment failed', [
        'user_id'    => $user->id,
        'amount'     => $paymentAmount,
        'request_id' => request()->header('X-Request-ID'),
        'input'      => $request->except(['password']), // avoid sensitive info
        'ip'         => request()->ip(),
    ]);
  ```
- Try to specify the line and file when catch exception
    ```
        try {
            // Logic here
    
        } catch (Exception $e) {
            Log::error('Failed to handle logic', [
                'Error' => $e->getMessage(),
                'File'  => $e->getFile(),
                'Line'  => $e->getLine(),
            ]);
        }

    ```






    
  
