---
title: azure'da bir Linux sanal makinede AMPUL aaaDeploy | Microsoft Docs
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Azure AMPUL yığında dağıtma
Bu makalede toodeploy Apache nasıl web sunucusu, MySQL ve Azure üzerinde PHP (Merhaba AMPUL yığını) aracılığıyla anlatılmaktadır. Bir Azure hesabınızın olması gerekir ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Hızlı komut Özet

1. Kaydetme ve hello düzenleme [azuredeploy.parameters.json dosya](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour tercih yerel makinenizde.
2. Bir kaynak grubu iki komutları toocreate aşağıdaki hello çalıştırın ve şablonunuzu dağıtma:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Var olan VM üzerinde AMPUL dağıtma
Merhaba aşağıdaki güncelleştirmeleri paketleri komutları sonra Apache, MySQL ve PHP yükler:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Yeni VM gözden geçirme üzerinde AMPUL dağıtma

1. Sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create) toocontain yeni VM hello:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate VM kendisini Merhaba, bulunan zaten yazılmış bir Azure Resource Manager şablonunu kullanabilirsiniz [github'da burada](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Merhaba Kaydet [azuredeploy.parameters.json dosya](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour yerel makine.
3. Merhaba Düzenle **azuredeploy.parameters.json** dosya tooyour girişleri tercih edilir.
4. Merhaba şablonla dağıtma [az grup dağıtımı Oluştur] hello başvuran indirilen json dosyası:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

Bir Linux VM üzerinde zaten yüklü AMPUL ile oluşturdunuz. İsterseniz, aşağı çok atlayarak hello yükleme doğrulayabilirsiniz[doğrulayın AMPUL başarıyla yüklendi](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>AMPUL üzerinde var olan VM izlenecek dağıtma
Bir Linux VM oluşturma yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate bir Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Ardından, Linux VM hello tooSSH gerekir. Bir SSH anahtarı oluşturma konusunda yardıma gereksinim duyarsanız, head [burada toolearn nasıl toocreate Linux/Mac üzerinde bir SSH anahtarı](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Bir SSH anahtarı zaten varsa, şimdi SSH komut satırından Linux VM ile uygulamasına gidin ve `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Linux VM içinde çalışan, biz hello AMPUL yığın Debian tabanlı dağıtımlar üzerinde yüklenmesinde size yol. Merhaba tam komutları için diğer Linux distro'lar farklı olabilir.

#### <a name="installing-on-debianubuntu"></a>Debian/Ubuntu üzerinde yükleme
Yüklü olan paketleri aşağıdaki hello gerekir: `apache2`, `mysql-server`, `php5`, ve `php5-mysql`. Bu paketler, doğrudan bu paketleri kapmasını veya Tasksel kullanarak yükleyebilirsiniz.
Yüklemeden önce toodownload gerekir ve güncelleştirme paketini listeler.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Tek paketler
Get apt kullanma:

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Tasksel kullanma
Alternatif olarak, Tasksel, birden çok ilişkili paketleri, sisteminize Eşgüdümlü "görev" olarak yükler Debian/Ubuntu aracı yükleyebilirsiniz.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Merhaba önceki seçeneklerinden birini çalıştırdıktan sonra şunları yapacaksınız istendiğinde tooinstall bu paketleri ve diğer çeşitli bağımlılıkları olabilir. tooset MySQL, bir yönetici parolası 'y', 'Enter' toocontinue basın ve diğer yönergeleri izleyin. Bu işlem hello minimum gerekli PHP uzantıları gerekli toouse PHP MySQL ile yükler. 

![][1]

Komut toosee aşağıdaki hello paketleri olarak kullanılabilir olan diğer PHP uzantılarının çalıştırın:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>İnfo.php belge oluşturma
Şimdi, Apache, MySQL ve PHP sürümünü hello komut satırı yazarak elinizde mümkün toocheck olmalısınız `apache2 -v`, `mysql -v`, veya `php -v`.

Tootest gibi daha fazla, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturabilirsiniz. Bir dosya ile Nano metin düzenleyicisi bu komutla oluşturun:

```bash
sudo nano /var/www/html/info.php
```

Merhaba GNU Nano metin düzenleyicisi içinde satırlardan hello ekleyin:

```php
<?php
phpinfo();
?>
```

Ardından kaydedin ve hello Metin Düzenleyicisi'nden çıkın.

Tüm yeni yüklemeler etkili şekilde Apache bu komutla yeniden başlatın.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Başarılı bir şekilde AMPUL doğrulayın
Şimdi bir tarayıcı açıp toohttp://youruniqueDNS/info.php gidip oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz. Benzer toothis görüntü görünmelidir.

![][2]

Merhaba Apache2 Ubuntu varsayılan sayfa tooyou http://youruniqueDNS/ giderek görüntüleyerek Apache yüklemenizi denetleyebilirsiniz. Merhaba, benzer toohello aşağıdaki örneğine çıktı:

![][3]

Tebrikler, yalnızca Kurulum, Azure VM'deki bir AMPUL yığınına sahiptir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hello AMPUL yığında Ubuntu belgelerine bakın:

* [https://help.ubuntu.com/Community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
