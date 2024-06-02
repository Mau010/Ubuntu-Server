# Ubuntu-Server

Documentação para Instalação de Apache, MySQL e PHP no Ubuntu Server
1. Ferramentas Necessárias
Para começar, você precisará das seguintes ferramentas:
•	VirtualBox: Instale o VirtualBox a partir do site oficial. Após a instalação, baixe e instale o pacote de extensão disponível no mesmo site.
•	Ubuntu Server: Baixe a ISO do Ubuntu Server a partir do site oficial.
•	PuTTY: Instale o PuTTY ou outro programa de sua preferência para acessar a VM através do SSH. Você pode baixar o PuTTY aqui.
•	WinSCP: Instale o WinSCP para facilitar a configuração e transferência de arquivos. Você pode baixar o WinSCP aqui.
2. Configuração da VM
1.	Criar uma VM:
o	Abra o VirtualBox e crie uma nova máquina virtual.
o	Selecione a ISO do Ubuntu Server baixada e prossiga com a instalação.
o	Configure a VM com pelo menos 1GB de RAM e 10GB de armazenamento, dependendo das suas necessidades.
2.	Configurar a Rede:
o	Acesse as configurações da VM no VirtualBox.
o	Vá para a seção de rede e selecione "Placa em modo Bridge". Isso permitirá que a VM se conecte à rede do seu PC real e obtenha um endereço IP.
3. Instalação do Ubuntu Server
1.	Instalar o Sistema Operacional:
o	Inicie a VM e siga os passos de instalação do Ubuntu Server.
o	Crie um usuário e configure a conta durante o processo de instalação.
4. Atualização do Sistema
1.	Atualizar Repositórios e Pacotes:
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
7. Instalação do MySQL
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
8. Instalação do PHP
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
9. Testar a Instalação do PHP
1.	Criar um Arquivo PHP de Teste:
o	Crie um arquivo chamado info.php no diretório /var/www/html com o seguinte conteúdo:
php
Copiar código
<?php
phpinfo();
?>
2.	Acessar o Arquivo de Teste:
o	No navegador web, acesse http://<IP_da_VM>/info.php. Você deve ver a página de informações do PHP, confirmando que o PHP está instalado e funcionando corretamente.
10. Conclusão
Com esses passos, você terá configurado um servidor Ubuntu com Apache, MySQL e PHP. Agora, você está pronto para hospedar seus aplicativos web. Certifique-se de manter o sistema atualizado e de configurar corretamente as permissões de segurança para garantir a proteção do seu servidor.
