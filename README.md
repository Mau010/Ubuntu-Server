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
# ⚠️⚠️BAIXAR PHP MYADMIN

### 11.	ACESSAR PHPMYADMIN:
- No navegador, acesse `http://<IP_da_VM>/phpmyadmin`
- Para logar, utilize a conta criada no MySQL.
- No phpMyAdmin, você pode configurar tabelas, bancos de dados e gerenciar tudo pela interface gráfica.


### 12. INSTALAÇÃO E CONFIGURAÇÃO DO WORDPRESS



Passo 1. Configure o MySQL e Crie um Nanco de Dados
Uma vez que o Apache esteja funcionando, o próximo passo é instalar o banco de dados MySQL. Para fazer isso, execute o seguinte comando:

apt install mysql-server -y
Será necessário digitar sua senha. Para completar a instalação, pressione Y e Enter quando solicitado.

Depois de instalar o MySQL em seu VPS, abra o terminal MySQL digitando o seguinte comando:

sudo mysql
Defina a senha para a conta raiz do MySQL usando este comando:

```
mysql>ALTER USER 'root'@'localhost' IDENTIFIED WITH
mysql_native_password BY ‘SUA SENHA’;
mysql>ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY ‘SUA SENHA’;
mysql>ALTER USER 'root'@'localhost' IDENTIFIED WITH
mysql_native_password BY ‘SUA SENHA’;
```

Certifique-se de digitar uma senha de root MySQL forte no lugar de SUA SENHA.

Para implementar estas mudanças, execute o comando flush:

mysql> FLUSH PRIVILEGES;
Use o seguinte comando para criar um banco de dados WordPress:

mysql> CREATE DATABASE WordPressDB DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
Agora, vamos criar uma conta de usuário MySQL para operar no novo banco de dados WordPress. Vamos usar o WordPressDB como nome do banco de dados e o testehostinger como nome de usuário:

GRANT ALL ON WordPressDB.* TO 'testehostinger'@'localhost' IDENTIFIED BY 'novasenha’;
Certifique-se de digitar uma senha forte no lugar de novasenha. Feito isso, faça o flush dos privilégios para que o MySQL implemente as mudanças.

mysql> FLUSH PRIVILEGES;
Finalmente, saia do MySQL digitando este comando:

mysql> EXIT;
Passo 4. Prepare a Instalação do WordPress no Ubuntu
É hora de preparar a instalação do WordPress criando um arquivo de configuração do CMS e um diretório WordPress.

Criando um arquivo WordPress.confComece criando um arquivo de configuração para Apache chamado WordPress.conf no diretório /etc/apache2/sites-available. Use o seguinte comando:

nano /etc/apache2/sites-available/WordPress.conf
Importante! Tenha em mente que os nomes de arquivos e locais são sensíveis a maiúsculas e minúsculas no Linux.

Uma vez executado esse comando, você chegará ao editor de texto Nano para editar o arquivo WordPress.conf. Habilite .htaccess adicionando estas linhas ao bloco VirtualHost:

Plain text
Copy to clipboard
Open code in new window
EnlighterJS 3 Syntax Highlighter
<Directory /var/www/wordpress/>
AllowOverride All
</Directory>
<Directory /var/www/wordpress/> AllowOverride All </Directory>
<Directory /var/www/wordpress/>
   AllowOverride All
</Directory>
Feche e salve o arquivo pressionando CTRL+X. Aperte Y e Enter quando solicitado.

Criando um Diretório WordPress

Em seguida, crie um diretório WordPress em /var/wwww/. Em nosso exemplo, seu caminho completo será em /var/wwww/wwwpress. Para isso, use o comando mkdir para criar o diretório:

mkdir /var/wwww/wwwpress
Agora, habilite o mod_rewrite para usar o recurso permalink do WordPress executando o seguinte comando no terminal:

sudo a2enmod reescrever
Você terá que reiniciar o servidor web Apache usando o seguinte comando:

systemctl restart apache2
O próximo passo é mudar a diretiva ServerName no arquivo /etc/apache2/apache2.conf. Abra o arquivo usando este comando:

nano /etc/apache2/apache2.conf
Você terá que configurar a diretiva ServerName para o endereço de IP ou hostname do servidor adicionando a seguinte linha ao arquivo /etc/apache2/apache2.conf:

ServerName <Seu endereço de IP>
Feche e salve o arquivo.

Agora, você tem que verificar se a configuração do Apache está correta, executando o seguinte comando no terminal:

apachectl configtest
Se a configuração funcionar bem, ela deverá imprimir a seguinte saída:

Syntax OK
Saída: Janela que indica que a sintaxe está OK
Passo 5. Download e Configuração do WordPress
Depois de todos os preparativos, é hora de instalar o WordPress. Há dois métodos – configurar o WordPress via interface web ou editar manualmente o arquivo wp-config.php.

Método 1. Configuração do WordPress Através de um Navegador
Primeiro, instale o pacote wget em seu VPS. Isto será útil para baixar arquivos do CMS. Execute este comando na linha de comando:

sudo apt install wget -y
Em seguida, use o comando wget seguido do link para download do WordPress:

wget https://wordpress.org/latest.zip
Uma vez que você tenha baixado o arquivo, instale o utilitário de descompactação usando estes comandos:

Plain text
Copy to clipboard
Open code in new window
EnlighterJS 3 Syntax Highlighter
ls
sudo apt install unzip -y
ls sudo apt install unzip -y
ls
sudo apt install unzip -y
Agora você terá que mover o arquivo para o diretório correto antes de descompactá-lo. Use o comando:

mv latest.zip /var/www/html
Então, navegue até o diretório e descompacte o arquivo usando estes comandos:

cd /var/www/html
unzip latest.zip
Depois disso, use o seguinte comando para mover o diretório:

mv -f wordpress/* ./
O último passo é remover o index.html. Use este comando aqui:

sudo rm -rf index.html
Você pode usar o comando ls para verificar se o arquivo index.html foi removido. Uma vez que tiver feito isso, reinicie o Apache usando estes comandos:

sudo systemctl restart apache2
sudo chown -R www-data:www-data /var/wwww/
Finalize o processo configurando o WordPress através de um navegador. Abra seu navegador preferido e digite o endereço de IP do servidor. Os seguintes passos serão similares a uma configuração padrão do WordPress.

Primeiro, selecione um idioma para WordPress e clique em Continuar.

Configuração WordPress - escolha do idioma.
Uma mensagem de boas-vindas do WordPress aparecerá listando as informações de que você precisará para completar a configuração. Clique no botão Let’s go! (Vamos lá!) para continuar.

Mensagem de bem-vindo ao WordPress - destacando o botão "Let's go" (Vamos Lá)
Ele o levará para a página principal de configuração. Preencha os seguintes detalhes:

Nome do banco de dados – digite o nome que você configurou ao configurar o banco de dados WordPress. Neste caso, será WordPressDB.
Nome de usuário – digite o nome de usuário MySQL que você configurou para o banco de dados antes.
Senha – insira a senha que você criou para o usuário do banco de dados.
Host do banco de dados – mantenha aqui o valor padrão do localhost.
Prefixo da tabela – deixar wp_ neste campo.
Clique em Submeter para continuar.

Página de configuração do WordPress mostrando o formulário para detalhes de conexão ao banco de dados
Uma nova mensagem aparecerá dizendo que o WordPress agora pode se comunicar com seu banco de dados. Clique em Executar a instalação.

Mensagem WordPress informando que a conexão ao banco de dados foi bem sucedida
Depois disso, você terá que inserir mais algumas informações:

Título do site – digite o nome do site WordPress. Para otimizar seu site, recomendamos que insira seu nome de domínio.
Nome de usuário – crie um novo nome de usuário que você usará para fazer o login no WordPress.
Senha – crie uma senha para o usuário do WordPress.
Seu e-mail – adicione o endereço de e-mail para atualizações e notificações.
Visibilidade dos motores de busca – deixe esta caixa desmarcada se você não quiser que os motores de busca indexem seu site até que ele esteja pronto.
Clique no botão Install WordPress (Instalar WordPress) para começar a instalação de fato.

Página de configuração do WordPress - formulário de instalação
Uma mensagem de sucesso aparecerá junto com um botão de login. Você pode acessar o WordPress diretamente desta página.

Mensagem de sucesso WordPress foi instalado
Uma vez logado, você será levado ao painel de administração do WordPress. Agora você pode começar a customizar o site instalando plugins e temas WordPress.

Se seu site WordPress ainda não tem um nome de domínio, compre um e aponte o domínio para o VPS antes de tornar o site público.


### (istalação pela interface grafica do phpmyadmin) [https://www.youtube.com/watch?v=PYrcdNfhyzU&list=WL&index=4&t=730s]

### 12. CONCLUSÃO
Com esses passos, você terá configurado um servidor Ubuntu com Apache, MySQL e PHP. Agora, você está pronto para hospedar seus aplicativos web. Certifique-se de manter o sistema atualizado e de configurar corretamente as permissões de segurança para garantir a proteção do seu servidor.


