---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - REST API ile aaaAnalyze ağ güvenliği | Microsoft Docs"
description: "Bu makalede, güvenlik grubu görünümü ile güvenliği nasıl toouse PowerShell tooanalyze sanal bir makine anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="a70c5-103">Güvenlik grubu REST API kullanarak görünümü ile sanal makine güvenliğinizi Çözümle</span><span class="sxs-lookup"><span data-stu-id="a70c5-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a70c5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a70c5-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="a70c5-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a70c5-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="a70c5-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a70c5-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="a70c5-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a70c5-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="a70c5-108">Güvenlik grubu görünümü uygulanan tooa sanal makine yapılandırılmış ve etkili ağ güvenlik kuralları döndürür.</span><span class="sxs-lookup"><span data-stu-id="a70c5-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="a70c5-109">Bu özellik kullanışlı tooaudit ve ağ güvenlik grupları tanılama ve bir VM tooensure trafiğinde yapılandırılmış kuralları yükleniyor doğru şekilde izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="a70c5-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="a70c5-110">Bu makalede, REST API kullanarak tooa sanal makine nasıl tooretrieve hello etkili ve uygulanan güvenlik kuralları gösteriyoruz</span><span class="sxs-lookup"><span data-stu-id="a70c5-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a70c5-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a70c5-111">Before you begin</span></span>

<span data-ttu-id="a70c5-112">Bu senaryoda, bir sanal makine için hello Ağ İzleyicisi Rest API'si tooget hello güvenlik grubu görünümü çağırın.</span><span class="sxs-lookup"><span data-stu-id="a70c5-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="a70c5-113">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="a70c5-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="a70c5-114">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="a70c5-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a70c5-115">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="a70c5-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a70c5-116">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="a70c5-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a70c5-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="a70c5-117">Scenario</span></span>

<span data-ttu-id="a70c5-118">Bu makalede ele alınan hello senaryo hello etkili ve uygulanan güvenlik kuralları belirli bir sanal makine için alır.</span><span class="sxs-lookup"><span data-stu-id="a70c5-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a70c5-119">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="a70c5-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="a70c5-120">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="a70c5-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="a70c5-121">Komut dosyası tooreturn sanal machineThe aşağıdaki hello çalıştırmak kod aşağıdaki değişkenleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a70c5-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="a70c5-122">**Subscriptionıd** -hello abonelik kimliği ile Merhaba da alınabilir **Get-AzureRMSubscription** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a70c5-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="a70c5-123">**resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="a70c5-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="a70c5-124">Merhaba gerekli bilgileri olduğu hello **kimliği** hello türü altında `Microsoft.Compute/virtualMachines` hello aşağıdaki örnekte görüldüğü gibi yanıt:</span><span class="sxs-lookup"><span data-stu-id="a70c5-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="a70c5-125">Sanal makine için güvenlik grubu görünümü Al</span><span class="sxs-lookup"><span data-stu-id="a70c5-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="a70c5-126">Aşağıdaki örnek hello hello güvenlik grubu görünümü hedeflenen bir sanal makinenin ister.</span><span class="sxs-lookup"><span data-stu-id="a70c5-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="a70c5-127">Bu örnek Hello sonuçlarından kullanılan toocompare toohello kuralları ve yapılandırma değişikliklerini hello oluşturulma toolook tarafından tanımlanan güvenlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="a70c5-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a><span data-ttu-id="a70c5-128">Merhaba yanıtı görüntüle</span><span class="sxs-lookup"><span data-stu-id="a70c5-128">View hello response</span></span>

<span data-ttu-id="a70c5-129">Aşağıdaki örnek hello komutu önceki hello döndürülen hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="a70c5-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="a70c5-130">Merhaba sonuçları tüm hello etkili ve uygulanan güvenlik kuralları hello sanal makineye gruplar halinde ayrıntılarıyla Göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="a70c5-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a70c5-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a70c5-131">Next steps</span></span>

<span data-ttu-id="a70c5-132">Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-security-group-view-powershell.md) toolearn nasıl tooautomate doğrulama ağ güvenlik grupları.</span><span class="sxs-lookup"><span data-stu-id="a70c5-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


