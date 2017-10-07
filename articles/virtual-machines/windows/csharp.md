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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Oluşturma ve C# kullanarak azure'da Windows sanal makineleri yönetme #

Bir [Azure sanal makine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) çeşitli destekleyici Azure kaynakları gerekir. Bu makalede, oluşturma, yönetme ve C# kullanarak VM kaynakları silme yer almaktadır. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Visual Studio projesi oluşturma
> * Merhaba paketini yükle
> * Kimlik bilgileri oluşturun
> * Kaynak oluşturma
> * Yönetim görevlerini gerçekleştirme
> * Kaynakları silin
> * Merhaba uygulamayı çalıştırın

Bu adımları toodo yaklaşık 20 dakika sürer.

## <a name="create-a-visual-studio-project"></a>Visual Studio projesi oluşturma

1. Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Seçin **.NET masaüstü geliştirme** üzerinde iş yükleri sayfa hello ve ardından **yükleme**. Hello Özet, görebilirsiniz **.NET Framework 4-4.6 geliştirme araçları** sizin için otomatik olarak seçilir. Visual Studio'nun zaten yüklediyseniz, hello .NET iş yükü hello Visual Studio Başlatıcısı kullanarak ekleyebilirsiniz.
2. Visual Studio'da sırasıyla **dosya** > **yeni** > **proje**.
3. İçinde **şablonları** > **Visual C#**seçin **konsol uygulaması (.NET Framework)**, girin *myDotnetProject* hello adı için Merhaba proje, select hello hello proje konumunu ve ardından **Tamam**.

## <a name="install-hello-package"></a>Merhaba paketini yükle

NuGet paketlerini hello kolay şekilde tooinstall hello kitaplıkları adımları toofinish ihtiyacınız var. Visual Studio'da gereksinim tooget hello kitaplıkları adımları yapın:

1. Tıklatın **Araçları** > **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.
2. Merhaba konsolunda aşağıdaki komutu yazın:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Kimlik bilgileri oluşturun

Bu adım başlamadan önce erişim tooan sahip olduğunuzdan emin olun [Active Directory hizmet asıl](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Ayrıca bir sonraki adımda hello uygulama kimliği, hello kimlik doğrulama anahtarı ve ihtiyacınız hello Kiracı kimliği kaydetmelisiniz.

### <a name="create-hello-authorization-file"></a>Merhaba yetkilendirme dosyası oluşturma

1. Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*. Ad hello dosyası *azureauth.properties*ve ardından **Ekle**.
2. Bu yetkilendirme özellikleri ekleyin:

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

    Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  hello Active Directory uygulaması ile tanımlayıcı,  **&lt;kimlik doğrulama anahtarı&gt;**  hello uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  hello Kiracı tanımlayıcı.

3. Merhaba azureauth.properties dosyasını kaydedin. 
4. Bir ortam değişkeni, oluşturduğunuz hello tam yolu tooauthorization dosyasıyla AZURE_AUTH_LOCATION adlı Windows ayarlayın. Örneğin, aşağıdaki PowerShell komutunu hello kullanılabilir:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Merhaba yönetim istemcisi oluşturma

1. Oluşturduğunuz hello projesi için Hello Program.cs dosyasını açın ve bunlar hello dosyasının üst kısmında using deyimleri toohello varolan deyimleri ekleyin:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. toocreate hello yönetim istemcisi, bu kod toohello Main yöntemi ekleyin:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Kaynak oluşturma

### <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Tüm kaynaklar içinde bulunması gereken bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).

toospecify değerleri hello uygulama ve hello kaynak grubu oluşturun, bu kodu toohello Main yöntemi ekleyin:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Merhaba kullanılabilirlik kümesi oluştur

[Kullanılabilirlik kümeleri](tutorial-availability-sets.md) sizin için toomaintain hello sanal makineler, uygulamanız tarafından kullanılan kolaylaştırır.

toocreate hello kullanılabilirlik kümesi, bu kodu toohello Main yöntemi ekleyin:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Merhaba ortak IP adresi oluştur

A [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hello sanal makineyle gerekli toocommunicate değil.

toocreate hello hello sanal makine için genel IP adresi bu kodu toohello Main yöntemi ekleyin:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Merhaba sanal ağ oluşturma

Bir sanal makine bir alt ağda olmalıdır bir [sanal ağ](../../virtual-network/virtual-networks-overview.md).

alt ağ a toocreate ve bir sanal ağ, bu kod toohello Main yöntemi ekleyin:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Merhaba ağ arabirimi oluştur

Bir sanal makine bir ağ arabirimi toocommunicate hello sanal ağda gerekir.

toocreate bir ağ arabirimi, bu kod toohello Main yöntemi ekleyin:

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

### <a name="create-hello-virtual-machine"></a>Merhaba sanal makine oluşturma

Kaynakları destekleyen tüm hello oluşturduğunuza göre bir sanal makine oluşturabilirsiniz.

toocreate Merhaba sanal makine, bu kod toohello Main yöntemi ekleyin:

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
> Bu öğretici hello Windows Server işletim sistemi sürümünü çalıştıran bir sanal makine oluşturur. diğer görüntüleri seçme hakkında daha fazla toolearn bkz [erişin ve seçin, Windows PowerShell ve Azure CLI hello Azure sanal makine görüntülerini](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Varolan bir diski bir Market görüntüsü yerine toouse istiyorsanız, bu kodu kullanın:

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

## <a name="perform-management-tasks"></a>Yönetim görevlerini gerçekleştirme

Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz. Ayrıca, toocreate, kod tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.

Merhaba VM ile herhangi bir şey toodo gerektiğinde, tooget bir örneği gerekir:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Merhaba VM hakkında bilgi edinin

Merhaba sanal makine tooget bilgilerini bu kodu toohello Main yöntemi ekleyin:

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

### <a name="stop-hello-vm"></a>Merhaba VM Durdur

Bir sanal makineyi durdurmak ve tüm ayarları korumak, ancak toobe için sizden ücret veya bir sanal makineyi durdurun ve bunu serbest bırakma devam edin. Bir sanal makine serbest bırakıldığında, kendisiyle ilişkili tüm kaynakları da deallocated ve fatura onun için edilir.

Bu, serbest bırakma olmadan toostop hello sanal makine bu kodu toohello Main yöntemi ekleyin:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Toodeallocate hello sanal makine istiyorsanız hello kapalı çağrısı toothis kodu değiştirin:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Merhaba VM Başlat

toostart Merhaba sanal makine, bu kod toohello Main yöntemi ekleyin:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Merhaba VM yeniden boyutlandırma

Dağıtım pek çok görünüşünün sanal makineniz için bir boyut karar verirken dikkate alınmalıdır. Daha fazla bilgi için bkz: [VM boyutları](sizes.md).  

toochange boyutunu hello sanal makine, bu kod toohello Main yöntemi ekleyin:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Bir veri diski toohello VM ekleme

tooadd bir veri diski toohello sanal makine bu kodu toohello ana yöntemi tooadd han 0 ve ReadWrite önbelleğe alma türü bir LUN boyutu 2 GB olan bir veri diski ekleyin:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Kaynakları silin

Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan iyi bir uygulama toodelete kaynaklarını aşıyor. Toodelete hello sanal makinelerin istediğiniz ve kaynakları destekleyen tüm hello tüm toodo varsa silme hello kaynak grubudur.

toodelete hello kaynak grubu, bu kod toohello Main yöntemi ekleyin:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer. 

1. toorun hello konsol uygulaması tıklatın **Başlat**.

2. Tuşuna önce **Enter** toostart silme kaynakları, birkaç dakika sürebilir hello kaynak tooverify hello oluşturmayı hello Azure portalı. Merhaba dağıtım durumu toosee hello dağıtım bilgilerini'ı tıklatın.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba bilgileri kullanarak bir sanal makine şablonu toocreate kullanma avantajından yararlanmak [C# ve Resource Manager şablonu kullanarak bir Azure sanal makine dağıtma](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Merhaba kullanma hakkında daha fazla bilgi edinin [.NET için Azure kitaplıkları](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

