---
title: "bir şablon olarak Azure Linux VM'de toouse aaaCapture | Microsoft Docs"
description: "Bilgi nasıl toocapture ve bir Linux tabanlı Azure sanal makinesinin hello Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş (VM) görüntüyü genelleştirin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="96a3e-103">Azure üzerinde çalışan Linux sanal makine yakalama</span><span class="sxs-lookup"><span data-stu-id="96a3e-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="96a3e-104">Bu makale toogeneralize Hello adımları izleyin ve hello Resource Manager dağıtım modelinde, Azure Linux sanal makine (VM) yakalayın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="96a3e-105">Merhaba VM generalize, kişisel hesap bilgilerini kaldırın ve bir görüntü olarak kullanılan hello VM toobe hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="96a3e-106">Ardından hello işletim sistemi, eklenen veri disklerini VHD'ler için genelleştirilmiş bir sanal sabit disk (VHD) görüntü yakalama ve [Resource Manager şablonu](../../azure-resource-manager/resource-group-overview.md) yeni VM dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="96a3e-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="96a3e-107">Bu makalede nasıl toocapture bir VM görüntü hello Azure CLI 1.0 ile yönetilmeyen diskleri kullanan bir VM için ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96a3e-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="96a3e-108">Ayrıca [hello Azure CLI 2.0 ile Azure yönetilen diskleri kullanan bir VM yakalama](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96a3e-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="96a3e-109">Yönetilen diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmeyen bunları.</span><span class="sxs-lookup"><span data-stu-id="96a3e-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="96a3e-110">Daha fazla bilgi için bkz. [Azure Yönetilen Disklere Genel Bakış](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96a3e-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="96a3e-111">toocreate hello görüntüsünü kullanarak sanal makineleri için yeni her VM ağ kaynakları ayarlamak ve hello ondan VHD görüntüleri yakalanan hello şablonu (JavaScript nesne gösterimi veya JSON, dosyası) toodeploy kullanın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="96a3e-112">Bu şekilde, geçerli yazılım yapılandırmasına benzer toohello şekilde hello Azure Marketi görüntüleri kullanmak'yle bir VM'yi çoğaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a3e-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="96a3e-113">Yedekleme veya hata ayıklama için toocreate, varolan bir Linux VM özel durumu ile bir kopyasını istiyorsanız, bkz: [Azure üzerinde çalışan Linux sanal makine bir kopyasını oluşturmak](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96a3e-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="96a3e-114">Ve bir şirket içi VM Linux VHD'den tooupload istiyorsanız, bkz: [karşıya yükleme ve özel disk görüntüsünden bir Linux VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96a3e-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="96a3e-115">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="96a3e-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="96a3e-116">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="96a3e-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="96a3e-117">[Azure CLI 1.0](#before-you-begin) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="96a3e-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="96a3e-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="96a3e-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96a3e-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="96a3e-119">Before you begin</span></span>
<span data-ttu-id="96a3e-120">Hello aşağıdaki önkoşulları karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="96a3e-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="96a3e-121">**Azure VM hello Resource Manager dağıtım modelinde oluşturulan** -bir Linux VM oluşturmadıysanız, hello kullanabilirsiniz [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), veya [Kaynak Yöneticisi Şablonları](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="96a3e-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="96a3e-122">Merhaba gerektiği gibi VM yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-122">Configure hello VM as needed.</span></span> <span data-ttu-id="96a3e-123">Örneğin, [veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)güncelleştirmeleri uygulamak ve uygulamaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="96a3e-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="96a3e-124">**Azure CLI** -yükleme hello [Azure CLI](../../cli-install-nodejs.md) yerel bir bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="96a3e-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="96a3e-125">1. adım: hello Azure Linux aracısı kaldırma</span><span class="sxs-lookup"><span data-stu-id="96a3e-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="96a3e-126">Öncelikle hello çalıştırın **waagent** hello komutunu **deprovision** hello Linux VM parametresi.</span><span class="sxs-lookup"><span data-stu-id="96a3e-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="96a3e-127">Bu komut dosyaları ve verileri toomake hello VM genelleme için hazır siler.</span><span class="sxs-lookup"><span data-stu-id="96a3e-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="96a3e-128">Merhaba Ayrıntılar için bkz [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96a3e-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="96a3e-129">Bir SSH istemcisi kullanarak Linux VM tooyour bağlayın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="96a3e-130">Merhaba SSH penceresinde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="96a3e-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="96a3e-131">Yalnızca bir görüntü olarak toocapture düşündüğünüz bu komutu bir VM üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="96a3e-132">Bu hello görüntüyü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtım için uygun garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="96a3e-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="96a3e-133">Tür **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="96a3e-133">Type **y** toocontinue.</span></span> <span data-ttu-id="96a3e-134">Merhaba ekleyebilirsiniz **-force** parametresi tooavoid bu onay adımı.</span><span class="sxs-lookup"><span data-stu-id="96a3e-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="96a3e-135">Merhaba komut tamamlandıktan sonra yazın **çıkmak**.</span><span class="sxs-lookup"><span data-stu-id="96a3e-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="96a3e-136">Bu adım hello SSH istemcisi kapatır.</span><span class="sxs-lookup"><span data-stu-id="96a3e-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="96a3e-137">2. adım: hello VM yakalama</span><span class="sxs-lookup"><span data-stu-id="96a3e-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="96a3e-138">Hello Azure CLI toogeneralize kullanın ve hello VM'yi yakalayın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="96a3e-139">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96a3e-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="96a3e-140">Örnek parametre adlarında **myResourceGroup**, **myVnet**, ve **myVM**.</span><span class="sxs-lookup"><span data-stu-id="96a3e-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="96a3e-141">Yerel bilgisayarınızdan hello Azure CLI açın ve [oturum açma tooyour Azure aboneliği](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="96a3e-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="96a3e-142">Kaynak Yöneticisi modunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96a3e-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="96a3e-143">Merhaba, zaten komutu aşağıdaki hello kullanarak sağlaması kaldırılıyor. sağlaması VM kapatın:</span><span class="sxs-lookup"><span data-stu-id="96a3e-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="96a3e-144">Merhaba VM komutu aşağıdaki hello ile generalize:</span><span class="sxs-lookup"><span data-stu-id="96a3e-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="96a3e-145">Merhaba Şimdi Çalıştır **azure vm yakalama** hangi yakalamaları hello VM komutu.</span><span class="sxs-lookup"><span data-stu-id="96a3e-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="96a3e-146">Aşağıdaki örneğine hello VHD ile yakalanır hello görüntü adları ile başlayan **MyVHDNamePrefix**ve hello **-t** seçeneği yolu toohello şablonunu belirtir **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="96a3e-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="96a3e-147">Varsayılan olarak özgün VM hello aynı depolama hesabındaki kullanılan hello Hello görüntü VHD dosyaları oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="96a3e-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="96a3e-148">Kullanım hello *aynı depolama hesabındaki* toostore hello VHD'ler hello görüntüden oluşturduğunuz yeni vm'leri.</span><span class="sxs-lookup"><span data-stu-id="96a3e-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="96a3e-149">bir metin düzenleyicide açık hello JSON şablonunu yakalanan bir görüntünün toofind başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="96a3e-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="96a3e-150">Merhaba, **storageProfile**, hello bulur **URI** Merhaba, **görüntü** hello bulunan **sistem** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="96a3e-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="96a3e-151">Örneğin, hello hello işletim sistemi disk görüntüsünün URI çok benzer.`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="96a3e-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="96a3e-152">3. adım: hello yakalanan görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="96a3e-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="96a3e-153">Şimdi hello görüntü şablonu toocreate bir Linux VM ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="96a3e-154">Aşağıdaki adımları ve yeni bir sanal ağ toocreate hello VM yakalanan JSON dosyası şablonu hello nasıl toouse hello Azure CLI gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96a3e-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="96a3e-155">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="96a3e-155">Create network resources</span></span>
<span data-ttu-id="96a3e-156">toouse hello şablonu, önce yeni VM için sanal ağ ve NIC tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="96a3e-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="96a3e-157">VM görüntüsü depolandığı hello konumda bu kaynakları için bir kaynak grubu oluşturma öneririz.</span><span class="sxs-lookup"><span data-stu-id="96a3e-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="96a3e-158">Aşağıdaki, kaynaklarınızın ve uygun bir Azure konumuna (Bu komutlarda "centralus") için adlarını değiştirerek benzer toohello komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="96a3e-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="96a3e-159">Merhaba hello NIC kimliğini Al</span><span class="sxs-lookup"><span data-stu-id="96a3e-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="96a3e-160">toodeploy hello yakalama sırasında kaydedilen JSON kullanarak hello görüntüsünden bir VM, hello hello NIC kimliği gerekiyor</span><span class="sxs-lookup"><span data-stu-id="96a3e-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="96a3e-161">Bu komutu aşağıdaki hello çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="96a3e-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="96a3e-162">Merhaba **kimliği** hello çok benzer bir çıkış`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="96a3e-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="96a3e-163">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="96a3e-163">Create a VM</span></span>
<span data-ttu-id="96a3e-164">Merhaba, VM'den toocreate çalışma hello şu komutu artık VM görüntüsü yakalandı.</span><span class="sxs-lookup"><span data-stu-id="96a3e-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="96a3e-165">Kullanım hello **-f** parametresi toospecify hello yolu toohello şablonu JSON dosya kaydettiniz.</span><span class="sxs-lookup"><span data-stu-id="96a3e-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="96a3e-166">Merhaba komutu çıktısı, yeni bir VM adı, hello Yöneticisi kullanıcı adı ve parola istendiğinde toosupply olan ve hello daha önce oluşturduğunuz NIC kimliğini hello.</span><span class="sxs-lookup"><span data-stu-id="96a3e-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="96a3e-167">Aşağıdaki örnek hello başarılı bir dağıtım için bkz: gösterir:</span><span class="sxs-lookup"><span data-stu-id="96a3e-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="96a3e-168">Merhaba dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="96a3e-168">Verify hello deployment</span></span>
<span data-ttu-id="96a3e-169">Şimdi SSH toohello, tooverify hello dağıtım ve başlangıç kullanılarak oluşturulan sanal makinenin yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="96a3e-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="96a3e-170">SSH, aracılığıyla tooconnect hello hello aşağıdaki komutu çalıştırarak oluşturulan VM hello IP adresini bulun:</span><span class="sxs-lookup"><span data-stu-id="96a3e-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="96a3e-171">Merhaba genel IP adresi hello komut çıktısında listelenir.</span><span class="sxs-lookup"><span data-stu-id="96a3e-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="96a3e-172">Varsayılan olarak toohello Linux VM SSH bağlantı noktası 22 tarafından bağlanır.</span><span class="sxs-lookup"><span data-stu-id="96a3e-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="96a3e-173">Ek VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="96a3e-173">Create additional VMs</span></span>
<span data-ttu-id="96a3e-174">Kullanım hello yakalanan görüntü ve şablon toodeploy bölüm önceki hello hello adımları kullanarak ek VM'ler.</span><span class="sxs-lookup"><span data-stu-id="96a3e-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="96a3e-175">Merhaba görüntüden diğer seçenekleri toocreate VM'ler arasında hızlı başlatma şablonunu kullanarak ya da çalışan hello **azure vm oluşturma** komutu.</span><span class="sxs-lookup"><span data-stu-id="96a3e-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="96a3e-176">Merhaba yakalanan şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="96a3e-176">Use hello captured template</span></span>
<span data-ttu-id="96a3e-177">görüntü ve şablon toouse hello yakalanan, (önceki bölümde hello ayrıntılı) aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="96a3e-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="96a3e-178">VM görüntüsü hello olduğundan emin olun VM VHD barındıran aynı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="96a3e-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="96a3e-179">Merhaba şablon JSON dosyasını kopyalayın ve hello işletim sistemi diski hello yeni VM'in VHD (veya VHD) için benzersiz bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="96a3e-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="96a3e-180">Örneğin, hello içinde **storageProfile**altında **vhd**, **URI**, hello için benzersiz bir ad belirtin **osDisk** VHD, benzer çok`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="96a3e-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="96a3e-181">Bir NIC ya da hello aynı veya farklı bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96a3e-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="96a3e-182">Değiştirilen hello şablonu JSON dosyasını kullanarak, bir dağıtım hello sanal ağ Kur ayarlamak hello kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96a3e-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="96a3e-183">Hızlı Başlatma şablonunu kullanma</span><span class="sxs-lookup"><span data-stu-id="96a3e-183">Use a quickstart template</span></span>
<span data-ttu-id="96a3e-184">Otomatik olarak bir VM hello görüntüden oluşturduğunuzda kümesi hello ağ istiyorsanız, bu kaynakları bir şablonda belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a3e-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="96a3e-185">Örneğin, hello bkz [101 vm gelen kullanıcı görüntüsü şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) github'dan.</span><span class="sxs-lookup"><span data-stu-id="96a3e-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="96a3e-186">Bu şablon bir VM, özel görüntü ve hello gerekli sanal ağ, genel IP adresi ve NIC kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="96a3e-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="96a3e-187">Merhaba şablonu hello Azure portal kullanarak bir anlatım için bkz: [nasıl toocreate Resource Manager şablonu kullanarak özel bir görüntü sanal makineden](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="96a3e-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="96a3e-188">Kullanım hello azure vm oluşturma komutu</span><span class="sxs-lookup"><span data-stu-id="96a3e-188">Use hello azure vm create command</span></span>
<span data-ttu-id="96a3e-189">Genellikle kolay toouse bir Resource Manager şablonu toocreate VM hello görüntüden olur.</span><span class="sxs-lookup"><span data-stu-id="96a3e-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="96a3e-190">Bununla birlikte, hello VM oluşturabilirsiniz *imperatively* hello kullanarak **azure vm oluşturma** hello komutunu **-Q** (**--görüntü urn**) parametresi .</span><span class="sxs-lookup"><span data-stu-id="96a3e-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="96a3e-191">Bu yöntemi kullanırsanız, ayrıca hello geçirdiğiniz **-d** (**--işletim sistemi disk vhd**) parametre toospecify hello hello OS .vhd dosyasının konumu hello yeni VM.</span><span class="sxs-lookup"><span data-stu-id="96a3e-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="96a3e-192">Bu dosya hello VHD'ler kapsayıcısında hello görüntü VHD dosyasının depolandığı hello depolama hesabının olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96a3e-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="96a3e-193">Merhaba kopyaları hello VHD Merhaba komut yeni VM otomatik olarak toohello **VHD'ler** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="96a3e-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="96a3e-194">Çalıştırmadan önce **azure vm oluşturma** hello görüntüsüyle hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="96a3e-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="96a3e-195">Bir kaynak grubu oluşturun veya varolan bir kaynak grubu hello dağıtımı için belirleyin.</span><span class="sxs-lookup"><span data-stu-id="96a3e-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="96a3e-196">Bir ortak oluşturmak IP adresi kaynağı ve NIC kaynağı için yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="96a3e-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="96a3e-197">Adımları toocreate için bir sanal ağ, ortak IP adresi ve Merhaba, CLI kullanarak NIC bu makalenin önceki bölümlerinde bkz.</span><span class="sxs-lookup"><span data-stu-id="96a3e-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="96a3e-198">(**azure vm oluşturma** bir NIC de oluşturabilirsiniz, ancak bir sanal ağ ve alt ağ için toopass ek parametreler gerekir.)</span><span class="sxs-lookup"><span data-stu-id="96a3e-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="96a3e-199">Daha sonra URI tooboth hello yeni işletim sistemi VHD dosyası ve görüntü varolan hello geçirmeden bir komut çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96a3e-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="96a3e-200">Bu örnekte, bir boyut Standard_A1 VM hello Doğu ABD bölgesinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="96a3e-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="96a3e-201">Ek komut seçeneklerini çalıştırmak `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="96a3e-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96a3e-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96a3e-202">Next steps</span></span>
<span data-ttu-id="96a3e-203">toomanage Vm'leriniz hello CLI, ile bkz hello görevlerinde [dağıtma ve Azure Resource Manager şablonları kullanarak sanal makineleri yönetme ve Azure CLI hello](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="96a3e-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

