---
title: "bir Linux VM görüntüsünü aaaCapture | Microsoft Docs"
description: "Toocapture bir Linux tabanlı Azure sanal makine (VM) görüntüsü hello Klasik dağıtım modeliyle nasıl oluşturulacağını öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="ad1ac-103">Nasıl toocapture klasik bir Linux sanal makinesini görüntü olarak</span><span class="sxs-lookup"><span data-stu-id="ad1ac-103">How toocapture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ad1ac-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ad1ac-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ad1ac-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ad1ac-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ad1ac-107">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad1ac-107">Learn how too[perform these steps using hello Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ad1ac-108">Bu makale size nasıl gösterir toocapture bir Klasik Azure Linux bir görüntü toocreate diğer sanal makineler çalıştıran sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="ad1ac-108">This article shows you how toocapture a classic Azure virtual machine (VM) running Linux as an image toocreate other virtual machines.</span></span> <span data-ttu-id="ad1ac-109">Bu görüntü hello işletim sistemi diski içerir ve veri diskleri toohello VM bağlı.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-109">This image includes hello OS disk and data disks attached toohello VM.</span></span> <span data-ttu-id="ad1ac-110">Tooconfigure gereken şekilde ağ yapılandırmasını, içermez, oluşturduğunuzda hello diğer VM hello görüntüden.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-110">It doesn't include networking configuration, so you need tooconfigure that when you create hello other VM from hello image.</span></span>

<span data-ttu-id="ad1ac-111">Azure depoları hello altındaki görüntüyü **görüntüleri**, karşıya tüm görüntüleri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-111">Azure stores hello image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="ad1ac-112">Görüntüleri hakkında daha fazla bilgi için bkz: [azure'da sanal makine görüntülerini hakkında][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="ad1ac-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ad1ac-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ad1ac-113">Before you begin</span></span>
<span data-ttu-id="ad1ac-114">Bu adımları hello Klasik dağıtım modeli ve veri diskleri ekleme de dahil olmak üzere yapılandırılmış hello işletim sistemi kullanarak bir Azure VM zaten oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-114">These steps assume that you've already created an Azure VM using hello Classic deployment model and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="ad1ac-115">Toocreate VM ihtiyacınız varsa okuyun [nasıl tooCreate Linux sanal makine][How tooCreate a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="ad1ac-115">If you need toocreate a VM, read [How tooCreate a Linux Virtual Machine][How tooCreate a Linux Virtual Machine].</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="ad1ac-116">Merhaba sanal makinesi yakalama</span><span class="sxs-lookup"><span data-stu-id="ad1ac-116">Capture hello virtual machine</span></span>
1. <span data-ttu-id="ad1ac-117">[Toohello VM bağlanmak](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tercih ettiğiniz bir SSH istemcisi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-117">[Connect toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="ad1ac-118">Merhaba SSH penceresinde hello aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-118">In hello SSH window, type hello following command.</span></span> <span data-ttu-id="ad1ac-119">Merhaba çıktı `waagent` bu yardımcı program hello sürümüne bağlı olarak biraz değişebilir:</span><span class="sxs-lookup"><span data-stu-id="ad1ac-119">hello output from `waagent` may vary slightly depending on hello version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="ad1ac-120">Merhaba yukarıdaki komut tooclean hello sistem çalışır ve sağlama işleminin uygun yapın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-120">hello preceding command attempts tooclean hello system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="ad1ac-121">Bu işlem hello aşağıdaki görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="ad1ac-121">This operation performs hello following tasks:</span></span>

   * <span data-ttu-id="ad1ac-122">(Provisioning.RegenerateSshHostKeyPair hello yapılandırma dosyasındaki ' y' ise) SSH ana bilgisayar anahtarlarını kaldırır</span><span class="sxs-lookup"><span data-stu-id="ad1ac-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="ad1ac-123">Ad sunucusu yapılandırmasında /etc/resolv.conf temizler</span><span class="sxs-lookup"><span data-stu-id="ad1ac-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="ad1ac-124">Kaldırır hello `root` (Provisioning.DeleteRootPassword 'y' hello yapılandırma dosyasında ise) / etc/gölge kullanıcı parolasından</span><span class="sxs-lookup"><span data-stu-id="ad1ac-124">Removes hello `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
   * <span data-ttu-id="ad1ac-125">Önbelleğe alınan istemci kiralamalarını kaldırır</span><span class="sxs-lookup"><span data-stu-id="ad1ac-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="ad1ac-126">Sıfırlama ana bilgisayar adı toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="ad1ac-126">Resets host name toolocalhost.localdomain</span></span>
   * <span data-ttu-id="ad1ac-127">Merhaba (/var/lib/waagent elde edilen) son sağlanan kullanıcının hesabını siler **ve veri ilişkili**.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-127">Deletes hello last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ad1ac-128">Sağlama kaldırmayı dosyalarını siler ve veri çok "Merhaba görüntü generalize".</span><span class="sxs-lookup"><span data-stu-id="ad1ac-128">Deprovisioning deletes files and data too"generalize" hello image.</span></span> <span data-ttu-id="ad1ac-129">Yalnızca yeni bir görüntü şablon olarak toocapture düşündüğünüz bu komutu bir VM üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-129">Only run this command on a VM that you intend toocapture as a new image template.</span></span> <span data-ttu-id="ad1ac-130">Bu hello görüntüyü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtımı toothird taraflar için uygun garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-130">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution toothird parties.</span></span>

3. <span data-ttu-id="ad1ac-131">Tür **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-131">Type **y** toocontinue.</span></span> <span data-ttu-id="ad1ac-132">Merhaba ekleyebilirsiniz `-force` parametresi tooavoid bu onay adımı.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-132">You can add hello `-force` parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="ad1ac-133">Tür **çıkış** tooclose hello SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-133">Type **Exit** tooclose hello SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad1ac-134">Merhaba Kalan adımların zaten sahip olduğu varsayılır [hello Azure CLI yüklenmiş](../../../cli-install-nodejs.md) istemci bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-134">hello remaining steps assume you have already [installed hello Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="ad1ac-135">Aşağıdaki adımları tüm hello hello de yapılabilir [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad1ac-135">All hello following steps can also be done in hello [Azure portal](http://portal.azure.com).</span></span>

5. <span data-ttu-id="ad1ac-136">İstemci bilgisayarından, Azure CLI ve oturum açma tooyour Azure aboneliği açın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-136">From your client computer, open Azure CLI and login tooyour Azure subscription.</span></span> <span data-ttu-id="ad1ac-137">Ayrıntılar için [tooan Azure aboneliği hello Azure CLI ' bağlanma](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ad1ac-137">For details, read [Connect tooan Azure subscription from hello Azure CLI](../../../xplat-cli-connect.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad1ac-138">Hello Azure portal, toohello Portalı'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-138">In hello Azure portal, log in toohello portal.</span></span>

6. <span data-ttu-id="ad1ac-139">Hizmet Yönetimi modunda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="ad1ac-139">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="ad1ac-140">Zaten sağlaması kaldırılıyor. sağlaması VM Hello kapatın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-140">Shut down hello VM that is already deprovisioned.</span></span> <span data-ttu-id="ad1ac-141">Merhaba aşağıdaki örnek kapatır adlı VM hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="ad1ac-141">hello following example shuts down hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```
   <span data-ttu-id="ad1ac-142">Gerekirse, tüm hello VM'ler aboneliğinizde kullanılarak oluşturulan bir listesini görüntüleyebilirsiniz`azure vm list`</span><span class="sxs-lookup"><span data-stu-id="ad1ac-142">If needed, you can view a list all hello VMs created in your subscription by using `azure vm list`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ad1ac-143">Hello Azure portalını kullanıyorsanız, hello VM seçin ve tıklatın **durdurmak** VM hello kapatılamadı.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-143">If you're using hello Azure portal, select hello VM and click **Stop** to shut down hello VM.</span></span>

8. <span data-ttu-id="ad1ac-144">Merhaba VM durdurulduğunda hello görüntüsünü yakalayın.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-144">When hello VM is stopped, capture hello image.</span></span> <span data-ttu-id="ad1ac-145">Örnek yakalamaları aşağıdaki hello hello adlı VM `myVM` ve adlı genelleştirilmiş bir yansıma oluşturur `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="ad1ac-145">hello following example captures hello VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="ad1ac-146">Merhaba `-t` siler hello özgün sanal makine alt.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-146">hello `-t` subcommand deletes hello original virtual machine.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad1ac-147">Hello Azure portal, seçerek bir görüntüsünü yakalayabilirsiniz **görüntü** hello hub menüsünde.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-147">In hello Azure portal, you can capture an image by selecting **Image** from hello hub menu.</span></span> <span data-ttu-id="ad1ac-148">Aşağıdaki bilgilerle hello görüntüsü için toosupply hello gerekir: adı, kaynak grubu, konum, işletim sistemi türü ve depolama blob yolu.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-148">You need toosupply hello following information for hello image: name, resource group, location, operating system type, and storage blob path.</span></span>

9. <span data-ttu-id="ad1ac-149">artık yeni bir VM olabilir görüntülerinin hello listesinde kullanılabilir tooconfigure kullanılan hello yeni görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-149">hello new image is now available in hello list of images that can be used tooconfigure any new VM.</span></span> <span data-ttu-id="ad1ac-150">Merhaba komutuyla görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ad1ac-150">You can view it with hello command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="ad1ac-151">Merhaba üzerinde [Azure portal](http://portal.azure.com), hello yeni görüntüsü görünür hello **VM görüntüleri (Klasik)** toohello ait **işlem** Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-151">On hello [Azure portal](http://portal.azure.com), hello new image appears in hello **VM images (classic)** that belongs toohello **Compute** services.</span></span> <span data-ttu-id="ad1ac-152">Erişebileceğiniz **VM görüntüleri (Klasik)** tıklayarak _daha fazla hizmet_ listesi hello Azure hello alt kısmındaki hizmet ve hello arayan **işlem** Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-152">You can access **VM images (classic)** by clicking _More services_ at hello bottom of hello Azure service list, and then looking in hello **Compute** services.</span></span>   

   ![Görüntü yakalama başarılı](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="ad1ac-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad1ac-154">Next steps</span></span>
<span data-ttu-id="ad1ac-155">Merhaba, kullanılan hazır toobe toocreate VM'ler görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-155">hello image is ready toobe used toocreate VMs.</span></span> <span data-ttu-id="ad1ac-156">Hello Azure CLI komutunu kullanabilirsiniz `azure vm create` ve oluşturduğunuz kaynağı hello görüntü adı.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-156">You can use hello Azure CLI command `azure vm create` and supply hello image name you created.</span></span> <span data-ttu-id="ad1ac-157">Daha fazla bilgi için bkz: [Klasik dağıtım modeli ile Azure CLI kullanarak hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ad1ac-157">For more information, see [Using hello Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="ad1ac-158">Alternatif olarak, hello kullanın [Azure portal](http://portal.azure.com) toocreate hello kullanarak özel bir VM **görüntü** yöntemi ve hello seçerek görüntü oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="ad1ac-158">Alternatively, use hello [Azure portal](http://portal.azure.com) toocreate a custom VM by using hello **Image** method and selecting hello image you created.</span></span> <span data-ttu-id="ad1ac-159">Daha fazla bilgi için bkz: [nasıl tooCreate özel VM][How tooCreate a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="ad1ac-159">For more information, see [How tooCreate a Custom VM][How tooCreate a Custom Virtual Machine].</span></span>

<span data-ttu-id="ad1ac-160">**Ayrıca bkz:** [Azure Linux Aracısı Kullanıcı Kılavuzu](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ad1ac-160">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
