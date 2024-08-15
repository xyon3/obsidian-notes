#### Database Seeders
`dir: database/seeders/DatabaseSeeder.php`

- generate random data to populate the database. It uses the `faker` library as the RNG.
- in this snippet, the seeder will create ten (10) random data for the `user table`.

```php
// it uses the model to push the random data to the database.
use \App\Models\User;

class DatabaseSeeder extends Seeder {
	public function run(): void {
		User::factory(10)->create();
	}
}
```


##### Creating Seeders
`# php artisan make:seeder <SeederClassName>`

##### Seeding
`# php artisan db:seed`
- this will seed all database tables

`# php artisan db:seed --class=<SeederClassName>`
- this will seed a specified table

#### Factories
`dir: database/factories`

- define what kind of data will be pushed to the columns.
- in this sinppet, the factory will defines that it will create data for the fields listed corresponding to their faker methods.

```php
class UserFactory extends Factory {
	public function definition(): array {
		"first_name" => fake()->firstName(),
		"last_name" => fake()->lastName(),
        "email" => fake()->unique()->safeEmail(),
        "password" => (static::$password ??= Hash::make("password")),
        "role_id" => $this->faker->numberBetween(1, 3),
	}
}
```

##### Creating factories
`# php artisan make:factory <FactoryName>`