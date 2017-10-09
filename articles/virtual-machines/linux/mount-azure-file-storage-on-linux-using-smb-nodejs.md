---
title: "Azure CLI 1.0 ile SMB kullanarak Azure File storage Linux sanal makineleri üzerinde aaaMount | Microsoft Docs"
description: "Nasıl toomount SMB kullanarak Azure File storage Linux sanal makineleri üzerinde"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Linux sanal makineleri üzerinde bağlama Azure File storage ile Azure CLI 1.0 SMB kullanarak

Bu makalede nasıl toomount Azure File storage'ı kullanarak bir Linux VM hello sunucu ileti bloğu (SMB) protokolü gösterilmektedir. Dosya depolama hello standart SMB protokolü aracılığıyla hello bulutta dosya paylaşımları sunar. Hello gereksinimleri şunlardır:

* Bir [Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
* [Güvenli Kabuk (SSH) ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>CLI sürümleri toouse
Merhaba görevi tamamlamak için komut satırı arabirimi (CLI) sürümleri aşağıdaki hello birini kullanarak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı komutlar
tooaccomplish hello görev hızlı bir şekilde, bu bölümdeki hello adımları izleyin. Daha ayrıntılı bilgi ve içerik için hello başlamak ["Ayrıntılı kılavuz"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) bölümü.

### <a name="prerequisites"></a>Ön koşullar
* Bir kaynak grubu
* Bir Azure sanal ağı
* Ağ güvenlik grubuyla bir SSH gelen
* Bir alt ağ
* Bir Azure depolama hesabı
* Azure depolama hesabı anahtarları
* Azure File storage paylaşımı
* Bir Linux VM

Tüm örnekleri kendi ayarlarınızla değiştirin.

### <a name="create-a-directory-for-hello-local-mount"></a>Merhaba yerel bağlama için bir dizin oluşturun

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Merhaba dosya depolama SMB paylaşımı toohello bağlama noktası bağlama

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Merhaba bağlama yeniden başlatmanın ardından sürdürülmesi
Satır çok aşağıdaki hello eklemek`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

File storage hello standart SMB protokolünü kullanan dosya paylaşımları hello bulutta sağlar. Merhaba en son sürümü File storage ile SMB 3.0 destekleyen herhangi bir işletim sistemi bir dosya paylaşımı bağlayabilir. Linux üzerinde bir SMB bağlama kullandığınızda, bir SLA tarafından desteklenen tooa güçlü, kalıcı arşivleme depolama konumu kolay yedeklemelerini alın.

Dosyalar barındırılan bir VM'nin tooan SMB bağlama File storage'ı taşıma mükemmel şekilde toodebug günlükleri olur. Aynı SMB paylaşımı hello yerel olarak takılan çünkü tooyour Mac, Linux veya Windows iş istasyonu. SMB Linux akış için en iyi çözüm hello değil veya uygulama günlükleri gerçek zamanlı olarak hello SMB protokolü olmadığından toohandle gibi yoğun günlük görevlerini yerleşik. Ayrılmış, birleşik günlük katman aracı Fluentd gibi Linux ve çıkış günlüğü uygulama toplanması için SMB daha iyi bir seçim olacaktır.

Bu ayrıntılı kılavuzda hello Önkoşullar toofirst hello File storage paylaşımı oluşturun ve ardından bir Linux VM SMB bağlamanız oluşturuyoruz.

1. Koddan hello kullanarak bir Azure depolama hesabı oluşturun:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Merhaba depolama hesabı anahtarlarını gösterir.

    Bir depolama hesabı oluşturduğunuzda, hizmet kesintisi Döndürülmüş hello hesabı anahtarları çiftler halinde oluşturulur. Merhaba çiftinin toohello ikinci anahtar geçiş yaptığınızda, yeni bir anahtar çifti oluşturun. Yeni depolama hesabı anahtarları, her zaman çiftler halinde her zaman en az bir kullanılmamış depolama için anahtar hazır tooswitch sahip olduktan oluşturulur. tooshow hello depolama hesabı anahtarları, koddan hello kullan:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Merhaba File storage paylaşımı oluşturun.

    Merhaba File storage paylaşımı hello SMB paylaşımı içerir. Merhaba kota her zaman gigabayt (GB) cinsinden ifade edilir. toocreate File storage paylaşımı Merhaba, koddan hello kullanın:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Merhaba bağlama noktası dizini oluşturun.

    Yerel bir dizine hello Linux dosya sistemi toomount hello SMB paylaşımı oluşturmanız gerekir. Herhangi bir şey yazıldığı veya hello yerel bağlama dizininden okuma File storage'ı barındırılan SMB paylaşımı toohello iletilir. toocreate hello dizini, kod aşağıdaki kullanım hello:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. SMB paylaşımı koddan hello kullanarak hello Bağla:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. SMB yeniden başlatmalar bağlama hello kalıcı olmasını sağlar.

    Merhaba Linux VM yeniden başlattığınızda hello takılı SMB paylaşımı kapatma sırasında kaldırılan değil. tooremount hello SMB paylaşımında önyükleme satır toohello Linux /etc/fstab eklemeniz gerekir. Linux hello fstab dosya toolist hello dosya sistemleri, toomount hello önyükleme işlemi sırasında gereken kullanır. Ekleme hello SMB paylaşımı bu hello File storage paylaşımı hello Linux VM için kalıcı bağlı dosya sistemi sağlar. Bulut init kullandığınızda hello dosya depolama SMB paylaşımı tooa ekleme yeni VM mümkündür.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Sonraki adımlar

- [Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Disk tooa Linux VM ekleme](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Hello Azure CLI kullanarak bir Linux VM disklerde şifrele](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
