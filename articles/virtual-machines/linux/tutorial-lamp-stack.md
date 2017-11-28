---
title: azure'da bir Linux sanal makinede AMPUL aaaDeploy | Microsoft Docs
description: "Öğretici - yükleme hello AMPUL azure'da bir Linux VM yığında"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="ea5f0-103">Azure VM temelinde bir AMPUL web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="ea5f0-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="ea5f0-104">Bu makalede toodeploy Apache nasıl web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (Merhaba AMPUL yığını) aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="ea5f0-105">Merhaba NGINX web sunucusu tercih ederseniz, hello bkz [LEMP yığın](tutorial-lemp-stack.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="ea5f0-106">toosee hello AMPUL sunucu eyleminde, isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="ea5f0-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea5f0-108">Bir Ubuntu VM (Merhaba 'L' hello AMPUL yığınında) oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea5f0-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="ea5f0-109">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="ea5f0-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="ea5f0-110">Apache, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="ea5f0-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="ea5f0-111">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ea5f0-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="ea5f0-112">WordPress hello AMPUL sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="ea5f0-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="ea5f0-113">Merhaba AMPUL yığını, bir üretim ortamı için öneriler dahil olmak üzere daha fazla bilgi için bkz: Merhaba [Ubuntu belgelerine](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="ea5f0-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ea5f0-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ea5f0-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ea5f0-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ea5f0-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="ea5f0-117">Apache, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="ea5f0-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="ea5f0-118">Aşağıdaki komut tooupdate Ubuntu paket kaynaklar hello çalıştırın ve Apache, MySQL ve PHP yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="ea5f0-119">Merhaba komutu hello sonunda Hello şapka (^) unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="ea5f0-120">İstendiğinde tooinstall hello paketler ve diğer bağımlılıklar var.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="ea5f0-121">İstendiğinde, MySQL, ardından [Enter] toocontinue için bir kök parola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="ea5f0-122">Merhaba kalan istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="ea5f0-123">Bu işlem hello minimum gerekli PHP uzantıları gerekli toouse PHP MySQL ile yükler.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="ea5f0-125">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ea5f0-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="ea5f0-126">Apache</span><span class="sxs-lookup"><span data-stu-id="ea5f0-126">Apache</span></span>

<span data-ttu-id="ea5f0-127">Onay hello sürümüyle Apache komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="ea5f0-128">Apache tooyour VM yüklü ve bağlantı noktası 80'i açın, hello web sunucusu artık erişilebilir hello Internet.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="ea5f0-129">tooview hello Apache2 Ubuntu sayfasında, varsayılan bir web tarayıcısı açın ve hello VM hello ortak IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="ea5f0-130">Merhaba tooSSH toohello VM kullanılan ortak IP adresini kullan:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Apache varsayılan sayfa][3]


### <a name="mysql"></a><span data-ttu-id="ea5f0-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="ea5f0-132">MySQL</span></span>

<span data-ttu-id="ea5f0-133">Komutu aşağıdaki hello ile MySQL Hello sürümünü denetleme (Not hello sermaye `V` parametresi):</span><span class="sxs-lookup"><span data-stu-id="ea5f0-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="ea5f0-134">Komut dosyası toohelp güvenli hello MySQL yüklenmesinden hello çalıştıran öneririz:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="ea5f0-135">MySQL kök parolanızı girin ve ortamınız için hello güvenlik ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="ea5f0-136">Toocreate bir MySQL veritabanı istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, oturum açma tooMySQL değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="ea5f0-137">İşiniz bittiğinde, yazarak hello mysql isteminden çıkın `\q`.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="ea5f0-138">PHP</span><span class="sxs-lookup"><span data-stu-id="ea5f0-138">PHP</span></span>

<span data-ttu-id="ea5f0-139">Onay hello sürümüyle PHP komut aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="ea5f0-140">Daha fazla tootest istiyorsanız, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="ea5f0-141">komutu aşağıdaki hello hello PHP bilgileri sayfası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="ea5f0-142">Şimdi, oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="ea5f0-143">Bir tarayıcı açın ve çok`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="ea5f0-144">VM Hello genel IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="ea5f0-145">Benzer toothis görüntü görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-145">It should look similar toothis image.</span></span>

![PHP bilgileri sayfası][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="ea5f0-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea5f0-147">Next steps</span></span>

<span data-ttu-id="ea5f0-148">Bu öğreticide, Azure AMPUL Server'da dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="ea5f0-149">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="ea5f0-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea5f0-150">Bir Ubuntu VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea5f0-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="ea5f0-151">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="ea5f0-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="ea5f0-152">Apache, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="ea5f0-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="ea5f0-153">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ea5f0-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="ea5f0-154">WordPress hello AMPUL sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="ea5f0-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="ea5f0-155">Toohello sonraki öğretici toolearn nasıl ilerlemek SSL sertifikaları web sunucularıyla toosecure.</span><span class="sxs-lookup"><span data-stu-id="ea5f0-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea5f0-156">SSL ile güvenli web sunucusu</span><span class="sxs-lookup"><span data-stu-id="ea5f0-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png