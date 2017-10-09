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
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Linux için Hello Azure CustomScript uzantısını kullanarak bir AMPUL uygulaması dağıtma
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Merhaba Resource Manager modelini kullanarak bir AMPUL yığını dağıtma hakkında daha fazla bilgi için bkz: [burada](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello Microsoft Azure CustomScript uzantısını Linux için bir yol toocustomize hello VM (örneğin, Python ve Bash) tarafından desteklenen tüm komut dosyası dilinde yazılmış rastgele kod çalıştırarak sanal makineleri (VM'ler) sağlar. Bu, uygulama dağıtım toomultiple makineler çok esnek bir şekilde tooautomate sağlar.

Merhaba CustomScript uzantısını dağıtabilirsiniz kullanarak hello Azure portalı, Windows PowerShell veya hello Azure komut satırı arabirimi (Azure CLI).

Kullanacağız. Bu makalede hello Azure CLI toodeploy basit bir AMPUL uygulama tooan Ubuntu VM hello Klasik dağıtım modeli kullanılarak oluşturulmuş.

## <a name="prerequisites"></a>Ön koşullar
Bu örnekte, ilk iki Azure Ubuntu 14.04 veya sonraki sürümünü çalıştıran VM oluşturun. Merhaba VM'ler denir *betik vm* ve *ampul vm*. Merhaba Vm'leri oluştururken benzersiz adlar kullanın. Kullanılan toorun hello CLI komutları biridir ve kullanılan toodeploy hello AMPUL uygulama biridir.

Bir Azure Storage hesabı ve anahtarı tooaccess etmeniz BT (alabilirsiniz bu hello Azure portal ').

Linux sanal makineleri Azure üzerinde oluşturma yardıma gereksinim duyarsanız çok başvuran[çalıştıran bir sanal makine Linux oluşturma](createportal.md).

Ubuntu Hello yükleme komutları varsayar ancak herhangi bir Linux distro desteklenen hello yükleme uyarlayabilirsiniz.

Merhaba betik vm VM çalışma bağlantı tooAzure ile Azure CLI, yüklü toohave gerekir. Bu Yardım çok başvurmak için[hello Azure komut satırı arabirimi yükleyip](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Bir komut dosyasını karşıya yükle
Bir uzak VM tooinstall hello AMPUL yığında hello CustomScript uzantısını toorun bir komut dosyası kullanır ve bir PHP sayfası oluşturmak. Sipariş tooaccess hello komut yerden biz bunu bir Azure blob'u olarak yükleyeceksiniz.

### <a name="script-overview"></a>Komut dosyası genel bakış
Merhaba komut dosyası örneği (MySQL sessiz bir yükleme ayarlama dahil) AMPUL yığın tooUbuntu yükler, basit bir PHP dosya yazar ve Apache başlatır.

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

### <a name="upload-script"></a>Komut dosyasını karşıya yükle
Merhaba komut dosyasını bir metin dosyası olarak örneğin kaydetmek *install_lamp.sh*ve tooAzure depolama yükleyin. Kolayca Azure CLI ile bunu yapabilirsiniz. Merhaba aşağıdaki örnekte "betikleri" adlı hello dosya tooa depolama kapsayıcı yükler. Merhaba kapsayıcı yoksa toocreate gerekir, ilk.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Ayrıca nasıl toodownload hello Azure Storage betikten açıklayan bir JSON dosyası oluşturun. Bu olarak Kaydet *public_config.json* ("mystorage" Merhaba depolama hesabınızın adını ile değiştirerek):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Merhaba uzantısı dağıtma
Artık hello sonraki komut toodeploy hello Linux CustomScript uzantısını toohello uzaktan kullanarak Azure CLI hello VM kullanma.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

Merhaba önceki komutu yükler ve çalıştırır hello *install_lamp.sh* VM adlı hello komut *ampul vm*.

Merhaba uygulamasını içeren bir web sunucusu olduğundan, tooopen bir HTTP dinleme bağlantı noktası hello unutmayın hello İleri komutu ile uzaktan VM.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>İzleme ve sorun giderme
Merhaba günlük dosyasına bakarak hello özel komut dosyası çalıştırır uzak VM ne kadar iyi hello kontrol edebilirsiniz. SSH çok*ampul vm* ve kuyruk hello günlük dosyası hello sonraki komutu.

    cd /var/log/azure/customscript
    tail -f handler.log

Merhaba CustomScript uzantısını çalıştırdıktan sonra bilgi için oluşturulan toohello PHP sayfası göz atabilirsiniz. Merhaba PHP sayfasında hello Örneğin bu makalede *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Ek kaynaklar
Kullanabileceğiniz hello aynı temel adımlar toodeploy daha karmaşık uygulamalar. Bu örnekte, bir ortak BLOB Azure storage'da hello yükleme betiği kaydedildi. Daha güvenli bir seçenek ile güvenli bir BLOB toostore hello yükleme betiği olacak bir [güvenli erişim imzası](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Ek kaynaklar için Azure CLI, Linux ve hello CustomScript uzantısını sonraki listelenir.

[CustomScript uzantısını kullanarak Linux VM özelleştirme görevlerini otomatik hale getirme](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Azure Linux Uzantıları (GitHub)](https://github.com/Azure/azure-linux-extensions)