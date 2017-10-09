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
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>Paket yakalama PowerShell kullanarak Azure Ağ İzleyicisi ile yönetme

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API'si](network-watcher-packet-capture-manage-rest.md)

Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar. Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır. Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur. Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir. Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.

Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.

- [**Paket yakalama Başlat**](#start-a-packet-capture)
- [**Paket yakalama işlemini durdurun**](#stop-a-packet-capture)
- [**Paket yakalama Sil**](#delete-a-packet-capture)
- [**Paket yakalama indirin**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:

* Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede

* Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.

> [!IMPORTANT]
> Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`. Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>VM uzantısı yükleyin

### <a name="step-1"></a>1. Adım

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>2. Adım

Merhaba alır hello uzantısı bilgi aşağıdaki örnek gerekli toorun hello `Set-AzureRmVMExtension` cmdlet'i. Bu cmdlet hello paket Yakalama aracı hello Konuk sanal makineye yükler.

> [!NOTE]
> Merhaba `Set-AzureRmVMExtension` cmdlet, birkaç dakika toocomplete alabilir.

Windows sanal makineler için:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

Linux sanal makineleri için:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

Merhaba aşağıdaki başarılı bir yanıt hello çalıştırdıktan sonra örnektir `Set-AzureRmVMExtension` cmdlet'i.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>3. Adım

Aracı hello tooensure yüklü hello çalıştırmak `Get-AzureRmVMExtension` cmdlet'i ve hello sanal makine adını ve hello uzantı adı geçirin.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

Aşağıdaki örnek hello hello yanıt çalışmasını örneğidir`Get-AzureRmVMExtension`

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

## <a name="start-a-packet-capture"></a>Paket yakalama Başlat

Merhaba önceki adımları tamamlandıktan sonra hello paket yakalama Aracısı hello sanal makineye yüklenir.

### <a name="step-1"></a>1. Adım

Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir. Bu değişken toohello geçirilen `New-AzureRmNetworkWatcherPacketCapture` 4. adımda cmdlet'i.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>2. Adım

Bir depolama hesabı alabilirsiniz. Bu depolama hesabı kullanılan toostore hello paket yakalama dosyasıdır.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>3. Adım

Filtreler hello paket yakalama tarafından depolanan kullanılan toolimit hello veriler olabilir. Merhaba aşağıdaki örnekte iki filtreleri ayarlar.  TCP Giden bir filtre toplar, 20, 80 ve 443 toodestination bağlantı noktalarını yalnızca yerel bir IP 10.0.0.3 trafiği.  Merhaba ikinci filtre yalnızca UDP trafiğini toplar.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Paket yakalama için birden çok filtre tanımlanabilir.

### <a name="step-4"></a>4. Adım

Merhaba çalıştırmak `New-AzureRmNetworkWatcherPacketCapture` adımları önceki hello alınan hello gerekli değerleri geçirme cmdlet toostart hello paket yakalama işlemi,.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

Merhaba aşağıdaki örnekte olduğu hello çalışmasını hello beklenen çıktı `New-AzureRmNetworkWatcherPacketCapture` cmdlet'i.

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

## <a name="get-a-packet-capture"></a>Paket yakalama Al

Merhaba çalıştıran `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama hello durumunu alır.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

Merhaba aşağıdaki örnekte olduğu hello hello çıktısını `Get-AzureRmNetworkWatcherPacketCapture` cmdlet'i. Merhaba yakalama işlemi tamamlandıktan sonra hello aşağıdaki örnektir. StopReason TimeExceeded ile Merhaba PacketCaptureStatus değer durdurulmuş. Bu değer hello paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.
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

## <a name="stop-a-packet-capture"></a>Paket yakalama işlemini durdurun

Merhaba çalıştırarak `Stop-AzureRmNetworkWatcherPacketCapture` yakalama oturumu Sürüyor ise cmdlet durduruldu.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Hello cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.

## <a name="delete-a-packet-capture"></a>Paket yakalama Sil

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Paket yakalama silindiğinde hello depolama hesabındaki hello dosya silinmez.

## <a name="download-a-packet-capture"></a>Paket yakalama indirin

Paket yakalama oturumunuz tamamladıktan sonra hello yakalama dosyasını karşıya yüklenen tooblob depolama veya tooa yerel dosya hello VM üzerinde olabilir. Merhaba paket yakalama Hello depolama konumu hello oturum oluşturma sırasında tanımlanır. Bu yakalama uygun aracı tooaccess kaydedilmiş tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini dosyaları: http://storageexplorer.com/

Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Sonraki adımlar

Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)

Belirli trafik VM dışında orr içinde ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->














