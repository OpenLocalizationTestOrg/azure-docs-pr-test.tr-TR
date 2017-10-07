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
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="f9120-103">SMB kullanarak Linux VM'ler üzerinde bağlama Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="f9120-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="f9120-104">Bu makalede nasıl tooutilize hello Azure dosya depolama hizmeti bir SMB kullanarak bir Linux VM üzerinde bağlama hello Azure CLI 2.0 ile gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f9120-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="f9120-105">Azure File storage hello bulutta hello standart SMB protokolünü kullanan dosya paylaşımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9120-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="f9120-106">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9120-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f9120-107">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f9120-107">hello requirements are:</span></span>

- [<span data-ttu-id="f9120-108">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="f9120-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="f9120-109">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="f9120-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="f9120-110">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="f9120-110">Quick Commands</span></span>

* <span data-ttu-id="f9120-111">Bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="f9120-111">A resource group</span></span>
* <span data-ttu-id="f9120-112">Bir Azure sanal ağı</span><span class="sxs-lookup"><span data-stu-id="f9120-112">An Azure virtual network</span></span>
* <span data-ttu-id="f9120-113">Ağ güvenlik grubuyla bir SSH gelen</span><span class="sxs-lookup"><span data-stu-id="f9120-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="f9120-114">Bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="f9120-114">A subnet</span></span>
* <span data-ttu-id="f9120-115">Bir Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="f9120-115">An Azure storage account</span></span>
* <span data-ttu-id="f9120-116">Azure depolama hesabı anahtarları</span><span class="sxs-lookup"><span data-stu-id="f9120-116">Azure storage account keys</span></span>
* <span data-ttu-id="f9120-117">Azure File storage paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f9120-117">An Azure File storage share</span></span>
* <span data-ttu-id="f9120-118">Bir Linux VM</span><span class="sxs-lookup"><span data-stu-id="f9120-118">A Linux VM</span></span>

<span data-ttu-id="f9120-119">Tüm örnekleri kendi ayarlarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f9120-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="f9120-120">Merhaba yerel bağlama için bir dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="f9120-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="f9120-121">Merhaba dosya depolama SMB paylaşımı toohello bağlama noktası bağlama</span><span class="sxs-lookup"><span data-stu-id="f9120-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="f9120-122">Merhaba bağlama yeniden başlatmanın ardından sürdürülmesi</span><span class="sxs-lookup"><span data-stu-id="f9120-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="f9120-123">toodo, bu nedenle, aşağıdaki satırı toohello hello ekleyin `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="f9120-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f9120-124">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="f9120-124">Detailed walkthrough</span></span>

<span data-ttu-id="f9120-125">File storage hello standart SMB protokolünü kullanan dosya paylaşımları hello bulutta sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9120-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="f9120-126">Merhaba en son sürümü File storage ile SMB 3.0 destekleyen herhangi bir işletim sistemi bir dosya paylaşımı bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="f9120-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="f9120-127">Linux üzerinde bir SMB bağlama kullandığınızda, bir SLA tarafından desteklenen tooa güçlü, kalıcı arşivleme depolama konumu kolay yedeklemelerini alın.</span><span class="sxs-lookup"><span data-stu-id="f9120-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="f9120-128">Dosyalar barındırılan bir VM'nin tooan SMB bağlama File storage'ı taşıma mükemmel şekilde toodebug günlükleri olur.</span><span class="sxs-lookup"><span data-stu-id="f9120-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="f9120-129">Aynı SMB paylaşımı hello yerel olarak takılan çünkü tooyour Mac, Linux veya Windows iş istasyonu.</span><span class="sxs-lookup"><span data-stu-id="f9120-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="f9120-130">SMB Linux akış için en iyi çözüm hello değil veya uygulama günlükleri gerçek zamanlı olarak hello SMB protokolü olmadığından toohandle gibi yoğun günlük görevlerini yerleşik.</span><span class="sxs-lookup"><span data-stu-id="f9120-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="f9120-131">Ayrılmış, birleşik günlük katman aracı Fluentd gibi Linux ve çıkış günlüğü uygulama toplanması için SMB daha iyi bir seçim olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f9120-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="f9120-132">Bu ayrıntılı kılavuzda hello Önkoşullar toofirst hello File storage paylaşımı oluşturun ve ardından bir Linux VM SMB bağlamanız oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f9120-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="f9120-133">Bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create) toohold hello dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="f9120-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="f9120-134">bir kaynak grubu adında toocreate `myResourceGroup` hello "Batı ABD" konum, aşağıdaki örneğine hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="f9120-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="f9120-135">Bir Azure depolama hesabıyla oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create) toostore hello gerçek dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f9120-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="f9120-136">bir depolama hesabı toocreate hello Standard_LRS depolama SKU, aşağıdaki örneğine kullanım hello kullanarak mystorageaccount adlı:</span><span class="sxs-lookup"><span data-stu-id="f9120-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="f9120-137">Merhaba depolama hesabı anahtarlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9120-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="f9120-138">Bir depolama hesabı oluşturduğunuzda, hizmet kesintisi Döndürülmüş hello hesabı anahtarları çiftler halinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f9120-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="f9120-139">Merhaba çiftinin toohello ikinci anahtar geçiş yaptığınızda, yeni bir anahtar çifti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9120-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="f9120-140">Yeni depolama hesabı anahtarları, her zaman çiftler halinde her zaman en az bir kullanılmamış depolama hesabı anahtar hazır tooswitch için sahip olduktan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f9120-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="f9120-141">Merhaba ile Merhaba depolama hesabı anahtarlarını görüntülemek [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="f9120-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="f9120-142">Depolama hesabı anahtarlarını adlı hello için hello `mystorageaccount` aşağıdaki örneğine hello listelenir:</span><span class="sxs-lookup"><span data-stu-id="f9120-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="f9120-143">tooextract tek bir anahtar kullanmak hello `--query` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="f9120-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="f9120-144">Merhaba aşağıdaki örnek ayıklar hello ilk anahtarı (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="f9120-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="f9120-145">Merhaba File storage paylaşımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9120-145">Create hello File storage share.</span></span>

    <span data-ttu-id="f9120-146">Merhaba File storage paylaşımı içeren SMB paylaşımıyla hello [az depolama paylaşımı oluşturmak](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="f9120-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="f9120-147">Merhaba kota her zaman gigabayt (GB) cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="f9120-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="f9120-148">Merhaba anahtarlarından birini hello önceki geçirmek `az storage account keys list` komutu.</span><span class="sxs-lookup"><span data-stu-id="f9120-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="f9120-149">Aşağıdaki örneğine hello kullanarak 10 GB kota mystorageshare adlı bir paylaşım oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f9120-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="f9120-150">Bir bağlama noktası dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9120-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="f9120-151">Yerel bir dizine hello Linux dosya sistemi toomount hello SMB paylaşımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9120-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="f9120-152">Herhangi bir şey yazıldığı veya hello yerel bağlama dizininden okuma File storage'ı barındırılan SMB paylaşımı toohello iletilir.</span><span class="sxs-lookup"><span data-stu-id="f9120-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="f9120-153">toocreate/mnt/mymountdirectory, aşağıdaki örneğine kullanım hello yerel dizininde:</span><span class="sxs-lookup"><span data-stu-id="f9120-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="f9120-154">Merhaba SMB paylaşımı toohello yerel dizin bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f9120-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="f9120-155">Aşağıdaki gibi kendi depolama hesap kullanıcı adı ve depolama hesabı anahtarı hello bağlama kimlik bilgilerini sağlayın:</span><span class="sxs-lookup"><span data-stu-id="f9120-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="f9120-156">SMB yeniden başlatmalar bağlama hello kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9120-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="f9120-157">Merhaba Linux VM yeniden başlattığınızda hello takılı SMB paylaşımı kapatma sırasında kaldırılan değil.</span><span class="sxs-lookup"><span data-stu-id="f9120-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="f9120-158">SMB paylaşımı önyüklemede tooremount hello satır toohello Linux /etc/fstab ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9120-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="f9120-159">Linux hello fstab dosya toolist hello dosya sistemleri, toomount hello önyükleme işlemi sırasında gereken kullanır.</span><span class="sxs-lookup"><span data-stu-id="f9120-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="f9120-160">Ekleme hello SMB paylaşımı bu hello File storage paylaşımı hello Linux VM için kalıcı bağlı dosya sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9120-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="f9120-161">Bulut init kullandığınızda hello dosya depolama SMB paylaşımı tooa ekleme yeni VM mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f9120-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="f9120-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9120-162">Next steps</span></span>

- [<span data-ttu-id="f9120-163">Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma</span><span class="sxs-lookup"><span data-stu-id="f9120-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="f9120-164">Disk tooa Linux VM ekleme</span><span class="sxs-lookup"><span data-stu-id="f9120-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="f9120-165">Hello Azure CLI kullanarak bir Linux VM disklerde şifrele</span><span class="sxs-lookup"><span data-stu-id="f9120-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
