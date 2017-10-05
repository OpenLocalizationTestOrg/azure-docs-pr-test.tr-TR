---
title: "Azure File storage'ı Linux ile kullanma | Microsoft Docs"
description: "Bir Azure dosya paylaşımı üzerinden SMB Linux'ta bağlama öğrenin."
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
ms.openlocfilehash: d8987082c559a374b8d19fd69e20cf5e81cb25ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="8da73-103">Azure File storage'ı Linux ile kullanma</span><span class="sxs-lookup"><span data-stu-id="8da73-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="8da73-104">[Azure Dosya depolama](../storage-dotnet-how-to-use-files.md), Windows’un kolay kullanılan bulut dosya sistemidir.</span><span class="sxs-lookup"><span data-stu-id="8da73-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="8da73-105">Azure dosya paylaşımları kullanarak Linux dağıtımları içinde takılı [CIFS yardımcı programları paket](https://wiki.samba.org/index.php/LinuxCIFS_utils) gelen [Samba proje](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="8da73-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="8da73-106">Bu makale bir Azure dosya paylaşımı bağlamak için iki yol gösterir: isteğe bağlı ile `mount` komut ve üzerinde önyükleme bir girişe oluşturarak `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="8da73-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="8da73-107">Azure dışında bir Azure dosya paylaşımı bağlamak için bu, şirket içi gibi veya farklı bir bölgede Azure, işletim sistemi barındırıldığı bölgeyi SMB 3.0 şifreleme işlevlerini desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da73-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="8da73-108">Linux için SMB 3.0 şifreleme özelliği 4.11 Çekirdeği'nde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8da73-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="8da73-109">Bu özellik Azure dosya paylaşımının şirket içi veya farklı bir Azure bölgesindeki bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="8da73-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="8da73-110">Yayımlama zaman bu işlevselliği 16.04 ve yukarıdaki backported Ubuntu için bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="8da73-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="8da73-111">Bir Azure dosya bağlanması için ön koşullar paylaşımı Linux ve yardımcı programları CIFS paketi</span><span class="sxs-lookup"><span data-stu-id="8da73-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="8da73-112">**Yüklü CIFS yardımcı programları paketi olabilir Linux dağıtım çekme**: Microsoft Azure görüntü Galerisi içinde aşağıdaki Linux dağıtımları önerir:</span><span class="sxs-lookup"><span data-stu-id="8da73-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="8da73-113">Ubuntu Server 14.04 +</span><span class="sxs-lookup"><span data-stu-id="8da73-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="8da73-114">RHEL 7 +</span><span class="sxs-lookup"><span data-stu-id="8da73-114">RHEL 7+</span></span>
    * <span data-ttu-id="8da73-115">CentOS 7 +</span><span class="sxs-lookup"><span data-stu-id="8da73-115">CentOS 7+</span></span>
    * <span data-ttu-id="8da73-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="8da73-116">Debian 8</span></span>
    * <span data-ttu-id="8da73-117">openSUSE 13.2 +</span><span class="sxs-lookup"><span data-stu-id="8da73-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="8da73-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="8da73-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="8da73-119"><a id="install-cifs-utils"></a>**CIFS yardımcı programları paketinin yüklü olduğu**: yardımcı programları CIFS tercih ettiğiniz Linux dağıtım noktasında Paket Yöneticisi kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8da73-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="8da73-120">Üzerinde **Ubuntu** ve **Debian tabanlı** dağıtımları kullanın `apt-get` Paket Yöneticisi:</span><span class="sxs-lookup"><span data-stu-id="8da73-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="8da73-121">Üzerinde **RHEL** ve **CentOS**, kullanın `yum` Paket Yöneticisi:</span><span class="sxs-lookup"><span data-stu-id="8da73-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="8da73-122">Üzerinde **openSUSE**, kullanın `zypper` Paket Yöneticisi:</span><span class="sxs-lookup"><span data-stu-id="8da73-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="8da73-123">Diğer dağıtımlar üzerinde uygun Paket Yöneticisi'ni kullanın veya [derleme kaynağından](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="8da73-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="8da73-124">**Bağlanılan paylaşımı dizin/dosya izinlerini karar**: 0777 kullanırız aşağıdaki örneklerde, okuma, yazma ve Yürütme izinleri tüm kullanıcılara.</span><span class="sxs-lookup"><span data-stu-id="8da73-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="8da73-125">Diğer değiştirebileceğiniz [chmod izinleri](https://en.wikipedia.org/wiki/Chmod) istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="8da73-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="8da73-126">**Depolama Hesabı Adı**: Azure Dosya paylaşımını bağlayabilmeniz için depolama hesabınızın adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da73-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="8da73-127">**Depolama Hesabı Anahtarı**: Azure Dosya paylaşımını bağlayabilmeniz için birincil (veya ikincil) depolama anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da73-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="8da73-128">SAS anahtarları şu an bağlama için desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="8da73-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="8da73-129">**445 bağlantı noktası açık olduğundan emin olun**: SMB 445 - TCP bağlantı noktası üzerinden iletişim kurar, güvenlik duvarının TCP engellemediğinden varsa görmek için istemci makineden 445 bağlantı noktalarını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="8da73-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="8da73-130">Azure dosya paylaşımı isteğe bağlı ile bağlama`mount`</span><span class="sxs-lookup"><span data-stu-id="8da73-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="8da73-131">**[Linux dağıtımınızı CIFS yardımcı programları paketini Yükle](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8da73-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8da73-132">**Bağlama noktası için bir klasör oluşturun**: Bu dosya sisteminde herhangi bir yere yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="8da73-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="8da73-133">**Azure dosya paylaşımını bağlama için bağlama komutunu kullanın**: değiştirmek unutmayın `<storage-account-name>`, `<share-name>`, ve `<storage-account-key>` uygun bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="8da73-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="8da73-134">İşiniz bittiğinde Azure dosya paylaşımı kullanarak `sudo umount ./mymountpoint` paylaşım çıkaramadı.</span><span class="sxs-lookup"><span data-stu-id="8da73-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="8da73-135">Azure dosya paylaşımının için kalıcı bağlama noktası oluştur`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="8da73-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="8da73-136">**[Linux dağıtımınızı CIFS yardımcı programları paketini Yükle](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8da73-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8da73-137">**Bağlama noktası için bir klasör oluşturun**: Bu dosya sisteminde herhangi bir yere yapılabilir, ancak klasör mutlak yolu not gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da73-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="8da73-138">Aşağıdaki örnek, kök altında bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8da73-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="8da73-139">**Aşağıdaki satırı eklemek için aşağıdaki komutu kullanın `/etc/fstab`** : değiştirmek unutmayın `<storage-account-name>`, `<share-name>`, ve `<storage-account-key>` uygun bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="8da73-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="8da73-140">Kullanabileceğiniz `sudo mount -a` düzenledikten sonra Azure dosya paylaşımını bağlama için `/etc/fstab` yerine yeniden başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="8da73-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="8da73-141">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="8da73-141">Feedback</span></span>
<span data-ttu-id="8da73-142">Linux kullanıcıları, sizden duymak istiyoruz!</span><span class="sxs-lookup"><span data-stu-id="8da73-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="8da73-143">Azure File storage Linux Kullanıcıları grubu için bir forum değerlendirin ve File storage Linux'ı benimsemeyi olarak geri bildirim paylaşmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8da73-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="8da73-144">E-posta [Azure File storage Linux kullanıcıları](mailto:azurefileslinuxusers@microsoft.com) kullanıcıların Gruba katılmak için.</span><span class="sxs-lookup"><span data-stu-id="8da73-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8da73-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8da73-145">Next steps</span></span>
<span data-ttu-id="8da73-146">Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.</span><span class="sxs-lookup"><span data-stu-id="8da73-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="8da73-147">Dosya Hizmeti REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="8da73-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="8da73-148">Microsoft Azure storage ile AzCopy kullanma</span><span class="sxs-lookup"><span data-stu-id="8da73-148">How to use AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="8da73-149">Azure storage ile Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="8da73-149">Using the Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="8da73-150">SSS</span><span class="sxs-lookup"><span data-stu-id="8da73-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="8da73-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="8da73-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
