# Projeto de Administração de Sistemas

Este projeto visa automatizar tarefas de administração de sistemas utilizando **Ansible** para provisionamento e configuração de servidores. O objetivo é configurar um ambiente de servidor com as seguintes características:

- Gerenciamento de pacotes e atualizações
- Configuração de usuários e grupos
- Configuração do SSH
- Criação de Volume Group e Logical Volume com LVM
- Configuração de NFS (Network File System)
- Criação de script de log de acessos e monitoramento

O projeto foi desenvolvido para ser facilmente configurável e escalável, podendo ser aplicado em servidores virtuais provisionados com **Vagrant**.

## Objetivo

O principal objetivo desse projeto é automatizar a configuração e manutenção de um servidor Linux utilizando **Ansible**. O playbook configura o sistema, cria usuários, grupos, configura o acesso SSH, monta volumes com LVM e configura NFS para compartilhamento de arquivos.

## Funcionalidades Implementadas

1. Gerenciamento de Pacotes e Atualizações
   - Atualização do cache de pacotes e execução de upgrade de todos os pacotes.
   - Remoção de pacotes obsoletos.
2. Configuração de Hostname
   - Configuração do nome do host do servidor.
3. Gestão de Usuários e Grupos
   - Criação de usuários.
   - Criação de grupos e adição de usuários a grupos específicos.
4. Configuração de SSH
   - Configuração do SSH para permitir o acesso apenas com chave pública.
   - Bloqueio do acesso SSH para o usuário root.
   - Permissão de acesso a usuários de grupos específicos via SSH.
5. Configuração de LVM (Logical Volume Manager)
   - Criação de volume físico (PV), grupo de volumes (VG) e volumes lógicos (LV).
   - Formatação e montagem dos volumes lógicos via fstab.
6. Configuração de NFS (Network File System)
   - Instalação do servidor NFS e criação de diretórios compartilhados.
   - Configuração de exportações no arquivo /etc/exports.
   - Criação de usuário para acessar as pastas compartilhadas via NFS.
7. Log de Acessos
   - Criação de um arquivo de log para monitorar acessos via SSH.
   - Criação de um script de monitoramento de login para execução no login do sistema.

## Estrutura do Projeto

O projeto é dividido em arquivos e diretórios conforme abaixo:

```
projeto/
├── playbook.yml             # Playbook principal que executa as tarefas
└── roles/                   # Diretório contendo as roles para diferentes tarefas
    ├── apt/                 # Atualizações e gerenciamento de pacotes
    │   └── tasks/
    │       └── main.yml
    ├── hostname/            # Configuração do hostname
    │   └── tasks/
    │       └── main.yml
    ├── users/               # Criação de usuários e grupos
    │   └── tasks/
    │       └── main.yml
    ├── ssh/                 # Configuração do SSH
    │   └── tasks/
    │       └── main.yml
    |   └── handlers/        # Handlers do SSH
    │       └── main.yml
    ├── lvm/                 # Configuração de LVM
    │   └── tasks/
    │       └── main.yml
    ├── nfs/                 # Configuração do NFS
    │   └── tasks/
    │       └── main.yml
    │   └── handlers/        # Handlers do NFS
    │       └── main.yml
    └── logging/             # Configuração do log de acessos
        └── tasks/
            └── main.yml
```

## Requisitos

- Vagrant - Para provisionamento de máquinas virtuais.
- VirtualBox ou outro provedor de Vagrant compatível.
- Ansible - Para automação de configuração.
- Sistema operacional baseado em Linux (ex: Ubuntu, Debian).

## Como Usar

1. Instalar dependências:
   - Certifique-se de que o **Vagrant** e o **Ansible** estão instalados em seu sistema.
2. Configuração do ambiente:
   - Clone o repositório para o seu diretório local:
     ```bash
     git clone https://github.com/Jacksoan-Eufrosino/projeto_ASA.git
     cd projeto_ASA
     ```
3. Configuração do Vagrant:
   - Instale as dependencias do **Ansible** como os modulos _ansible.posix_ e _community.general_
     ```bash
     ansible-galaxy install -r requirements.yml
     ```
   - Inicie a máquina virtual com o Vagrant:
     ```bash
     vagrant up
     ```
   - Isso irá provisionar a máquina virtual automaticamente usando o **Ansible**.
