---
title: "Azure üzerinde aaaIntroduction tooFreeBSD | Microsoft Docs"
description: "Azure üzerinde FreeBSD sanal makineleri kullanma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Azure ile ilgili giriş tooFreeBSD
Bu konuda FreeBSD sanal makine Azure'da çalışan bir genel bakış sağlar.

## <a name="overview"></a>Genel Bakış
Microsoft Azure FreeBSD gelişmiş bilgisayar işletim sistemi toopower modern sunucular, masaüstü bilgisayarları ve katıştırılmış platformları kullanılır.

Microsoft Corporation'ın yapmadan FreeBSD görüntülerini kullanılabilir Azure'da hello ile [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) önceden yapılandırılmış. Şu anda hello aşağıdaki FreeBSD sürümlerini görüntüler olarak Microsoft tarafından sunulan:

- FreeBSD 10.3-sürüm
- FreeBSD 11.0-sürüm

Merhaba FreeBSD VM arasındaki iletişim için Hello Aracısı sorumludur ve hello Azure yapı sağlama gibi işlemler için (kullanıcı adı, parola veya SSH anahtarı, ana bilgisayar adı, vb.) ilk kullanım ve seçmeli VM uzantıları için etkinleştirme işlevselliği VM hello.

FreeBSD gelecek sürümlerinde, olduğu gibi hello stratejisi toostay geçerli olduğundan ve hello FreeBSD yayın mühendislik ekibi tarafından kısa süre içinde yayımladıktan sonra hello en son sürümlerde kullanılabilir yapın.

## <a name="deploying-a-freebsd-virtual-machine"></a>FreeBSD sanal makine dağıtma
FreeBSD sanal makine dağıtma hello Azure Marketi hello Azure Portalı'ndan bir görüntüden kullanarak bir işlemdir:

- [Hello Azure Marketi üzerinde FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [Hello Azure Marketi üzerinde FreeBSD 11.0](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Azure CLI 2.0 aracılığıyla bir FreeBSD VM üzerinde FreeBSD oluşturma
Tooinstall gereken ilk [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) FreeBSD makinede komutu aşağıdaki olsa.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Bash FreeBSD makinenize yüklü değilse, komutu hello yüklemeden önce aşağıdaki çalıştırın. 

```bash
sudo pkg install bash
```

Python FreeBSD makinenize yüklü değilse, komutları hello yüklemeden önce aşağıdaki çalıştırın. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Merhaba yükleme sırasında istendiğinde `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Yanıtı verirseniz `y` ve girin `/etc/rc.conf` olarak `a path tooan rc file tooupdate`, hello sorunu karşılayan `ERROR: [Errno 13] Permission denied`. tooresolve bu sorunu hello yazma sağ toocurrent kullanıcı hello dosya karşı vermelisiniz `etc/rc.conf`.

Şimdi Azure'da oturum ve FreeBSD VM oluşturun. Bir örnek toocreate FreeBSD 11.0 VM aşağıdadır. Merhaba parametresi de ekleyebilirsiniz `--public-ip-address-dns-name` yeni oluşturulan bir genel IP için genel benzersiz bir DNS adına sahip. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

Ardından dağıtım yukarıda hello çıktısını yazdırılmıştır hello IP adresi üzerinden tooyour FreeBSD VM olarak oturum açabilir. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>FreeBSD VM uzantıları
Desteklenen VM uzantıları FreeBSD aşağıda verilmiştir.

### <a name="vmaccess"></a>VMAccess
Merhaba [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) uzantısı kullanabilirsiniz:

* Merhaba özgün sudo kullanıcı Hello parolasını sıfırlayın.
* Yeni bir sudo kullanıcı belirtilen hello parolasıyla oluşturun.
* Verilen hello anahtarla Hello genel ana bilgisayar anahtarını ayarlayın.
* VM Hello ana makine anahtarı sağlanmazsa, sağlama sırasında sağlanan hello genel ana bilgisayar anahtarını sıfırlayın.
* Merhaba SSH bağlantı noktası (22) açın ve reset_ssh tootrue ayarlarsanız hello sshd_config geri yükleyin.
* Merhaba varolan kullanıcı kaldırın.
* Diskleri denetleyin.
* Eklenen bir disk onarın.

### <a name="customscript"></a>CustomScript
Merhaba [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) uzantısı kullanabilirsiniz:

* Sağlanırsa, özelleştirilmiş hello betikleri Azure Storage veya dış ortak depolama (örneğin, GitHub) indirin.
* Merhaba giriş noktası komut dosyasını çalıştırın.
* Satır içi komutları destekler.
* Windows stili yeni satır kabuk ve Python komut dosyaları otomatik olarak dönüştürür.
* Ürün reçetesi kabuk ve Python komut dosyaları otomatik olarak kaldırın.
* CommandToExecute gizli verileri koruyun.

> [!NOTE]
> FreeBSD VM yalnızca destekler CustomScript sürüm 1.x şimdi tarafından.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Kimlik doğrulaması: kullanıcı adları, parolalar ve SSH anahtarları
Hello Azure portal kullanarak bir FreeBSD sanal makine oluştururken, bir kullanıcı adı, parola veya SSH ortak anahtarı sağlamanız gerekir.
Azure FreeBSD sanal makine dağıtmak için kullanıcı adları system hesaplarının adlarını değil eşleşmesi gerekir (UID < 100) hello sanal makine ("Kök", örneğin) zaten mevcut.
Şu anda yalnızca hello RSA SSH anahtarı desteklenir. Çok satırlı SSH anahtarı ile başlamalıdır `---- BEGIN SSH2 PUBLIC KEY ----` ve sonunda `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Süper kullanıcı ayrıcalıkları alma
Azure üzerinde sanal makine örneği dağıtımı sırasında belirtilen hello kullanıcı hesabı ayrıcalıklı bir hesaptır. Merhaba sudo paketi olarak yüklendiği hello yayımlanan FreeBSD görüntü.
Bu kullanıcı hesabıyla oturum açtınız sonra hello komut sözdizimini kullanarak kök olarak komutları çalıştırabilirsiniz.

```
$ sudo <COMMAND>
```

Bir kök Kabuğu'nu kullanarak isteğe bağlı olarak elde edebilirsiniz `sudo -s`.

## <a name="known-issues"></a>Bilinen sorunlar
Merhaba [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) 2.2.2 sahip [bilinen bir sorun] sürüm (https://github.com/Azure/WALinuxAgent/pull/517) neden hello sağlama hatası Azure FreeBSD sanal makine için. Merhaba düzeltme tarafından yakalanan [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) sürüm 2.2.3 ve sonraki sürümlerinde. 

## <a name="next-steps"></a>Sonraki adımlar
* Çok Git[Azure Marketi](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD VM.
* Kendi FreeBSD tooAzure toobring istiyorsanız, çok başvuran[oluşturma ve karşıya yükleme FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).
