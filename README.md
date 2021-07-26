### Sobre

Playbook Ansible que criar uma instância EC2 na AWS e já instala e faz algumas configurações do Apache. Dentre as caracteristicas o playbook executa.

- Criação do security group, liberando ssh somente pro nosso IP
- Criação de uma role para utilizar na instância
- Criação da instância EC2 na AWS (c/criação da keypair)
- Instalação dos pacotes apache2 e amazon-cloudwatch-agent
- Configuração para enviar logs do apache para o cloudwatch :nice:

No final do playbook basta acessar o IP público da instância criada que o servidor já estará acessível

### Pré requisitos

- ansible instalado
- conta na aws

### Como executar o playbook

Primeiramente precisamos ajustar algumas variáveis de ambiente, uma do Ansible para não esperar a confirmação da chave ssh e outras duas relativo ao acesso a AWS

```
export AWS_ACCESS_KEY_ID="XXXXXXXXXX"
export AWS_SECRET_ACCESS_KEY="XXXXXXXXXXXXXXXXXX"
export ANSIBLE_HOST_KEY_CHECKING=False
```

Agora precisamos ajustar as variáveis que serão utilizadas no Ansible, fica no arquivo `group_vars/all.yml`. A variável que obrigatoriamente precisa ser ajustada é a `vpc_subnet_id`, que deve ser uma subnet pública da sua conta AWS. A ami utilizada é do Ubuntu 20.04.

Após ajustar as variáveis bata executar o seguinte comando:

```
ansible-playbook -i hosts webserver.yaml
```

No final da execução será exibido o endereço http do seu servidor para acessar e testar se está tudo funcionando.