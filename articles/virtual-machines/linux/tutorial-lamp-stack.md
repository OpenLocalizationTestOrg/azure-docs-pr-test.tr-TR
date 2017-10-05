---
title: "Azure'da bir Linux sanal makinede AMPUL dağıtma | Microsoft Docs"
description: "Öğretici - yükleme azure'da bir Linux VM AMPUL yığında"
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
ms.openlocfilehash: 9148ac9646e4e1cfeff8f20c096e390499437e78
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="05ec5-103">Azure VM temelinde bir AMPUL web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="05ec5-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="05ec5-104">Bu makalede bir Apache web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (AMPUL yığını) dağıtma konusunda size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="05ec5-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="05ec5-105">NGINX web sunucusu tercih ederseniz, bkz. [LEMP yığın](tutorial-lemp-stack.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="05ec5-105">If you prefer the NGINX web server, see the [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="05ec5-106">Eylem AMPUL Server'da görmek için isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="05ec5-106">To see the LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="05ec5-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05ec5-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05ec5-108">Bir Ubuntu VM (' L' AMPUL yığınında) oluşturma</span><span class="sxs-lookup"><span data-stu-id="05ec5-108">Create an Ubuntu VM (the 'L' in the LAMP stack)</span></span>
> * <span data-ttu-id="05ec5-109">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="05ec5-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="05ec5-110">Apache, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="05ec5-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="05ec5-111">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="05ec5-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="05ec5-112">AMPUL sunucu üzerinde WordPress yükleme</span><span class="sxs-lookup"><span data-stu-id="05ec5-112">Install WordPress on the LAMP server</span></span>


<span data-ttu-id="05ec5-113">AMPUL yığında öneriler bir üretim ortamı için de dahil olmak üzere daha fazla bilgi için bkz: [Ubuntu belgelerine](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="05ec5-113">For more on the LAMP stack, including recommendations for a production environment, see the [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="05ec5-114">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="05ec5-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="05ec5-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05ec5-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="05ec5-116">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="05ec5-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="05ec5-117">Apache, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="05ec5-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="05ec5-118">Ubuntu paket kaynaklarını güncelleştirmek ve Apache, MySQL ve PHP yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05ec5-118">Run the following command to update Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="05ec5-119">Komut sonunda şapka (^) unutmayın.</span><span class="sxs-lookup"><span data-stu-id="05ec5-119">Note the caret (^) at the end of the command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="05ec5-120">Paketler ve diğer bağımlılıklar yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="05ec5-120">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="05ec5-121">İstendiğinde, MySQL için bir kök parola ayarlayın ve ardından devam etmek için Enter.</span><span class="sxs-lookup"><span data-stu-id="05ec5-121">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="05ec5-122">Kalan istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="05ec5-122">Follow the remaining prompts.</span></span> <span data-ttu-id="05ec5-123">Bu işlem, PHP, MySQL ile kullanmak için gerekli en düşük gerekli PHP uzantıları yükler.</span><span class="sxs-lookup"><span data-stu-id="05ec5-123">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="05ec5-125">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="05ec5-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="05ec5-126">Apache</span><span class="sxs-lookup"><span data-stu-id="05ec5-126">Apache</span></span>

<span data-ttu-id="05ec5-127">Aşağıdaki komutu Apache sürümüyle denetleyin:</span><span class="sxs-lookup"><span data-stu-id="05ec5-127">Check the version of Apache with the following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="05ec5-128">Apache yüklü ve bağlantı noktası 80 VM'nize açık ile web sunucusu artık Internet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="05ec5-128">With Apache installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="05ec5-129">Varsayılan Apache2 Ubuntu sayfasını görüntülemek için bir web tarayıcısı açın ve VM ortak IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="05ec5-129">To view the Apache2 Ubuntu Default Page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="05ec5-130">SSH VM için kullanılan ortak IP adresini kullan:</span><span class="sxs-lookup"><span data-stu-id="05ec5-130">Use the public IP address you used to SSH to the VM:</span></span>

![Apache varsayılan sayfa][3]


### <a name="mysql"></a><span data-ttu-id="05ec5-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="05ec5-132">MySQL</span></span>

<span data-ttu-id="05ec5-133">MySQL sürümü aşağıdaki komutla denetleyin (büyük harf Not `V` parametresi):</span><span class="sxs-lookup"><span data-stu-id="05ec5-133">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="05ec5-134">MySQL yükleme güvenliğinin sağlanmasına yardımcı olmak için aşağıdaki betiği çalıştıran öneririz:</span><span class="sxs-lookup"><span data-stu-id="05ec5-134">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="05ec5-135">MySQL kök parolanızı girin ve ortamınız için güvenlik ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="05ec5-135">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="05ec5-136">Bir MySQL veritabanı oluşturmak istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, MySQL oturum açma değiştirin:</span><span class="sxs-lookup"><span data-stu-id="05ec5-136">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="05ec5-137">İşiniz bittiğinde, mysql istemi yazarak çıkmak `\q`.</span><span class="sxs-lookup"><span data-stu-id="05ec5-137">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="05ec5-138">PHP</span><span class="sxs-lookup"><span data-stu-id="05ec5-138">PHP</span></span>

<span data-ttu-id="05ec5-139">PHP sürümünü aşağıdaki komutla denetleyin:</span><span class="sxs-lookup"><span data-stu-id="05ec5-139">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="05ec5-140">Daha fazla test etmek isterseniz, bir tarayıcıda görüntülemek üzere hızlı bir PHP bilgileri sayfası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05ec5-140">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="05ec5-141">Aşağıdaki komut, PHP bilgileri sayfası oluşturur:</span><span class="sxs-lookup"><span data-stu-id="05ec5-141">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="05ec5-142">Şimdi, oluşturduğunuz PHP bilgileri sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05ec5-142">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="05ec5-143">Bir tarayıcı açın ve gidin `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="05ec5-143">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="05ec5-144">VM ortak IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="05ec5-144">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="05ec5-145">Bu görüntüsüne benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="05ec5-145">It should look similar to this image.</span></span>

![PHP bilgileri sayfası][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="05ec5-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05ec5-147">Next steps</span></span>

<span data-ttu-id="05ec5-148">Bu öğreticide, Azure AMPUL Server'da dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="05ec5-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="05ec5-149">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="05ec5-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05ec5-150">Bir Ubuntu VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="05ec5-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="05ec5-151">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="05ec5-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="05ec5-152">Apache, MySQL ve PHP yükleme</span><span class="sxs-lookup"><span data-stu-id="05ec5-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="05ec5-153">Yükleme ve yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="05ec5-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="05ec5-154">AMPUL sunucu üzerinde WordPress yükleme</span><span class="sxs-lookup"><span data-stu-id="05ec5-154">Install WordPress on the LAMP server</span></span>

<span data-ttu-id="05ec5-155">SSL sertifikaları web sunucularıyla güvenli öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="05ec5-155">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="05ec5-156">SSL ile güvenli web sunucusu</span><span class="sxs-lookup"><span data-stu-id="05ec5-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png