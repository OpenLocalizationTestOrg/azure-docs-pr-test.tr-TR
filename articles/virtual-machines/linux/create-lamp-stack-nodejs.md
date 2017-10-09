---
title: bir Linux sanal makinede hello Azure CLI 1.0 ile AMPUL aaaDeploy | Microsoft Docs
description: "Nasıl tooinstall hello AMPUL yığın azure'da bir Linux VM hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="58894-103">AMPUL yığın hello Azure CLI 1.0 ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="58894-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="58894-104">Bu makalede toodeploy Apache nasıl web sunucusu, MySQL ve Azure üzerinde PHP (Merhaba AMPUL yığını) aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="58894-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="58894-105">Bir Azure hesabınızın olması gerekir ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve hello [Azure CLI](../../cli-install-nodejs.md) diğer bir deyişle [bağlı tooyour Azure hesabı](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="58894-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="58894-106">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="58894-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="58894-107">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="58894-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="58894-108">[Azure CLI 1.0] – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="58894-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="58894-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="58894-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="58894-110">Var olan VM üzerinde AMPUL dağıtma</span><span class="sxs-lookup"><span data-stu-id="58894-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="58894-111">Yeni VM gözden geçirme üzerinde AMPUL dağıtma</span><span class="sxs-lookup"><span data-stu-id="58894-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="58894-112">Oluşturarak başlayın bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md) içerecek yeni VM hello:</span><span class="sxs-lookup"><span data-stu-id="58894-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="58894-113">toocreate VM kendisini Merhaba, bulunan zaten yazılmış bir Azure Resource Manager şablonunu kullanabilirsiniz [github'da burada](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="58894-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="58894-114">Daha fazla bazı girişler isteyen bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="58894-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="58894-115">Bir Linux VM üzerinde zaten yüklü AMPUL ile oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="58894-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="58894-116">İsterseniz, aşağı çok atlayarak hello yükleme doğrulayabilirsiniz[doğrulayın AMPUL başarıyla yüklendi](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="58894-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="58894-117">AMPUL üzerinde var olan VM izlenecek dağıtma</span><span class="sxs-lookup"><span data-stu-id="58894-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="58894-118">Bir Linux VM oluşturma yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate bir Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58894-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="58894-119">Ardından, Linux VM hello tooSSH gerekir.</span><span class="sxs-lookup"><span data-stu-id="58894-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="58894-120">Bir SSH anahtarı oluşturma konusunda yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate Linux/Mac üzerinde bir SSH anahtarı](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58894-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="58894-121">Bir SSH anahtarı zaten varsa, şimdi SSH komut satırından Linux VM ile uygulamasına gidin ve `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="58894-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="58894-122">Linux VM içinde çalışan, biz hello AMPUL yığın Debian tabanlı dağıtımlar üzerinde yüklenmesinde size yol.</span><span class="sxs-lookup"><span data-stu-id="58894-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="58894-123">Merhaba tam komutları için diğer Linux distro'lar farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="58894-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="58894-124">Debian/Ubuntu üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="58894-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="58894-125">Yüklü olan paketleri aşağıdaki hello gerekir: `apache2`, `mysql-server`, `php5`, ve `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="58894-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="58894-126">Bu paketler, doğrudan bu paketleri kapmasını veya Tasksel kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58894-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="58894-127">Her iki seçenek için yönergeler aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="58894-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="58894-128">Yüklemeden önce toodownload gerekir ve güncelleştirme paketini listeler.</span><span class="sxs-lookup"><span data-stu-id="58894-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="58894-129">Tek paketler</span><span class="sxs-lookup"><span data-stu-id="58894-129">Individual packages</span></span>
<span data-ttu-id="58894-130">Get apt kullanma:</span><span class="sxs-lookup"><span data-stu-id="58894-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="58894-131">Tasksel kullanma</span><span class="sxs-lookup"><span data-stu-id="58894-131">Using tasksel</span></span>
<span data-ttu-id="58894-132">Alternatif olarak, Tasksel, birden çok ilişkili paketleri, sisteminize Eşgüdümlü "görev" olarak yükler Debian/Ubuntu aracı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58894-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="58894-133">Merhaba önceki seçeneklerinden birini çalıştırdıktan sonra şunları yapacaksınız istendiğinde tooinstall bu paketleri ve diğer çeşitli bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="58894-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="58894-134">'Y', 'Enter' toocontinue basın ve herhangi diğer istemleri tooset yönetici parolası için MySQL izleyin.</span><span class="sxs-lookup"><span data-stu-id="58894-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="58894-135">Bu MySQL ile Merhaba minimum gerekli PHP uzantıları gerekli toouse PHP yükler.</span><span class="sxs-lookup"><span data-stu-id="58894-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="58894-136">Komut toosee aşağıdaki hello paketleri olarak kullanılabilir olan diğer PHP uzantılarının çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="58894-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="58894-137">İnfo.php belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="58894-137">Create info.php document</span></span>
<span data-ttu-id="58894-138">Şimdi, Apache, MySQL ve PHP sürümünü hello komut satırı yazarak elinizde mümkün toocheck olmalısınız `apache2 -v`, `mysql -v`, veya `php -v`.</span><span class="sxs-lookup"><span data-stu-id="58894-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="58894-139">Tootest gibi daha fazla, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58894-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="58894-140">Bir dosya ile Nano metin düzenleyicisi bu komutla oluşturun:</span><span class="sxs-lookup"><span data-stu-id="58894-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="58894-141">Merhaba GNU Nano metin düzenleyicisi içinde satırlardan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="58894-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="58894-142">Ardından kaydedin ve hello Metin Düzenleyicisi'nden çıkın.</span><span class="sxs-lookup"><span data-stu-id="58894-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="58894-143">Tüm yeni yüklemeler etkili şekilde Apache bu komutla yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="58894-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="58894-144">Başarılı bir şekilde AMPUL doğrulayın</span><span class="sxs-lookup"><span data-stu-id="58894-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="58894-145">Şimdi bir tarayıcı açıp toohttp://youruniqueDNS/info.php gidip oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58894-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="58894-146">Benzer toothis görüntü görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="58894-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="58894-147">Merhaba Apache2 Ubuntu varsayılan sayfa tooyou http://youruniqueDNS/ giderek görüntüleyerek Apache yüklemenizi denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58894-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="58894-148">Bu görüntü gibi bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58894-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="58894-149">Tebrikler, yalnızca Kurulum, Azure VM'deki bir AMPUL yığınına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="58894-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="58894-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58894-150">Next steps</span></span>
<span data-ttu-id="58894-151">Merhaba hello AMPUL yığında Ubuntu belgelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="58894-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="58894-152">https://help.ubuntu.com/Community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="58894-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png