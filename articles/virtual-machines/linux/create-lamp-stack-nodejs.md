---
title: "Azure CLI 1.0 ile Linux sanal makinede AMPUL dağıtma | Microsoft Docs"
description: "Azure'da bir Linux VM üzerinde AMPUL yığını yüklemeyi öğrenin"
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
ms.openlocfilehash: feba2fb20d1831e92358ff5d1b4c9589d63d28dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a>AMPUL yığın Azure CLI 1.0 ile dağıtma
Bu makalede bir Apache web sunucusu, MySQL ve Azure üzerinde PHP (AMPUL yığını) dağıtma konusunda size yol göstermektedir. Bir Azure hesabınızın olması gerekir ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve [Azure CLI](../../cli-install-nodejs.md) diğer bir deyişle [Azure hesabınıza bağlı](../../xplat-cli-connect.md).

## <a name="cli-versions-to-complete-the-task"></a>Görevi tamamlamak için kullanılacak CLI sürümleri
Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:

- [Azure CLI 1.0] – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Var olan VM üzerinde AMPUL dağıtma

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Yeni VM gözden geçirme üzerinde AMPUL dağıtma
Oluşturarak başlayın bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md) yeni VM içerecek:

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

VM oluşturmak için bulunan zaten yazılmış bir Azure Resource Manager şablonunu kullanabilirsiniz [github'da burada](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Daha fazla bazı girişler isteyen bir yanıt görmeniz gerekir:

    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment to complete
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

Bir Linux VM üzerinde zaten yüklü AMPUL ile oluşturdunuz. İsterseniz, aşağı atlayarak yüklemeyi doğrulayabilirsiniz [doğrulayın AMPUL başarıyla yüklendi](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>AMPUL üzerinde var olan VM izlenecek dağıtma
Bir Linux VM oluşturma yardıma gereksinim duyarsanız, head [bir Linux VM oluşturma hakkında bilgi edinmek için burada](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ardından, Linux VM'de oturum için SSH gerekir. Bir SSH anahtarı oluşturma konusunda yardıma gereksinim duyarsanız, head [Linux/Mac üzerinde SSH anahtarı oluşturma hakkında bilgi edinmek için burada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Bir SSH anahtarı zaten varsa, şimdi SSH komut satırından Linux VM ile uygulamasına gidin ve `ssh exampleUsername@exampleDNS`.

Linux VM içinde çalışan, biz AMPUL yığın Debian tabanlı dağıtımlar üzerinde yüklenmesinde size yol. Tam komutları için diğer Linux distro'lar farklı olabilir.

#### <a name="installing-on-debianubuntu"></a>Debian/Ubuntu üzerinde yükleme
Yüklenen aşağıdaki paketler gerekir: `apache2`, `mysql-server`, `php5`, ve `php5-mysql`. Bu paketler, doğrudan bu paketleri kapmasını veya Tasksel kullanarak yükleyebilirsiniz. Her iki seçenek için yönergeler aşağıda listelenmiştir.
Yüklemeden önce indirin ve paketini listelerini güncelleştirmek gerekir.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Tek paketler
Get apt kullanma:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Tasksel kullanma
Alternatif olarak, Tasksel, birden çok ilişkili paketleri, sisteminize Eşgüdümlü "görev" olarak yükler Debian/Ubuntu aracı yükleyebilirsiniz.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Önceki seçeneklerinden birini çalıştırdıktan sonra bu paketleri ve diğer çeşitli bağımlılıkları yüklemeniz istenir. 'Y', sonra da devam etmek için ve MySQL için yönetici parolasını ayarlamak için başka bir yönergeleri izleyerek ' Enter' tuşuna basın. Bu, PHP, MySQL ile kullanmak için gerekli en düşük gerekli PHP uzantıları yükler. 

![][1]

Paketleri olarak kullanılabilir olan diğer PHP uzantılarının görmek için aşağıdaki komutu çalıştırın:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>İnfo.php belge oluşturma
Şimdi Apache, MySQL ve PHP sürümünü, komut satırı yazarak olduğunu denetlemek görüntüleyebiliyor olmalısınız `apache2 -v`, `mysql -v`, veya `php -v`.

Daha fazla test etmek isterseniz, bir tarayıcıda görüntülemek üzere hızlı bir PHP bilgileri sayfası oluşturabilirsiniz. Bir dosya ile Nano metin düzenleyicisi bu komutla oluşturun:

    user@ubuntu$ sudo nano /var/www/html/info.php

GNU Nano metin düzenleyici içinde aşağıdaki satırları ekleyin:

    <?php
    phpinfo();
    ?>

Ardından kaydedin ve Metin Düzenleyicisi'nden çıkın.

Tüm yeni yüklemeler etkili şekilde Apache bu komutla yeniden başlatın.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Başarılı bir şekilde AMPUL doğrulayın
Şimdi bir tarayıcı açıp http://youruniqueDNS/info.php için giderek tarafından oluşturulan PHP bilgileri sayfasını kontrol edebilirsiniz. Bu görüntüsüne benzer görünmelidir.

![][2]

Http://youruniqueDNS/ giderek Apache2 Ubuntu varsayılan sayfa görüntüleyerek Apache yüklemenizi denetleyebilirsiniz. Bu görüntü gibi bir şey görmeniz gerekir.

![][3]

Tebrikler, yalnızca Kurulum, Azure VM'deki bir AMPUL yığınına sahiptir.

## <a name="next-steps"></a>Sonraki adımlar
AMPUL yığında Ubuntu belgelerine göz atın:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png