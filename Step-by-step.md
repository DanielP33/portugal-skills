Crie três VPCs, duas em US-EAST-1 e a outra em US-WEST-2.
----------VPC----------

VPC em US-EAST-1
Name: pdl-vpc                      <--- Auto Generate, metes memo pdl.
IPv4 CIDR block: 10.0.0.0/20
IPv6 CIDR block: None
Tenancy: Default
Number of Availability Zones: 1
Number of public subnets: 1            
Number of private subnets: 2
NAT gateways: None
VPC endpoints: S3 Gateway
Enable DNS hostnames: Yes
Enable DNS resolution: Yes



VPC em US-EAST-1
Name: web-vpc                      <--- Auto Generate, metes memo web.
IPv4 CIDR block: 10.0.16.0/20
IPv6 CIDR block: None
Tenancy: Default
Number of Availability Zones: 3
Number of public subnets: 3
Number of private subnets: 0
NAT gateways: None
VPC endpoints: S3 Gateway
Enable DNS hostnames: Yes
Enable DNS resolution: Yes



VPC em US-WEST-2
Name: angra-vpc
IPv4 CIDR block: 172.16.0.0/16
IPv6 CIDR block: AWS-provided
Tenancy: Default
Number of Availability Zones: 1
Number of public subnets: 1
Number of private subnets: 2
NAT gateways: None
Egress only internet gateway: Yes
VPC endpoints: S3 Gateway
Enable DNS hostnames: Yes
Enable DNS resolution: Yes

Renomear as VPCs que já veio para "DEFAULT VPC"

-----Configurar o transit Gateway:-----
No Console AWS, vá para o serviço "VPC" e, em seguida, procure por Transit Gateway no menu lateral.
Clique em Create Transit Gateway.

Pode ficar tudo default, tens e de fazer dois transit gateways, um para cada região.

Após a criação da Transit Gateway, precisas anexar as VPCs que queres interligar.
Ainda no Console AWS, vá para Transit Gateway Attachments.

Clique em Create Transit Gateway Attachment.

Escolha a Transit Gateway recém-criada.
VPC Attachment: Escolha a VPC pdl-vpc (em US-EAST-1) e selecione a subnet privada 1.
Repita o processo para anexar a VPC angra-vpc (em US-WEST-2) e selecione a subnet privada 1.

Create Transit Gateway Attachment denovo.

Attachment type: Peering

mete o transit gateway id da outra regiao: ex : tgw-039672365aa938288

vai inicializar, depois é so aceitar. Transit gateway peering é so um, não precisas duas vezes!

O acceptance só funciona da segunda region. (porque mandaste da priemira)


----------END VPC----------




----------S3 BUCKET----------
Ir ao S3 e clicar create bucket

danielpimentel96742
---------END S3--------------

----------INSTANCES----------
srv.pdl.local
ubuntu
t2.small
meter a chave
meter a vpc (pdl-vpc)
subnet publica

network interfaces...
public 1 : 10.0.0.100
private 1 : 10.0.8.100
private 2 : 10.0.9.100

na esquerda meter as subnets direitas para cada interface
anotar a interface publica e ir associar um ip elastico





dmzwin.pdl.local
t2.micro
meter chave
meter vpc (pdl-vpc)
subnet private2

network interfaces...
private 2 : 10.0.9.101





















































































---------END INSTANCES---------
