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
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="495a8-103">Güvenlik grubu PowerShell kullanarak görünümü ile sanal makine güvenliğinizi Çözümle</span><span class="sxs-lookup"><span data-stu-id="495a8-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="495a8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="495a8-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="495a8-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="495a8-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="495a8-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="495a8-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="495a8-107">REST API</span><span class="sxs-lookup"><span data-stu-id="495a8-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="495a8-108">Güvenlik grubu görünümü uygulanan tooa sanal makine yapılandırılmış ve etkili ağ güvenlik kuralları döndürür.</span><span class="sxs-lookup"><span data-stu-id="495a8-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="495a8-109">Bu özellik kullanışlı tooaudit ve ağ güvenlik grupları tanılama ve bir VM tooensure trafiğinde yapılandırılmış kuralları yükleniyor doğru şekilde izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="495a8-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="495a8-110">Bu makalede, tooretrieve hello nasıl yapılandırılacağı ve PowerShell kullanarak etkin güvenlik kuralları tooa sanal makine gösteriyoruz</span><span class="sxs-lookup"><span data-stu-id="495a8-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="495a8-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="495a8-111">Before you begin</span></span>

<span data-ttu-id="495a8-112">Bu senaryoda, çalıştırdığınız hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello güvenlik kuralı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="495a8-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="495a8-113">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="495a8-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="495a8-114">Senaryo</span><span class="sxs-lookup"><span data-stu-id="495a8-114">Scenario</span></span>

<span data-ttu-id="495a8-115">Bu makalede ele alınan hello senaryo yapılandırılmış hello ve belirli bir sanal makine için etkili güvenlik kurallarını alır.</span><span class="sxs-lookup"><span data-stu-id="495a8-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="495a8-116">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="495a8-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="495a8-117">Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="495a8-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="495a8-118">Bu değişken toohello geçirilen `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="495a8-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="495a8-119">VM Al</span><span class="sxs-lookup"><span data-stu-id="495a8-119">Get a VM</span></span>

<span data-ttu-id="495a8-120">Gerekli toorun hello bir sanal makinedir `Get-AzureRmNetworkWatcherSecurityGroupView` karşı cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="495a8-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="495a8-121">Aşağıdaki örnek hello VM nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="495a8-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="495a8-122">Güvenlik grubu görünümü alma</span><span class="sxs-lookup"><span data-stu-id="495a8-122">Retrieve security group view</span></span>

<span data-ttu-id="495a8-123">Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır.</span><span class="sxs-lookup"><span data-stu-id="495a8-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="495a8-124">Merhaba sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="495a8-124">Viewing hello results</span></span>

<span data-ttu-id="495a8-125">Merhaba aşağıdaki kısaltılmış bir yanıt döndürdü hello sonuçlarının bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="495a8-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="495a8-126">Merhaba sonuçları tüm hello etkili ve uygulanan güvenlik kuralları hello sanal makineye gruplar halinde ayrıntılarıyla Göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="495a8-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="495a8-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="495a8-127">Next steps</span></span>

<span data-ttu-id="495a8-128">Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md) toolearn nasıl tooautomate doğrulama ağ güvenlik grupları.</span><span class="sxs-lookup"><span data-stu-id="495a8-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


