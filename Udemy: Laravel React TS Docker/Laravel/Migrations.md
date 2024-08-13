`database/migrations`
#### Commands:

###### `# php artisan make:migration <migration_name>`
- Creates a migration file

###### `# php artisan migrate`
- Creates the tables in the connected database

###### `# php artisan migrate:fresh` 
- Use this when there are new relationship errors when migrating.
- DO NOT USE IN PROD, It will delete all data in the tables


#### Examples:

##### Creating a new table

I this example, `up()` runs the migrations that will create a `users` table and add the columns respectively.

```php
// create_users_table.php
    public function up(): void
    {
        Schema::create("users", function (Blueprint $table) {
            $table->id();
            $table->string("first_name");
            $table->string("last_name");
            $table->string("email")->unique();
            $table->string("password");
            $table->timestamps();
        });
    }
```

`down()` runs when reversing the migrations.
```php
    public function down(): void
    {
        Schema::dropIfExists("users");
    }
```

##### Creating a relationship table

Creates a new column `users.role_id` in the `users` table and assigning a foreign key which referenses `roles.id` on `roles` table.

```php
// add_role_id_to_users_table.php
    public function up(): void
    {
        Schema::table("users", function (Blueprint $table) {
            $table->unsignedBigInteger("role_id");
            $table->foreign("role_id")->references("id")->on("roles");
        });
    }
```

Drops the foreign key `role_id` first then the column `role_id`
```php
    public function down(): void
    {
        Schema::table("users", function (Blueprint $table) {
            //
            $table->dropForeign(["role_id"]);
            $table->dropColumn("role_id");
        });
    }
```

