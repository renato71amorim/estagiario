## Criando o subdomínio `app.sieca.net` com HTTPS no Debian 10

Como exemplo vamos criar o subdomínio `app.sieca.net` com HTTPS no Debian 10, você precisará seguir estes passos:

**1. Configurar o servidor web (Apache ou Nginx):**

* **Apache:**
    * **Criar o diretório virtual:** Crie um diretório para o subdomínio `app.sieca.net` dentro do diretório raiz do Apache, geralmente `/var/www/`. Por exemplo: `mkdir /var/www/app.sieca.net`.
    * **Criar o arquivo de configuração do site:** Crie um arquivo de configuração para o subdomínio `app.sieca.net` dentro do diretório `/etc/apache2/sites-available`. Por exemplo, `nano /etc/apache2/sites-available/app.sieca.net.conf`.
    * **Configurar o arquivo de configuração:** Adicione as seguintes linhas no arquivo de configuração:

    ```apache
    <VirtualHost *:80>
        ServerName app.sieca.net
        DocumentRoot /var/www/app.sieca.net
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>

    <VirtualHost *:443>
        ServerName app.sieca.net
        DocumentRoot /var/www/app.sieca.net
        SSLEngine on
        SSLCertificateFile /etc/letsencrypt/live/app.sieca.net/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/app.sieca.net/privkey.pem
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    ```

    * **Habilitar o site:** Habilite o site criado: `a2ensite app.sieca.net`.
    * **Reiniciar o Apache:** Reinicie o servidor Apache: `systemctl restart apache2`.

* **Nginx:**
    * **Criar o diretório virtual:** Crie um diretório para o subdomínio `app.sieca.net` dentro do diretório raiz do Nginx, geralmente `/var/www/html`. Por exemplo: `mkdir /var/www/app.sieca.net`.
    * **Criar o arquivo de configuração do site:** Crie um arquivo de configuração para o subdomínio `app.sieca.net` dentro do diretório `/etc/nginx/sites-available`. Por exemplo, `nano /etc/nginx/sites-available/app.sieca.net.conf`.
    * **Configurar o arquivo de configuração:** Adicione as seguintes linhas no arquivo de configuração:

    ```nginx
    server {
        listen 80;
        server_name app.sieca.net;
        root /var/www/app.sieca.net;

        location / {
            try_files $uri $uri/ =404;
        }
    }

    server {
        listen 443 ssl;
        server_name app.sieca.net;
        root /var/www/app.sieca.net;

        ssl_certificate /etc/letsencrypt/live/app.sieca.net/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/app.sieca.net/privkey.pem;
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
        ssl_prefer_server_ciphers on;

        location / {
            try_files $uri $uri/ =404;
        }
    }
    ```

    * **Habilitar o site:** Habilite o site criado: `ln -s /etc/nginx/sites-available/app.sieca.net.conf /etc/nginx/sites-enabled/app.sieca.net.conf`.
    * **Reiniciar o Nginx:** Reinicie o servidor Nginx: `systemctl restart nginx`.

**2. Obter certificado SSL (HTTPS):**

* **Utilizando o Let's Encrypt:** O Let's Encrypt é uma autoridade de certificação gratuita e automatizada. Para obter um certificado SSL para `app.sieca.net` utilizando o Let's Encrypt, você pode usar o Certbot:

    ```bash
    sudo certbot certonly --standalone -d app.sieca.net
    ```

    * **Instalar o Certbot:** Se você não tiver o Certbot instalado, use o comando: `sudo apt update && sudo apt install certbot`.
    * **Especificar o servidor web:** Se você estiver usando o Apache, use a opção `--apache`. Se estiver usando o Nginx, use a opção `--nginx`.
    * **Renovar o certificado:** O certificado Let's Encrypt tem validade de 90 dias. Para renovar o certificado, execute o comando: `sudo certbot renew`.

**3. Configurar o DNS:**

* **Criar o registro A:** Crie um registro A para `app.sieca.net` apontando para o endereço IP do servidor onde o subdomínio está configurado.
* **Criar o registro CNAME:** Crie um registro CNAME para `app.sieca.net` apontando para o domínio principal `sieca.net`.

**4. Testar a configuração:**

* Acesse `https://app.sieca.net` no seu navegador. Você deve ver o site do subdomínio funcionando com HTTPS.

**Observações:**

* **Configuração do DNS:** O tempo de propagação do DNS pode variar, então pode levar algum tempo para o subdomínio ficar disponível.
* **Segurança:** Certifique-se de que o servidor web e o sistema operacional estejam atualizados e com as últimas correções de segurança.
* **Firewall:** Configure o firewall para permitir o tráfego HTTPS na porta 443.

**Importante:**

* **Backup:** Faça backup de todos os arquivos e configurações antes de realizar alterações.
* **Documentação:** Documente todas as alterações realizadas para facilitar a manutenção e o troubleshooting.
* **Ajuda:** Se você tiver dificuldades com a configuração, consulte a documentação do seu servidor web, do Let's Encrypt e do seu provedor de DNS.