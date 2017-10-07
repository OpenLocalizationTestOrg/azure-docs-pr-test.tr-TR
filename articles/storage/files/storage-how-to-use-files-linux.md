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
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="3d426-103">Azure File storage'ı Linux ile kullanma</span><span class="sxs-lookup"><span data-stu-id="3d426-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="3d426-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) Microsoft'un kolay toouse bulut dosya sistemidir.</span><span class="sxs-lookup"><span data-stu-id="3d426-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="3d426-105">Azure dosya paylaşımları hello kullanarak Linux dağıtımları içinde takılı [CIFS yardımcı programları paket](https://wiki.samba.org/index.php/LinuxCIFS_utils) hello gelen [Samba proje](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="3d426-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="3d426-106">Bu makale bir Azure dosya paylaşımı iki yolu toomount gösterir: isteğe bağlı hello ile `mount` komut ve üzerinde önyükleme bir girişe oluşturarak `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="3d426-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="3d426-107">Sipariş toomount hello dışında bir Azure dosya paylaşımı, bu, şirket içi gibi veya farklı bir bölgede Azure, hello OS barındırıldığı Azure bölgesi SMB 3.0 hello şifreleme işlevlerini desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d426-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="3d426-108">Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3d426-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="3d426-109">Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d426-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="3d426-110">Yayımlama Hello anda bu işlevselliği backported tooUbuntu 16.04 ve yukarıdaki olmuştur.</span><span class="sxs-lookup"><span data-stu-id="3d426-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="3d426-111">Linux ve hello CIFS yardımcı programları paketine sahip bir Azure dosya paylaşımına bağlanması için ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3d426-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="3d426-112">**Merhaba CIFS yardımcı programları paketi yüklü olan bir Linux dağıtım çekme**: Microsoft hello Azure görüntü Galerisi Linux dağıtımları aşağıdaki hello önerir:</span><span class="sxs-lookup"><span data-stu-id="3d426-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="3d426-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="3d426-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="3d426-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="3d426-114">RHEL 7+</span></span>
    * <span data-ttu-id="3d426-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="3d426-115">CentOS 7+</span></span>
    * <span data-ttu-id="3d426-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="3d426-116">Debian 8</span></span>
    * <span data-ttu-id="3d426-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="3d426-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="3d426-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="3d426-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="3d426-119"><a id="install-cifs-utils"></a>**Merhaba CIFS yardımcı programları paketinin yüklü olduğu**: hello CIFS yardımcı programları, tercih ettiğiniz hello Linux dağıtım noktasında hello Paket Yöneticisi kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3d426-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="3d426-120">Üzerinde **Ubuntu** ve **Debian tabanlı** dağıtımları, hello kullan `apt-get` Paket Yöneticisi:</span><span class="sxs-lookup"><span data-stu-id="3d426-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="3d426-121">Üzerinde **RHEL** ve **CentOS**, hello kullan `yum` Paket Yöneticisi:</span><span class="sxs-lookup"><span data-stu-id="3d426-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="3d426-122">Üzerinde **openSUSE**, hello kullan `zypper` Paket Yöneticisi:</span><span class="sxs-lookup"><span data-stu-id="3d426-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="3d426-123">Diğer dağıtımları hello uygun Paket Yöneticisi'ni kullanın veya [derleme kaynağından](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="3d426-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="3d426-124">**Merhaba dizin/dosya izinlerini hello takılı paylaşımının karar**: 0777, kullandığımız hello aşağıdaki örnekte, toogive okuma, yazma ve Yürütme izinleri tooall kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="3d426-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="3d426-125">Diğer değiştirebileceğiniz [chmod izinleri](https://en.wikipedia.org/wiki/Chmod) istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="3d426-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="3d426-126">**Depolama hesabı adı**: toomount bir Azure dosya paylaşımı, hello depolama hesabının adını hello.</span><span class="sxs-lookup"><span data-stu-id="3d426-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="3d426-127">**Depolama hesabı anahtarı**: toomount bir Azure dosya paylaşımı, birincil (veya ikincil) depolama anahtarı hello.</span><span class="sxs-lookup"><span data-stu-id="3d426-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="3d426-128">SAS anahtarları şu an bağlama için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="3d426-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="3d426-129">**445 bağlantı noktası açık olduğundan emin olun**: SMB 445 - TCP bağlantı noktası üzerinden iletişim kurar, güvenlik duvarının TCP engellemediğinden varsa toosee istemci makineden 445 bağlantı noktalarını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="3d426-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="3d426-130">Azure dosya paylaşımı isteğe bağlı ile Merhaba bağlama`mount`</span><span class="sxs-lookup"><span data-stu-id="3d426-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="3d426-131">**[Linux dağıtımınız için Hello CIFS yardımcı programları paketini Yükle](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="3d426-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="3d426-132">**Merhaba bağlama noktası için bir klasör oluşturun**: herhangi bir yere hello dosya sisteminde yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="3d426-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="3d426-133">**Kullanım hello bağlama komutu toomount hello Azure dosya paylaşımı**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, ve `<storage-account-key>` hello uygun bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="3d426-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="3d426-134">İşiniz bittiğinde hello Azure dosya paylaşımı kullanarak, kullanabilirsiniz `sudo umount ./mymountpoint` toounmount hello paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="3d426-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="3d426-135">Hello Azure dosya paylaşımının için kalıcı bağlama noktası oluştur`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="3d426-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="3d426-136">**[Linux dağıtımınız için Hello CIFS yardımcı programları paketini Yükle](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="3d426-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="3d426-137">**Merhaba bağlama noktası için bir klasör oluşturun**: herhangi bir yere hello dosya sisteminde yapılabilir, ancak toonote hello hello klasörünün mutlak bir yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d426-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="3d426-138">Aşağıdaki örnek hello kök altında bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d426-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="3d426-139">**Kullanım hello aşağıdaki komut satırı çok aşağıdaki tooappend hello`/etc/fstab`**: tooreplace unutmayın `<storage-account-name>`, `<share-name>`, ve `<storage-account-key>` hello uygun bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="3d426-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="3d426-140">Kullanabileceğiniz `sudo mount -a` düzenleme sonrasında toomount hello Azure dosya paylaşımı `/etc/fstab` yerine yeniden başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="3d426-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="3d426-141">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="3d426-141">Feedback</span></span>
<span data-ttu-id="3d426-142">Linux kullanıcıları, sizden toohear bekliyoruz!</span><span class="sxs-lookup"><span data-stu-id="3d426-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="3d426-143">değerlendirin ve File storage Linux'ı benimsemeyi gibi hello Azure File storage Linux Kullanıcıları grubu için bir forum sizin için tooshare geri bildirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d426-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="3d426-144">E-posta [Azure File storage Linux kullanıcıları](mailto:azurefileslinuxusers@microsoft.com) toojoin hello kullanıcıların Grup.</span><span class="sxs-lookup"><span data-stu-id="3d426-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d426-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d426-145">Next steps</span></span>
<span data-ttu-id="3d426-146">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="3d426-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="3d426-147">Dosya Hizmeti REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="3d426-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="3d426-148">Nasıl Microsoft Azure storage ile AzCopy toouse</span><span class="sxs-lookup"><span data-stu-id="3d426-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="3d426-149">Azure storage ile Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="3d426-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="3d426-150">SSS</span><span class="sxs-lookup"><span data-stu-id="3d426-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="3d426-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3d426-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
