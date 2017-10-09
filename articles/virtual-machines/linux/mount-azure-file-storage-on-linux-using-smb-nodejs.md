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
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="ea0eb-103">Linux sanal makineleri üzerinde bağlama Azure File storage ile Azure CLI 1.0 SMB kullanarak</span><span class="sxs-lookup"><span data-stu-id="ea0eb-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="ea0eb-104">Bu makalede nasıl toomount Azure File storage'ı kullanarak bir Linux VM hello sunucu ileti bloğu (SMB) protokolü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="ea0eb-105">Dosya depolama hello standart SMB protokolü aracılığıyla hello bulutta dosya paylaşımları sunar.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="ea0eb-106">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-106">hello requirements are:</span></span>

* <span data-ttu-id="ea0eb-107">Bir [Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="ea0eb-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="ea0eb-108">Güvenli Kabuk (SSH) ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="ea0eb-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="ea0eb-109">CLI sürümleri toouse</span><span class="sxs-lookup"><span data-stu-id="ea0eb-109">CLI versions toouse</span></span>
<span data-ttu-id="ea0eb-110">Merhaba görevi tamamlamak için komut satırı arabirimi (CLI) sürümleri aşağıdaki hello birini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="ea0eb-111">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="ea0eb-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ea0eb-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="ea0eb-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ea0eb-113">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="ea0eb-113">Quick commands</span></span>
<span data-ttu-id="ea0eb-114">tooaccomplish hello görev hızlı bir şekilde, bu bölümdeki hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="ea0eb-115">Daha ayrıntılı bilgi ve içerik için hello başlamak ["Ayrıntılı kılavuz"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ea0eb-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ea0eb-116">Prerequisites</span></span>
* <span data-ttu-id="ea0eb-117">Bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="ea0eb-117">A resource group</span></span>
* <span data-ttu-id="ea0eb-118">Bir Azure sanal ağı</span><span class="sxs-lookup"><span data-stu-id="ea0eb-118">An Azure virtual network</span></span>
* <span data-ttu-id="ea0eb-119">Ağ güvenlik grubuyla bir SSH gelen</span><span class="sxs-lookup"><span data-stu-id="ea0eb-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="ea0eb-120">Bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="ea0eb-120">A subnet</span></span>
* <span data-ttu-id="ea0eb-121">Bir Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="ea0eb-121">An Azure storage account</span></span>
* <span data-ttu-id="ea0eb-122">Azure depolama hesabı anahtarları</span><span class="sxs-lookup"><span data-stu-id="ea0eb-122">Azure storage account keys</span></span>
* <span data-ttu-id="ea0eb-123">Azure File storage paylaşımı</span><span class="sxs-lookup"><span data-stu-id="ea0eb-123">An Azure File storage share</span></span>
* <span data-ttu-id="ea0eb-124">Bir Linux VM</span><span class="sxs-lookup"><span data-stu-id="ea0eb-124">A Linux VM</span></span>

<span data-ttu-id="ea0eb-125">Tüm örnekleri kendi ayarlarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="ea0eb-126">Merhaba yerel bağlama için bir dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="ea0eb-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="ea0eb-127">Merhaba dosya depolama SMB paylaşımı toohello bağlama noktası bağlama</span><span class="sxs-lookup"><span data-stu-id="ea0eb-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="ea0eb-128">Merhaba bağlama yeniden başlatmanın ardından sürdürülmesi</span><span class="sxs-lookup"><span data-stu-id="ea0eb-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="ea0eb-129">Satır çok aşağıdaki hello eklemek`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ea0eb-130">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="ea0eb-130">Detailed walkthrough</span></span>

<span data-ttu-id="ea0eb-131">File storage hello standart SMB protokolünü kullanan dosya paylaşımları hello bulutta sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="ea0eb-132">Merhaba en son sürümü File storage ile SMB 3.0 destekleyen herhangi bir işletim sistemi bir dosya paylaşımı bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="ea0eb-133">Linux üzerinde bir SMB bağlama kullandığınızda, bir SLA tarafından desteklenen tooa güçlü, kalıcı arşivleme depolama konumu kolay yedeklemelerini alın.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="ea0eb-134">Dosyalar barındırılan bir VM'nin tooan SMB bağlama File storage'ı taşıma mükemmel şekilde toodebug günlükleri olur.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="ea0eb-135">Aynı SMB paylaşımı hello yerel olarak takılan çünkü tooyour Mac, Linux veya Windows iş istasyonu.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="ea0eb-136">SMB Linux akış için en iyi çözüm hello değil veya uygulama günlükleri gerçek zamanlı olarak hello SMB protokolü olmadığından toohandle gibi yoğun günlük görevlerini yerleşik.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="ea0eb-137">Ayrılmış, birleşik günlük katman aracı Fluentd gibi Linux ve çıkış günlüğü uygulama toplanması için SMB daha iyi bir seçim olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="ea0eb-138">Bu ayrıntılı kılavuzda hello Önkoşullar toofirst hello File storage paylaşımı oluşturun ve ardından bir Linux VM SMB bağlamanız oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="ea0eb-139">Koddan hello kullanarak bir Azure depolama hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="ea0eb-140">Merhaba depolama hesabı anahtarlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="ea0eb-141">Bir depolama hesabı oluşturduğunuzda, hizmet kesintisi Döndürülmüş hello hesabı anahtarları çiftler halinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="ea0eb-142">Merhaba çiftinin toohello ikinci anahtar geçiş yaptığınızda, yeni bir anahtar çifti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="ea0eb-143">Yeni depolama hesabı anahtarları, her zaman çiftler halinde her zaman en az bir kullanılmamış depolama için anahtar hazır tooswitch sahip olduktan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="ea0eb-144">tooshow hello depolama hesabı anahtarları, koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="ea0eb-145">Merhaba File storage paylaşımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-145">Create hello File storage share.</span></span>

    <span data-ttu-id="ea0eb-146">Merhaba File storage paylaşımı hello SMB paylaşımı içerir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="ea0eb-147">Merhaba kota her zaman gigabayt (GB) cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="ea0eb-148">toocreate File storage paylaşımı Merhaba, koddan hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="ea0eb-149">Merhaba bağlama noktası dizini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="ea0eb-150">Yerel bir dizine hello Linux dosya sistemi toomount hello SMB paylaşımı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="ea0eb-151">Herhangi bir şey yazıldığı veya hello yerel bağlama dizininden okuma File storage'ı barındırılan SMB paylaşımı toohello iletilir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="ea0eb-152">toocreate hello dizini, kod aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="ea0eb-153">SMB paylaşımı koddan hello kullanarak hello Bağla:</span><span class="sxs-lookup"><span data-stu-id="ea0eb-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="ea0eb-154">SMB yeniden başlatmalar bağlama hello kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="ea0eb-155">Merhaba Linux VM yeniden başlattığınızda hello takılı SMB paylaşımı kapatma sırasında kaldırılan değil.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="ea0eb-156">tooremount hello SMB paylaşımında önyükleme satır toohello Linux /etc/fstab eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="ea0eb-157">Linux hello fstab dosya toolist hello dosya sistemleri, toomount hello önyükleme işlemi sırasında gereken kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="ea0eb-158">Ekleme hello SMB paylaşımı bu hello File storage paylaşımı hello Linux VM için kalıcı bağlı dosya sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="ea0eb-159">Bulut init kullandığınızda hello dosya depolama SMB paylaşımı tooa ekleme yeni VM mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ea0eb-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="ea0eb-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea0eb-160">Next steps</span></span>

- [<span data-ttu-id="ea0eb-161">Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma</span><span class="sxs-lookup"><span data-stu-id="ea0eb-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="ea0eb-162">Disk tooa Linux VM ekleme</span><span class="sxs-lookup"><span data-stu-id="ea0eb-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="ea0eb-163">Hello Azure CLI kullanarak bir Linux VM disklerde şifrele</span><span class="sxs-lookup"><span data-stu-id="ea0eb-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
