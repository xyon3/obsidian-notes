It determines if a user is able to perfrom a given action.


#### Example:

In this example the Gate defines an ability `update-post` where if the current user's `id` owns the posts's `user_id`

```php
// app/providers/AppServiceProvider.php

public function boot(): void
{
    Gate::define('update-post', function (User $user, Post $post) {
        return $user->id === $post->user_id;
    });
}
```

When the condition is true, it will proceed. When false, it will return `403 Unauthorized`

This is how it would look like to secure a `Controller` with `Gates`

```php
// app/Http/Controllers/PostController.php
<?php

class PostController extends Controller
{
    public function update(Request $request, Post $post): RedirectResponse
    {
        if (! Gate::allows('update-post', $post)) {
            abort(403);
        }
 
        return redirect('/posts');
    }
}
```


#### Roles & Permissions

`// TODO`