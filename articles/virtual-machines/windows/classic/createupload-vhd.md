---
title: "aaaCreate ve karşıya yükleme VM görüntü Powershell kullanarak | Microsoft Docs"
description: "Toocreate öğrenin ve hello Klasik dağıtım modeli ve Azure Powershell kullanılarak genelleştirilmiş bir Windows Server yansıma (VHD) yükleyin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="e2173-103">Oluşturma ve Windows Server VHD tooAzure yükleme</span><span class="sxs-lookup"><span data-stu-id="e2173-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="e2173-104">Bu makalede nasıl tooupload genelleştirilmiş VM görüntü sanal sabit disk (VHD) toocreate sanal makineleri kullanabilmesi için gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e2173-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="e2173-105">Diskleri ve Microsoft Azure içinde VHD'leri hakkında daha fazla ayrıntı için [hakkında diskleri ve sanal makineler için VHD'ler](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2173-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2173-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e2173-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e2173-107">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e2173-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e2173-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="e2173-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e2173-109">Ayrıca [karşıya](../upload-generalized-managed.md) hello Resource Manager modelini kullanarak bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="e2173-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2173-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e2173-110">Prerequisites</span></span>
<span data-ttu-id="e2173-111">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="e2173-111">This article assumes you have:</span></span>

* <span data-ttu-id="e2173-112">**Bir Azure aboneliği** -yoksa, şunları yapabilirsiniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e2173-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="e2173-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -hello Microsoft Azure PowerShell sahip modülü yüklenir ve aboneliğinizi toouse yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e2173-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="e2173-114">**A. VHD dosyasını** - desteklenen Windows işletim sistemi bir .vhd dosyası ekli tooa sanal makine depolanır.</span><span class="sxs-lookup"><span data-stu-id="e2173-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="e2173-115">VHD Hello üzerinde çalışan hello sunucu rolleri Sysprep tarafından destekleniyorsa toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e2173-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="e2173-116">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="e2173-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e2173-117">Microsoft Azure'da Hello VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e2173-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="e2173-118">Hyper-V Yöneticisi'ni veya hello kullanarak hello disk tooVHD biçimine dönüştürebilirsiniz [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2173-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="e2173-119">Ayrıntılar için bu bkz [blog gönderisi](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2173-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="e2173-120">1. adım: Hazırlığı hello VHD</span><span class="sxs-lookup"><span data-stu-id="e2173-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="e2173-121">Merhaba VHD tooAzure karşıya yüklemeden önce hello Sysprep aracını kullanılarak genelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2173-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="e2173-122">Bir görüntü olarak kullanılan hello VHD toobe hazırlar.</span><span class="sxs-lookup"><span data-stu-id="e2173-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="e2173-123">Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2173-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="e2173-124">VM Hello, Sysprep çalıştırılmadan önce yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="e2173-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="e2173-125">Merhaba sanal makineden işletim sistemi hello hello aşağıdaki yordamı tamamlamak için yüklendi:</span><span class="sxs-lookup"><span data-stu-id="e2173-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="e2173-126">Toohello işletim sisteminde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e2173-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="e2173-127">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="e2173-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="e2173-128">Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="e2173-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Bir komut istemi penceresi açın](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="e2173-130">Merhaba **Sistem Hazırlama aracı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e2173-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Sysprep Başlat](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="e2173-132">Merhaba, **Sistem Hazırlama aracı**seçin **girin sistem ilk çalıştırma deneyimi (OOBE)** emin olun **Generalize** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="e2173-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="e2173-133">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="e2173-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="e2173-134">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2173-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="e2173-135">2. adım: bir depolama hesabı ve kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2173-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="e2173-136">Bir yerde tooupload hello .vhd dosyası için bir Azure depolama hesabında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2173-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="e2173-137">Bu adım nasıl toocreate bir hesap veya get hello bilgileri gösterir, var olan bir hesaptan gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2173-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="e2173-138">Merhaba değişkenleri değiştirin &lsaquo; köşeli &rsaquo; kendi bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="e2173-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="e2173-139">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="e2173-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="e2173-140">Azure aboneliğiniz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e2173-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="e2173-141">Yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2173-141">Create a new storage account.</span></span> <span data-ttu-id="e2173-142">Merhaba hello depolama hesabı adının benzersiz olması 3-24 karakter.</span><span class="sxs-lookup"><span data-stu-id="e2173-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="e2173-143">Merhaba adı harfler ve sayıların birleşiminden oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="e2173-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="e2173-144">Ayrıca toospecify "Doğu ABD" gibi bir yerde gerekir</span><span class="sxs-lookup"><span data-stu-id="e2173-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="e2173-145">Merhaba yeni depolama hesabı hello varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e2173-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="e2173-146">Yeni bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2173-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="e2173-147">3. adım: hello .vhd dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e2173-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="e2173-148">Kullanım hello [Ekle AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span><span class="sxs-lookup"><span data-stu-id="e2173-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="e2173-149">Merhaba önceki adımda kullanılan hello Azure PowerShell penceresi türü hello aşağıdaki komut ve hello değişkenleri değiştirin &lsaquo; köşeli &rsaquo; kendi bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="e2173-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="e2173-150">4. adım: hello görüntü tooyour özel resimler listesi ekleme</span><span class="sxs-lookup"><span data-stu-id="e2173-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="e2173-151">Kullanım hello [Ekle AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello görüntü toohello listesi özel görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e2173-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="e2173-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2173-152">Next steps</span></span>
<span data-ttu-id="e2173-153">Artık [özel bir VM oluşturma](createportal.md) hello kullanarak karşıya görüntü.</span><span class="sxs-lookup"><span data-stu-id="e2173-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
