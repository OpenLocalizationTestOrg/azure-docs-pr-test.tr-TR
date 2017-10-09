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
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>AMPUL yığın hello Azure CLI 1.0 ile dağıtma
Bu makalede toodeploy Apache nasıl web sunucusu, MySQL ve Azure üzerinde PHP (Merhaba AMPUL yığını) aracılığıyla anlatılmaktadır. Bir Azure hesabınızın olması gerekir ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve hello [Azure CLI](../../cli-install-nodejs.md) diğer bir deyişle [bağlı tooyour Azure hesabı](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0] – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Var olan VM üzerinde AMPUL dağıtma

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Yeni VM gözden geçirme üzerinde AMPUL dağıtma
Oluşturarak başlayın bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md) içerecek yeni VM hello:

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

toocreate VM kendisini Merhaba, bulunan zaten yazılmış bir Azure Resource Manager şablonunu kullanabilirsiniz [github'da burada](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Daha fazla bazı girişler isteyen bir yanıt görmeniz gerekir:

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

Bir Linux VM üzerinde zaten yüklü AMPUL ile oluşturdunuz. İsterseniz, aşağı çok atlayarak hello yükleme doğrulayabilirsiniz[doğrulayın AMPUL başarıyla yüklendi](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>AMPUL üzerinde var olan VM izlenecek dağıtma
Bir Linux VM oluşturma yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate bir Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ardından, Linux VM hello tooSSH gerekir. Bir SSH anahtarı oluşturma konusunda yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate Linux/Mac üzerinde bir SSH anahtarı](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Bir SSH anahtarı zaten varsa, şimdi SSH komut satırından Linux VM ile uygulamasına gidin ve `ssh exampleUsername@exampleDNS`.

Linux VM içinde çalışan, biz hello AMPUL yığın Debian tabanlı dağıtımlar üzerinde yüklenmesinde size yol. Merhaba tam komutları için diğer Linux distro'lar farklı olabilir.

#### <a name="installing-on-debianubuntu"></a>Debian/Ubuntu üzerinde yükleme
Yüklü olan paketleri aşağıdaki hello gerekir: `apache2`, `mysql-server`, `php5`, ve `php5-mysql`. Bu paketler, doğrudan bu paketleri kapmasını veya Tasksel kullanarak yükleyebilirsiniz. Her iki seçenek için yönergeler aşağıda listelenmiştir.
Yüklemeden önce toodownload gerekir ve güncelleştirme paketini listeler.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Tek paketler
Get apt kullanma:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Tasksel kullanma
Alternatif olarak, Tasksel, birden çok ilişkili paketleri, sisteminize Eşgüdümlü "görev" olarak yükler Debian/Ubuntu aracı yükleyebilirsiniz.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Merhaba önceki seçeneklerinden birini çalıştırdıktan sonra şunları yapacaksınız istendiğinde tooinstall bu paketleri ve diğer çeşitli bağımlılıkları olabilir. 'Y', 'Enter' toocontinue basın ve herhangi diğer istemleri tooset yönetici parolası için MySQL izleyin. Bu MySQL ile Merhaba minimum gerekli PHP uzantıları gerekli toouse PHP yükler. 

![][1]

Komut toosee aşağıdaki hello paketleri olarak kullanılabilir olan diğer PHP uzantılarının çalıştırın:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>İnfo.php belge oluşturma
Şimdi, Apache, MySQL ve PHP sürümünü hello komut satırı yazarak elinizde mümkün toocheck olmalısınız `apache2 -v`, `mysql -v`, veya `php -v`.

Tootest gibi daha fazla, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturabilirsiniz. Bir dosya ile Nano metin düzenleyicisi bu komutla oluşturun:

    user@ubuntu$ sudo nano /var/www/html/info.php

Merhaba GNU Nano metin düzenleyicisi içinde satırlardan hello ekleyin:

    <?php
    phpinfo();
    ?>

Ardından kaydedin ve hello Metin Düzenleyicisi'nden çıkın.

Tüm yeni yüklemeler etkili şekilde Apache bu komutla yeniden başlatın.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Başarılı bir şekilde AMPUL doğrulayın
Şimdi bir tarayıcı açıp toohttp://youruniqueDNS/info.php gidip oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz. Benzer toothis görüntü görünmelidir.

![][2]

Merhaba Apache2 Ubuntu varsayılan sayfa tooyou http://youruniqueDNS/ giderek görüntüleyerek Apache yüklemenizi denetleyebilirsiniz. Bu görüntü gibi bir şey görmeniz gerekir.

![][3]

Tebrikler, yalnızca Kurulum, Azure VM'deki bir AMPUL yığınına sahiptir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hello AMPUL yığında Ubuntu belgelerine bakın:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png