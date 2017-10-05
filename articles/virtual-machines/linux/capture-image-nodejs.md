---
title: "Bir şablon olarak kullanmak üzere bir Azure Linux VM yakalama | Microsoft Docs"
description: "Yakalama ve görüntüyü bir Linux tabanlı Azure sanal makinesinin Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş (VM) generalize öğrenin."
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
ms.openlocfilehash: b1164fbd816eea5189786850f096438e32f8f802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="06e7d-103">Azure üzerinde çalışan Linux sanal makine yakalama</span><span class="sxs-lookup"><span data-stu-id="06e7d-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="06e7d-104">Generalize ve Resource Manager dağıtım modelinde, Azure Linux sanal makine (VM) yakalamak için bu makaledeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-104">Follow the steps in this article to generalize and capture your Azure Linux virtual machine (VM) in the Resource Manager deployment model.</span></span> <span data-ttu-id="06e7d-105">VM generalize, kişisel hesap bilgilerini kaldırın ve bir görüntü olarak kullanılacak VM hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-105">When you generalize the VM, you remove personal account information and prepare the VM to be used as an image.</span></span> <span data-ttu-id="06e7d-106">Ardından VHD'ler, bağlı veri diskleri için işletim sistemi için genelleştirilmiş bir sanal sabit disk (VHD) görüntü yakalama ve [Resource Manager şablonu](../../azure-resource-manager/resource-group-overview.md) yeni VM dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="06e7d-106">You then capture a generalized virtual hard disk (VHD) image for the OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="06e7d-107">Bu makalede yönetilmeyen diskleri kullanan bir VM için Azure CLI 1.0 ile bir VM görüntüsü yakalama ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-107">This article details how to capture a VM image with the Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="06e7d-108">Ayrıca [Azure CLI 2.0 ile Azure yönetilen diskleri kullanarak bir VM yakalama](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e7d-108">You can also [capture a VM using Azure Managed Disks with the Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="06e7d-109">Yönetilen diskleri Azure platformu tarafından işlenir ve hazırlık veya konum depolamaya gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="06e7d-109">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="06e7d-110">Daha fazla bilgi için bkz. [Azure Yönetilen Disklere Genel Bakış](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e7d-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="06e7d-111">Görüntü kullanarak VM'ler oluşturmak için her yeni VM için ağ kaynakları ayarlamak ve yakalanan VHD yansımalarını dağıtmak için şablonu (JavaScript nesne gösterimi veya JSON, dosyası) kullanın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-111">To create VMs using the image, set up network resources for each new VM, and use the template (a JavaScript Object Notation, or JSON, file) to deploy it from the captured VHD images.</span></span> <span data-ttu-id="06e7d-112">Bu şekilde, geçerli yazılım yapılandırması, benzer şekilde Azure Marketi'nde görüntüleri kullanmak'yle bir VM'yi çoğaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06e7d-112">In this way, you can replicate a VM with its current software configuration, similar to the way you use images in the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="06e7d-113">Yedekleme veya hata ayıklama için özel durumu ile bir kopyasını, varolan bir Linux VM oluşturmak istiyorsanız, bkz: [Azure üzerinde çalışan Linux sanal makine bir kopyasını oluşturmak](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e7d-113">If you want to create a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="06e7d-114">Ve bir şirket içi VM Linux VHD'den karşıya yüklemek istiyorsanız, bkz: [karşıya yükleme ve özel disk görüntüsünden bir Linux VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e7d-114">And if you want to upload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="06e7d-115">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="06e7d-115">CLI versions to complete the task</span></span>
<span data-ttu-id="06e7d-116">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="06e7d-116">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="06e7d-117">[Azure CLI 1.0](#before-you-begin) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="06e7d-117">[Azure CLI 1.0](#before-you-begin) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="06e7d-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="06e7d-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="06e7d-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="06e7d-119">Before you begin</span></span>
<span data-ttu-id="06e7d-120">Aşağıdaki önkoşulları karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="06e7d-120">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="06e7d-121">**Azure VM Resource Manager dağıtım modelinde oluşturulan** -bir Linux VM oluşturmadıysanız, kullanabileceğiniz [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), veya [Resource Manager şablonları ](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="06e7d-121">**Azure VM created in the Resource Manager deployment model** - If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), the [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="06e7d-122">VM gerektiği gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-122">Configure the VM as needed.</span></span> <span data-ttu-id="06e7d-123">Örneğin, [veri diski Ekle](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)güncelleştirmeleri uygulamak ve uygulamaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="06e7d-124">**Azure CLI** -yükleme [Azure CLI](../../cli-install-nodejs.md) yerel bir bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="06e7d-124">**Azure CLI** - Install the [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-the-azure-linux-agent"></a><span data-ttu-id="06e7d-125">1. adım: Azure Linux Aracısı'nı kaldırma</span><span class="sxs-lookup"><span data-stu-id="06e7d-125">Step 1: Remove the Azure Linux agent</span></span>
<span data-ttu-id="06e7d-126">Öncelikle çalıştırın **waagent** komutunu **deprovision** Linux VM'de parametresi.</span><span class="sxs-lookup"><span data-stu-id="06e7d-126">First, run the **waagent** command with the **deprovision** parameter on the Linux VM.</span></span> <span data-ttu-id="06e7d-127">Bu komut dosyaları ve VM genelleme için hazır hale getirmek için verileri siler.</span><span class="sxs-lookup"><span data-stu-id="06e7d-127">This command deletes files and data to make the VM ready for generalizing.</span></span> <span data-ttu-id="06e7d-128">Ayrıntılar için bkz [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06e7d-128">For details, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="06e7d-129">Bir SSH istemcisi kullanarak Linux VM'NİZDE bağlayın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-129">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="06e7d-130">SSH penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="06e7d-130">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="06e7d-131">Yalnızca resim olarak yakalamasına düşündüğünüz bir VM'de bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-131">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="06e7d-132">Görüntü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtım için uygun garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="06e7d-132">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="06e7d-133">Tür **y** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="06e7d-133">Type **y** to continue.</span></span> <span data-ttu-id="06e7d-134">Ekleyebileceğiniz **-force** bu onay adım önlemek için parametre.</span><span class="sxs-lookup"><span data-stu-id="06e7d-134">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="06e7d-135">Komut tamamlandığında yazın **çıkmak**.</span><span class="sxs-lookup"><span data-stu-id="06e7d-135">After the command completes, type **exit**.</span></span> <span data-ttu-id="06e7d-136">Bu adım, SSH istemcisi kapatır.</span><span class="sxs-lookup"><span data-stu-id="06e7d-136">This step closes the SSH client.</span></span>

## <a name="step-2-capture-the-vm"></a><span data-ttu-id="06e7d-137">2. adım: VM yakalama</span><span class="sxs-lookup"><span data-stu-id="06e7d-137">Step 2: Capture the VM</span></span>
<span data-ttu-id="06e7d-138">Generalize ve VM yakalama için Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-138">Use the Azure CLI to generalize and capture the VM.</span></span> <span data-ttu-id="06e7d-139">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-139">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="06e7d-140">Örnek parametre adlarında **myResourceGroup**, **myVnet**, ve **myVM**.</span><span class="sxs-lookup"><span data-stu-id="06e7d-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="06e7d-141">Azure CLI yerel bilgisayarınızdan açın ve [Azure aboneliğinizde oturum açma](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="06e7d-141">From your local computer, open the Azure CLI and [login to your Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="06e7d-142">Kaynak Yöneticisi modunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="06e7d-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="06e7d-143">Zaten aşağıdaki komutu kullanarak sağlaması kaldırılıyor. sağlaması VM kapatın:</span><span class="sxs-lookup"><span data-stu-id="06e7d-143">Shut down the VM that you already deprovisioned by using the following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="06e7d-144">VM şu komutla generalize:</span><span class="sxs-lookup"><span data-stu-id="06e7d-144">Generalize the VM with the following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="06e7d-145">Şimdi Çalıştır **azure vm yakalama** VM yakalar komutu.</span><span class="sxs-lookup"><span data-stu-id="06e7d-145">Now run the **azure vm capture** command, which captures the VM.</span></span> <span data-ttu-id="06e7d-146">Aşağıdaki örnekte, VHD ile yakalanan görüntü adları ile başlayan **MyVHDNamePrefix**ve **-t** seçeneği, şablonun yolunu belirtir **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="06e7d-146">In the following example, the image VHDs are captured with names beginning with **MyVHDNamePrefix**, and the **-t** option specifies a path to the template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="06e7d-147">Görüntü VHD dosyaları, varsayılan olarak özgün VM kullanılan aynı depolama hesabındaki oluşturulmasına.</span><span class="sxs-lookup"><span data-stu-id="06e7d-147">The image VHD files get created by default in the same storage account that the original VM used.</span></span> <span data-ttu-id="06e7d-148">Kullanım *aynı depolama hesabındaki* görüntüden oluşturduğunuz yeni vm'leri VHD'lerin depolanmasını.</span><span class="sxs-lookup"><span data-stu-id="06e7d-148">Use the *same storage account* to store the VHDs for any new VMs you create from the image.</span></span> 

6. <span data-ttu-id="06e7d-149">Yakalanan görüntüye konumunu bulmak için JSON şablonunu bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-149">To find the location of a captured image, open the JSON template in a text editor.</span></span> <span data-ttu-id="06e7d-150">İçinde **storageProfile**, bulma **URI** , **görüntü** bulunan **sistem** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="06e7d-150">In the **storageProfile**, find the **uri** of the **image** located in the **system** container.</span></span> <span data-ttu-id="06e7d-151">Örneğin, işletim sistemi disk görüntüsü URI'sini benzer.`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="06e7d-151">For example, the URI of the OS disk image is similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="06e7d-152">3. adım: yakalanan görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="06e7d-152">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="06e7d-153">Şimdi görüntünün bir Linux VM oluşturmak için sahip bir şablon kullanın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-153">Now use the image with a template to create a Linux VM.</span></span> <span data-ttu-id="06e7d-154">Bu adımlar, Azure CLI ve yeni bir sanal ağ oluşturmak için yakalanan JSON dosyası şablonu nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-154">These steps show you how to use the Azure CLI and the JSON file template you captured to create the VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="06e7d-155">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="06e7d-155">Create network resources</span></span>
<span data-ttu-id="06e7d-156">Şablonu kullanmak için önce yeni VM için bir sanal ağ ve NIC ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-156">To use the template, you first need to set up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="06e7d-157">VM görüntüsü depolandığı konumda bu kaynakları için bir kaynak grubu oluşturma öneririz.</span><span class="sxs-lookup"><span data-stu-id="06e7d-157">We recommend you create a resource group for these resources in the location where your VM image is stored.</span></span> <span data-ttu-id="06e7d-158">Çalıştırma komutları aşağıdaki değiştirerek adları, kaynaklarınızı ve uygun bir Azure konumuna (Bu komutlarda "centralus") için benzer:</span><span class="sxs-lookup"><span data-stu-id="06e7d-158">Run commands similar to the following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-the-id-of-the-nic"></a><span data-ttu-id="06e7d-159">NIC kimliğini Al</span><span class="sxs-lookup"><span data-stu-id="06e7d-159">Get the Id of the NIC</span></span>
<span data-ttu-id="06e7d-160">Görüntüden VM yakalama sırasında kaydedilen JSON kullanarak dağıtmak için NIC kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-160">To deploy a VM from the image by using the JSON you saved during capture, you need the Id of the NIC.</span></span> <span data-ttu-id="06e7d-161">Bunu, aşağıdaki komutu çalıştırarak alın:</span><span class="sxs-lookup"><span data-stu-id="06e7d-161">Obtain it by running the following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="06e7d-162">**Kimliği** çıktıda benzer`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="06e7d-162">The **Id** in the output is similar to `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="06e7d-163">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="06e7d-163">Create a VM</span></span>
<span data-ttu-id="06e7d-164">Şimdi, yakalanan VM görüntüsünü oluşturmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-164">Now run the following command to create your VM from the captured VM image.</span></span> <span data-ttu-id="06e7d-165">Kullanım **-f** parametresi kaydettiğiniz şablon JSON dosyasının yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-165">Use the **-f** parameter to specify the path to the template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="06e7d-166">Komut çıktısında, yeni bir VM adı, yönetici kullanıcı adı ve parola ve daha önce oluşturduğunuz NIC kimliğini sağlamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-166">In the command output, you are prompted to supply a new VM name, the admin user name and password, and the Id of the NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="06e7d-167">Aşağıdaki örnek, başarılı bir dağıtım için gördüğünüz gösterir:</span><span class="sxs-lookup"><span data-stu-id="06e7d-167">The following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment to complete
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

### <a name="verify-the-deployment"></a><span data-ttu-id="06e7d-168">Dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="06e7d-168">Verify the deployment</span></span>
<span data-ttu-id="06e7d-169">Şimdi SSH dağıtım ve yeni VM kullanarak başlangıç doğrulamak için oluşturduğunuz sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="06e7d-169">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="06e7d-170">SSH bağlanmak için aşağıdaki komutu çalıştırarak oluşturulan VM IP adresini bulun:</span><span class="sxs-lookup"><span data-stu-id="06e7d-170">To connect via SSH, find the IP address of the VM you created by running the following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="06e7d-171">Genel IP adresi komut çıktısında listelenir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-171">The public IP address is listed in the command output.</span></span> <span data-ttu-id="06e7d-172">Varsayılan olarak Linux VM'ye SSH bağlantı noktası 22 tarafından bağlanır.</span><span class="sxs-lookup"><span data-stu-id="06e7d-172">By default you connect to the Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="06e7d-173">Ek VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="06e7d-173">Create additional VMs</span></span>
<span data-ttu-id="06e7d-174">Şablon ve yakalanan görüntü önceki bölümde yer alan adımları kullanarak ek sanal makineleri dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-174">Use the captured image and template to deploy additional VMs using the steps in the preceding section.</span></span> <span data-ttu-id="06e7d-175">Hızlı Başlatma şablonunu kullanarak veya çalıştıran VM'ler görüntüsünü oluşturmak için diğer seçenekleri dahil **azure vm oluşturma** komutu.</span><span class="sxs-lookup"><span data-stu-id="06e7d-175">Other options to create VMs from the image include using a quickstart template or running the **azure vm create** command.</span></span>

### <a name="use-the-captured-template"></a><span data-ttu-id="06e7d-176">Yakalanan şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="06e7d-176">Use the captured template</span></span>
<span data-ttu-id="06e7d-177">Yakalanan görüntü ve şablonu kullanmak için (önceki bölümde ayrıntılı) aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="06e7d-177">To use the captured image and template, follow these steps (detailed in the preceding section):</span></span>

* <span data-ttu-id="06e7d-178">VM görüntüsü VM VHD barındıran aynı depolama hesabı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="06e7d-178">Ensure that your VM image is in the same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="06e7d-179">Şablon JSON dosyasını kopyalayın ve işletim sistemi diski yeni VM'nin VHD (veya VHD) için benzersiz bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-179">Copy the template JSON file and specify a unique name for the OS disk of the new VM's VHD (or VHDs).</span></span> <span data-ttu-id="06e7d-180">Örneğin, **storageProfile**altında **vhd**, **URI**, için benzersiz bir ad belirtin **osDisk** VHD, benzer`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="06e7d-180">For example, in the **storageProfile**, under **vhd**, in **uri**, specify a unique name for the **osDisk** VHD, similar to `https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="06e7d-181">Bir NIC aynı veya farklı bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06e7d-181">Create a NIC in either the same or a different virtual network.</span></span>
* <span data-ttu-id="06e7d-182">Değiştirilen şablon JSON dosyasını kullanarak, sanal ağı kümesi kaynak grubundaki bir dağıtım oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06e7d-182">Using the modified template JSON file, create a deployment in the resource group in which you set up the virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="06e7d-183">Hızlı Başlatma şablonunu kullanma</span><span class="sxs-lookup"><span data-stu-id="06e7d-183">Use a quickstart template</span></span>
<span data-ttu-id="06e7d-184">Otomatik olarak bir VM görüntüsünü oluşturduğunuzda kümesi ağ istiyorsanız, bu kaynakları bir şablonda belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06e7d-184">If you want the network set up automatically when you create a VM from the image, you can specify those resources in a template.</span></span> <span data-ttu-id="06e7d-185">Örneğin, [101 vm gelen kullanıcı görüntüsü şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) github'dan.</span><span class="sxs-lookup"><span data-stu-id="06e7d-185">For example, see the [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="06e7d-186">Bu şablon bir VM özel görüntünüzü ve gerekli sanal ağ, genel IP adresi ve NIC kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06e7d-186">This template creates a VM from your custom image and the necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="06e7d-187">Azure portalında şablonu kullanarak bir anlatım için bkz: [Resource Manager şablonu kullanarak özel bir görüntüden sanal makine oluşturmak nasıl](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="06e7d-187">For a walkthrough of using the template in the Azure portal, see [How to create a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-the-azure-vm-create-command"></a><span data-ttu-id="06e7d-188">Azure vm komutu oluşturun</span><span class="sxs-lookup"><span data-stu-id="06e7d-188">Use the azure vm create command</span></span>
<span data-ttu-id="06e7d-189">Genellikle bir VM görüntüsünü oluşturmak için Resource Manager şablonu kullanmak en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="06e7d-189">Usually it's easiest to use a Resource Manager template to create a VM from the image.</span></span> <span data-ttu-id="06e7d-190">Ancak, VM oluşturabilirsiniz *imperatively* kullanarak **azure vm oluşturma** komutunu **-Q** (**--görüntü urn**) parametre.</span><span class="sxs-lookup"><span data-stu-id="06e7d-190">However, you can create the VM *imperatively* by using the **azure vm create** command with the **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="06e7d-191">Bu yöntemi kullanırsanız, ayrıca geçirdiğiniz **-d** (**--işletim sistemi disk vhd**) parametresini kullanarak yeni bir VM için işletim sistemi .vhd dosyası konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-191">If you use this method, you also pass the **-d** (**--os-disk-vhd**) parameter to specify the location of the OS .vhd file for the new VM.</span></span> <span data-ttu-id="06e7d-192">Bu dosya görüntü VHD dosyasının depolandığı depolama hesabını VHD'ler kapsayıcısında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="06e7d-192">This file must be in the vhds container of the storage account where the image VHD file is stored.</span></span> <span data-ttu-id="06e7d-193">Yeni VM için VHD komutu otomatik olarak kopyalar **VHD'ler** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="06e7d-193">The command copies the VHD for the new VM automatically to the **vhds** container.</span></span>

<span data-ttu-id="06e7d-194">Çalıştırmadan önce **azure vm oluşturma** görüntüsüyle aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="06e7d-194">Before running **azure vm create** with the image, complete the following steps:</span></span>

1. <span data-ttu-id="06e7d-195">Bir kaynak grubu oluşturun veya varolan bir kaynak grubu dağıtımı için belirleyin.</span><span class="sxs-lookup"><span data-stu-id="06e7d-195">Create a resource group, or identify an existing resource group for the deployment.</span></span>
2. <span data-ttu-id="06e7d-196">Yeni VM için genel bir IP adresi kaynağı ve NIC kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06e7d-196">Create a public IP address resource and a NIC resource for the new VM.</span></span> <span data-ttu-id="06e7d-197">CLI kullanarak bir sanal ağ, genel IP adresi ve NIC oluşturma adımları için bu makalenin önceki bölümlerinde bkz.</span><span class="sxs-lookup"><span data-stu-id="06e7d-197">For steps to create a virtual network, public IP address, and NIC by using the CLI, see earlier in this article.</span></span> <span data-ttu-id="06e7d-198">(**azure vm oluşturma** bir NIC de oluşturabilirsiniz, ancak bir sanal ağ ve alt ağ için ek parametreler gerekir.)</span><span class="sxs-lookup"><span data-stu-id="06e7d-198">(**azure vm create** can also create a NIC, but you need to pass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="06e7d-199">Daha sonra yeni işletim sistemi VHD dosyasının hem mevcut görüntü URI'ler geçirmeden bir komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="06e7d-199">Then run a command that passes URIs to both the new OS VHD file and the existing image.</span></span> <span data-ttu-id="06e7d-200">Bu örnekte, bir boyut Doğu ABD bölgesinde Standard_A1 VM oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="06e7d-200">In this example, a size Standard_A1 VM is created in the East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="06e7d-201">Ek komut seçeneklerini çalıştırmak `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="06e7d-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06e7d-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06e7d-202">Next steps</span></span>
<span data-ttu-id="06e7d-203">Vm'leriniz CLI ile yönetmek için görevleri görmek [dağıtma ve Azure Resource Manager şablonları ve Azure CLI kullanarak sanal makineleri yönetme](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="06e7d-203">To manage your VMs with the CLI, see the tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

