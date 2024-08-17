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


##### Eloquent Model Custom Attributes

This allows the model to have specific attribute that is customized.

###### Example


This returns the full name. It can be accessed through `$this->name` or an instantiated object `$order->name`.
```php
    public function getNameAttribute() {
        return $this->first_name . " " . $this->last_name;
    }
```


This returns the total price of an order. It can be accessed through `$this->total_price` or an instantiated object `$order->total_price`.
```php
    public function getTotalPriceAttribute() {
        return $this->orderItems->sum(
	        fn (OrderItem $orderItem) 
		        => $orderItem->quantity * $orderItem->price
	    );
    }
```
