# Messenger

A one-to-one realtime chat app.

## Working inside a Cloud Environment
### Environment Setup
This repository supports Gitpod, so you can quickly setup your dev environment in the cloud by opening `https://gitpod.io/#https://github.com/<your-username>/<your-repo-name>` in your browser. A Gitpod workspace looks almost identical to Visual Studio Code.
![gitpod-demo](https://user-images.githubusercontent.com/8978815/154584026-8d252528-869a-4587-8387-5db0fb6213b6.png)
When you open a Gitpod page,
- Setup scripts will be automatically run in two integrated terminals - one for backend and the other for frontend.
- You can find Remote Explorer extension on the left edge. This extension shows the list of open ports and lets you connect to those ports by clicking the browser icon.

All changes you make inside this Gitpod workspace remains in the cloud even after you close the tab. You can access your existing workspaces on [Gitpod dashboard](https://gitpod.io/workspaces), and resume your work by opening the workspace again.

### Using Git inside Gitpod
You have full access to `git` CLI within Gitpod terminal, and Visual Studio Code's git integration is available too if your prefer GUI. You would need to create a new branch and push it in order to open a PR on GitHub. Some common commands are listed below:
- `git checkout <branch-name>`: switch to a specific branch.
- `git checkout -b <branch-name>`: create a new branch.
- `git push`: push changes to the remote repository (GitHub in this case).

## Local Setup

Create the PostgreSQL database (these instructions may need to be adapted for your operating system):

```
psql
CREATE DATABASE messenger;
\q
```

Alternatively, if you have docker installed, you can use it to spawn a postgres instance on your machine:

```
docker run -it -p 5432:5432 -e POSTGRES_DB=<database-name> -e POSTGRES_USER=<database-username> -e POSTGRES_PASSWORD=<database-password> postgres -c log_statement=all
```

Create a `.env` file in the server directory and add the following variables (make any modifications to fit your local installation):
```
SECRET_KEY="YourSecretKey"
ENV="development"
POSTGRES_ENGINE="django.db.backends.postgresql_psycopg2"
POSTGRES_HOST="localhost"
POSTGRES_PORT=5432
POSTGRES_DATABASE="messenger"
POSTGRES_USER="user"
POSTGRES_PASSWORD="password"

```


In the server folder, install dependencies and then seed the database (you may want to use a virtual environment):

```
cd server
pip install -r requirements.txt

python manage.py makemigrations
python manage.py migrate 

python manage.py shell
from messenger_backend.seed import seed
seed()
exit()

```

In the client folder, install dependencies:

```
cd client
npm install
```

### Running the Application Locally

In one terminal, start the front end:

```
cd client
npm start
```

In a separate terminal, start the back end:

```
cd server
python manage.py runserver
```

### Running Tests on the Server
```
cd server
python manage.py test
```
