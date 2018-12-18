
## 在centos7上安装kafka


### 1. 安装Docker（如果已有docker则无需安装）

sudo yum install -y yum-utils device-mapper-persistent-data lvm2

sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce

sudo usermod -aG docker $(whoami)

sudo systemctl enable docker.service

sudo systemctl start docker.service



### 2. 安装Docker Compose（如果已有docker compose则无需安装）

sudo yum install epel-release

sudo yum install -y python-pip

sudo pip install docker-compose

sudo yum upgrade python*

docker-compose version

### 3. 使用Docker启动kafka

在一个文件夹创建docker-compose.yml文件，内容为（注意47.106.143.76要改成你的机器的IP地址）：

version: '3'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    depends_on: [ zookeeper ]
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 47.106.143.76
      KAFKA_CREATE_TOPICS: "test:1:1"
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
	  
	  
### 4. 构建
docker-compose build

### 5. 启动
docker-compose up -d

### 6. 测试
docker ps -a

### 7. kafka-manager监控（注意47.106.143.76要改成你的机器的IP地址）
docker pull sheepkiller/kafka-manager
docker run --name kafka_manager_1 -it --rm -p 9000:9000 -e ZK_HOSTS="47.106.143.76:2181" -e APPLICATION_SECRET=letmein sheepkiller/kafka-manager
如：docker run --name kafka_manager_1 -it --rm -p 9000:9000 -e ZK_HOSTS="192.168.101.64:2181" -e APPLICATION_SECRET=letmein sheepkiller/kafka-manager


### 常见问题

#### 1. Firewalld error with Docker 'No route to host'
This issue applies to: RHEL/CentOS 7.x and later

firewall-cmd --permanent --direct --add-rule ipv4 filter INPUT 4 -i docker0 -j ACCEPT

firewall-cmd --reload
systemctl restart docker