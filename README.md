## Disciplina
* Disciplina: Administração de Sistemas Abertos


## 👤 Discentes

* Maria Carlyni Pereira de Oliveira ** - Matrícula: 20231380003
* Lucas dos Santos Carvalho ** - Matrícula: 20222380007



# WordPress com Nginx Proxy via Vagrant e Ansible

Este projeto provisiona automaticamente um ambiente de desenvolvimento WordPress completo, utilizando Vagrant para criar a máquina virtual, Ansible para configurar o ambiente e Docker Compose para orquestrar uma arquitetura de 3 camadas.

A arquitetura final consiste em:
* Um **Proxy Reverso** com Nginx para gerenciar o tráfego de entrada.
* Um **Servidor Web** com a aplicação WordPress.
* Um **Banco de Dados** MySQL para persistência de dados.

---

## 🏛️ Arquitetura

O fluxo da aplicação funciona da seguinte maneira:

```
Usuário (Navegador)
       |
       v
Máquina Host (Porta 8080)
       |
       v
Vagrant VM (Debian 12)
       |
       v
Docker (Rede 'wordpress')
       |
       +----------------------------+
       |                            |
       v                            v
[ Container: webproxy ] ----> [ Container: webserver ]
  (Nginx - Porta 8080)        (WordPress - Porta 80)
                                    |
                                    v
                              [ Container: database ]
                                    (MySQL)
```

---

## 🛠️ Tecnologias Utilizadas

* **[Vagrant](https://www.vagrantup.com/):** Criação e gerenciamento da máquina virtual de desenvolvimento.
* **[Ansible](https://www.ansible.com/):** Provisionamento e configuração da VM (instalação de Docker e dependências).
* **[Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/):** Orquestração dos contêineres da aplicação.
* **[Nginx](https://www.nginx.com/):** Proxy reverso e balanceador de carga de Camada 4.
* **[WordPress](https://wordpress.org/):** A aplicação web principal.
* **[MySQL](https://www.mysql.com/):** O banco de dados da aplicação.

---

### Subindo o Ambiente

Com tudo configurado, basta um único comando para iniciar todo o ambiente:

```bash
vagrant up
```
Este comando irá:
1.  Baixar e configurar uma VM Debian 12.
2.  Executar o playbook Ansible para instalar o Docker e o Docker Compose.
3.  Copiar o `docker-compose.yml` para a VM.
4.  Iniciar todos os 3 contêineres (`webproxy`, `webserver`, `database`).

###  Acessando a Aplicação

Após o `vagrant up` ser concluído com sucesso, abra seu navegador e acesse:

**[http://IPDAVM:8080]**

Você deverá ver a tela de instalação inicial do WordPress.

---

## 📂 Estrutura do Projeto

```
.
├── Vagrantfile             # Configuração da Máquina Virtual
├── playbook_ansible.yml    # Playbook de automação da configuração
├── docker-compose.yml      # Definição da stack de contêineres
├── nginx/                    # (Opcional) Pasta para construir a imagem Nginx
│   ├── Dockerfile
│   └── nginx.conf
└── README.md               # Este arquivo
```

---

## ⚙️ Comandos Úteis do Vagrant

* `vagrant up`: Inicia e provisiona o ambiente.
* `vagrant provision`: Re-executa o provisionamento Ansible em uma VM já ativa.
* `vagrant ssh`: Conecta-se via SSH ao terminal da VM.
* `vagrant halt`: Desliga a VM.
* `vagrant destroy -f`: Deleta permanentemente a VM.
* http://192.168.56.137:8080/

---

