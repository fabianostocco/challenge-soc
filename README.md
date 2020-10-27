

### Índice
<!--ts-->
 * [Introdução](#Introdução)</li>
 * [Resolução do Teste](#resolução-do-teste)</li>
 * [Resultados](#resultados)</li>
<!--te-->

---
### Introdução

Segue possível resolução para o Teste de SOC.

- Ambiente EC2 Amazon, se utilizando de comandos “awscli” para provisionamento.
Partindo do bate papo, referenciaram a utilização da Amazon como Cloud padrão.

- Foi utilizado o Docker Compose para Start dos contêineres.

- (Solicitado) Efetuar uma analise de vulnerabilidade no ambiente (utilizando ferramentas de análise de vulnerabilidade do mercado ou qualquer uma opensource):
Sera implementando GVM (Greenbone Vulnerability Manager ). Tal ferramenta consegue detectar aplicações, versões e possíveis vulnerabilidades.

- (Solicitado) Enviar todos logs para um concentrador de logs (utilizar a stack ELK):
Utilizado o Filebeat como ferramenta de coleta e envio dos logs ao ElasticSearch.

- (Solicitado) Monitorar todo ambiente com IDS/IPS (suricata ou snort):
Utilizado o Suricata em contêiner privilegiado para monitoramento da interface de entrada do servidor. Não iremos monitorar a comunicação entre as aplicações(DMZ).

- (Solicitado)  Subir uma aplicação web qualquer - CMS (wp,joomla,phpbb etc..):
Iniciado CMS Wordpress conforme exemplo.

- (Solicitado) O objetivo desse teste é monitorar todos serviços como CMS e o banco de dados, tanto as métricas quanto os logs dos containers. Dashboard de monitoramento de métricas dos recursos das aplicações e do serviço de banco de dados:
Utilizado o MetricBeat e HeatBeat para tal solicitação.

- (Solicitado)Dashboard para monitoramento das aplicações, podendo ser no modelo do APM ou busca de logs/erros via pesquisa (requer documentação caso os logs sejam via pesquisa**):
A FAZER

- (Solicitado)Envio de alertas em caso de problemas:
A FAZER


---
### Resolução do Teste

### Provisionamento ambiente Amazon EC2

Partindo que possui o AWS Cli configurado iremos:

- Criar a Security Group liberando o IP de origem;
`aws ec2 create-security-group --group-name SocSG --description "Security group minimo para SOC" --vpc-id vpc-da44c4bd` 
`aws ec2 authorize-security-group-ingress --group-id sg-0d756a342ae3e0e21 --protocol tcp --port 1-65535 --cidr 45.235.52.206/32`

- Criar um EBS onde rodara o volume /var/lib/docker;
`aws ec2 create-volume --volume-type gp2 --size 32 --availability-zone us-east-1a`

- Criar a instancia;
`aws ec2 run-instances --image-id ami-0947d2ba12ee1ff75 --count 1 --instance-type t2.large --key-name soc --security-group-ids sg-0d756a342ae3e0e21 --subnet-id subnet-b41560d1`

- Conectar o EBS a instancia;
`aws ec2 attach-volume --volume-id vol-0a37d4825e052b9f1 --instance-id i-005fe4d4469de5c14 --device /dev/sdb`

- Descobrir o IP Publico;
`aws ec2 describe-instances --instance-ids i-005fe4d4469de5c14 | grep PublicIp`

- Instalar e configurar pré-requisitos;
`ssh -i Downloads/soc.pem ec2-user@18.235.0.245
#Elevação
sudo su -

#Atualizar S.O
yum update -y

#Particionar o disco
parted -s  /dev/xvdb  mklabel msdos
parted -s /dev/xvdb unit mib mkpart primary 1 100% set 1 lvm on
pvcreate /dev/xvdb1
vgcreate vg00.local /dev/xvdb1
lvcreate -L30G --name lv.docker vg00.local
mkfs.xfs  /dev/vg00.local/lv.docker
mkdir /var/lib/docker
echo "/dev/vg00.local/lv.docker  /var/lib/docker  xfs  defaults  1   1" >> /etc/fstab
mount -a

#Instalar o Docker
yum install docker -y
systemctl enable docker
systemctl start docker

#Instalar Docker Compose
curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

echo "vm.max_map_count=262144" >> /etc/sysctl.conf
sysctl -p`
