#### Nltk

_Python ternminal_:-

```
$import nltk  
$nltk.download('wordnet')
$nltk.download('stopwords')
```

#### --CELERY--

run celery worker

```shell script
$celery worker -A newsdigest --loglevel=INFO -Q news,dashboard,default
```

#### -- AWS CodeDeploy --

- ###### [Click](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html) -to check codedeploy-agent installation instruction

- ###### check code [deploy agent status](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html#:~:text=deb%20%3E%20/tmp/logfile-,To%20check%20that%20the%20service%20is%20running,sudo%20service%20codedeploy%2Dagent%20status,-Did%20this%20page) on instances-

    ```shell
    sudo service codedeploy-agent status
    ```
- ###### codedeploy agent log check-
    ```shell
      $ tail -f /var/log/aws/codedeploy-agent/codedeploy-agent.log
    ```

###### WeasyPrint installation ubuntu:-

    sudo apt-get install libxml2-dev libxslt-dev libffi-dev libcairo2-dev libpango1.0-dev
    pip3 install WeasyPrint==52.0



## Installation Guide

1. Clone the repository
    ```
    git clone https://github.com/Fairstays/x-news-digest.git
    ```

2. Create a virtual environment and activate it
    ```
    python -m venv env
    source env/bin/activate
    ```

3. Install the project dependencies
    * Install redis on the system
    * Install Elastic Search 
    * Install Postgres database
    * Install Pgadmin
    * Need to create a 'tnd-production-4306c-1e4c2964822b.json' file on the project root directory.
    * Need to create a .env file in the project root directory.
    * Need to create a apple.key file in the project root directory.
    * Need to run the migrations
        ```
        python3 manage.py migrate_schemas
        ```
     Note: If you are facing the issues while above the commands then you need to run serval commands:
        ```
        python3 manage.py migrate_schemas "app_name" --schema='schemas_name'
        ```
     Note: If still you are facing issues then you need to run migrate files
    * Need to run the fixtures
        ```
        python3 manage.py loaddata client_data
        ```
     Note: Before run this commands redis and elasicsearch must be run the background.
     If you still not able to load fixtures then you need to comments some lines:
    * go to the file_name: 'flavour/signals.py'
    * then comments three lines:
        cache.set('short_link_host', instance.short_link_host)
        cache.set('frontend_host', instance.frontend_host)
        cache.set('static_host', instance.static_host)
    * then try to run again fixtures commands:
        ```
        python3 manage.py loaddata client_data
        ```
    ```
    pip install -r requirements.txt
    ```

4. Create a new file .env in the root directory, and set the environment variables
    * SECRET_KEY=key
    * DEBUG=set_value(True/False)
    * ALLOWED_HOSTS=localhost,127.0.0.1
    * DATABASE_NAME=database_name
    * DATABASE_USER=database_owner
    * DATABASE_PASSWORD=database_password
    * DATABASE_HOST=database_host
    * DATABASE_PORT=database_port
    * SENTRY_DSN='url'
    * SENTRY_ENV='product/local'
    * SENTRY_TRACES_SAMPLE_RATE='0.5'
    * SENTRY_DSN='url'
    * REFER_CODE_LINK='url'
    * CORS_ORIGIN_WHITELIST='allow_host_url'
    * CORS_ALLOW_HEADERS='allow_host_headers'
    * CATEGORY_MINIMUM='3'
