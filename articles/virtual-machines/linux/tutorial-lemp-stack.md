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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="139b4-103">Azure VM temelinde bir LEMP web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="139b4-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="139b4-104">Bu makalede nasıl NGINX web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (LEMP yığını) dağıtılacağı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="139b4-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="139b4-105">LEMP yığın popüler bir alternatif olan [AMPUL yığın](tutorial-lamp-stack.md), hangi Azure ile de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="139b4-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="139b4-106">Eylem LEMP Server'da görmek için isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="139b4-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="139b4-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="139b4-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="139b4-108">Bir Ubuntu VM (' L' LEMP yığınında) oluşturma</span><span class="sxs-lookup"><span data-stu-id="139b4-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="139b4-109">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="139b4-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="139b4-110">NGINX, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="139b4-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="139b4-111">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="139b4-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="139b4-112">WordPress LEMP sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="139b4-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="139b4-113">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="139b4-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="139b4-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="139b4-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="139b4-115">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="139b4-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="139b4-116">NGINX, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="139b4-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="139b4-117">Ubuntu paket kaynaklarını güncelleştirmek ve NGINX, MySQL ve PHP yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="139b4-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="139b4-118">Paketler ve diğer bağımlılıklar yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="139b4-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="139b4-119">İstendiğinde, MySQL için bir kök parola ayarlayın ve ardından devam etmek için Enter.</span><span class="sxs-lookup"><span data-stu-id="139b4-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="139b4-120">Kalan istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="139b4-120">Follow the remaining prompts.</span></span> <span data-ttu-id="139b4-121">Bu işlem, PHP, MySQL ile kullanmak için gerekli en düşük gerekli PHP uzantıları yükler.</span><span class="sxs-lookup"><span data-stu-id="139b4-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="139b4-123">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="139b4-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="139b4-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="139b4-124">NGINX</span></span>

<span data-ttu-id="139b4-125">Aşağıdaki komutu NGINX sürümüyle denetleyin:</span><span class="sxs-lookup"><span data-stu-id="139b4-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="139b4-126">Yüklü NGINX ve bağlantı noktası 80 VM'nize açık ile web sunucusu artık Internet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="139b4-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="139b4-127">NGINX Hoş Geldiniz sayfasını görüntülemek için bir web tarayıcısı açın ve VM ortak IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="139b4-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="139b4-128">SSH VM için kullanılan ortak IP adresini kullan:</span><span class="sxs-lookup"><span data-stu-id="139b4-128">Use the public IP address you used to SSH to the VM:</span></span>

![NGINX varsayılan sayfa][3]


### <a name="mysql"></a><span data-ttu-id="139b4-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="139b4-130">MySQL</span></span>

<span data-ttu-id="139b4-131">MySQL sürümü aşağıdaki komutla denetleyin (büyük harf Not `V` parametresi):</span><span class="sxs-lookup"><span data-stu-id="139b4-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="139b4-132">MySQL yükleme güvenliğinin sağlanmasına yardımcı olmak için aşağıdaki betiği çalıştıran öneririz:</span><span class="sxs-lookup"><span data-stu-id="139b4-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="139b4-133">MySQL kök parolanızı girin ve ortamınız için güvenlik ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="139b4-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="139b4-134">Bir MySQL veritabanı oluşturmak istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, MySQL oturum açma değiştirin:</span><span class="sxs-lookup"><span data-stu-id="139b4-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="139b4-135">İşiniz bittiğinde, mysql istemi yazarak çıkmak `\q`.</span><span class="sxs-lookup"><span data-stu-id="139b4-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="139b4-136">PHP</span><span class="sxs-lookup"><span data-stu-id="139b4-136">PHP</span></span>

<span data-ttu-id="139b4-137">PHP sürümünü aşağıdaki komutla denetleyin:</span><span class="sxs-lookup"><span data-stu-id="139b4-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="139b4-138">PHP Fastcgı işlem yöneticisi (PHP-FPM) kullanmak için NGINX yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="139b4-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="139b4-139">Özgün NGINX server blok yapılandırma dosyasını yedekleyin ve tercih ettiğiniz bir düzenleyicide özgün dosyayı düzenlemek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="139b4-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="139b4-140">Düzenleyicide Değiştir `/etc/nginx/sites-available/default` aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="139b4-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="139b4-141">Açıklamaları ayarları hakkında ayrıntılı açıklamalar için bkz.</span><span class="sxs-lookup"><span data-stu-id="139b4-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="139b4-142">VM için genel IP adresi yerine *yourPublicIPAddress*ve geri kalan ayarları bırakın.</span><span class="sxs-lookup"><span data-stu-id="139b4-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="139b4-143">Ardından dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="139b4-143">Then save the file.</span></span>

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

<span data-ttu-id="139b4-144">Sözdizimi hataları NGINX yapılandırmasını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="139b4-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="139b4-145">Sözdizimi doğru ise, NGINX aşağıdaki komutla yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="139b4-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="139b4-146">Daha fazla test etmek isterseniz, bir tarayıcıda görüntülemek üzere hızlı bir PHP bilgileri sayfası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="139b4-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="139b4-147">Aşağıdaki komut, PHP bilgileri sayfası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="139b4-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="139b4-148">Şimdi, oluşturduğunuz PHP bilgileri sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="139b4-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="139b4-149">Bir tarayıcı açın ve gidin `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="139b4-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="139b4-150">VM ortak IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="139b4-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="139b4-151">Bu görüntüsüne benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="139b4-151">It should look similar to this image.</span></span>

![PHP bilgileri sayfası][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="139b4-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="139b4-153">Next steps</span></span>

<span data-ttu-id="139b4-154">Bu öğreticide, Azure LEMP Server'da dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="139b4-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="139b4-155">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="139b4-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="139b4-156">Bir Ubuntu VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="139b4-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="139b4-157">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="139b4-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="139b4-158">NGINX, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="139b4-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="139b4-159">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="139b4-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="139b4-160">WordPress LEMP yığında yükleme</span><span class="sxs-lookup"><span data-stu-id="139b4-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="139b4-161">SSL sertifikaları web sunucularıyla güvenli öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="139b4-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="139b4-162">SSL ile güvenli web sunucusu</span><span class="sxs-lookup"><span data-stu-id="139b4-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
