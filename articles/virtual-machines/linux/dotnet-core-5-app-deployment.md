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
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Linux VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı

Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra hello gerçek uygulama dağıtımı ele toobe gerekir. Uygulama dağıtımı burada tooinstalling hello gerçek uygulama ikililerini Azure kaynaklarını üzerine başvuruyor. Merhaba müzik deposu örnek, .net için çekirdek, NGINX ve yönetici her sanal makineye yükleyip toobe gerekir. Merhaba müzik deposu ikili dosyaları hello sanal makineye yüklenmesi yüklü toobe gerekir ve hello müzik deposu veritabanı önceden oluşturulmuş.

Bu belge, sanal makine uzantıları uygulama dağıtımı ve yapılandırması tooAzure sanal makineleri nasıl otomatikleştirebilirsiniz ayrıntıları. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın. Merhaba tam şablon burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Yapılandırma komut dosyası
Sanal makine, sanal makineleri tooprovide yapılandırma Otomasyon karşı yürütme özel programları uzantılarıdır. Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir. Bir özel betik uzantısı herhangi bir sanal makine komut dosyası kullanılan toorun olabilir. Merhaba müzik deposu örnekle bu toohello özel betik uzantısı tooconfigure hello Ubuntu sanal makineleri ve hello müzik deposu uygulamayı yükleyin. 

Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılır hello komut dosyasını inceleyin. Bu komut dosyası hello Ubuntu sanal makine toohost hello müzik deposu uygulama yapılandırır. Çalıştırdığınızda, tüm gerekli yazılım hello betik yükler kaynak denetiminden hello müzik deposu uygulamayı yükleyip hello veritabanı hazırlayın. 

bir .net barındırma hakkında daha fazla toolearn çekirdek uygulama Linux üzerinde bkz [Yayımla tooa Linux üretim ortamına](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Bu örnek tanıtım amacıyla kullanılır.
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

## <a name="vm-script-extension"></a>VM betik uzantısı
VM uzantıları bir sanal makine hello Azure Resource Manager şablonunda hello uzantısı kaynak ekleyerek derleme zamanında çalıştırılabilir. Merhaba uzantısı hello Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON hello şablonuna ekleyerek eklenebilir. Merhaba betik uzantısı kaynak sanal makine kaynağı hello içinde iç içe yerleştirilmiş; Bu örnekte aşağıdaki hello görülebilir.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Merhaba aşağıdaki betik hello JSON Github'da depolanan dikkat edin. Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir. Ayrıca, şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir, Azure Resource Manager şablonları hello komut dosyası yürütme dize tooconstructed izin verin. Bu durumda veri hello şablonları dağıtırken sağlanır ve bu değerler, daha sonra hello komut dosyası yürütülürken kullanılabilir.

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

Merhaba özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Sonraki adım
<hr>

[Daha fazla Azure Resource Manager şablonları keşfedin](https://github.com/Azure/azure-quickstart-templates)

