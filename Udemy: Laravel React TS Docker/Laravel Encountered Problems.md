### Default session driver set to `Database`
- Depends what is intended to use, having Custom Form Requests needs to check the session. When the session driver is set to 'database', it checks the session in the  `DatabaseName.session` table which leads to an error.

- If the session doesn't need to be stored in the database, change the value of `SESSION_DRIVER` enviroment variable to `cookie`.

#### Custom form requests sends back a laravel page
- To fix, add heder `X-Requestion-With: XLMHttpRequest`

#### File Permission/Ownership problems
- When an atrisan command is created a file inside the container, its file owner will be set to `root` which prevents file write actions.
- To fix, invoke `chown 1000:1000 */**/* -R` inside the container