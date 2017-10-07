---
title: "Linux VM parola aaaReset ve SSH anahtarı CLI hello | Microsoft Docs"
description: "Nasıl toouse hello VMAccess uzantısını hello Azure komut satırı arabirimi (CLI) tooreset bir Linux VM parola veya SSH anahtarı hello SSH yapılandırmasını düzeltmek ve disk tutarlılık denetimi"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Nasıl tooreset bir Linux VM parola veya SSH anahtarı hello SSH yapılandırmasını düzeltmek ve hello VMAccess uzantısını kullanarak disk tutarlılık denetimi
Unutulan parolayı, yanlış bir güvenli Kabuk (SSH) anahtarının veya hello SSH yapılandırması ile ilgili bir sorun nedeniyle Azure tooa Linux sanal makineye bağlanamıyorsanız, hello VMAccessForLinux uzantısını hello Azure CLI tooreset hello parola veya SSH anahtarı ile birlikte kullanmak için düzeltme SSH yapılandırması hello ve disk tutarlılık denetimi. 

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Hello Azure CLI ile kullandığınız hello **azure vm uzantısı kümesi** komut satırı arabirimi (Bash, Terminal, komut istemi) tooaccess komutlarının komutu. Çalıştırma **azure Yardım vm uzantısı kümesi** ayrıntılı uzantısını kullanım için.

Hello Azure CLI ile yapabileceğiniz hello görevler:

* [Merhaba parola sıfırlama](#pwresetcli)
* [Merhaba SSH anahtarını Sıfırla](#sshkeyresetcli)
* [Merhaba parola ve hello SSH anahtarını Sıfırla](#resetbothcli)
* [Yeni bir sudo kullanıcı hesabı oluşturma](#createnewsudocli)
* [Merhaba SSH yapılandırmasını sıfırlayın](#sshconfigresetcli)
* [Kullanıcı silme](#deletecli)
* [Merhaba VMAccess uzantısını Hello durumunu görüntüleyin](#statuscli)
* [Eklenen diskler tutarlılık denetimi](#checkdisk)
* [Linux VM eklenen disklerde onarın](#repairdisk)

## <a name="prerequisites"></a>Ön koşullar
Toodo hello aşağıdaki gerekir:

* Çok gerekir[hello Azure CLI yükleme](../../../cli-install-nodejs.md) ve [tooyour abonelik bağlanmak](../../../xplat-cli-connect.md) toouse Azure hesabınızla ilişkili kaynakları.
* Merhaba Klasik dağıtım modeli için doğru moda Hello hello komut isteminde hello aşağıdakileri yazarak ayarlayın:
    ``` 
        azure config mode asm
    ```
* Tooreset herhangi birini isterseniz yeni bir parola veya SSH anahtarlarını gerekir. Tooreset hello SSH yapılandırması istiyorsanız bu gerekmez.

## <a name="pwresetcli"></a>Merhaba parola sıfırlama
1. Bu satırlar ile PrivateConf.json adlı yerel bilgisayarınızdaki bir dosya oluşturun. Değiştir **KullanıcıAdım** ve  **myP@ssW0rd**  kendi kullanıcı adı ve parola ile ve kendi sona erme tarihini ayarlayın.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Merhaba SSH anahtarını Sıfırla
1. Bu içerikle PrivateConf.json adlı bir dosya oluşturun. Hello yerine **KullanıcıAdım** ve **mySSHKey** kendi bilgilerinizi değerlerle.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Merhaba parola ve hello SSH anahtarını Sıfırla
1. Bu içerikle PrivateConf.json adlı bir dosya oluşturun. Hello yerine **KullanıcıAdım**, **mySSHKey** ve  **myP@ssW0rd**  kendi bilgilerinizi değerlerle.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Yeni bir sudo kullanıcı hesabı oluşturma

Kullanıcı adınızı unutursanız, Vmaccess'in toocreate hello sudo yetkisine sahip yeni bir tane kullanabilirsiniz. Bu durumda, hello olan bir kullanıcı adı ve parola değiştirilmeyecek.

komut dosyası kullan hello parola erişimine sahip yeni bir sudo kullanıcı toocreate [hello parola sıfırlama](#pwresetcli) ve hello yeni bir kullanıcı adı belirtin.

SSH anahtar erişimi, komut dosyası kullan hello sahip yeni bir sudo kullanıcı toocreate [sıfırlama hello SSH anahtarı](#sshkeyresetcli) ve hello yeni bir kullanıcı adı belirtin.

Aynı zamanda [hello parola ve hello SSH anahtarını Sıfırla](#resetbothcli) toocreate hem parola hem de SSH anahtar erişimi olan yeni bir kullanıcı.

## <a name="sshconfigresetcli"></a>Merhaba SSH yapılandırmasını sıfırlayın
Merhaba SSH yapılandırması istenmeyen bir durumda ise, erişim toohello VM de kaybedebilirsiniz. Merhaba VMAccess uzantısını tooreset hello yapılandırma tooits varsayılan durumu kullanabilirsiniz. toodo, tooset hello "reset_ssh" anahtar çok "True" yeterlidir. Merhaba uzantısı hello SSH sunucuyu yeniden başlatın, VM'yi hello SSH bağlantı noktası açın ve hello SSH yapılandırma toodefault değerlerini sıfırlayın. Merhaba kullanıcı hesabı (adı, parola veya SSH anahtarları) değiştirilmez.

> [!NOTE]
> sıfırlama hello SSH yapılandırma dosyası /etc/ssh/sshd_config bulunur.
> 
> 

1. Bu içerikle PrivateConf.json adlı bir dosya oluşturun.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Kullanıcı silme
Toodelete doğrudan oturum açmayı toohello VM olmadan bir kullanıcı hesabı istiyorsanız, bu komut dosyasını kullanabilirsiniz.

1. Merhaba kullanıcı adı tooremove değiştirerek bu içerikle PrivateConf.json adlı bir dosya oluşturun **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Merhaba VMAccess uzantısını Hello durumunu görüntüleyin
Merhaba VMAccess uzantısını toodisplay hello durumu bu komutu çalıştırın.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Eklenen diskler tutarlılık denetimi
toorun fsck Linux sanal makinedeki tüm disklerde toodo hello aşağıdaki gerekir:

1. Bu içerikle PublicConf.json adlı bir dosya oluşturun. Onay Disk olup olmadığını toocheck diskleri tooyour sanal makine veya bağlı için bir Boole değeri alır. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Sanal makine için Hello adını değiştirerek bu komut tooexecute çalıştırmak **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Onarım diskleri
bağlama yapılandırma hataları, değil bağlanması veya toorepair diskler Linux sanal makinenizde hello VMAccess uzantısını tooreset hello bağlama yapılandırması kullanın. Merhaba adını değiştirerek diskiniz için **myDisk**.

1. Bu içerikle PublicConf.json adlı bir dosya oluşturun. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Sanal makine için Hello adını değiştirerek bu komut tooexecute çalıştırmak **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Sonraki adımlar
* Toouse Azure PowerShell cmdlet'lerini veya Azure Resource Manager şablonları tooreset hello parola veya SSH anahtarı istiyorsanız, hello SSH yapılandırmasını düzeltmek ve disk tutarlılık denetimi, hello bkz [VMAccess uzantısını belgelerine github'da](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* Merhaba de kullanabilirsiniz [Azure portal](https://portal.azure.com) tooreset hello parola veya SSH anahtarı bir Linux VM dağıtılan hello Klasik dağıtım modelinde. Bir Linux VM hello Resource Manager dağıtım modelinde dağıtılan hello portal toothis şu anda kullanamazsınız.
* Bkz: [sanal makine uzantıları ve özellikleri hakkında](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure sanal makineler için VM uzantıları kullanma hakkında daha fazla bilgi için.

