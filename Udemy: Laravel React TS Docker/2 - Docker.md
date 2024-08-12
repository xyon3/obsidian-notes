## Installing Docker (Windows)
- Enable Windows Subsystem for Linux (WSL) in Windows Features
- Enable WSL2 in Powershell `wls.exe --set-default 2`
- Download and install Docker Desktop
- Done..


#### Docker Compose Port
```yml
ports:
	- <any-port>:<application-port>
```


#### Executing a command inside a docker container
```bash
#command
docker-compose exec <container-name> <command>

# example - this example lets you access the terminal of `backend` container
docker-compose exec backend sh
```


