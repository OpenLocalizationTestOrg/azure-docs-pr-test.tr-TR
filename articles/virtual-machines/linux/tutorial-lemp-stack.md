---
title: "Azure'da bir Linux sanal makinede LEMP dağıtma | Microsoft Docs"
description: "Öğretici - yükleme azure'da bir Linux VM LEMP yığında"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Azure VM temelinde bir LEMP web sunucusunu yükleme
Bu makalede nasıl NGINX web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (LEMP yığını) dağıtılacağı anlatılmaktadır. LEMP yığın popüler bir alternatif olan [AMPUL yığın](tutorial-lamp-stack.md), hangi Azure ile de yükleyebilirsiniz. Eylem LEMP Server'da görmek için isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Bir Ubuntu VM (' L' LEMP yığınında) oluşturma
> * Web trafiği için 80 numaralı bağlantı noktasını açın
> * NGINX, MySQL ve PHP yükleme
> * Yükleme ve yapılandırmasını doğrulayın
> * WordPress LEMP sunucusuna yükleyin


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>NGINX, MySQL ve PHP yükleme

Ubuntu paket kaynaklarını güncelleştirmek ve NGINX, MySQL ve PHP yüklemek için aşağıdaki komutu çalıştırın. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Paketler ve diğer bağımlılıklar yüklemeniz istenir. İstendiğinde, MySQL için bir kök parola ayarlayın ve ardından devam etmek için Enter. Kalan istemleri izleyin. Bu işlem, PHP, MySQL ile kullanmak için gerekli en düşük gerekli PHP uzantıları yükler. 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a>Yükleme ve yapılandırmasını doğrulayın


### <a name="nginx"></a>NGINX

Aşağıdaki komutu NGINX sürümüyle denetleyin:
```bash
nginx -v
```

Yüklü NGINX ve bağlantı noktası 80 VM'nize açık ile web sunucusu artık Internet üzerinden erişilebilir. NGINX Hoş Geldiniz sayfasını görüntülemek için bir web tarayıcısı açın ve VM ortak IP adresini girin. SSH VM için kullanılan ortak IP adresini kullan:

![NGINX varsayılan sayfa][3]


### <a name="mysql"></a>MySQL

MySQL sürümü aşağıdaki komutla denetleyin (büyük harf Not `V` parametresi):

```bash
msql -V
```

MySQL yükleme güvenliğinin sağlanmasına yardımcı olmak için aşağıdaki betiği çalıştıran öneririz:

```bash
mysql_secure_installation
```

MySQL kök parolanızı girin ve ortamınız için güvenlik ayarlarını yapılandırın.

Bir MySQL veritabanı oluşturmak istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, MySQL oturum açma değiştirin:

```bash
mysql -u root -p
```

İşiniz bittiğinde, mysql istemi yazarak çıkmak `\q`.

### <a name="php"></a>PHP

PHP sürümünü aşağıdaki komutla denetleyin:

```bash
php -v
```

PHP Fastcgı işlem yöneticisi (PHP-FPM) kullanmak için NGINX yapılandırın. Özgün NGINX server blok yapılandırma dosyasını yedekleyin ve tercih ettiğiniz bir düzenleyicide özgün dosyayı düzenlemek için aşağıdaki komutları çalıştırın:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

Düzenleyicide Değiştir `/etc/nginx/sites-available/default` aşağıdaki. Açıklamaları ayarları hakkında ayrıntılı açıklamalar için bkz. VM için genel IP adresi yerine *yourPublicIPAddress*ve geri kalan ayarları bırakın. Ardından dosyayı kaydedin.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

Sözdizimi hataları NGINX yapılandırmasını kontrol edin:

```bash
sudo nginx -t
```

Sözdizimi doğru ise, NGINX aşağıdaki komutla yeniden başlatın:

```bash
sudo service nginx restart
```

Daha fazla test etmek isterseniz, bir tarayıcıda görüntülemek üzere hızlı bir PHP bilgileri sayfası oluşturun. Aşağıdaki komut, PHP bilgileri sayfası oluşturur:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Şimdi, oluşturduğunuz PHP bilgileri sayfasını kontrol edebilirsiniz. Bir tarayıcı açın ve gidin `http://yourPublicIPAddress/info.php`. VM ortak IP adresini değiştirin. Bu görüntüsüne benzer görünmelidir.

![PHP bilgileri sayfası][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure LEMP Server'da dağıtıldı. Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Bir Ubuntu VM oluşturma
> * Web trafiği için 80 numaralı bağlantı noktasını açın
> * NGINX, MySQL ve PHP yükleme
> * Yükleme ve yapılandırmasını doğrulayın
> * WordPress LEMP yığında yükleme

SSL sertifikaları web sunucularıyla güvenli öğrenmek için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"]
> [SSL ile güvenli web sunucusu](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
