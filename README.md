# Documentação para Instalação do Apache, MySQL e PHP no Ubuntu Server

---

### 1. FERRAMENTAS NECESSÁRIAS
Para começar, você precisará das seguintes ferramentas:
- **VirtualBox**: 
Instale o VirtualBox a partir do site oficial. Após a instalação, baixe e instale o pacote de extensão disponível no mesmo site.

- **Ubuntu Server**: 
Baixe a ISO do Ubuntu Server a partir do site oficial.

- **PuTTY**: 
Instale o PuTTY ou outro programa de sua preferência para acessar a VM através do SSH. Você pode baixar o PuTTY aqui.

- **WinSCP**: 
Instale o WinSCP para facilitar a configuração e transferência de arquivos. Você pode baixar o WinSCP aqui.
- **phpMyAdmin**: 
Baixe o arquivo zip do phpMyAdmin no site oficial.

---

### 2. CONFIGURAÇÃO DA VM
##### 2.1. Criar uma VM
- Abra o VirtualBox e crie uma nova máquina virtual.
- Selecione a ISO do Ubuntu Server baixada e prossiga com a instalação.
- Configure a VM com pelo menos 2 GB de RAM e 20GB de armazenamento, dependendo das suas necessidades.

##### 2.2. Configurar a Rede
- Acesse as configurações da VM no VirtualBox.
- Vá para a seção de **rede** e selecione **Placa em modo Bridge**. Isso permitirá que a VM se conecte à rede do seu PC real e obtenha um endereço IP.

---

### 3. GERENCIAR ARQUIVOS DA VM COM WINSCP:
##### 3.1. Gerenciar Arquivos
- No WinSCP, acesse a máquina através do SFTP usando o IP da VM e logue com a conta criada no Ubuntu Server. Dessa forma, você pode acessar os arquivos da VM.

---

### 4.	INSTALAR SISTEMA OPERACIONAL:
- Inicie a VM e siga os passos de instalação do Ubuntu Server.
- Crie um usuário e configure a conta durante o processo de instalação.
 
---

### 5. ATUALIZAÇÃO DO SISTEMA
##### 5.1. Instalar Net-tools
- Usaremos o comando ```ifconfig``` para isso, instale o **```net-tools```** utilizando o seguinte comando:
```
sudo apt-get install net-tools
```
##### 5.2.	Atualizar Repositórios e Pacotes
- Após a instalação, faça login na VM.
- Execute os seguintes comandos para atualizar os repositórios e os pacotes instalados:
```
sudo apt-get update
sudo apt-get upgrade
```

---

### 6. Instalação do Apache
##### 6.1. Instalar o Servidor Apache
- Após a atualização do sistema, instale o Apache com o seguinte comando:
```
sudo apt-get install apache2
```

##### 6.2. Verificar Status do Apache
- Para garantir que o Apache foi instalado corretamente e está funcionando, execute:
```
sudo systemctl status apache2
```
- Você deve ver uma mensagem indicando que o serviço Apache está ativo e em execução.

##### 6.3.	Acessar a Página Padrão do Apache

- Abra um navegador web no seu computador real.
- Digite o endereço IP da sua VM no navegador. Você deve ver a página padrão do Apache, indicando que o servidor está funcionando corretamente.

---

### 7. ACESSAR ARQUIVOS COM WINSCP
##### 7.1 Renomear o Arquivo HTML
- No terminal, dentro da pasta, insira o seguinte comando para renomear o arquivo:
```
sudo mv index.html novo_nome.html
```
- No WinSCP, acesse a pasta `/var/www/html` e visualize o arquivo `index.html`.
Para permitir que o arquivo seja renomeado através do WinSCP, insira o seguinte comando no terminal. 
```
sudo chmod 777 -R /var/www/html/
```
##### 7.2. Mover phpMyAdmin para a VM
- Mova o arquivo zip do phpMyAdmin do seu PC real para a pasta `/var/www/html/` na VM usando o WinSCP.
---

### 8. CRIAR UM NOVO ARQUIVO HTML
##### 8.1. Criar o Arquivo index.html
- Crie um novo arquivo index.html no diretório `/var/www/html` com o seguinte conteúdo:
```
<!DOCTYPE html>
<html>
    <head><title> Teste </title></head>
        <body>
            <h3>Olá, Mundo!</h3>
        </body>
</html>
```

##### 8.2.	Acessar o Arquivo no Navegador
- No navegador web, acesse ` http://<IP_da_VM>/index.html ` e deve retornar o texto que declaramos acima em HTML.

### 9. INSTALAÇÃO DO MYSQL
##### 9.1.Instalar o MySQL
- Execute o seguinte comando para instalar o MySQL:

```
sudo apt-get install mysql-server
sudo mysql_secure_installation
```
- Siga as instruções na tela e após a instalação, execute o comando abaixo para acessar o MySQL e configurar uma senha de root e outras opções de segurança do MySQL:

##### 9.2.	Configurar o MySQL
- Acesse o MySQL através do comando:
```
sudo mysql -u root
```

##### 9.3. Crie um novo usuário
- No MySQL, insira o código abaixo para criar um novo usuário e liberar todos os privilégios para o mesmo. Usaremos ele posteriormente para acessar a interface gráfica do php.
```
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';
FLUSH PRIVILEGES;
```
- Utilize o comando `exit` para sair do MySQL.
Para acessa-lo novamente, utilize `mysql -u admin -p`

---

### 10. INSTALÇÃO DO PHP
##### 10.1. Instalar o PHP
- Execute o seguinte comando para instalar o PHP juntamente com os módulos necessários para o Apache:
```
sudo apt-get install php libapache2-mod-php php-mysql
```
##### 10.2.	Reiniciar o Apache
- Para que o Apache reconheça o PHP, reinicie o serviço:
```
sudo systemctl restart apache2
```

#BAIXAR PHP MYADMIN

##### 10.3. Testar a Instalação do PHP
###### 10.3.1. Criar um Arquivo PHP de Teste
- Utilize o terminal ou o WinSCP para criar um arquivo chamado `info.php` no diretório `/var/www/html/` com o seguinte conteúdo:
```
<?php
phpinfo();
?>
```
###### 10.3.2.	Acessar o Arquivo de Teste
- No navegador web, acesse http://<IP_da_VM>/info.php. Você deve ver a página de informações do PHP, confirmando que o PHP está instalado e funcionando corretamente.

---

### 11.	ACESSAR PHPMYADMIN:
- No navegador, acesse `http://<IP_da_VM>/phpmyadmin`
- Para logar, utilize a conta criada no MySQL.
- No phpMyAdmin, você pode configurar tabelas, bancos de dados e gerenciar tudo pela interface gráfica.

### 12. CONCLUSÃO
Com esses passos, você terá configurado um servidor Ubuntu com Apache, MySQL e PHP. Agora, você está pronto para hospedar seus aplicativos web. Certifique-se de manter o sistema atualizado e de configurar corretamente as permissões de segurança para garantir a proteção do seu servidor.

