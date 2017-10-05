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
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Linux VM'ler için Azure Resource Manager şablonları ile uygulama dağıtımı

Tüm Azure infrastructural gereksinimleri belirledikten ve bir dağıtım şablonuna çevrilen sonra gerçek uygulama dağıtımı ele alınması gerekir. Uygulama dağıtımı burada gerçek uygulama ikili dosyaların Azure kaynaklarını üzerine yüklenmesi için başvuruyor. Müzik deposu örnek, .net için çekirdek, NGINX ve Supervisor gereken yüklenmeli ve her sanal makinede yapılandırılmalıdır. Müzik deposu ikili dosyasının sanal makineye yüklenmesi gerekmez ve müzik deposu veritabanı önceden oluşturulmuş.

Bu belge, uygulama dağıtımı ve yapılandırması Azure sanal makineler için sanal makine uzantıları nasıl otomatikleştirebilirsiniz ayrıntıları. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın. Tam veri şablonunun burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Yapılandırma komut dosyası
Sanal makine uzantıları yapılandırma Otomasyon sağlamak için sanal makinelere karşı yürütme özelleştirilmiş programlardır. Uzantıları, virüsten koruma, günlük yapılandırmasını ve Docker yapılandırması gibi birçok belirli amaçlar için kullanılabilir. Bir özel betik uzantısı, bir sanal makine herhangi komut dosyasını çalıştırmak için kullanılabilir. Müzik deposu örnekle Ubuntu sanal makineleri yapılandırmak ve müzik mağaza uygulamasını yüklemek için özel betik uzantısı kadar değil. 

Sanal makine uzantıları bir Azure Resource Manager şablonu nasıl bildirilir ayrıntılı önce çalıştırılan komut dosyasını inceleyin. Bu komut dosyası müzik mağaza uygulamasını barındırmak için Ubuntu sanal makine yapılandırır. Çalıştırdığınızda, betik tüm yazılım, müzik deposu uygulama kaynak denetiminden yükleyin ve veritabanını hazırlama yükler. 

Bir .net barındırma hakkında daha fazla bilgi edinmek için çekirdek Linux uygulama için bkz: [Linux üretim ortamına yayınlama](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

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
VM uzantıları bir sanal makine uzantısı kaynak Azure Resource Manager şablonunda ekleyerek derleme zamanında çalıştırılabilir. Uzantı, Visual Studio kaynak Ekleme Sihirbazı'nı ya da geçerli JSON şablonuna ekleyerek eklenebilir. Betik uzantısı kaynak sanal makine kaynağı içinde iç içe yerleştirilmiş; Bu aşağıdaki örnekte görülebilir.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [VM betik uzantısı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Fark aşağıda JSON betiği Github'da depolanır. Bu komut dosyası ayrıca Azure Blob Depolama alanında depolanabilir. Ayrıca, Azure Resource Manager şablonları şablonu parametrelerinin değerlerini komut dosyası yürütme için parametre olarak kullanılabilir olacağı şekilde oluşturulan için komut dosyası yürütme dizesi izin verin. Bu durumda veri şablonları dağıtırken sağlanır ve bu değerler, daha sonra komut dosyasını yürütürken kullanılabilir.

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

Özel betik uzantısı kullanma hakkında daha fazla bilgi için bkz: [özel betik uzantılarının Resource Manager şablonları ile](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Sonraki adım
<hr>

[Daha fazla Azure Resource Manager şablonları keşfedin](https://github.com/Azure/azure-quickstart-templates)

