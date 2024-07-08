# PART 1 - Alembic-FastAPI

# PART 2 - Alembic-FastAPI `https://github.com/Alamnzr123/alembic-fastapi-part2`

This is simple init how to create data using Alembic ORM with FastAPI.
I separate 2 part which Part 1 : Init project and simple setup
Part 2 : More structure files and use Best Practice. 

![screenshot](ss.png)

## Set Up Project

1. clone repo `https://github.com/Alamnzr123/alembic-fastapi`
2. Install package: 
```
pip install fastapi fastapi-sqlalchemy pydantic alembic psycopg2 uvicorn
```
3. Delete this "alembic" folder and Create new using :

```
 alembic init alembic
```
4. Open "alembic.ini" and Edit :

```
sqlalchemy.url = driver://user:pass@localhost/dbname
```

To :

```
sqlalchemy.url = 
```

5. Install env package :

```
pip install python-dotenv
```

6. create a .env file :

```
DATABASE_URL = postgresql+psycopg2://postgres:alam@localhost:5432/alembic_test
```
Edit with your configuration

7. Edit "alembic/env.py" :

```
from logging.config import fileConfig

from sqlalchemy import engine_from_config
from sqlalchemy import poolfrom alembic import context
# ---------------- added code here -------------------------#
import os, sys
from dotenv import load_dotenv

BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
load_dotenv(os.path.join(BASE_DIR, ".env"))
sys.path.append(BASE_DIR)
#------------------------------------------------------------#
# this is the Alembic Config object, which provides
# access to the values within the .ini file in use.
config = context.config
# ---------------- added code here -------------------------#
# this will overwrite the ini-file sqlalchemy.url path
# with the path given in the config of the main code
config.set_main_option("sqlalchemy.url", os.environ["DATABASE_URL"])
#------------------------------------------------------------#
# Interpret the config file for Python logging.
# This line sets up loggers basically.
fileConfig(config.config_file_name)

# add your model's MetaData object here
# for 'autogenerate' support
# from myapp import mymodel
# target_metadata = mymodel.Base.metadata
# ---------------- added code here -------------------------#
import models
#------------------------------------------------------------#
# ---------------- changed code here -------------------------#
# here target_metadata was equal to None
target_metadata = models.Base.metadata
#------------------------------------------------------------#
```

Do not delete all just edit same as above


8. make our first migration on PostgreSQL :

```
alembic revision --autogenerate -m "First migration"
```

9. run the migration :

```
alembic upgrade head
```

10. Run SERVER/APP :

```
uvicorn main:app
```

11. Open PGAdmin4 and find your DB
12. Open `http://127.0.0.1:8000/docs` FASTAPI SERVER to CREATE data
or using POSTMAN
13. DONE.

* IGNORE THE `Pipfile` using pip package manager

## Package

alembic
fastAPI
Pydantic
