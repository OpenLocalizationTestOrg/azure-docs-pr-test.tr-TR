---
title: "aaaCreate ve bir Azure sanal makine kullanarak C# yönetme | Microsoft Docs"
description: "C# ve Azure Resource Manager toodeploy bir sanal makine ve tüm destekleyici kaynakları kullanın."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="bd5f8-103">Oluşturma ve C# kullanarak azure'da Windows sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="bd5f8-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="bd5f8-104">Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="bd5f8-105">Bu makalede, oluşturma, yönetme ve C# kullanarak VM kaynakları silme yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="bd5f8-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd5f8-107">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="bd5f8-108">Merhaba paketini yükle</span><span class="sxs-lookup"><span data-stu-id="bd5f8-108">Install hello package</span></span>
> * <span data-ttu-id="bd5f8-109">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="bd5f8-109">Create credentials</span></span>
> * <span data-ttu-id="bd5f8-110">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-110">Create resources</span></span>
> * <span data-ttu-id="bd5f8-111">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="bd5f8-111">Perform management tasks</span></span>
> * <span data-ttu-id="bd5f8-112">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="bd5f8-112">Delete resources</span></span>
> * <span data-ttu-id="bd5f8-113">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd5f8-113">Run hello application</span></span>

<span data-ttu-id="bd5f8-114">Bu adımları toodo yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="bd5f8-115">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="bd5f8-116">Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="bd5f8-117">Seçin **.NET masaüstü geliştirme** üzerinde iş yükleri sayfa hello ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="bd5f8-118">Hello Özet, görebilirsiniz **.NET Framework 4-4.6 geliştirme araçları** sizin için otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="bd5f8-119">Visual Studio'nun zaten yüklediyseniz, hello .NET iş yükü hello Visual Studio Başlatıcısı kullanarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="bd5f8-120">Visual Studio'da sırasıyla **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="bd5f8-121">İçinde **şablonları** > **Visual C#**seçin **konsol uygulaması (.NET Framework)**, girin *myDotnetProject* hello adı için Merhaba proje, select hello hello proje konumunu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="bd5f8-122">Merhaba paketini yükle</span><span class="sxs-lookup"><span data-stu-id="bd5f8-122">Install hello package</span></span>

<span data-ttu-id="bd5f8-123">NuGet paketlerini hello kolay şekilde tooinstall hello kitaplıkları adımları toofinish ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="bd5f8-124">Visual Studio'da gereksinim tooget hello kitaplıkları adımları yapın:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="bd5f8-125">Tıklatın **Araçları** > **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="bd5f8-126">Merhaba konsolunda aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="bd5f8-127">Kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="bd5f8-127">Create credentials</span></span>

<span data-ttu-id="bd5f8-128">Bu adım başlamadan önce erişim tooan sahip olduğunuzdan emin olun [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="bd5f8-129">Ayrıca bir sonraki adımda hello uygulama kimliği, hello kimlik doğrulama anahtarı ve ihtiyacınız hello Kiracı kimliği kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="bd5f8-130">Merhaba yetkilendirme dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-130">Create hello authorization file</span></span>

1. <span data-ttu-id="bd5f8-131">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="bd5f8-132">Ad hello dosyası *azureauth.properties*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="bd5f8-133">Bu yetkilendirme özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="bd5f8-134">Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  hello Active Directory uygulaması ile tanımlayıcı,  **&lt;kimlik doğrulama anahtarı&gt;**  hello uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  hello Kiracı tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="bd5f8-135">Merhaba azureauth.properties dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="bd5f8-136">Bir ortam değişkeni, oluşturduğunuz hello tam yolu tooauthorization dosyasıyla AZURE_AUTH_LOCATION adlı Windows ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="bd5f8-137">Örneğin, aşağıdaki PowerShell komutunu hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="bd5f8-138">Merhaba yönetim istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-138">Create hello management client</span></span>

1. <span data-ttu-id="bd5f8-139">Oluşturduğunuz hello projesi için Hello Program.cs dosyasını açın ve bunlar hello dosyasının üst kısmında using deyimleri toohello varolan deyimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="bd5f8-140">toocreate hello yönetim istemcisi, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="bd5f8-141">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="bd5f8-142">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="bd5f8-142">Create hello resource group</span></span>

<span data-ttu-id="bd5f8-143">Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="bd5f8-144">toospecify değerleri hello uygulama ve hello kaynak grubu oluşturun, bu kodu toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="bd5f8-145">Merhaba kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="bd5f8-145">Create hello availability set</span></span>

<span data-ttu-id="bd5f8-146">[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) sizin için toomaintain hello sanal makineler, uygulamanız tarafından kullanılan kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="bd5f8-147">toocreate hello kullanılabilirlik kümesi, bu kodu toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="bd5f8-148">Merhaba ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="bd5f8-148">Create hello public IP address</span></span>

<span data-ttu-id="bd5f8-149">A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello sanal makineyle gerekli toocommunicate değil.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="bd5f8-150">toocreate hello hello sanal makine için genel IP adresi bu kodu toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="bd5f8-151">Merhaba sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-151">Create hello virtual network</span></span>

<span data-ttu-id="bd5f8-152">Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="bd5f8-153">alt ağ a toocreate ve bir sanal ağ, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="bd5f8-154">Merhaba ağ arabirimi oluştur</span><span class="sxs-lookup"><span data-stu-id="bd5f8-154">Create hello network interface</span></span>

<span data-ttu-id="bd5f8-155">Bir sanal makine bir ağ arabirimi toocommunicate hello sanal ağda gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="bd5f8-156">toocreate bir ağ arabirimi, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-156">toocreate a network interface, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="bd5f8-157">Merhaba sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-157">Create hello virtual machine</span></span>

<span data-ttu-id="bd5f8-158">Kaynakları destekleyen tüm hello oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="bd5f8-159">toocreate Merhaba sanal makine, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="bd5f8-160">Bu öğretici hello Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="bd5f8-161">diğer görüntüleri seçme hakkında daha fazla toolearn bkz [erişin ve seçin, Windows PowerShell ve Azure CLI hello Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="bd5f8-162">Varolan bir diski bir Market görüntüsü yerine toouse istiyorsanız, bu kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="bd5f8-163">Yönetim görevlerini gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="bd5f8-163">Perform management tasks</span></span>

<span data-ttu-id="bd5f8-164">Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="bd5f8-165">Ayrıca, toocreate, kod tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="bd5f8-166">Merhaba VM ile herhangi bir şey toodo gerektiğinde, tooget bir örneği gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="bd5f8-167">Merhaba VM hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="bd5f8-167">Get information about hello VM</span></span>

<span data-ttu-id="bd5f8-168">Merhaba sanal makine tooget bilgilerini bu kodu toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="bd5f8-169">Merhaba VM Durdur</span><span class="sxs-lookup"><span data-stu-id="bd5f8-169">Stop hello VM</span></span>

<span data-ttu-id="bd5f8-170">Bir sanal makineyi durdurmak ve tüm ayarları korumak, ancak toobe için sizden ücret veya bir sanal makineyi durdurun ve bunu serbest bırakma devam edin.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="bd5f8-171">Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="bd5f8-172">Bu, serbest bırakma olmadan toostop hello sanal makine bu kodu toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="bd5f8-173">Toodeallocate hello sanal makine istiyorsanız hello kapalı çağrısı toothis kodu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="bd5f8-174">Merhaba VM Başlat</span><span class="sxs-lookup"><span data-stu-id="bd5f8-174">Start hello VM</span></span>

<span data-ttu-id="bd5f8-175">toostart Merhaba sanal makine, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="bd5f8-176">Merhaba VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="bd5f8-176">Resize hello VM</span></span>

<span data-ttu-id="bd5f8-177">Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="bd5f8-178">Daha fazla bilgi için bkz: [VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="bd5f8-179">toochange boyutunu hello sanal makine, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="bd5f8-180">Bir veri diski toohello VM ekleme</span><span class="sxs-lookup"><span data-stu-id="bd5f8-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="bd5f8-181">tooadd bir veri diski toohello sanal makine bu kodu toohello ana yöntemi tooadd han 0 ve ReadWrite önbelleğe alma türü bir LUN boyutu 2 GB olan bir veri diski ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="bd5f8-182">Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="bd5f8-182">Delete resources</span></span>

<span data-ttu-id="bd5f8-183">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan iyi bir uygulama toodelete kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="bd5f8-184">Toodelete hello sanal makinelerin istediğiniz ve kaynakları destekleyen tüm hello tüm toodo varsa silme hello kaynak grubudur.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="bd5f8-185">toodelete hello kaynak grubu, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd5f8-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="bd5f8-186">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd5f8-186">Run hello application</span></span>

<span data-ttu-id="bd5f8-187">Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="bd5f8-188">toorun hello konsol uygulaması tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="bd5f8-189">Tuşuna önce **Enter** toostart silme kaynakları, birkaç dakika sürebilir hello kaynak tooverify hello oluşturmayı hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="bd5f8-190">Merhaba dağıtım durumu toosee hello dağıtım bilgilerini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bd5f8-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd5f8-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd5f8-191">Next steps</span></span>
* <span data-ttu-id="bd5f8-192">Merhaba bilgileri kullanarak bir sanal makine şablonu toocreate kullanma avantajından yararlanmak [C# ve Resource Manager şablonu kullanarak bir Azure sanal makine dağıtma](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="bd5f8-193">Merhaba kullanma hakkında daha fazla bilgi edinin [.NET için Azure kitaplıkları](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="bd5f8-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

