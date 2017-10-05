---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - REST API'si ile ağ güvenliği çözümleme | Microsoft Docs"
description: "Bu makalede PowerShell güvenlik grubu görünümü ile sanal makineleri güvenliği çözümlemek için nasıl kullanılacağını anlatmaktadır."
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
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="695fb-103">Güvenlik grubu REST API kullanarak görünümü ile sanal makine güvenliğinizi Çözümle</span><span class="sxs-lookup"><span data-stu-id="695fb-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="695fb-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="695fb-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="695fb-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="695fb-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="695fb-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="695fb-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="695fb-107">REST API</span><span class="sxs-lookup"><span data-stu-id="695fb-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="695fb-108">Güvenlik grubu görünümü bir sanal makineye uygulanan yapılandırılmış ve etkili ağ güvenlik kuralları döndürür.</span><span class="sxs-lookup"><span data-stu-id="695fb-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="695fb-109">Bu denetim ve ağ güvenlik grupları ve trafik yükleniyor emin olmak için bir VM üzerinde yapılandırılmış kurallarını tanılamak yararlı bir yetenektir doğru şekilde izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="695fb-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="695fb-110">Bu makalede, sizi, REST API kullanarak bir sanal makine için etkili ve uygulanan güvenlik kuralları nasıl alınacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="695fb-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="695fb-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="695fb-111">Before you begin</span></span>

<span data-ttu-id="695fb-112">Bu senaryoda, bir sanal makine için güvenlik grubu görünümü almak için Ağ İzleyicisi Rest API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="695fb-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="695fb-113">ARMclient PowerShell kullanarak REST API'sini çağırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="695fb-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="695fb-114">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="695fb-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="695fb-115">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="695fb-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="695fb-116">Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="695fb-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="695fb-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="695fb-117">Scenario</span></span>

<span data-ttu-id="695fb-118">Bu makalede ele alınan senaryo, belirli bir sanal makine için etkili ve uygulanan güvenlik kurallarını alır.</span><span class="sxs-lookup"><span data-stu-id="695fb-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="695fb-119">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="695fb-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="695fb-120">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="695fb-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="695fb-121">Aşağıdaki kod, sanal machineThe döndürmek için aşağıdaki betiği çalıştırın değişkenleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="695fb-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="695fb-122">**Subscriptionıd** -abonelik kimliği ile aynı zamanda alınabilir **Get-AzureRMSubscription** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="695fb-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="695fb-123">**resourceGroupName** -sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="695fb-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="695fb-124">Gerekli bilgileri **kimliği** türü'nün altında `Microsoft.Compute/virtualMachines` aşağıdaki örnekte görüldüğü gibi yanıt:</span><span class="sxs-lookup"><span data-stu-id="695fb-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

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

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="695fb-125">Sanal makine için güvenlik grubu görünümü Al</span><span class="sxs-lookup"><span data-stu-id="695fb-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="695fb-126">Aşağıdaki örnek, hedeflenen bir sanal makinenin güvenlik grubu görünümü ister.</span><span class="sxs-lookup"><span data-stu-id="695fb-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="695fb-127">Bu örnek sonuçlarından kurallara ve yapılandırma değişikliklerini aramak için oluşturulma tarafından tanımlanan güvenlik karşılaştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="695fb-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

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

## <a name="view-the-response"></a><span data-ttu-id="695fb-128">Yanıtı görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="695fb-128">View the response</span></span>

<span data-ttu-id="695fb-129">Aşağıdaki örnek, önceki komuttan döndürülen yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="695fb-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="695fb-130">Gruplar halinde ayrılmış sanal makine üzerinde etkili ve uygulanan güvenlik kuralları sonuçları göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="695fb-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="695fb-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="695fb-131">Next steps</span></span>

<span data-ttu-id="695fb-132">Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-security-group-view-powershell.md) ağ güvenlik grupları doğrulanması otomatikleştirmek öğrenmek için.</span><span class="sxs-lookup"><span data-stu-id="695fb-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


