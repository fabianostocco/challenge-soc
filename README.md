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


aws ec2 create-security-group --group-name SocSG --description "Security group minimo para SOC" --vpc-id vpc-da44c4bd
aws ec2 authorize-security-group-ingress --group-id SocSG --protocol tcp --port 1-65535 --cidr 45.235.52.206/32

aws ec2 create-volume --volume-type gp2 --size 32 --availability-zone us-east-1a
aws ec2 run-instances --image-id ami-0947d2ba12ee1ff75 --count 1 --instance-type t2.large --key-name soc --security-group-ids SocSG --subnet-id subnet-b41560d1

aws ec2 describe-volumes
aws ec2 describe-instances

aws ec2 attach-volume --volume-id vol-1234567890abcdef0 --instance-id i-01474ef662b89480 --device /dev/sdb
