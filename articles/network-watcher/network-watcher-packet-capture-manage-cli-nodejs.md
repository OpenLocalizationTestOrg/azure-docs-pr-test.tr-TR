---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - Azure CLI 1.0 | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama özelliği ağ Azure CLI 1.0 kullanarak izleyicisinin açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Paket yakalama Azure CLI 1.0 kullanarak Azure Ağ İzleyicisi ile yönetme

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API'si](network-watcher-packet-capture-manage-rest.md)

Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar. Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır. Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur. Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir. Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.

Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.

Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.

- [**Paket yakalama Başlat**](#start-a-packet-capture)
- [**Paket yakalama işlemini durdurun**](#stop-a-packet-capture)
- [**Paket yakalama Sil**](#delete-a-packet-capture)
- [**Paket yakalama indirin**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:

- Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede
- Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.

> [!IMPORTANT]
> Paket yakalama hello sanal makine üzerinde çalışan bir aracı toobe gerektirir. Merhaba Aracısı bir uzantısı olarak yüklenir. VM uzantıları hakkında yönergeler için ziyaret [sanal makine uzantıları ve özellikleri](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>VM uzantısı yükleyin

### <a name="step-1"></a>1. Adım

Merhaba çalıştırmak `azure vm extension set` cmdlet tooinstall hello paket Yakalama aracı hello Konuk sanal makinedeki.

Windows sanal makineler için:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

Linux sanal makineleri için:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>2. Adım

Aracı hello tooensure yüklü hello çalıştırmak `vm extension get` cmdlet'i ve hello kaynak grubu ve sanal makine adı geçirin. Merhaba sonuç listesi tooensure hello aracısı yüklü olup olmadığını denetleyin.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

Aşağıdaki örnek hello hello yanıt çalışmasını örneğidir`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Paket yakalama Başlat

Merhaba önceki adımları tamamlandıktan sonra hello paket yakalama Aracısı hello sanal makineye yüklenir.

### <a name="step-1"></a>1. Adım

Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir. Bu değişken toohello geçirilen `network watcher show` 4. adımda cmdlet'i.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>2. Adım

Bir depolama hesabı alabilirsiniz. Bu depolama hesabı kullanılan toostore hello paket yakalama dosyasıdır.

```azurecli
azure storage account list
```

### <a name="step-3"></a>3. Adım

Filtreler hello paket yakalama tarafından depolanan kullanılan toolimit hello veriler olabilir. Merhaba aşağıdaki örnekte bir paket yakalama kurduğunuzda birkaç filtrelerle ayarlar.  Merhaba ilk üç filtreleri giden TCP trafiğine yalnızca yerel bir IP 10.0.0.3 toplamak 20, 80 ve 443 toodestination bağlantı noktaları.  Merhaba son filtre yalnızca UDP trafiğini toplar.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Paket yakalama için birden çok filtre tanımlanabilir. Karmaşık filtre yapısı kullanıyorsanız, bir json dosyası tooavoid sözdizimi hatalı daha iyi toouse filtreleri sayısıdır. Örneğin, hello bayrağını kullanın "-r" (yerine "-f") ve filtreleri aşağıdaki hello içeren bir json dosyası hello konumunu geçirin:

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


Merhaba aşağıdaki örnekte olduğu hello çalışmasını hello beklenen çıktı `network watcher packet-capture create` cmdlet'i.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>Paket yakalama Al

Merhaba çalıştıran `network watcher packet-capture show` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama hello durumunu alır.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

Merhaba aşağıdaki örnekte olduğu hello hello çıktısını `network watcher packet-capture show` cmdlet'i. Merhaba yakalama işlemi tamamlandıktan sonra hello aşağıdaki örnektir. StopReason TimeExceeded ile Merhaba PacketCaptureStatus değer durdurulmuş. Bu değer hello paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>Paket yakalama işlemini durdurun

Merhaba çalıştırarak `network watcher packet-capture stop` yakalama oturumu Sürüyor ise cmdlet durduruldu.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Hello cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.

## <a name="delete-a-packet-capture"></a>Paket yakalama Sil

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
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

Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
