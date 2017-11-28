---
title: "Bir Linux VM CustomScript uzantısını kullanın | Microsoft Docs"
description: "CustomScript uzantısını uygulamalar üzerinde Azure Klasik dağıtım modeli kullanılarak oluşturulan Linux sanal makineleri dağıtmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="e5255-103">Linux için Azure CustomScript Uzantısı’nı kullanarak bir LAMP uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5255-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e5255-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e5255-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e5255-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5255-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e5255-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="e5255-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="e5255-107">Resource Manager modelini kullanarak bir AMPUL yığını dağıtma hakkında daha fazla bilgi için bkz: [burada](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5255-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e5255-108">Linux için Microsoft Azure CustomScript uzantısını (örneğin, Python ve Bash) VM tarafından desteklenen tüm komut dosyası dilinde yazılmış rastgele kod çalıştırarak sanal makineleri (VM'ler) özelleştirmek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5255-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="e5255-109">Bu, birden fazla makine için uygulama dağıtımı otomatik hale getirmek için çok esnek bir şekilde sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5255-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="e5255-110">CustomScript uzantısını Azure portalı, Windows PowerShell veya Azure komut satırı arabirimi (Azure CLI) kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="e5255-111">Kullanacağız. Bu makalede Klasik dağıtım modeli kullanılarak bir basit bir Ubuntu VM AMPUL uygulamayı dağıtmak için Azure CLI oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5255-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5255-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e5255-112">Prerequisites</span></span>
<span data-ttu-id="e5255-113">Bu örnekte, ilk iki Azure Ubuntu 14.04 veya sonraki sürümünü çalıştıran VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5255-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="e5255-114">Sanal makineleri adlı *betik vm* ve *ampul vm*.</span><span class="sxs-lookup"><span data-stu-id="e5255-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="e5255-115">Sanal makineleri oluştururken benzersiz adlar kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5255-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="e5255-116">CLI komutları çalıştırmak için kullanılır ve bir AMPUL uygulama dağıtmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5255-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="e5255-117">Ayrıca bir Azure Storage hesabını ve (Bu Azure portalından alabilirsiniz) erişmek için bir anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5255-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="e5255-118">Linux sanal makineleri Azure üzerinde oluşturma yardıma gereksinim duyarsanız başvurmak [çalıştıran bir sanal makine Linux oluşturma](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="e5255-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="e5255-119">Ubuntu yükleme komutları varsayar ancak desteklenen tüm Linux distro yüklemede uyarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="e5255-120">Komut dosyası vm VM Azure CLI, Azure çalışan bir bağlantı yüklenmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e5255-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="e5255-121">Bu Yardım başvurmak için [Azure komut satırı arabirimi yükleyip](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e5255-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="e5255-122">Bir komut dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e5255-122">Upload a script</span></span>
<span data-ttu-id="e5255-123">AMPUL yığını yüklemek ve bir PHP sayfası oluşturmak için uzak bir VM üzerinde bir komut dosyasını çalıştırmak için CustomScript uzantısını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e5255-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="e5255-124">Betik yerden erişmek için size bir Azure blob'u olarak karşıya.</span><span class="sxs-lookup"><span data-stu-id="e5255-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="e5255-125">Komut dosyası genel bakış</span><span class="sxs-lookup"><span data-stu-id="e5255-125">Script overview</span></span>
<span data-ttu-id="e5255-126">Komut dosyası örneği AMPUL yığını Ubuntu (MySQL sessiz bir yükleme ayarlama dahil) yükler, basit bir PHP dosya yazar ve Apache başlatır.</span><span class="sxs-lookup"><span data-stu-id="e5255-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="e5255-127">Komut dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e5255-127">Upload script</span></span>
<span data-ttu-id="e5255-128">Komut dosyası gibi bir metin dosyası olarak kaydetmeniz *install_lamp.sh*ve ardından Azure Storage'a yükler.</span><span class="sxs-lookup"><span data-stu-id="e5255-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="e5255-129">Kolayca Azure CLI ile bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="e5255-130">Aşağıdaki örnekte "betikleri" adlı bir depolama kapsayıcısı dosyayı yükler.</span><span class="sxs-lookup"><span data-stu-id="e5255-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="e5255-131">Kapsayıcı yoksa önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5255-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="e5255-132">Ayrıca komut dosyası Azure depolama biriminden indirmek nasıl açıklayan bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5255-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="e5255-133">Bu olarak Kaydet *public_config.json* ("mystorage" değerini depolama hesabınızın adıyla değiştirin):</span><span class="sxs-lookup"><span data-stu-id="e5255-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="e5255-134">Uzantısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5255-134">Deploy the extension</span></span>
<span data-ttu-id="e5255-135">Artık Azure CLI kullanarak uzaktan VM Linux CustomScript uzantısını dağıtmak için sonraki komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="e5255-136">Önceki komutu yükler ve çalıştırır *install_lamp.sh* adlı VM üzerinde komut dosyası *ampul vm*.</span><span class="sxs-lookup"><span data-stu-id="e5255-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="e5255-137">Uygulamasını içeren bir web sunucusu olduğundan, bir HTTP dinleme bağlantı noktası uzaktan VM sonraki komutla açın unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e5255-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="e5255-138">İzleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e5255-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="e5255-139">Ne kadar iyi uzaktan VM günlük dosyasını bakarak özel bir komut dosyası çalıştığı kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="e5255-140">SSH için *ampul vm* ve günlük dosyası İleri komutu ile kuyruk.</span><span class="sxs-lookup"><span data-stu-id="e5255-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="e5255-141">CustomScript uzantısını çalıştırdıktan sonra bilgi için oluşturduğunuz PHP sayfasına göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="e5255-142">Bu makalede örneğin PHP sayfasıdır *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="e5255-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5255-143">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5255-143">Additional resources</span></span>
<span data-ttu-id="e5255-144">Daha karmaşık uygulamaları dağıtmak için aynı temel adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5255-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="e5255-145">Bu örnekte, Azure storage'da bir ortak BLOB yükleme betiği kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="e5255-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="e5255-146">Daha güvenli bir seçenek ile güvenli bir BLOB yükleme betiği depolamak uygulanacak bir [güvenli erişim imzası](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="e5255-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="e5255-147">Ek kaynaklar için Azure CLI, Linux ve CustomScript uzantısını sonraki listelenir.</span><span class="sxs-lookup"><span data-stu-id="e5255-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="e5255-148">CustomScript uzantısını kullanarak Linux VM özelleştirme görevlerini otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="e5255-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="e5255-149">Azure Linux Uzantıları (GitHub)</span><span class="sxs-lookup"><span data-stu-id="e5255-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)