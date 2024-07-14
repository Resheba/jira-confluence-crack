# Jira

[README](README.md)

+ Long Term Support Version: v9.12.11
+ Latest Version: v9.17.0
+ The new way of use allows you to conveniently upgrade and modify parameters on your own, and it offers convenient support for HTTPS.

+ [Arm Version](#arm)

New Confluence/Jira releases support only Data Center licenses. To generate a Data Center licenses, add the `-d` parameter.

default port: `8080`

## requirement
- docker: 17.09.0+
- docker-compose: 1.24.0+

## How to run with docker-compose

- start jira & mysql

```
git clone ... \
    && cd jira \
    && git checkout rm \
    && docker-compose pull \
    && docker-compose up
```

- start jira & mysql daemon

```
docker-compose up -d
```

- default db(mysql8.0) configure:

```bash
driver=mysql8.0
host=mysql-jira
port=3306
db=jira
user=root
passwd=123456
```

## How to run with docker

- start jira

```
docker volume create jira_home_data && docker network create jira-network && docker run -p 8080:8080 -v jira_home_data:/var/jira --network jira-network --name jira-srv -e TZ='Asia/Shanghai' haxqer/jira:9.17.0
```

- config your own db:


## How to hack jira

```
docker exec jira-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p jira \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

## How to hack jira plugin

- .eg I want to use BigGantt plugin
1. Install BigGantt from jira marketplace.
2. Find `App Key` of BigGantt is : `eu.softwareplant.biggantt`
3. Execute :

```
docker exec jira-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p eu.softwareplant.biggantt \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

4. Paste your license

## How to upgrade

```shell
cd jira && git pull
docker pull haxqer/jira:rm && docker-compose stop
docker-compose rm
```

enter `y`, then start server

```shell
docker-compose up -d
```

## Arm
Not completely tested.
Tested machines:
+ Mac mini(M1,2020)


```
git clone ... \
    && cd jira \
    && git checkout rm && cd lts_arm \
    && docker-compose pull \
    && docker-compose up
```

## Hack Jira Service Management(jsm) Plugin

```
docker exec jira-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p jsm \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org/ \
    -s you-server-id
```


# Confluence


New Confluence/Jira releases support only Data Center licenses. To generate a Data Center licenses, add the `-d` parameter.


[README](README.md)

default port: 8090

## Requirement
- docker-compose: 17.09.0+

## How to run with docker-compose

- start confluence & mysql

```
git clone ... \
    && cd confluence \
    && docker-compose up
```

- start confluence & mysql daemon

```
docker-compose up -d
```

- default db(mysql8.0) configure:

```bash
driver=mysql8.0
host=mysql-jira
port=3306
db=jira
user=root
passwd=123456
```

## How to run with docker

- start confluence

```
docker volume create confluence_home_data && docker network create confluence-network && docker run -p 8090:8090 -v confluence_home_data:/var/confluence --network confluence-network --name confluence-srv -e TZ='Asia/Shanghai' haxqer/confluence:8.9.4
```

- config your own db:


## How to hack confluence

```
docker exec confluence-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p conf \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

## How to hack confluence plugin

- .eg I want to use BigGantt plugin
1. Install BigGantt from confluence marketplace.
2. Find `App Key` of BigGantt is : `eu.softwareplant.biggantt`
3. Execute :

```
docker exec confluence-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p eu.softwareplant.biggantt \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

4. Paste your license


## How to upgrade

```shell
cd confluence && git pull
docker pull haxqer/confluence:latest && docker-compose stop
docker-compose rm
```

enter `y`, then start server

```shell
docker-compose up -d
```
