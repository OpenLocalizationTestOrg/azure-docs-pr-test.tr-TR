---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - PowerShell ile aaaAnalyze ağ güvenliği | Microsoft Docs"
description: "Bu makalede, güvenlik grubu görünümü ile güvenliği nasıl toouse PowerShell tooanalyze sanal bir makine anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a>Güvenlik grubu PowerShell kullanarak görünümü ile sanal makine güvenliğinizi Çözümle

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Güvenlik grubu görünümü uygulanan tooa sanal makine yapılandırılmış ve etkili ağ güvenlik kuralları döndürür. Bu özellik kullanışlı tooaudit ve ağ güvenlik grupları tanılama ve bir VM tooensure trafiğinde yapılandırılmış kuralları yükleniyor doğru şekilde izin verilen veya reddedilen. Bu makalede, tooretrieve hello nasıl yapılandırılacağı ve PowerShell kullanarak etkin güvenlik kuralları tooa sanal makine gösteriyoruz

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, çalıştırdığınız hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello güvenlik kuralı bilgileri.

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo yapılandırılmış hello ve belirli bir sanal makine için etkili güvenlik kurallarını alır.

## <a name="retrieve-network-watcher"></a>Ağ İzleyicisi alma

Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir. Bu değişken toohello geçirilen `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet'i.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a>VM Al

Gerekli toorun hello bir sanal makinedir `Get-AzureRmNetworkWatcherSecurityGroupView` karşı cmdlet'i. Aşağıdaki örnek hello VM nesnesini alır.

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a>Güvenlik grubu görünümü alma

Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a>Merhaba sonuçları görüntüleme

Merhaba aşağıdaki kısaltılmış bir yanıt döndürdü hello sonuçlarının bir örnektir. Merhaba sonuçları tüm hello etkili ve uygulanan güvenlik kuralları hello sanal makineye gruplar halinde ayrıntılarıyla Göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a>Sonraki adımlar

Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md) toolearn nasıl tooautomate doğrulama ağ güvenlik grupları.


