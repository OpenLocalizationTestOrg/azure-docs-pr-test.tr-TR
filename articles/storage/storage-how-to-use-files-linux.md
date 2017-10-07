---
title: Azure File storage ile Linux aaaUse | Microsoft Docs
description: "Nasıl toomount bir Azure dosya paylaşımı Linux'ta SMB üzerinden öğrenin."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: ed6ba9b98f121d6629d858320ca3760384303ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Azure File storage'ı Linux ile kullanma
[Azure File storage](storage-dotnet-how-to-use-files.md) Microsoft'un kolay toouse bulut dosya sistemidir. Azure dosya paylaşımları hello kullanarak Linux dağıtımları içinde takılı [CIFS yardımcı programları paket](https://wiki.samba.org/index.php/LinuxCIFS_utils) hello gelen [Samba proje](https://www.samba.org/). Bu makale bir Azure dosya paylaşımı iki yolu toomount gösterir: isteğe bağlı hello ile `mount` komut ve üzerinde önyükleme bir girişe oluşturarak `/etc/fstab`.

> [!NOTE]  
> Sipariş toomount hello dışında bir Azure dosya paylaşımı, bu, şirket içi gibi veya farklı bir bölgede Azure, hello OS barındırıldığı Azure bölgesi SMB 3.0 hello şifreleme işlevlerini desteklemesi gerekir. Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur. Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar. Yayımlama Hello anda bu işlevselliği backported tooUbuntu 16.04 ve yukarıdaki olmuştur.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Linux ve hello CIFS yardımcı programları paketine sahip bir Azure dosya paylaşımına bağlanması için ön koşullar
* **Merhaba CIFS yardımcı programları paketi yüklü olan bir Linux dağıtım çekme**: Microsoft hello Azure görüntü Galerisi Linux dağıtımları aşağıdaki hello önerir:

    * Ubuntu Server 14.04 +
    * RHEL 7 +
    * CentOS 7 +
    * Debian 8
    * openSUSE 13.2 +
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Merhaba CIFS yardımcı programları paketinin yüklü olduğu**: hello CIFS yardımcı programları, tercih ettiğiniz hello Linux dağıtım noktasında hello Paket Yöneticisi kullanılarak yüklenebilir. 

    Üzerinde **Ubuntu** ve **Debian tabanlı** dağıtımları, hello kullan `apt-get` Paket Yöneticisi:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    Üzerinde **RHEL** ve **CentOS**, hello kullan `yum` Paket Yöneticisi:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    Üzerinde **openSUSE**, hello kullan `zypper` Paket Yöneticisi:

    ```
    sudo zypper install samba*
    ```

    Diğer dağıtımları hello uygun Paket Yöneticisi'ni kullanın veya [derleme kaynağından](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Merhaba dizin/dosya izinlerini hello takılı paylaşımının karar**: 0777, kullandığımız hello aşağıdaki örnekte, toogive okuma, yazma ve Yürütme izinleri tooall kullanıcılar. Diğer değiştirebileceğiniz [chmod izinleri](https://en.wikipedia.org/wiki/Chmod) istenen şekilde. 

* **Depolama hesabı adı**: toomount bir Azure dosya paylaşımı, hello depolama hesabının adını hello.

* **Depolama hesabı anahtarı**: toomount bir Azure dosya paylaşımı, birincil (veya ikincil) depolama anahtarı hello. SAS anahtarları şu an bağlama için desteklenmemektedir.

* **445 bağlantı noktası açık olduğundan emin olun**: SMB 445 - TCP bağlantı noktası üzerinden iletişim kurar, güvenlik duvarının TCP engellemediğinden varsa toosee istemci makineden 445 bağlantı noktalarını kontrol edin.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Azure dosya paylaşımı isteğe bağlı ile Merhaba bağlama`mount`
1. **[Linux dağıtımınız için Hello CIFS yardımcı programları paketini Yükle](#install-cifs-utils)**.

2. **Merhaba bağlama noktası için bir klasör oluşturun**: herhangi bir yere hello dosya sisteminde yapılabilir.

    ```
    mkdir mymountpoint
    ```

3. **Kullanım hello bağlama komutu toomount hello Azure dosya paylaşımı**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, ve `<storage-account-key>` hello uygun bilgilerle.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> İşiniz bittiğinde hello Azure dosya paylaşımı kullanarak, kullanabilirsiniz `sudo umount ./mymountpoint` toounmount hello paylaşımı.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Hello Azure dosya paylaşımının için kalıcı bağlama noktası oluştur`/etc/fstab`
1. **[Linux dağıtımınız için Hello CIFS yardımcı programları paketini Yükle](#install-cifs-utils)**.

2. **Merhaba bağlama noktası için bir klasör oluşturun**: herhangi bir yere hello dosya sisteminde yapılabilir, ancak toonote hello hello klasörünün mutlak bir yol gerekir. Aşağıdaki örnek hello kök altında bir klasör oluşturur.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Kullanım hello aşağıdaki komut satırı çok aşağıdaki tooappend hello`/etc/fstab`**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, ve `<storage-account-key>` hello uygun bilgilerle.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> Kullanabileceğiniz `sudo mount -a` düzenleme sonrasında toomount hello Azure dosya paylaşımı `/etc/fstab` yerine yeniden başlatılıyor.

## <a name="feedback"></a>Geri Bildirim
Linux kullanıcıları, sizden toohear bekliyoruz!

değerlendirin ve File storage Linux'ı benimsemeyi gibi hello Azure File storage Linux Kullanıcıları grubu için bir forum sizin için tooshare geri bildirim sağlar. E-posta [Azure File storage Linux kullanıcıları](mailto:azurefileslinuxusers@microsoft.com) toojoin hello kullanıcıların Grup.

## <a name="next-steps"></a>Sonraki adımlar
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.
* [Dosya Hizmeti REST API başvurusu](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Azure storage ile Azure PowerShell'i kullanma](storage-powershell-guide-full.md)
* [Nasıl Microsoft Azure storage ile AzCopy toouse](storage-use-azcopy.md)
* [Azure storage ile Hello Azure CLI kullanma](storage-azure-cli.md#create-and-manage-file-shares)
* [SSS](storage-files-faq.md)
* [Sorun giderme](storage-troubleshoot-file-connection-problems.md)
