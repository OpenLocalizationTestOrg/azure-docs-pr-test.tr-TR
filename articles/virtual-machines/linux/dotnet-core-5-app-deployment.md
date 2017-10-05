---
title: "Sanal makine uzantıları ile uygulama dağıtımı otomatikleştirme | Microsoft Docs"
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
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="7782f-103">Linux VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="7782f-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="7782f-104">Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra gerçek uygulama dağıtımı ele alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7782f-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="7782f-105">Uygulama dağıtımı burada gerçek uygulama ikili dosyaların Azure kaynaklarını üzerine yüklenmesi için başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="7782f-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="7782f-106">Müzik deposu örnek, .net için çekirdek, NGINX ve Supervisor gereken yüklenmeli ve her sanal makinede yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7782f-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="7782f-107">Müzik deposu ikili dosyasının sanal makineye yüklenmesi gerekmez ve müzik deposu veritabanı önceden oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="7782f-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="7782f-108">Bu belge, uygulama dağıtımı ve yapılandırması Azure sanal makineler için sanal makine uzantıları nasıl otomatikleştirebilirsiniz ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="7782f-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="7782f-109">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="7782f-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="7782f-110">En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7782f-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="7782f-111">Tam veri şablonunun burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="7782f-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="7782f-112">Yapılandırma komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7782f-112">Configuration script</span></span>
<span data-ttu-id="7782f-113">Sanal makine uzantıları yapılandırma Otomasyon sağlamak için sanal makinelere karşı yürütme özelleştirilmiş programlardır.</span><span class="sxs-lookup"><span data-stu-id="7782f-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="7782f-114">Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="7782f-115">Bir özel betik uzantısı, bir sanal makine herhangi komut dosyasını çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="7782f-116">Müzik deposu örnekle Ubuntu sanal makineleri yapılandırmak ve müzik mağaza uygulamasını yüklemek için özel betik uzantısı kadar değil.</span><span class="sxs-lookup"><span data-stu-id="7782f-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="7782f-117">Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılan komut dosyasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="7782f-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="7782f-118">Bu komut dosyası müzik mağaza uygulamasını barındırmak için Ubuntu sanal makine yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7782f-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="7782f-119">Çalıştırdığınızda, betik tüm yazılım, müzik deposu uygulama kaynak denetiminden yükleyin ve veritabanını hazırlama yükler.</span><span class="sxs-lookup"><span data-stu-id="7782f-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="7782f-120">Bir .net barındırma hakkında daha fazla bilgi edinmek için çekirdek Linux uygulama için bkz: [Linux üretim ortamına yayınlama](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="7782f-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="7782f-121">Bu örnek tanıtım amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7782f-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="7782f-122">VM betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="7782f-122">VM Script Extension</span></span>
<span data-ttu-id="7782f-123">VM uzantıları bir sanal makine uzantısı kaynak Azure Resource Manager şablonunda ekleyerek derleme zamanında çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="7782f-124">Uzantı, Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON şablonuna ekleyerek eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="7782f-125">Betik uzantısı kaynak sanal makine kaynağı içinde iç içe yerleştirilmiş; Bu aşağıdaki örnekte görülebilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="7782f-126">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="7782f-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="7782f-127">Fark aşağıda JSON betiği Github'da depolanır.</span><span class="sxs-lookup"><span data-stu-id="7782f-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="7782f-128">Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="7782f-129">Ayrıca, Azure Resource Manager şablonları şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir olacağı şekilde oluşturulan için komut dosyası yürütme dizesi izin verin.</span><span class="sxs-lookup"><span data-stu-id="7782f-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="7782f-130">Bu durumda veri şablonları dağıtırken sağlanır ve bu değerler, daha sonra komut dosyasını yürütürken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7782f-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

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

<span data-ttu-id="7782f-131">Özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7782f-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="7782f-132">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="7782f-132">Next Step</span></span>
<hr>

[<span data-ttu-id="7782f-133">Daha fazla Azure Resource Manager şablonları keşfedin</span><span class="sxs-lookup"><span data-stu-id="7782f-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

