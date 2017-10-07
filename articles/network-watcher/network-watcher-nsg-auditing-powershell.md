---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü ile NSG aaaAutomate denetim | Microsoft Docs"
description: "Bu sayfa hakkında yönergeler sağlar. bir ağ güvenlik grubunun tooconfigure denetleme"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Azure Ağ İzleyicisi güvenlik grubu görünümü ile NSG denetim otomatikleştirme

Müşteriler genellikle altyapılarını hello güvenlik duruşunu doğrulama hello sınama ile karşı karşıya kalmaktadır. Bu sorunu Azure Vm'leri için farklı değildir. Benzer bir güvenlik profili uygulanan hello ağ güvenlik grubu (NSG) kurallara göre önemli toohave olur. Merhaba güvenlik grubu görünümü kullanarak, şimdi uygulanan kurallar tooa bir NSG içinde VM hello listesini elde edebilirsiniz. Altın NSG güvenlik profili tanımlamak ve güvenlik grubu görünümü haftalık bir tempoyla üzerinde başlatmak ve hello çıktı toohello altın profili karşılaştırın ve bir rapor oluşturun. Bu şekilde güvenlik profili belirlenen toohello uymayan tüm hello VM'ler kolayca tanımlayabilirsiniz.

Ağ güvenlik gruplarıyla tanımıyorsanız ziyaret [ağ güvenliğine genel bakış](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, bir bilinen iyi temel toohello güvenlik grubu karşılaştırmak için bir sanal makine döndürülen sonuçları görüntüleyin.

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo hello güvenlik grubu görünümü bir sanal makine için alır.

Bu senaryoda, şunları yapacaksınız:

- Bilinen iyi kural kümesini Al
- Rest API sahip bir sanal makine alma
- Sanal makine için güvenlik grubu görünümü Al
- Yanıt değerlendir

## <a name="retrieve-rule-set"></a>Kural kümesini Al

Bu örnekte Hello ilk adımı, var olan bir taban çizgisi toowork oluşturur. Merhaba aşağıdaki örnekte olduğu bir mevcut ağ güvenlik hello kullanarak grubundan ayıklanan bazı json `Get-AzureRmNetworkSecurityGroup` hello taban çizgisi olarak bu örnek için kullanılan cmdlet.

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a>Kural kümesi tooPowerShell nesneleri dönüştürme

Bu adımda, biz Bu örnek için ağ güvenlik grubu hello üzerinde beklenen toobe hello kurallar ile daha önce oluşturulmuş bir json dosyası okur.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Ağ İzleyicisi alma

Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir. Merhaba `$networkWatcher` değişkeni toohello geçirilen `AzureRmNetworkWatcherSecurityGroupView` cmdlet'i.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>VM Al

Gerekli toorun hello bir sanal makinedir `Get-AzureRmNetworkWatcherSecurityGroupView` karşı cmdlet'i. Aşağıdaki örnek hello VM nesnesini alır.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Güvenlik grubu görünümü alma

Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır. Daha önce gösterilen karşılaştırılan toohello "temel" json sonucudur.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Merhaba sonuçlarını çözümleme

Merhaba yanıt ağ arabirimleri tarafından gruplandırılır. Merhaba farklı tür döndürülen kuralların etkili olur ve güvenlik kuralları varsayılan. Merhaba sonuç daha fazla nasıl, bir alt ağ veya bir sanal NIC uygulandığı tarafından ayrılmıştır

Merhaba aşağıdaki PowerShell betiğini hello güvenlik grubu görünümü tooan varolan çıktısı bir NSG hello sonuçlarını karşılaştırır. Merhaba aşağıdaki örnekte nasıl hello sonuçları ile karşılaştırılabilir bir basit örneğidir `Compare-Object` cmdlet'i.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Aşağıdaki örnek hello hello sonucudur. İki hello ilk kural kümesinde olan hello kuralları hello Karşılaştırmada mevcut değil görebilirsiniz.

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a>Sonraki adımlar

Ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.













