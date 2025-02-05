

# art

## This project was generated by [Flatlogic Platform](https://flatlogic.com).

  - Frontend: [React.js](https://flatlogic.com/templates?framework%5B%5D=react&sort=default)

- Backend: [NoBackend](https://flatlogic.com/templates?backend%5B%5D=no-backend&sort=trending)

  -----------------------
### We offer 2 ways how to start the project locally: by running Frontend and Backend or with Docker.
-----------------------

## To start the project:

### Frontend:

## To start the project with Docker:
### Description:

The project contains the **docker folder** and the `Dockerfile`.

The `Dockerfile` is used to Deploy the project to Google Cloud.

The **docker folder** contains a couple of helper scripts:

- `docker-compose.yml` (all our services: web, backend, db are described here)
- `start-backend.sh` (starts backend, but only after the database)
- `wait-for-it.sh` (imported from https://github.com/vishnubob/wait-for-it)

    > To avoid breaking the application, we recommend you don't edit the following files: everything that includes the **docker folder** and `Dokerfile`.

## Run services:

1. Install docker compose (https://docs.docker.com/compose/install/)

2. Move to `docker` folder. All next steps should be done from this folder.

   ``` cd docker ```

3. Make executables from `wait-for-it.sh` and `start-backend.sh`:

   ``` chmod +x start-backend.sh && chmod +x wait-for-it.sh ```

4. Download dependend projects for services.

5. Review the docker-compose.yml file. Make sure that all services have Dockerfiles. Only db service doesn't require a Dockerfile.

6. Make sure you have needed ports (see them in `ports`) available on your local machine.

7. Start services:

   7.1. With an empty database `rm -rf data && docker-compose up`

   7.2. With a stored (from previus runs) database data `docker-compose up`

8. Check http://localhost:3000

9. Stop services:

   9.1. Just press `Ctr+C`

## Most common errors:

1. `connection refused`

   There could be many reasons, but the most common are:

  - The port is not open on the destination machine.

  - The port is open on the destination machine, but its backlog of pending connections is full.

  - A firewall between the client and server is blocking access (also check local firewalls).

   After checking for firewalls and that the port is open, use telnet to connect to the IP/port to test connectivity. This removes any potential issues from your application.

   ***MacOS:***

   If you suspect that your SSH service might be down, you can run this command to find out:

   `sudo service ssh status`

   If the command line returns a status of down, then you’ve likely found the reason behind your connectivity error.

   ***Ubuntu:***

   Sometimes a connection refused error can also indicate that there is an IP address conflict on your network. You can search for possible IP conflicts by running:

   `arp-scan -I eth0 -l | grep <ipaddress>`

   `arp-scan -I eth0 -l | grep <ipaddress>`

   and

   `arping <ipaddress>`

2. `yarn db:create` creates database with the assembled tables (on MacOS with Postgres database)

   The workaround - put the next commands to your Postgres database terminal:

   `DROP SCHEMA public CASCADE;`

   `CREATE SCHEMA public;`

   `GRANT ALL ON SCHEMA public TO postgres;`

   `GRANT ALL ON SCHEMA public TO public;`

   Afterwards, continue to start your project in the backend directory by running:

   `yarn start`
