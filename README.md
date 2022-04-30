# Commands in order

```
sudo apt-get update
```

## Install git
```
sudo apt install -y git
```

## Install docker
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## Install Docker composer

```
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}

mkdir -p $DOCKER_CONFIG/cli-plugins

curl -SL https://github.com/docker/compose/releases/download/v2.4.1/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose

chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
```

## Clone repositories
```
git clone git@github.com:howkins/todo-dockerize.git

git clone git@github.com:howkins/todo-application.git

git clone git@github.com:howkins/todo-backend.git
```

## Install node & npm
```
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt-get install -y nodejs
```


## exec `npm i` to projects todo-application & todo-backend
```
npm install --prefix ./todo-backend/
npm install --prefix ./todo-application/
```

## Run containers
```
sudo docker compose up -d
```

## Custom exec commands to backend
```
sudo docker exec -i todo-backend npm i -g dotenv-cli
sudo docker exec -i todo-backend npm run migrate:postgres
```

## Integration tests
```
sudo docker exec -i todo-backend npm run test
```