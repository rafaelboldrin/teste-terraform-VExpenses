Este repositório contém um código Terraform para provisionar uma infraestrutura básica na AWS, incluindo:
- Uma VPC
- Uma Subnet
- Um Security Group
- Uma instância EC2 com Nginx instalado

## Recursos Criados

1. **VPC**:
   - CIDR Block: `10.0.0.0/16`
   - Tag: `Name = "VPC-Main"`

2. **Subnet**:
   - CIDR Block: `10.0.1.0/24`
   - Tag: `Name = "Subnet-Main"`

3. **Security Group**:
   - Permite tráfego SSH de um IP específico (`203.0.113.0/24`).
   - Permite tráfego HTTP (`port 80`) e HTTPS (`port 443`) de qualquer IP.
   - Permite todo o tráfego de saída.
   - Tag: `Name = "Security-Group-Web"`

4. **Instância EC2**:
   - AMI: `ami-0c55b159cbfafe1f0` (Amazon Linux 2 na região `us-east-1`).
   - Tipo de Instância: `t2.micro`.
   - Subnet: Associada à subnet criada.
   - Security Group: Associado ao security group criado.
   - Chave SSH: Utiliza a chave pública em `~/.ssh/id_rsa.pub`.
   - User Data: Instala e configura o Nginx automaticamente.
   - Tags: `Name = "Instancia-Web"`, `Environment = "Producao

## Análise Técnica do Código Terraform

O arquivo main.tf fornecido provavelmente cria uma infraestrutura básica na AWS, incluindo os seguintes recursos:
VPC (Virtual Private Cloud):
Uma VPC é criada para isolar os recursos da AWS em uma rede privada.
## Subnet:
Uma subnet é criada dentro da VPC para segmentar a rede.
## Grupo de Segurança (Security Group):
Um grupo de segurança é criado para controlar o tráfego de entrada e saída da instância EC2.
## Key Pair:
Um par de chaves é criado para permitir o acesso SSH à instância EC2.
## Instância EC2:
Uma instância EC2 é criada para hospedar a aplicação.
## Observações sobre o Código Fornecido
O código pode estar expondo a instância EC2 a acessos SSH de qualquer IP (0.0.0.0/0), o que não é seguro.
Falta a configuração de automação para instalar e configurar o Nginx na instância EC2.
Pode ser interessante adicionar tags aos recursos para melhor organização e gerenciamento.
## Modificação e Melhoria do Código Terraform
## Melhorias de Segurança
Restringir Acesso SSH:
Limitar o acesso SSH a um IP específico (ex.: seu IP público).
## Adicionar Regras de Segurança para o Nginx:
Permitir tráfego HTTP (porta 80) e HTTPS (porta 443).
## Automação da Instalação do Nginx
Usar o user_data para instalar e iniciar o Nginx automaticamente.
## Outras Melhorias
Adicionar tags para identificar os recursos:


   - Passo 1 - Ao invés de permitir acesso SSH de qualquer lugar, restringi o acesso apenas aos endereços IP específicos que precisam se conectar ao servidor. 
   -  Passo 2 - Limitei o tráfego de saída. Ao invés de permitir todo o tráfego de saída, especifiquei apenas os protocolos e portas necessários. 
   -  Passo 3 - Usei grupos de segurança por função, ou seja, criei grupos de segurança diferentes para diferentes funções ou serviços em sua infraestrutura. Isso ajuda 
a minimizar o impacto de uma possível violação.
    - Passo 4 - Revisei e atualizei regularmente as regras de segurança para garantir que elas ainda sejam necessárias e estejam alinhadas com as melhores práticas de 
segurança.
  - Passo 5 - Implementei monitoramento e alertas para detectar e responder rapidamente a atividades suspeitas. Para isso, usei serviços como AWS CloudTrail e AWS 
Config para rastrear mudanças e atividades.
  - Passo 6 - Apliquei o princípio do menor privilégio, garantindo que cada recurso tenha apenas as permissões necessárias para realizar suas funções.
