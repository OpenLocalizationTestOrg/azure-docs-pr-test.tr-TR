---
title: "aaaUse hello CustomScript uzantısını bir Linux VM üzerinde | Microsoft Docs"
description: "Toouse hello CustomScript uzantısını toodeploy uygulamaları üzerindeki Linux sanal makineleri azure'da hello Klasik dağıtım modeli kullanılarak nasıl oluşturulacağını öğrenin."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="d5627-103">Linux için Hello Azure CustomScript uzantısını kullanarak bir AMPUL uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="d5627-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d5627-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d5627-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d5627-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d5627-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d5627-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="d5627-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d5627-107">Merhaba Resource Manager modelini kullanarak bir AMPUL yığını dağıtma hakkında daha fazla bilgi için bkz: [burada](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5627-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d5627-108">Hello Microsoft Azure CustomScript uzantısını Linux için bir yol toocustomize hello VM (örneğin, Python ve Bash) tarafından desteklenen tüm komut dosyası dilinde yazılmış rastgele kod çalıştırarak sanal makineleri (VM'ler) sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5627-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="d5627-109">Bu, uygulama dağıtım toomultiple makineler çok esnek bir şekilde tooautomate sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5627-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="d5627-110">Merhaba CustomScript uzantısını dağıtabilirsiniz kullanarak hello Azure portalı, Windows PowerShell veya hello Azure komut satırı arabirimi (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="d5627-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="d5627-111">Kullanacağız. Bu makalede hello Azure CLI toodeploy basit bir AMPUL uygulama tooan Ubuntu VM hello Klasik dağıtım modeli kullanılarak oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="d5627-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5627-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d5627-112">Prerequisites</span></span>
<span data-ttu-id="d5627-113">Bu örnekte, ilk iki Azure Ubuntu 14.04 veya sonraki sürümünü çalıştıran VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d5627-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="d5627-114">Merhaba VM'ler denir *betik vm* ve *ampul vm*.</span><span class="sxs-lookup"><span data-stu-id="d5627-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="d5627-115">Merhaba Vm'leri oluştururken benzersiz adlar kullanın.</span><span class="sxs-lookup"><span data-stu-id="d5627-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="d5627-116">Kullanılan toorun hello CLI komutları biridir ve kullanılan toodeploy hello AMPUL uygulama biridir.</span><span class="sxs-lookup"><span data-stu-id="d5627-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="d5627-117">Bir Azure Storage hesabı ve anahtarı tooaccess etmeniz BT (alabilirsiniz bu hello Azure portal ').</span><span class="sxs-lookup"><span data-stu-id="d5627-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="d5627-118">Linux sanal makineleri Azure üzerinde oluşturma yardıma gereksinim duyarsanız çok başvuran[çalıştıran bir sanal makine Linux oluşturma](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="d5627-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="d5627-119">Ubuntu Hello yükleme komutları varsayar ancak herhangi bir Linux distro desteklenen hello yükleme uyarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5627-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="d5627-120">Merhaba betik vm VM çalışma bağlantı tooAzure ile Azure CLI, yüklü toohave gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5627-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="d5627-121">Bu Yardım çok başvurmak için[hello Azure komut satırı arabirimi yükleyip](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d5627-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="d5627-122">Bir komut dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d5627-122">Upload a script</span></span>
<span data-ttu-id="d5627-123">Bir uzak VM tooinstall hello AMPUL yığında hello CustomScript uzantısını toorun bir komut dosyası kullanır ve bir PHP sayfası oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="d5627-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="d5627-124">Sipariş tooaccess hello komut yerden biz bunu bir Azure blob'u olarak yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d5627-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="d5627-125">Komut dosyası genel bakış</span><span class="sxs-lookup"><span data-stu-id="d5627-125">Script overview</span></span>
<span data-ttu-id="d5627-126">Merhaba komut dosyası örneği (MySQL sessiz bir yükleme ayarlama dahil) AMPUL yığın tooUbuntu yükler, basit bir PHP dosya yazar ve Apache başlatır.</span><span class="sxs-lookup"><span data-stu-id="d5627-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="d5627-127">Komut dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d5627-127">Upload script</span></span>
<span data-ttu-id="d5627-128">Merhaba komut dosyasını bir metin dosyası olarak örneğin kaydetmek *install_lamp.sh*ve tooAzure depolama yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d5627-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="d5627-129">Kolayca Azure CLI ile bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5627-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="d5627-130">Merhaba aşağıdaki örnekte "betikleri" adlı hello dosya tooa depolama kapsayıcı yükler.</span><span class="sxs-lookup"><span data-stu-id="d5627-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="d5627-131">Merhaba kapsayıcı yoksa toocreate gerekir, ilk.</span><span class="sxs-lookup"><span data-stu-id="d5627-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="d5627-132">Ayrıca nasıl toodownload hello Azure Storage betikten açıklayan bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d5627-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="d5627-133">Bu olarak Kaydet *public_config.json* ("mystorage" Merhaba depolama hesabınızın adını ile değiştirerek):</span><span class="sxs-lookup"><span data-stu-id="d5627-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="d5627-134">Merhaba uzantısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="d5627-134">Deploy hello extension</span></span>
<span data-ttu-id="d5627-135">Artık hello sonraki komut toodeploy hello Linux CustomScript uzantısını toohello uzaktan kullanarak Azure CLI hello VM kullanma.</span><span class="sxs-lookup"><span data-stu-id="d5627-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="d5627-136">Merhaba önceki komutu yükler ve çalıştırır hello *install_lamp.sh* VM adlı hello komut *ampul vm*.</span><span class="sxs-lookup"><span data-stu-id="d5627-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="d5627-137">Merhaba uygulamasını içeren bir web sunucusu olduğundan, tooopen bir HTTP dinleme bağlantı noktası hello unutmayın hello İleri komutu ile uzaktan VM.</span><span class="sxs-lookup"><span data-stu-id="d5627-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="d5627-138">İzleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d5627-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="d5627-139">Merhaba günlük dosyasına bakarak hello özel komut dosyası çalıştırır uzak VM ne kadar iyi hello kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5627-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="d5627-140">SSH çok*ampul vm* ve kuyruk hello günlük dosyası hello sonraki komutu.</span><span class="sxs-lookup"><span data-stu-id="d5627-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="d5627-141">Merhaba CustomScript uzantısını çalıştırdıktan sonra bilgi için oluşturulan toohello PHP sayfası göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5627-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="d5627-142">Merhaba PHP sayfasında hello Örneğin bu makalede *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="d5627-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5627-143">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d5627-143">Additional resources</span></span>
<span data-ttu-id="d5627-144">Kullanabileceğiniz hello aynı temel adımlar toodeploy daha karmaşık uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="d5627-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="d5627-145">Bu örnekte, bir ortak BLOB Azure storage'da hello yükleme betiği kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="d5627-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="d5627-146">Daha güvenli bir seçenek ile güvenli bir BLOB toostore hello yükleme betiği olacak bir [güvenli erişim imzası](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="d5627-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="d5627-147">Ek kaynaklar için Azure CLI, Linux ve hello CustomScript uzantısını sonraki listelenir.</span><span class="sxs-lookup"><span data-stu-id="d5627-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="d5627-148">CustomScript uzantısını kullanarak Linux VM özelleştirme görevlerini otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="d5627-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="d5627-149">Azure Linux Uzantıları (GitHub)</span><span class="sxs-lookup"><span data-stu-id="d5627-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)