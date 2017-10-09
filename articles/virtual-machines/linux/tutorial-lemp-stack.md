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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="8d43c-103">Azure VM temelinde bir LEMP web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="8d43c-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="8d43c-104">Bu makalede toodeploy bir NGINX nasıl web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (Merhaba LEMP yığını) aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8d43c-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="8d43c-105">Merhaba LEMP yığını olan popüler bir alternatif toohello [AMPUL yığın](tutorial-lamp-stack.md), hangi Azure ile de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d43c-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="8d43c-106">toosee hello LEMP sunucu eyleminde, isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8d43c-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="8d43c-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8d43c-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d43c-108">Bir Ubuntu VM (Merhaba 'L' hello LEMP yığınında) oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d43c-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="8d43c-109">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="8d43c-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="8d43c-110">NGINX, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="8d43c-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="8d43c-111">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8d43c-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="8d43c-112">WordPress hello LEMP sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="8d43c-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8d43c-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="8d43c-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8d43c-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="8d43c-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8d43c-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8d43c-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="8d43c-116">NGINX, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="8d43c-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="8d43c-117">Aşağıdaki komut tooupdate Ubuntu paket kaynaklar hello çalıştırın ve NGINX, MySQL ve PHP yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8d43c-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="8d43c-118">İstendiğinde tooinstall hello paketler ve diğer bağımlılıklar var.</span><span class="sxs-lookup"><span data-stu-id="8d43c-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="8d43c-119">İstendiğinde, MySQL, ardından [Enter] toocontinue için bir kök parola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8d43c-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="8d43c-120">Merhaba kalan istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8d43c-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="8d43c-121">Bu işlem hello minimum gerekli PHP uzantıları gerekli toouse PHP MySQL ile yükler.</span><span class="sxs-lookup"><span data-stu-id="8d43c-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="8d43c-123">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8d43c-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="8d43c-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="8d43c-124">NGINX</span></span>

<span data-ttu-id="8d43c-125">Onay hello sürümüyle NGINX komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="8d43c-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="8d43c-126">NGINX ile tooyour VM yüklü ve bağlantı noktası 80'i açın, hello web sunucusu artık erişilebilir hello Internet.</span><span class="sxs-lookup"><span data-stu-id="8d43c-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="8d43c-127">tooview hello NGINX Hoş Geldiniz sayfasında, bir web tarayıcısı açın ve hello VM hello ortak IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="8d43c-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="8d43c-128">Merhaba tooSSH toohello VM kullanılan ortak IP adresini kullan:</span><span class="sxs-lookup"><span data-stu-id="8d43c-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![NGINX varsayılan sayfa][3]


### <a name="mysql"></a><span data-ttu-id="8d43c-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="8d43c-130">MySQL</span></span>

<span data-ttu-id="8d43c-131">Komutu aşağıdaki hello ile MySQL Hello sürümünü denetleme (Not hello sermaye `V` parametresi):</span><span class="sxs-lookup"><span data-stu-id="8d43c-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="8d43c-132">Komut dosyası toohelp güvenli hello MySQL yüklenmesinden hello çalıştıran öneririz:</span><span class="sxs-lookup"><span data-stu-id="8d43c-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="8d43c-133">MySQL kök parolanızı girin ve ortamınız için hello güvenlik ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8d43c-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="8d43c-134">Toocreate bir MySQL veritabanı istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, oturum açma tooMySQL değiştirin:</span><span class="sxs-lookup"><span data-stu-id="8d43c-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="8d43c-135">İşiniz bittiğinde, yazarak hello mysql isteminden çıkın `\q`.</span><span class="sxs-lookup"><span data-stu-id="8d43c-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="8d43c-136">PHP</span><span class="sxs-lookup"><span data-stu-id="8d43c-136">PHP</span></span>

<span data-ttu-id="8d43c-137">Onay hello sürümüyle PHP komut aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="8d43c-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="8d43c-138">NGINX toouse hello PHP Fastcgı işlem yöneticisi (PHP-FPM) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8d43c-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="8d43c-139">Tooback hello özgün NGINX sunucusu yapılandırma dosyası engelleme ve tercih ettiğiniz bir düzenleyicide hello özgün dosya düzenleme komutları aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8d43c-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="8d43c-140">Merhaba Düzenleyicisi'nde hello Değiştir `/etc/nginx/sites-available/default` hello aşağıdaki ile.</span><span class="sxs-lookup"><span data-stu-id="8d43c-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="8d43c-141">Açıklama hello ayarlarının Merhaba açıklamalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="8d43c-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="8d43c-142">Merhaba, VM için genel IP adresi yerine *yourPublicIPAddress*ve ayarları kalan hello bırakın.</span><span class="sxs-lookup"><span data-stu-id="8d43c-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="8d43c-143">Ardından hello dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8d43c-143">Then save hello file.</span></span>

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

<span data-ttu-id="8d43c-144">Merhaba NGINX yapılandırma sözdizimi hataları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="8d43c-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="8d43c-145">Merhaba sözdiziminin doğru olup olmadığını NGINX komutu aşağıdaki hello ile yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="8d43c-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="8d43c-146">Daha fazla tootest istiyorsanız, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8d43c-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="8d43c-147">komutu aşağıdaki hello hello PHP bilgileri sayfası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="8d43c-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="8d43c-148">Şimdi, oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d43c-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="8d43c-149">Bir tarayıcı açın ve çok`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="8d43c-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="8d43c-150">VM Hello genel IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8d43c-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="8d43c-151">Benzer toothis görüntü görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="8d43c-151">It should look similar toothis image.</span></span>

![PHP bilgileri sayfası][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="8d43c-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d43c-153">Next steps</span></span>

<span data-ttu-id="8d43c-154">Bu öğreticide, Azure LEMP Server'da dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="8d43c-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="8d43c-155">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="8d43c-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d43c-156">Bir Ubuntu VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d43c-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="8d43c-157">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="8d43c-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="8d43c-158">NGINX, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="8d43c-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="8d43c-159">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8d43c-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="8d43c-160">Merhaba LEMP yığında WordPress yükleme</span><span class="sxs-lookup"><span data-stu-id="8d43c-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="8d43c-161">Toohello sonraki öğretici toolearn nasıl ilerlemek SSL sertifikaları web sunucularıyla toosecure.</span><span class="sxs-lookup"><span data-stu-id="8d43c-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d43c-162">SSL ile güvenli web sunucusu</span><span class="sxs-lookup"><span data-stu-id="8d43c-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
