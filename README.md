# Gitea

Gitea provides automatically updated Docker images within its Docker Hub organization. It is possible to always use the latest stable tag or to use another service that handles updating Docker images.

This reference setup guides users through the setup based on docker-compose, but the installation of docker-compose is out of scope of this documentation. To install docker-compose itself, follow the official install instructions.


source: https://docs.gitea.io/en-us/install-with-docker/ <br />

## Start
To start this setup based on docker-compose, execute docker-compose up -d, to launch Gitea in the background. Using docker-compose ps will show if Gitea started properly. Logs can be viewed with docker-compose logs. <br />

To shut down the setup, execute docker-compose down. This will stop and kill the containers. The volumes will still exist. <br />

Notice: if using a non-3000 port on http, change app.ini to match LOCAL_ROOT_URL = http://localhost:3000/. <br />

## Install
After starting the Docker setup via docker-compose, Gitea should be available using a favorite browser to finalize the installation. Visit http://server-ip:3000 and follow the installation wizard. If the database was started with the docker-compose setup as documented above, please note that db must be used as the database hostname.

## Environments variables
You can configure some of Gitea’s settings via environment variables:

(Default values are provided in bold) <br />

APP_NAME: “Gitea: Git with a cup of tea”: Application name, used in the page title. <br />
RUN_MODE: dev: For performance and other purposes, change this to prod when deployed to a production environment. <br />
DOMAIN: localhost: Domain name of this server, used for the displayed http clone URL in Gitea’s UI. <br />
SSH_DOMAIN: localhost: Domain name of this server, used for the displayed ssh clone URL in Gitea’s UI. If the install page is enabled, SSH Domain Server takes DOMAIN value in the form (which overwrite this setting on save). <br />
SSH_PORT: 22: SSH port displayed in clone URL. <br />
SSH_LISTEN_PORT: %(SSH_PORT)s: Port for the built-in SSH server. <br />
DISABLE_SSH: false: Disable SSH feature when it’s not available. <br />
HTTP_PORT: 3000: HTTP listen port. <br />
ROOT_URL: "": Overwrite the automatically generated public URL. This is useful if the internal and the external URL don’t match (e.g. in Docker). <br />
LFS_START_SERVER: false: Enables git-lfs support. <br />
DB_TYPE: sqlite3: The database type in use [mysql, postgres, mssql, sqlite3]. <br />
DB_HOST: localhost:3306: Database host address and port. <br />
DB_NAME: gitea: Database name. <br />
DB_USER: root: Database username. <br />
DB_PASSWD: "<empty>”: Database user password. Use `your password` for quoting if you use special characters in the password. <br />
INSTALL_LOCK: false: Disallow access to the install page. <br />
SECRET_KEY: "": Global secret key. This should be changed. If this has a value and INSTALL_LOCK is empty, INSTALL_LOCK will automatically set to true. <br />
DISABLE_REGISTRATION: false: Disable registration, after which only admin can create accounts for users. <br />
REQUIRE_SIGNIN_VIEW: false: Enable this to force users to log in to view any page. <br />
USER_UID: 1000: The UID (Unix user ID) of the user that runs Gitea within the container. Match this to the UID of the owner of the /data volume if using host volumes (this is not necessary with named volumes). <br />
USER_GID: 1000: The GID (Unix group ID) of the user that runs Gitea within the container. Match this to the GID of the owner of the /data volume if using host volumes (this is not necessary with named volumes). <br />
Customization
Customization files described here should be placed in /data/gitea directory. If using host volumes, it’s quite easy to access these files; for named volumes, this is done through another container or by direct access at /var/lib/docker/volumes/gitea_gitea/_data. The configuration file will be saved at /data/gitea/conf/app.ini after the installation.
