---
title: "aaaAutomating sanal makine uzantıları ile uygulama dağıtımı | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="18236-103">Linux VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="18236-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="18236-104">Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra hello gerçek uygulama dağıtımı ele toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="18236-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="18236-105">Uygulama dağıtımı burada tooinstalling hello gerçek uygulama ikililerini Azure kaynaklarını üzerine başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="18236-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="18236-106">Merhaba müzik deposu örnek, .net için çekirdek, NGINX ve yönetici her sanal makineye yükleyip toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="18236-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="18236-107">Merhaba müzik deposu ikili dosyaları hello sanal makineye yüklenmesi yüklü toobe gerekir ve hello müzik deposu veritabanı önceden oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="18236-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="18236-108">Bu belge, sanal makine uzantıları uygulama dağıtımı ve yapılandırması tooAzure sanal makineleri nasıl otomatikleştirebilirsiniz ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="18236-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="18236-109">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="18236-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="18236-110">Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="18236-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="18236-111">Merhaba tam şablon burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="18236-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="18236-112">Yapılandırma komut dosyası</span><span class="sxs-lookup"><span data-stu-id="18236-112">Configuration script</span></span>
<span data-ttu-id="18236-113">Sanal makine, sanal makineleri tooprovide yapılandırma Otomasyon karşı yürütme özel programları uzantılarıdır.</span><span class="sxs-lookup"><span data-stu-id="18236-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="18236-114">Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="18236-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="18236-115">Bir özel betik uzantısı herhangi bir sanal makine komut dosyası kullanılan toorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="18236-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="18236-116">Merhaba müzik deposu örnekle bu toohello özel betik uzantısı tooconfigure hello Ubuntu sanal makineleri ve hello müzik deposu uygulamayı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="18236-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="18236-117">Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılır hello komut dosyasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="18236-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="18236-118">Bu komut dosyası hello Ubuntu sanal makine toohost hello müzik deposu uygulama yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="18236-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="18236-119">Çalıştırdığınızda, tüm gerekli yazılım hello betik yükler kaynak denetiminden hello müzik deposu uygulamayı yükleyip hello veritabanı hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="18236-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="18236-120">bir .net barındırma hakkında daha fazla toolearn çekirdek uygulama Linux üzerinde bkz [Yayımla tooa Linux üretim ortamına](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="18236-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="18236-121">Bu örnek tanıtım amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="18236-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="18236-122">VM betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="18236-122">VM Script Extension</span></span>
<span data-ttu-id="18236-123">VM uzantıları bir sanal makine hello Azure Resource Manager şablonunda hello uzantısı kaynak ekleyerek derleme zamanında çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="18236-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="18236-124">Merhaba uzantısı hello Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON hello şablonuna ekleyerek eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="18236-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="18236-125">Merhaba betik uzantısı kaynak sanal makine kaynağı hello içinde iç içe yerleştirilmiş; Bu örnekte aşağıdaki hello görülebilir.</span><span class="sxs-lookup"><span data-stu-id="18236-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="18236-126">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="18236-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="18236-127">Merhaba aşağıdaki betik hello JSON Github'da depolanan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="18236-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="18236-128">Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="18236-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="18236-129">Ayrıca, şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir, Azure Resource Manager şablonları hello komut dosyası yürütme dize tooconstructed izin verin.</span><span class="sxs-lookup"><span data-stu-id="18236-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="18236-130">Bu durumda veri hello şablonları dağıtırken sağlanır ve bu değerler, daha sonra hello komut dosyası yürütülürken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="18236-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="18236-131">Merhaba özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18236-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="18236-132">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="18236-132">Next Step</span></span>
<hr>

[<span data-ttu-id="18236-133">Daha fazla Azure Resource Manager şablonları keşfedin</span><span class="sxs-lookup"><span data-stu-id="18236-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

