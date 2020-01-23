# Prisma Template!
> 🚧 (WIP) Please don't use it because it's still under development :P



![PRISMA LOGO](https://i.imgur.com/OSP03AP.png)



# 🚀 Spec

- GraphQL & NodeJs & Prisma & Typescript
- Optimized AWS EC2 & AWS RDS.



## 🧩 Installation

```bash
git clone https://github.com/hmmhmmhm/prisma-template.git
npm install
npm start
```



## 🧩 Guide for Connect of RDS <-> Prisma

🤔 This template helps a connection with the DB server to actually use it.

> You can connect to DB server that is compatible with Prisma. [See Primsa Support Database List](https://www.prisma.io/docs/get-started/01-setting-up-prisma-new-database-JAVASCRIPT-a002/)



### 📙 1 - Create AWS RDS Instance

> This template recommends using AWS RDS as a Database service. The AWS RDS gives you free control over performance and ensures reliable service.

[See Connect Prisma With AWS RDS Guide](https://www.prisma.io/docs/1.4/tutorials/cluster-deployment/prisma-cloud-(aws-rds)-ua9gai4kie)



##### ⚠️ NO HIGHEST DB VERSION

> 😓 It is recommended that the DB version be used exactly like the manual. The latest version has a very high probability of error. (In particular, the **version 8 of MySQL was not available** at all.)



##### ⚠️ CHECK PORT FORWARDING

> 🤓 In the security group, direct ports should be specified and opened in the in-bound and outbound options. (Example: If you are operating an RDS server on a port 3306, you must specify port 3306. **Perhaps an option named "MYSQL/Aurora" exists**.)



### 📙 2 - Pre Setup "docker-compose.yml"

If you do not know anything about Prisma setting, you can obtain the default setting value for Prisma by using the command below.

```bash
sudo npm i -g prisma
prisma init hello-world
```

If you proceed with the above process, you will get the **"docker-compose.yml"** file. Move the file to **"[template path]/docker-compose.yml"**. 



##### ‼️(IMPORTANT) YOU MUST REMOVE "SCHEMA" KEY IN DOCKER-COMPOSE.YML

> 👩🏻‍💻 If you using mysql, delete the **schema** key that exists in environment -> databases -> default.



##### ‼️(IMPORTANT) YOU MUST SET FALSE "rawAccess" KEY IN DOCKER-COMPOSE.YML

> 👩🏻‍💻 If you using prisma admin page, change to false the **rawAccess** key that exists in environment -> databases -> default.



##### ⚠️ IF YOU WANT CONNECT TO AT HOME CHECK PUBLICLY

> 🤓 If you want your DB to be accessible not only from within AWS but from other IPs outside, the "**Publicly accessible**" option should be set to yes.



### 📙 3 - Create AWS EC2 Instance

> In prisma 1, you must use the docker without fail, I would like to recommend a preconfigured uuntu image with a preinstalled version of the docker.



**💽 Recommended EC2 Image Name**: <u>ubuntu-lts-18.04-base-1542848667</u>

**♻️ How to Install Node v13.x**

```bash
sudo apt -y update && sudo apt -y upgrade
curl -sL https://deb.nodesource.com/setup_13.x | sudo bash -
sudo apt-get install -y nodejs
sudo apt-get install gcc g++ make
```



**🔐 Configuration your .env keys.**

Before you run the server, modify the .env file that exists in the top-level path of the project.

```bash
PRISMA_SECRET="prisma_type_your_any_key"
PRISMA_MANAGEMENT_API_SECRET="prisma_type_your_any_key"
APP_SECRET="app_type_your_any_key"
```

[See detail of secret manage kes.](https://www.prisma.io/docs/reference/service-configuration/prisma.yml/yaml-structure-ufeshusai8#secret-(optional))

[See detail of authentication keys.](https://www.prisma.io/docs/reference/prisma-api/concepts-utee3eiquo#authentication)



**🥾 Install & Run Prisma Docker Server**

Use the command below to install the docker image before running the server.

```bash
sudo docker-compose up -d
```



##### 😇 YOU CAN USE DOCKER RE-INSTALL COMMAND

> 🚧 If there is a problem with the Prisma docker server, you can run the docker server again with the command below.

```bash
sudo docker-compose kill
sudo docker-compose down
sudo docker-compose up -d
```



##### 😇 YOU CAN ALSO CHECK DOCKER LOGS

> 🚧 If there is a problem with the Prisma docker server, you can run the docker server again with the command below.

```bash
sudo docker-compose logs
sudo docker ps (you can check docker list)
```



**🥾 Run Prisma Instance Server**

Use the command below to start  the prisma server as production mode.

```bash
sudo npm run production-build
sudo npm run production
```

or you can start immediately as below,

```bash
sudo npm run start
```



### 📙 4 - Check your endpoints

You will be can enter the **Prisma Playground**, and **Prisma Admin Server**,

**Prisma Playground URL**: <u>http://<YOUR_DOMAIN_OR_IP>:4000</u>

**Prisma Admin Page URL**: <u>http://<YOUR_DOMAIN_OR_IP>:4466</u>



##### 😓 YOU NEED TO CHECK YOUR ADMIN TOKEN

> 🚧  The administrator page must access the page and enter the token by clicking on the cog-shaped icon. Token can be obtained by typing prisma token on the server where the docker server is running.

```bash
sudo npm install -g prisma
prisma token
```





##### 👋 FINISHED INSTALLATION

> If you have finished all of the above, the installation process is now complete. Now modify the files in the paths below to configure the Graphql server.



**Model Path:** (PROJECT_FOLDER)/prisma/datamodel.graphql

**Schema Path:** (PROJECT_FOLDER)/src/schema.graphql

**Resolver Path:** (PROJECT_FOLDER)/src/resolvers/



## 📙 LICENSE

MIT LIncesed.