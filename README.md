# Base Infrastructure

What the codes do is about how to setup a standard infrastructure on Public/Private clouds.

## Network Topology

### Diagram

### Virtual Network

Only one in this infrastructure.

### Subnets

Several subnets in one Virtual Network. In my code, there are five standard subnets.

1. Bastion Subnet

   Only jump host.

2. Database Subnet

   It's most important subnet in the whole Virtual Network. There are many private and important data stored in databases/caches/message-queues. Such as PostgreSQL/MySQL/Oracle, Redis/Memached/Cassandra, Kafka/ActiveMQ/RabbitMQ.

3. Application Subnet

   Java/PHP applications, Kubenetes nodes, API Gateway and something like these.

4. OAM(Operation and Management) Subnet

    Deployment Host, Monitoring System(Zabbix, Prometheus), Central Logging(ELK, rsyslog), PKI System(EJBCA), Authentication/Authorization System(LDAP)

5. CEP(Cloud Entry Point) Subnet

   CEP subnet is the only subnet which can be visited from Public Internet. Instances in CEP subnet are allowed to access Internet. Nginx/HaProxy/F5 is the regular CEP middleware in the world. And HTTP Proxy(Squid) of the site is located in CEP subnet too.

### Security Rules

1. Inbound rules of site.

    1. Allow SSH/HTTP/HTTPS traffic from trusted IP/Network.
    2. Allow HTTP/HTTPS and other business traffic from Internet.
    3. Allow several traffic from cloud platform if neccesary.
    4. Disallow other traffic from anywhere.

2. Outbound rules of site.

    1. Allow outbound traffic to Virtual Network.
    2. Allow outbound traffic to Cloud Services.
    3. Disallow outbound traffic to Internet except CEP and Bastion Subnet

3. Internal rules between instances.

    It's hard to say what rules should be set by default. It depends on business model and software design. Just follow the basic rule: Do not open the ports to other instances unless it is neccesary.

## Basic Services of Site

1. Jump Host

2. Deployment Host

3. HTTP Proxy

4. Monitoring System(Optional)

5. Central Logging(Optional)