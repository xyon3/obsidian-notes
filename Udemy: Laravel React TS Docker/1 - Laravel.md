If common problems were encountered, please refer to [[Encountered Problems]]
#### Creating a new project
`composer create-project --prefer-dist laravel/laravel <project-name>`

#### [[Dockerizing a project]]
#### [[Sanctum]]


#### Migrations
Inside the terminal of the container, do `php artisan migrate` to create the tables according to the file `database/migrations`


#### Routing
`/routes`
- `api.php` serves the endpoints to `/api/` as the root endpoint
- `web.php` serves the views to the `/` root endpoint

###### If `api.php` does not exist in `routes/` folder
- Invoke `# php artisan install:api` 

#### Controllers
Controllers from `namespace App\Http\Controllers`

###### Creating new controllers
- Invoke `/app # php artisan make:controller <ControllerName>`

#### Requests
Class from `use Illuminate\Http\Request`
###### Creating a custom request
Enables validations and error handling for requests
- Invoke `/app # php artisan make:request <RequestName>`


