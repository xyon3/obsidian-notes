- For setting up relatioships in the database please refer to [[Migrations#Creating a relationship table]]
- Laravel won't reconize the relationship right away. It needs to be defined in the respective Models.


##### Setting up relationships in Laravel Eloquent:

This defines `User` model has a **one to many relationship** with `Role`.
```php
// app\Models\User.php
class User extends Model
{
	//
    public function roles(): BelongsTo
    {
        return $this->belongsTo(Role::class);
    }
}
```

This defines `Role` model has a **many to one relationship** with `User`.
```php
// app\Models\Role.php
class Role extends Model
{
	//
    public function users(): HasMany
    {
        return $this->hasMany(User::class);
    }
}
```

This defines `Role` model has a **many to one relationship** with `User`.
```php
// app\Models\Role.php
class Role extends Model
{
	//
    public function permissions()
    {
        return $this->belongsToMany(User::class);
    }
}
```