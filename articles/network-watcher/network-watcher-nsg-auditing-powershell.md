---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü ile NSG denetim otomatikleştirmek | Microsoft Docs"
description: "Bu sayfa bir ağ güvenlik grubunun denetimi yapılandırma hakkında yönergeler sağlar"
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
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="08cb5-103">Azure Ağ İzleyicisi güvenlik grubu görünümü ile NSG denetim otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="08cb5-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="08cb5-104">Müşteriler genellikle güvenlik yaklaşımı altyapılarını, doğrulama, bir güçlükle karşı karşıya kalmaktadır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="08cb5-105">Bu sorunu Azure Vm'leri için farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="08cb5-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="08cb5-106">Uygulanan ağ güvenlik grubu (NSG) kurallara göre benzer bir güvenlik profili olması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="08cb5-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="08cb5-107">Güvenlik grubu görünümü kullanarak, bir VM bir NSG içinde uygulanan kurallar listesi şimdi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08cb5-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="08cb5-108">Bir altın NSG güvenlik profili tanımlamak ve güvenlik grubu görünümü haftalık bir tempoyla üzerinde başlatmak ve altın profili çıkışı karşılaştırın ve bir rapor oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08cb5-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="08cb5-109">Bu şekilde, önceden belirlenen güvenlik profili uymayan tüm sanal makineleri kolayca tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08cb5-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="08cb5-110">Ağ güvenlik gruplarıyla tanımıyorsanız ziyaret [ağ güvenliğine genel bakış](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="08cb5-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="08cb5-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="08cb5-111">Before you begin</span></span>

<span data-ttu-id="08cb5-112">Bu senaryoda, bir sanal makine için döndürülen güvenlik grubu görünümü sonuçları bilinen iyi taban çizgisi karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="08cb5-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="08cb5-113">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="08cb5-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="08cb5-114">Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="08cb5-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="08cb5-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="08cb5-115">Scenario</span></span>

<span data-ttu-id="08cb5-116">Bu makalede ele alınan senaryo, bir sanal makine için güvenlik grubu görünümü alır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="08cb5-117">Bu senaryoda, şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="08cb5-117">In this scenario, you will:</span></span>

- <span data-ttu-id="08cb5-118">Bilinen iyi kural kümesini Al</span><span class="sxs-lookup"><span data-stu-id="08cb5-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="08cb5-119">Rest API sahip bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="08cb5-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="08cb5-120">Sanal makine için güvenlik grubu görünümü Al</span><span class="sxs-lookup"><span data-stu-id="08cb5-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="08cb5-121">Yanıt değerlendir</span><span class="sxs-lookup"><span data-stu-id="08cb5-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="08cb5-122">Kural kümesini Al</span><span class="sxs-lookup"><span data-stu-id="08cb5-122">Retrieve rule set</span></span>

<span data-ttu-id="08cb5-123">İlk Bu örnekte varolan bir taban çizgisi ile çalışmak için adımdır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="08cb5-124">Aşağıdaki örnekte olduğu bir mevcut ağ güvenlik grubu kullanımından ayıklanan bazı json `Get-AzureRmNetworkSecurityGroup` taban çizgisi olarak bu örnek için kullanılan cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08cb5-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

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

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="08cb5-125">Kural kümesi için PowerShell nesneleri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="08cb5-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="08cb5-126">Bu adımda, biz Bu örnek için ağ güvenlik grubu olması beklenen kurallar ile daha önce oluşturulmuş bir json dosyası okur.</span><span class="sxs-lookup"><span data-stu-id="08cb5-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="08cb5-127">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="08cb5-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="08cb5-128">Ağ İzleyicisi örneği almak için sonraki adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="08cb5-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="08cb5-129">`$networkWatcher` Değişkeni iletilir `AzureRmNetworkWatcherSecurityGroupView` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="08cb5-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="08cb5-130">VM Al</span><span class="sxs-lookup"><span data-stu-id="08cb5-130">Get a VM</span></span>

<span data-ttu-id="08cb5-131">Bir sanal makineyi çalıştırmak için gerekli `Get-AzureRmNetworkWatcherSecurityGroupView` karşı cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="08cb5-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="08cb5-132">Aşağıdaki örnek, VM nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="08cb5-133">Güvenlik grubu görünümü alma</span><span class="sxs-lookup"><span data-stu-id="08cb5-133">Retrieve security group view</span></span>

<span data-ttu-id="08cb5-134">Güvenlik grubu Görünüm sonucu almak için sonraki adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="08cb5-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="08cb5-135">Bu sonuç, daha önce gösterilen "temel" json karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="08cb5-136">Sonuçlarını çözümleme</span><span class="sxs-lookup"><span data-stu-id="08cb5-136">Analyzing the results</span></span>

<span data-ttu-id="08cb5-137">Yanıt ağ arabirimleri tarafından gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="08cb5-138">Farklı tür döndürülen kuralların etkili olur ve güvenlik kuralları varsayılan.</span><span class="sxs-lookup"><span data-stu-id="08cb5-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="08cb5-139">Sonuç daha fazla nasıl, bir alt ağ veya bir sanal NIC uygulandığı tarafından ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="08cb5-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="08cb5-140">Aşağıdaki PowerShell betiğini bir NSG varolan çıktısı güvenlik grubu görünümüne sonuçlarını karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="08cb5-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="08cb5-141">Aşağıdaki örnekte nasıl sonuçları ile karşılaştırılabilir bir basit örneğidir `Compare-Object` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="08cb5-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="08cb5-142">Aşağıdaki örnek sonucudur.</span><span class="sxs-lookup"><span data-stu-id="08cb5-142">The following example is the result.</span></span> <span data-ttu-id="08cb5-143">İki ilk kuralında ayarlanan kuralların Karşılaştırmada mevcut değil görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08cb5-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="08cb5-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08cb5-144">Next steps</span></span>

<span data-ttu-id="08cb5-145">Ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olan ağ güvenlik grubu ve güvenlik kuralları izlemek için.</span><span class="sxs-lookup"><span data-stu-id="08cb5-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













