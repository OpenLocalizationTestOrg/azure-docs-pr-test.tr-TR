---
title: azure'da bir Linux sanal makinede aaaDeploy LEMP | Microsoft Docs
description: "Öğretici - yükleme hello LEMP azure'da bir Linux VM yığında"
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
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Azure VM temelinde bir LEMP web sunucusunu yükleme
Bu makalede toodeploy bir NGINX nasıl web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (Merhaba LEMP yığını) aracılığıyla anlatılmaktadır. Merhaba LEMP yığını olan popüler bir alternatif toohello [AMPUL yığın](tutorial-lamp-stack.md), hangi Azure ile de yükleyebilirsiniz. toosee hello LEMP sunucu eyleminde, isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Bir Ubuntu VM (Merhaba 'L' hello LEMP yığınında) oluşturma
> * Web trafiği için 80 numaralı bağlantı noktasını açın
> * NGINX, MySQL ve PHP yükleme
> * Yükleme ve yapılandırmasını doğrulayın
> * WordPress hello LEMP sunucusuna yükleyin


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>NGINX, MySQL ve PHP yükleme

Aşağıdaki komut tooupdate Ubuntu paket kaynaklar hello çalıştırın ve NGINX, MySQL ve PHP yükleyin. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

İstendiğinde tooinstall hello paketler ve diğer bağımlılıklar var. İstendiğinde, MySQL, ardından [Enter] toocontinue için bir kök parola ayarlayın. Merhaba kalan istemleri izleyin. Bu işlem hello minimum gerekli PHP uzantıları gerekli toouse PHP MySQL ile yükler. 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a>Yükleme ve yapılandırmasını doğrulayın


### <a name="nginx"></a>NGINX

Onay hello sürümüyle NGINX komutu aşağıdaki hello:
```bash
nginx -v
```

NGINX ile tooyour VM yüklü ve bağlantı noktası 80'i açın, hello web sunucusu artık erişilebilir hello Internet. tooview hello NGINX Hoş Geldiniz sayfasında, bir web tarayıcısı açın ve hello VM hello ortak IP adresini girin. Merhaba tooSSH toohello VM kullanılan ortak IP adresini kullan:

![NGINX varsayılan sayfa][3]


### <a name="mysql"></a>MySQL

Komutu aşağıdaki hello ile MySQL Hello sürümünü denetleme (Not hello sermaye `V` parametresi):

```bash
msql -V
```

Komut dosyası toohelp güvenli hello MySQL yüklenmesinden hello çalıştıran öneririz:

```bash
mysql_secure_installation
```

MySQL kök parolanızı girin ve ortamınız için hello güvenlik ayarlarını yapılandırın.

Toocreate bir MySQL veritabanı istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, oturum açma tooMySQL değiştirin:

```bash
mysql -u root -p
```

İşiniz bittiğinde, yazarak hello mysql isteminden çıkın `\q`.

### <a name="php"></a>PHP

Onay hello sürümüyle PHP komut aşağıdaki hello:

```bash
php -v
```

NGINX toouse hello PHP Fastcgı işlem yöneticisi (PHP-FPM) yapılandırın. Tooback hello özgün NGINX sunucusu yapılandırma dosyası engelleme ve tercih ettiğiniz bir düzenleyicide hello özgün dosya düzenleme komutları aşağıdaki hello çalıştırın:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

Merhaba Düzenleyicisi'nde hello Değiştir `/etc/nginx/sites-available/default` hello aşağıdaki ile. Açıklama hello ayarlarının Merhaba açıklamalarına bakın. Merhaba, VM için genel IP adresi yerine *yourPublicIPAddress*ve ayarları kalan hello bırakın. Ardından hello dosyayı kaydedin.

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

Merhaba NGINX yapılandırma sözdizimi hataları kontrol edin:

```bash
sudo nginx -t
```

Merhaba sözdiziminin doğru olup olmadığını NGINX komutu aşağıdaki hello ile yeniden başlatın:

```bash
sudo service nginx restart
```

Daha fazla tootest istiyorsanız, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturun. komutu aşağıdaki hello hello PHP bilgileri sayfası oluşturur:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Şimdi, oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz. Bir tarayıcı açın ve çok`http://yourPublicIPAddress/info.php`. VM Hello genel IP adresini değiştirin. Benzer toothis görüntü görünmelidir.

![PHP bilgileri sayfası][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure LEMP Server'da dağıtıldı. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bir Ubuntu VM oluşturma
> * Web trafiği için 80 numaralı bağlantı noktasını açın
> * NGINX, MySQL ve PHP yükleme
> * Yükleme ve yapılandırmasını doğrulayın
> * Merhaba LEMP yığında WordPress yükleme

Toohello sonraki öğretici toolearn nasıl ilerlemek SSL sertifikaları web sunucularıyla toosecure.

> [!div class="nextstepaction"]
> [SSL ile güvenli web sunucusu](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
