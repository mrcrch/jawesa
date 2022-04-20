# JAWESA: Just Another Working Environment Setup with Ansible

<center>

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white) ![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

</center>

## 🖊️ Introdução

Esse projeto consiste de um Playbook [Ansible](https://www.ansible.com/) totalmente parametrizável para instalação de aplicações e ferramentas

### 📝 Escopo

Por padrão, nenhuma ação é realizada. Para cada ação é necessário a sua configuração prévia

* APT
  * Instalar Pacotes
  * Remover Pacotes
  * Atualizar Pacotes
* Snap
  * Instalar Pacotes (Clássicos ou Não)
  * Remover Pacotes
* Ferramentas de Desenvolvimento
  * RVM (Instalação)
  * NVM (Instalação)
  * Docker (Instalação)
* Outros
  * Google Chrome (Instalação)

## ⚓ Pré-Requisitos

* [Ansible](https://www.ansible.com/)

```
sudo apt-get install ansible
```

## 💻 Execução

* Faça download do código desse repositório

* Instale as _collections_ utilizadas como dependências:

```bash
ansible-galaxy collection install -r requirements.yml
```

* Execute o Playbook

```bash
ansible-playbook playbook.yml --ask-become
```

No início da execução, será solicitado o `BECOME password` e deve ser informado a senha de `root`. 
Esse passo é necessário para que não seja executado todo o processo com um usuário privilegiado

## ⚙️ Configuração 

Os arquivos de configuração estão localizados na pasta `vars`. 

* O arquivo `default.yml` contém a configuração padrão e não deve ser alterado.
* Os arquivos `sample-*.yml` são fornecidos como exemplo e não são carregados
* Qualquer configuração deve ser armazenada no arquivo `custom.yml`

| **Chave**                     | **Descrição**                                                      | **Tipo** | **Default** |
|-------------------------------|--------------------------------------------------------------------|:--------:|:-----------:|
| rvm_install                   | RVM deve ser instalado?                                            |  Boolean |    false    |
| nvm_install                   | NVM deve ser instalado?                                            |  Boolean |    false    |
| docker_install                | Docker deve ser instalado?                                         |  Boolean |    false    |
| google_chrome_install         | Google Chrome deve ser instalado?                                  |  Boolean |    false    |
| apt_manage                    | Operações (update/autoremove/autoclean) APT devem ser gerenciadas? |  Boolean |    false    |
| apt_install_packages          | Pacotes a serem instalados via APT                                 |   Array  |      []     |
| apt_remove_packages           | Pacotes a serem removidos via APT                                  |   Array  |      []     |
| snap_install_packages         | Pacotes a serem instalados via Snap                                |   Array  |      []     |
| snap_install_classic_packages | Pacotes a serem instalados via Snap, com a flag `--classic`        |   Array  |      []     |
| snap_remove_packages          | Pacotes a serem removidos via Snap                                 |   Array  |      []     |

💡 Uma maneira simples de encarar as configurações relacionadas a instalação e remoção de pacotes é: garanta que esse pacote esteja instalado (ou não 🤷)

### ❗ Ponto de Atenção 

O objetivo do projeto é realizar (ou não) a instalação das aplicações e ferramentas solicitadas de acordo com a configuração daquele ciclo de execução.

Por exemplo, a indicação de que o RVM não será instalado (`rvm_install: false`) sinaliza que o RVM não será instalado naquela execução e não que ele será removido caso tenha sido instalado anteriormente.

De forma semelhante, a remoção de um item de uma lista de instalação de pacotes não faz com que ele seja removido, para isso ele deve ser incluído na lista de pacotes a serem desinstalados.

## 🔮 Futuro 

* [ ] Definir Licença
* [ ] Instalação do Docker Compose
* [ ] Desinstalação das Aplicações
  * [ ] NVM
  * [ ] RVM
  * [ ] Docker
  * [ ] Google Chrome
* [ ] Acompanhamento de Fluxo de Atualização

