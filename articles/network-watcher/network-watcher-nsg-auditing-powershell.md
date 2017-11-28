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
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="2458a-103">Azure Ağ İzleyicisi güvenlik grubu görünümü ile NSG denetim otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="2458a-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="2458a-104">Müşteriler genellikle altyapılarını hello güvenlik duruşunu doğrulama hello sınama ile karşı karşıya kalmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2458a-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="2458a-105">Bu sorunu Azure Vm'leri için farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="2458a-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="2458a-106">Benzer bir güvenlik profili uygulanan hello ağ güvenlik grubu (NSG) kurallara göre önemli toohave olur.</span><span class="sxs-lookup"><span data-stu-id="2458a-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="2458a-107">Merhaba güvenlik grubu görünümü kullanarak, şimdi uygulanan kurallar tooa bir NSG içinde VM hello listesini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2458a-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="2458a-108">Altın NSG güvenlik profili tanımlamak ve güvenlik grubu görünümü haftalık bir tempoyla üzerinde başlatmak ve hello çıktı toohello altın profili karşılaştırın ve bir rapor oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2458a-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="2458a-109">Bu şekilde güvenlik profili belirlenen toohello uymayan tüm hello VM'ler kolayca tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2458a-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="2458a-110">Ağ güvenlik gruplarıyla tanımıyorsanız ziyaret [ağ güvenliğine genel bakış](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="2458a-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2458a-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="2458a-111">Before you begin</span></span>

<span data-ttu-id="2458a-112">Bu senaryoda, bir bilinen iyi temel toohello güvenlik grubu karşılaştırmak için bir sanal makine döndürülen sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="2458a-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="2458a-113">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="2458a-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="2458a-114">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="2458a-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2458a-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="2458a-115">Scenario</span></span>

<span data-ttu-id="2458a-116">Bu makalede ele alınan hello senaryo hello güvenlik grubu görünümü bir sanal makine için alır.</span><span class="sxs-lookup"><span data-stu-id="2458a-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="2458a-117">Bu senaryoda, şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="2458a-117">In this scenario, you will:</span></span>

- <span data-ttu-id="2458a-118">Bilinen iyi kural kümesini Al</span><span class="sxs-lookup"><span data-stu-id="2458a-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="2458a-119">Rest API sahip bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="2458a-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="2458a-120">Sanal makine için güvenlik grubu görünümü Al</span><span class="sxs-lookup"><span data-stu-id="2458a-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="2458a-121">Yanıt değerlendir</span><span class="sxs-lookup"><span data-stu-id="2458a-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="2458a-122">Kural kümesini Al</span><span class="sxs-lookup"><span data-stu-id="2458a-122">Retrieve rule set</span></span>

<span data-ttu-id="2458a-123">Bu örnekte Hello ilk adımı, var olan bir taban çizgisi toowork oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2458a-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="2458a-124">Merhaba aşağıdaki örnekte olduğu bir mevcut ağ güvenlik hello kullanarak grubundan ayıklanan bazı json `Get-AzureRmNetworkSecurityGroup` hello taban çizgisi olarak bu örnek için kullanılan cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2458a-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

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

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="2458a-125">Kural kümesi tooPowerShell nesneleri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="2458a-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="2458a-126">Bu adımda, biz Bu örnek için ağ güvenlik grubu hello üzerinde beklenen toobe hello kurallar ile daha önce oluşturulmuş bir json dosyası okur.</span><span class="sxs-lookup"><span data-stu-id="2458a-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2458a-127">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="2458a-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="2458a-128">Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="2458a-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2458a-129">Merhaba `$networkWatcher` değişkeni toohello geçirilen `AzureRmNetworkWatcherSecurityGroupView` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2458a-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="2458a-130">VM Al</span><span class="sxs-lookup"><span data-stu-id="2458a-130">Get a VM</span></span>

<span data-ttu-id="2458a-131">Gerekli toorun hello bir sanal makinedir `Get-AzureRmNetworkWatcherSecurityGroupView` karşı cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2458a-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="2458a-132">Aşağıdaki örnek hello VM nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="2458a-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="2458a-133">Güvenlik grubu görünümü alma</span><span class="sxs-lookup"><span data-stu-id="2458a-133">Retrieve security group view</span></span>

<span data-ttu-id="2458a-134">Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır.</span><span class="sxs-lookup"><span data-stu-id="2458a-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="2458a-135">Daha önce gösterilen karşılaştırılan toohello "temel" json sonucudur.</span><span class="sxs-lookup"><span data-stu-id="2458a-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="2458a-136">Merhaba sonuçlarını çözümleme</span><span class="sxs-lookup"><span data-stu-id="2458a-136">Analyzing hello results</span></span>

<span data-ttu-id="2458a-137">Merhaba yanıt ağ arabirimleri tarafından gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="2458a-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="2458a-138">Merhaba farklı tür döndürülen kuralların etkili olur ve güvenlik kuralları varsayılan.</span><span class="sxs-lookup"><span data-stu-id="2458a-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="2458a-139">Merhaba sonuç daha fazla nasıl, bir alt ağ veya bir sanal NIC uygulandığı tarafından ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="2458a-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="2458a-140">Merhaba aşağıdaki PowerShell betiğini hello güvenlik grubu görünümü tooan varolan çıktısı bir NSG hello sonuçlarını karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="2458a-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="2458a-141">Merhaba aşağıdaki örnekte nasıl hello sonuçları ile karşılaştırılabilir bir basit örneğidir `Compare-Object` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2458a-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="2458a-142">Aşağıdaki örnek hello hello sonucudur.</span><span class="sxs-lookup"><span data-stu-id="2458a-142">hello following example is hello result.</span></span> <span data-ttu-id="2458a-143">İki hello ilk kural kümesinde olan hello kuralları hello Karşılaştırmada mevcut değil görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2458a-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2458a-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2458a-144">Next steps</span></span>

<span data-ttu-id="2458a-145">Ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="2458a-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













