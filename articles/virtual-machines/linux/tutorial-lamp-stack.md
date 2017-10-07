---
title: azure'da bir Linux sanal makinede AMPUL aaaDeploy | Microsoft Docs
description: "Öğretici - yükleme hello AMPUL azure'da bir Linux VM yığında"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Azure VM temelinde bir AMPUL web sunucusunu yükleme
Bu makalede toodeploy Apache nasıl web sunucusu, MySQL ve azure'da bir Ubuntu VM üzerinde PHP (Merhaba AMPUL yığını) aracılığıyla anlatılmaktadır. Merhaba NGINX web sunucusu tercih ederseniz, hello bkz [LEMP yığın](tutorial-lemp-stack.md) Öğreticisi. toosee hello AMPUL sunucu eyleminde, isteğe bağlı olarak yükleyebilir ve bir WordPress sitesi yapılandırın. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Bir Ubuntu VM (Merhaba 'L' hello AMPUL yığınında) oluşturma
> * Web trafiği için 80 numaralı bağlantı noktasını açın
> * Apache, MySQL ve PHP yükleme
> * Yükleme ve yapılandırmasını doğrulayın
> * WordPress hello AMPUL sunucusuna yükleyin


Merhaba AMPUL yığını, bir üretim ortamı için öneriler dahil olmak üzere daha fazla bilgi için bkz: Merhaba [Ubuntu belgelerine](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Apache, MySQL ve PHP yükleme

Aşağıdaki komut tooupdate Ubuntu paket kaynaklar hello çalıştırın ve Apache, MySQL ve PHP yükleyin. Merhaba komutu hello sonunda Hello şapka (^) unutmayın.


```bash
sudo apt update && sudo apt install lamp-server^
```



İstendiğinde tooinstall hello paketler ve diğer bağımlılıklar var. İstendiğinde, MySQL, ardından [Enter] toocontinue için bir kök parola ayarlayın. Merhaba kalan istemleri izleyin. Bu işlem hello minimum gerekli PHP uzantıları gerekli toouse PHP MySQL ile yükler. 

![MySQL kök parola sayfası][1]

## <a name="verify-installation-and-configuration"></a>Yükleme ve yapılandırmasını doğrulayın


### <a name="apache"></a>Apache

Onay hello sürümüyle Apache komutu aşağıdaki hello:
```bash
apache2 -v
```

Apache tooyour VM yüklü ve bağlantı noktası 80'i açın, hello web sunucusu artık erişilebilir hello Internet. tooview hello Apache2 Ubuntu sayfasında, varsayılan bir web tarayıcısı açın ve hello VM hello ortak IP adresini girin. Merhaba tooSSH toohello VM kullanılan ortak IP adresini kullan:

![Apache varsayılan sayfa][3]


### <a name="mysql"></a>MySQL

Komutu aşağıdaki hello ile MySQL Hello sürümünü denetleme (Not hello sermaye `V` parametresi):

```bash
msql -V
```

Komut dosyası toohelp güvenli hello MySQL yüklenmesinden hello çalıştıran öneririz:

```bash
mysql_secure_installation
```

MySQL kök parolanızı girin ve ortamınız için hello güvenlik ayarlarını yapılandırın.

Toocreate bir MySQL veritabanı istiyorsanız, kullanıcı ekleme ya da yapılandırma ayarlarını, oturum açma tooMySQL değiştirin:

```bash
mysql -u root -p
```

İşiniz bittiğinde, yazarak hello mysql isteminden çıkın `\q`.

### <a name="php"></a>PHP

Onay hello sürümüyle PHP komut aşağıdaki hello:

```bash
php -v
```

Daha fazla tootest istiyorsanız, hızlı bir PHP bilgi sayfası tooview bir tarayıcıda oluşturun. komutu aşağıdaki hello hello PHP bilgileri sayfası oluşturur:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Şimdi, oluşturduğunuz hello PHP bilgileri sayfasını kontrol edebilirsiniz. Bir tarayıcı açın ve çok`http://yourPublicIPAddress/info.php`. VM Hello genel IP adresini değiştirin. Benzer toothis görüntü görünmelidir.

![PHP bilgileri sayfası][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure AMPUL Server'da dağıtıldı. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bir Ubuntu VM oluşturma
> * Web trafiği için 80 numaralı bağlantı noktasını açın
> * Apache, MySQL ve PHP yükleme
> * Yükleme ve yapılandırmasını doğrulayın
> * WordPress hello AMPUL sunucusuna yükleyin

Toohello sonraki öğretici toolearn nasıl ilerlemek SSL sertifikaları web sunucularıyla toosecure.

> [!div class="nextstepaction"]
> [SSL ile güvenli web sunucusu](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png