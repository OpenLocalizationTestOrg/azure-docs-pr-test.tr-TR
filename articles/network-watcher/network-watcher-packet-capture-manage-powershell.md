---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - PowerShell | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama Ağ İzleyicisi'ni PowerShell kullanarak özelliğini açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="153a5-103">Paket yakalama PowerShell kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="153a5-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="153a5-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="153a5-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="153a5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="153a5-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="153a5-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="153a5-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="153a5-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="153a5-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="153a5-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="153a5-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="153a5-109">Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar.</span><span class="sxs-lookup"><span data-stu-id="153a5-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="153a5-110">Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="153a5-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="153a5-111">Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="153a5-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="153a5-112">Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="153a5-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="153a5-113">Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="153a5-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="153a5-114">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.</span><span class="sxs-lookup"><span data-stu-id="153a5-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="153a5-115">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="153a5-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="153a5-116">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="153a5-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="153a5-117">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="153a5-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="153a5-118">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="153a5-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="153a5-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="153a5-119">Before you begin</span></span>

<span data-ttu-id="153a5-120">Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="153a5-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="153a5-121">Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede</span><span class="sxs-lookup"><span data-stu-id="153a5-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="153a5-122">Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.</span><span class="sxs-lookup"><span data-stu-id="153a5-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="153a5-123">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="153a5-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="153a5-124">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="153a5-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="153a5-125">VM uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="153a5-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="153a5-126">1. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="153a5-127">2. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-127">Step 2</span></span>

<span data-ttu-id="153a5-128">Merhaba alır hello uzantısı bilgi aşağıdaki örnek gerekli toorun hello `Set-AzureRmVMExtension` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="153a5-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="153a5-129">Bu cmdlet hello paket Yakalama aracı hello Konuk sanal makineye yükler.</span><span class="sxs-lookup"><span data-stu-id="153a5-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="153a5-130">Merhaba `Set-AzureRmVMExtension` cmdlet, birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="153a5-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="153a5-131">Windows sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="153a5-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="153a5-132">Linux sanal makineleri için:</span><span class="sxs-lookup"><span data-stu-id="153a5-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="153a5-133">Merhaba aşağıdaki başarılı bir yanıt hello çalıştırdıktan sonra örnektir `Set-AzureRmVMExtension` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="153a5-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="153a5-134">3. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-134">Step 3</span></span>

<span data-ttu-id="153a5-135">Aracı hello tooensure yüklü hello çalıştırmak `Get-AzureRmVMExtension` cmdlet'i ve hello sanal makine adını ve hello uzantı adı geçirin.</span><span class="sxs-lookup"><span data-stu-id="153a5-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="153a5-136">Aşağıdaki örnek hello hello yanıt çalışmasını örneğidir`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="153a5-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="153a5-137">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="153a5-137">Start a packet capture</span></span>

<span data-ttu-id="153a5-138">Merhaba önceki adımları tamamlandıktan sonra hello paket yakalama Aracısı hello sanal makineye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="153a5-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="153a5-139">1. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-139">Step 1</span></span>

<span data-ttu-id="153a5-140">Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="153a5-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="153a5-141">Bu değişken toohello geçirilen `New-AzureRmNetworkWatcherPacketCapture` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="153a5-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="153a5-142">2. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-142">Step 2</span></span>

<span data-ttu-id="153a5-143">Bir depolama hesabı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="153a5-143">Retrieve a storage account.</span></span> <span data-ttu-id="153a5-144">Bu depolama hesabı kullanılan toostore hello paket yakalama dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="153a5-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="153a5-145">3. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-145">Step 3</span></span>

<span data-ttu-id="153a5-146">Filtreler hello paket yakalama tarafından depolanan kullanılan toolimit hello veriler olabilir.</span><span class="sxs-lookup"><span data-stu-id="153a5-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="153a5-147">Merhaba aşağıdaki örnekte iki filtreleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="153a5-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="153a5-148">TCP Giden bir filtre toplar, 20, 80 ve 443 toodestination bağlantı noktalarını yalnızca yerel bir IP 10.0.0.3 trafiği.</span><span class="sxs-lookup"><span data-stu-id="153a5-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="153a5-149">Merhaba ikinci filtre yalnızca UDP trafiğini toplar.</span><span class="sxs-lookup"><span data-stu-id="153a5-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="153a5-150">Paket yakalama için birden çok filtre tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="153a5-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="153a5-151">4. Adım</span><span class="sxs-lookup"><span data-stu-id="153a5-151">Step 4</span></span>

<span data-ttu-id="153a5-152">Merhaba çalıştırmak `New-AzureRmNetworkWatcherPacketCapture` adımları önceki hello alınan hello gerekli değerleri geçirme cmdlet toostart hello paket yakalama işlemi,.</span><span class="sxs-lookup"><span data-stu-id="153a5-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="153a5-153">Merhaba aşağıdaki örnekte olduğu hello çalışmasını hello beklenen çıktı `New-AzureRmNetworkWatcherPacketCapture` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="153a5-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="153a5-154">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="153a5-154">Get a packet capture</span></span>

<span data-ttu-id="153a5-155">Merhaba çalıştıran `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama hello durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="153a5-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="153a5-156">Merhaba aşağıdaki örnekte olduğu hello hello çıktısını `Get-AzureRmNetworkWatcherPacketCapture` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="153a5-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="153a5-157">Merhaba yakalama işlemi tamamlandıktan sonra hello aşağıdaki örnektir.</span><span class="sxs-lookup"><span data-stu-id="153a5-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="153a5-158">StopReason TimeExceeded ile Merhaba PacketCaptureStatus değer durdurulmuş.</span><span class="sxs-lookup"><span data-stu-id="153a5-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="153a5-159">Bu değer hello paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.</span><span class="sxs-lookup"><span data-stu-id="153a5-159">This value shows that hello packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="153a5-160">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="153a5-160">Stop a packet capture</span></span>

<span data-ttu-id="153a5-161">Merhaba çalıştırarak `Stop-AzureRmNetworkWatcherPacketCapture` yakalama oturumu Sürüyor ise cmdlet durduruldu.</span><span class="sxs-lookup"><span data-stu-id="153a5-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="153a5-162">Hello cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.</span><span class="sxs-lookup"><span data-stu-id="153a5-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="153a5-163">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="153a5-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="153a5-164">Paket yakalama silindiğinde hello depolama hesabındaki hello dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="153a5-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="153a5-165">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="153a5-165">Download a packet capture</span></span>

<span data-ttu-id="153a5-166">Paket yakalama oturumunuz tamamladıktan sonra hello yakalama dosyasını karşıya yüklenen tooblob depolama veya tooa yerel dosya hello VM üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="153a5-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="153a5-167">Merhaba paket yakalama Hello depolama konumu hello oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="153a5-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="153a5-168">Bu yakalama uygun aracı tooaccess kaydedilmiş tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini dosyaları: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="153a5-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="153a5-169">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="153a5-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="153a5-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="153a5-170">Next steps</span></span>

<span data-ttu-id="153a5-171">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="153a5-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="153a5-172">Belirli trafik VM dışında orr içinde ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="153a5-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














