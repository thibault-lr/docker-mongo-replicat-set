# MongoDB Local replicatSet with AUTH

This repo helps to configure a local replicat set for MongoDB version 7 using authentication database. This read


## Configuration

Create a .env file from the file .env.template and fill  the variables. Example : 

```
MONGO_INITDB_ROOT_USERNAME=admin_user
MONGO_INITDB_ROOT_PASSWORD=admin_password
MONGO_APP_DB=app_db
MONGO_APP_USER=app_user
MONGO_APP_PASSWORD=app_password

```


### Generate a replica-key 
You need to create a KeyFile to set up the authentication  (https://www.mongodb.com/docs/manual/tutorial/enforce-keyfile-access-control-in-existing-replica-set/)

Create one using openssl : 

```bash
openssl rand -base64 756 > example-replica.key 
```


Move that key to the mongo folder : 
```
mv example-replica.key mongo
```

And set up the correct permissions 
```
chmod 400 mongo/example-replica.key
```


Note : if you use another name that `example-replica.key` you need to change the Dockerfile line 11 : 
```
COPY <fileName.key> /data/replica.key
```


Give execution permission on script file :
```
chmod +x scripts/mongo-replicat-setup.sh
```

The script will create the MongoDB replicat SET + authentication database

## Run docker 
You can simply run : 
```
docker-compose up
```


Using the above example will allow you to connect to this URI : 
```
mongodb://app_user:app_password@localhost:27017/app_db?directConnection=true&authSource=app_db
```

You can also connect directly with the admin account : 
```
mongodb://admin_user:admin_root@localhost:27017
```