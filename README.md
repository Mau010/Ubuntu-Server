Documentação para Instalação de Apache, MySQL e PHP no Ubuntu Server
1. Ferramentas Necessárias
Para começar, você precisará das seguintes ferramentas:
•	VirtualBox: Instale o VirtualBox a partir do site oficial. Após a instalação, baixe e instale o pacote de extensão disponível no mesmo site.
•	Ubuntu Server: Baixe a ISO do Ubuntu Server a partir do site oficial.
•	PuTTY: Instale o PuTTY ou outro programa de sua preferência para acessar a VM através do SSH. Você pode baixar o PuTTY aqui.
•	WinSCP: Instale o WinSCP para facilitar a configuração e transferência de arquivos. Você pode baixar o WinSCP aqui.
•	phpMyAdmin: Baixe o arquivo zip do phpMyAdmin no site oficial.
2. Configuração da VM
1.	Criar uma VM:
o	Abra o VirtualBox e crie uma nova máquina virtual.
o	Selecione a ISO do Ubuntu Server baixada e prossiga com a instalação.
o	Configure a VM com pelo menos 2GB de RAM e 20GB de armazenamento, dependendo das suas necessidades.
2.	Configurar a Rede:
o	Acesse as configurações da VM no VirtualBox.
o	Vá para a seção de rede e selecione "Placa em modo Bridge". Isso permitirá que a VM se conecte à rede do seu PC real e obtenha um endereço IP.
3.	Acessar a Máquina com WinSCP:
o	No WinSCP, acesse a máquina através do SFTP usando o IP da VM e logue com a conta criada no Ubuntu Server. Dessa forma, você pode acessar os arquivos da VM.
3. Instalação do Ubuntu Server
1.	Instalar o Sistema Operacional:
o	Inicie a VM e siga os passos de instalação do Ubuntu Server.
o	Crie um usuário e configure a conta durante o processo de instalação.
4. Atualização do Sistema
1.	Instalar Net-tools:
o	Para usar o comando ifconfig, instale o net-tools:
bash
Copiar código
sudo apt-get install net-tools
2.	Atualizar Repositórios e Pacotes:
o	Após a instalação, faça login na VM.
o	Execute os seguintes comandos para atualizar os repositórios e os pacotes instalados:
bash
Copiar código
sudo apt-get update
sudo apt-get upgrade
5. Instalação do Apache
1.	Instalar o Servidor Apache:
o	Após a atualização do sistema, instale o Apache com o seguinte comando:
bash
Copiar código
sudo apt-get install apache2
6. Verificar Instalação do Apache
1.	Verificar Status do Apache:
o	Para garantir que o Apache foi instalado corretamente e está funcionando, execute:
bash
Copiar código
sudo systemctl status apache2
o	Você deve ver uma mensagem indicando que o serviço Apache está ativo e em execução.
2.	Acessar a Página Padrão do Apache:
o	Abra um navegador web no seu computador real.
o	Digite o endereço IP da sua VM no navegador. Você deve ver a página padrão do Apache, indicando que o servidor está funcionando corretamente.
3.	Acessar a Pasta Web com WinSCP:
o	No WinSCP, acesse a pasta /var/www/html e visualize o arquivo index.html.
4.	Renomear o Arquivo HTML:
o	Use o terminal ou o WinSCP para renomear o arquivo:
bash
Copiar código
sudo mv /var/www/html/index.html /var/www/html/novo_nome.html
o	Caso não tenha permissão, utilize:
bash
Copiar código
sudo chmod 777 -R /var/www/html/
7. Criar um Novo Arquivo HTML
1.	Criar o Arquivo index.html:
o	Crie um novo arquivo index.html no diretório /var/www/html com o seguinte conteúdo:
html
Copiar código
<!DOCTYPE html>
<html>
<head><title>Teste</title></head>
<body>
    <h3>Olá Mundo</h3>
</body>
</html>
2.	Acessar o Arquivo no Navegador:
o	No navegador web, acesse http://<IP_da_VM>/index.html.
8. Mover phpMyAdmin para a VM
1.	Transferir phpMyAdmin:
o	Mova o arquivo zip do phpMyAdmin do seu PC real para a pasta /var/www/html na VM usando o WinSCP.
9. Instalação do MySQL
1.	Instalar o MySQL:
o	Execute o seguinte comando para instalar o MySQL:
bash
Copiar código
sudo apt-get install mysql-server
2.	Configurar o MySQL:
o	Após a instalação, execute o comando abaixo para configurar a segurança do MySQL:
bash
Copiar código
sudo mysql_secure_installation
o	Siga as instruções na tela para configurar uma senha de root e outras opções de segurança.
o	Para acessar o MySQL, utilize:
bash
Copiar código
sudo mysql -u root
o	Crie um novo usuário:
sql
Copiar código
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';
o	Dê todos os privilégios para o novo usuário:
sql
Copiar código
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';
FLUSH PRIVILEGES;
o	Saia do MySQL e acesse novamente com o novo usuário:
bash
Copiar código
exit
mysql -u admin -p
10. Instalação do PHP
1.	Instalar o PHP:
o	Execute o seguinte comando para instalar o PHP juntamente com os módulos necessários para o Apache:
bash
Copiar código
sudo apt-get install php libapache2-mod-php php-mysql
2.	Reiniciar o Apache:
o	Para que o Apache reconheça o PHP, reinicie o serviço:
bash
Copiar código
sudo systemctl restart apache2
11. Testar a Instalação do PHP
1.	Criar um Arquivo PHP de Teste:
o	Utilize o terminal ou o WinSCP para criar um arquivo chamado info.php no diretório /var/www/html com o seguinte conteúdo:
php
Copiar código
<?php
phpinfo();
?>
2.	Acessar o Arquivo de Teste:
o	No navegador web, acesse http://<IP_da_VM>/info.php. Você deve ver a página de informações do PHP, confirmando que o PHP está instalado e funcionando corretamente.
3.	Acessar phpMyAdmin:
o	No navegador, acesse http://<IP_da_VM>/phpmyadmin.
o	Para logar, utilize a conta criada no MySQL.
o	No phpMyAdmin, você pode configurar tabelas, bancos de dados e gerenciar tudo pela interface gráfica.
12. Conclusão
Com esses passos, você terá configurado um servidor Ubuntu com Apache, MySQL e PHP. Agora, você está pronto para hospedar seus aplicativos web. Certifique-se de manter o sistema atualizado e de configurar corretamente as permissões de segurança para garantir a proteção do seu servidor.
