---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - Azure CLI 2.0 ile aaaAnalyze ağ güvenliği | Microsoft Docs"
description: "Bu makalede, Azure CLI 2.0 toouse tooanalyze sanal bir güvenlik grubu görünümü ile güvenliği nasıl makineleri anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="fc51a-103">Güvenlik grubu Azure CLI 2.0 kullanarak görünümü ile sanal makine güvenliğinizi Çözümle</span><span class="sxs-lookup"><span data-stu-id="fc51a-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fc51a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc51a-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="fc51a-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fc51a-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="fc51a-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fc51a-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="fc51a-107">REST API</span><span class="sxs-lookup"><span data-stu-id="fc51a-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="fc51a-108">Güvenlik grubu görünümü uygulanan tooa sanal makine yapılandırılmış ve etkili ağ güvenlik kuralları döndürür.</span><span class="sxs-lookup"><span data-stu-id="fc51a-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="fc51a-109">Bu özellik kullanışlı tooaudit ve ağ güvenlik grupları tanılama ve bir VM tooensure trafiğinde yapılandırılmış kuralları yükleniyor doğru şekilde izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="fc51a-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="fc51a-110">Bu makalede, tooretrieve hello nasıl yapılandırılacağı ve Azure CLI kullanarak etkin güvenlik kuralları tooa sanal makine gösteriyoruz</span><span class="sxs-lookup"><span data-stu-id="fc51a-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="fc51a-111">Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc51a-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="fc51a-112">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="fc51a-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fc51a-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fc51a-113">Before you begin</span></span>

<span data-ttu-id="fc51a-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="fc51a-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="fc51a-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="fc51a-115">Scenario</span></span>

<span data-ttu-id="fc51a-116">Bu makalede ele alınan hello senaryo yapılandırılmış hello ve belirli bir sanal makine için etkili güvenlik kurallarını alır.</span><span class="sxs-lookup"><span data-stu-id="fc51a-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="fc51a-117">VM Al</span><span class="sxs-lookup"><span data-stu-id="fc51a-117">Get a VM</span></span>

<span data-ttu-id="fc51a-118">Gerekli toorun hello bir sanal makinedir `vm list` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fc51a-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="fc51a-119">Merhaba aşağıdaki komut bir kaynak grubunda hello sanal makineleri listeler:</span><span class="sxs-lookup"><span data-stu-id="fc51a-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="fc51a-120">Merhaba sanal makine öğrendikten sonra hello kullanabilirsiniz `vm show` cmdlet tooget kendi kaynak kimliği:</span><span class="sxs-lookup"><span data-stu-id="fc51a-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="fc51a-121">Güvenlik grubu görünümü alma</span><span class="sxs-lookup"><span data-stu-id="fc51a-121">Retrieve security group view</span></span>

<span data-ttu-id="fc51a-122">Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır.</span><span class="sxs-lookup"><span data-stu-id="fc51a-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="fc51a-123">Merhaba sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="fc51a-123">Viewing hello results</span></span>

<span data-ttu-id="fc51a-124">Merhaba aşağıdaki kısaltılmış bir yanıt döndürdü hello sonuçlarının bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="fc51a-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="fc51a-125">Merhaba sonuçları tüm hello etkili ve uygulanan güvenlik kuralları hello sanal makineye gruplar halinde ayrıntılarıyla Göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="fc51a-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="fc51a-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc51a-126">Next steps</span></span>

<span data-ttu-id="fc51a-127">Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md) toolearn nasıl tooautomate doğrulama ağ güvenlik grupları.</span><span class="sxs-lookup"><span data-stu-id="fc51a-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="fc51a-128">Şu adresi ziyaret ederek uygulanan tooyour ağ kaynaklarına olan hello güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fc51a-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
