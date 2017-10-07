---
title: "Azure File storage'ı SMB kullanarak Linux VM'ler aaaMount | Microsoft Docs"
description: "Nasıl toomount Azure File storage'ı Linux ile SMB kullanarak VM'ler hello Azure CLI 2.0"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>SMB kullanarak Linux VM'ler üzerinde bağlama Azure dosya depolama

Bu makalede nasıl tooutilize hello Azure dosya depolama hizmeti bir SMB kullanarak bir Linux VM üzerinde bağlama hello Azure CLI 2.0 ile gösterilmektedir. Azure File storage hello bulutta hello standart SMB protokolünü kullanan dosya paylaşımları sağlar. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hello gereksinimleri şunlardır:

- [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
- [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Hızlı Komutlar

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
toodo, bu nedenle, aşağıdaki satırı toohello hello ekleyin `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

File storage hello standart SMB protokolünü kullanan dosya paylaşımları hello bulutta sağlar. Merhaba en son sürümü File storage ile SMB 3.0 destekleyen herhangi bir işletim sistemi bir dosya paylaşımı bağlayabilir. Linux üzerinde bir SMB bağlama kullandığınızda, bir SLA tarafından desteklenen tooa güçlü, kalıcı arşivleme depolama konumu kolay yedeklemelerini alın.

Dosyalar barındırılan bir VM'nin tooan SMB bağlama File storage'ı taşıma mükemmel şekilde toodebug günlükleri olur. Aynı SMB paylaşımı hello yerel olarak takılan çünkü tooyour Mac, Linux veya Windows iş istasyonu. SMB Linux akış için en iyi çözüm hello değil veya uygulama günlükleri gerçek zamanlı olarak hello SMB protokolü olmadığından toohandle gibi yoğun günlük görevlerini yerleşik. Ayrılmış, birleşik günlük katman aracı Fluentd gibi Linux ve çıkış günlüğü uygulama toplanması için SMB daha iyi bir seçim olacaktır.

Bu ayrıntılı kılavuzda hello Önkoşullar toofirst hello File storage paylaşımı oluşturun ve ardından bir Linux VM SMB bağlamanız oluşturuyoruz.

1. Bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create) toohold hello dosya paylaşımı.

    bir kaynak grubu adında toocreate `myResourceGroup` hello "Batı ABD" konum, aşağıdaki örneğine hello kullanın:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Bir Azure depolama hesabıyla oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create) toostore hello gerçek dosyaları.

    bir depolama hesabı toocreate hello Standard_LRS depolama SKU, aşağıdaki örneğine kullanım hello kullanarak mystorageaccount adlı:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Merhaba depolama hesabı anahtarlarını gösterir.

    Bir depolama hesabı oluşturduğunuzda, hizmet kesintisi Döndürülmüş hello hesabı anahtarları çiftler halinde oluşturulur. Merhaba çiftinin toohello ikinci anahtar geçiş yaptığınızda, yeni bir anahtar çifti oluşturun. Yeni depolama hesabı anahtarları, her zaman çiftler halinde her zaman en az bir kullanılmamış depolama hesabı anahtar hazır tooswitch için sahip olduktan oluşturulur.

    Merhaba ile Merhaba depolama hesabı anahtarlarını görüntülemek [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list). Depolama hesabı anahtarlarını adlı hello için hello `mystorageaccount` aşağıdaki örneğine hello listelenir:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract tek bir anahtar kullanmak hello `--query` bayrağı. Merhaba aşağıdaki örnek ayıklar hello ilk anahtarı (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Merhaba File storage paylaşımı oluşturun.

    Merhaba File storage paylaşımı içeren SMB paylaşımıyla hello [az depolama paylaşımı oluşturmak](/cli/azure/storage/share#create). Merhaba kota her zaman gigabayt (GB) cinsinden ifade edilir. Merhaba anahtarlarından birini hello önceki geçirmek `az storage account keys list` komutu. Aşağıdaki örneğine hello kullanarak 10 GB kota mystorageshare adlı bir paylaşım oluşturun:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Bir bağlama noktası dizin oluşturun.

    Yerel bir dizine hello Linux dosya sistemi toomount hello SMB paylaşımı oluşturun. Herhangi bir şey yazıldığı veya hello yerel bağlama dizininden okuma File storage'ı barındırılan SMB paylaşımı toohello iletilir. toocreate/mnt/mymountdirectory, aşağıdaki örneğine kullanım hello yerel dizininde:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Merhaba SMB paylaşımı toohello yerel dizin bağlayın.

    Aşağıdaki gibi kendi depolama hesap kullanıcı adı ve depolama hesabı anahtarı hello bağlama kimlik bilgilerini sağlayın:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. SMB yeniden başlatmalar bağlama hello kalıcı olmasını sağlar.

    Merhaba Linux VM yeniden başlattığınızda hello takılı SMB paylaşımı kapatma sırasında kaldırılan değil. SMB paylaşımı önyüklemede tooremount hello satır toohello Linux /etc/fstab ekleyin. Linux hello fstab dosya toolist hello dosya sistemleri, toomount hello önyükleme işlemi sırasında gereken kullanır. Ekleme hello SMB paylaşımı bu hello File storage paylaşımı hello Linux VM için kalıcı bağlı dosya sistemi sağlar. Bulut init kullandığınızda hello dosya depolama SMB paylaşımı tooa ekleme yeni VM mümkündür.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Sonraki adımlar

- [Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Disk tooa Linux VM ekleme](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Hello Azure CLI kullanarak bir Linux VM disklerde şifrele](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
