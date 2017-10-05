---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - Azure CLI 1.0 ile ağ güvenliği çözümleme | Microsoft Docs"
description: "Bu makalede, Azure CLI 1.0 güvenlik grubu görünümü ile sanal makineleri güvenliği çözümlemek için nasıl kullanılacağını anlatmaktadır."
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
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="fb577-103">Güvenlik grubu Azure CLI 1.0 kullanarak görünümü ile sanal makine güvenliğinizi Çözümle</span><span class="sxs-lookup"><span data-stu-id="fb577-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fb577-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb577-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="fb577-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fb577-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="fb577-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fb577-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="fb577-107">REST API</span><span class="sxs-lookup"><span data-stu-id="fb577-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="fb577-108">Güvenlik grubu görünümü bir sanal makineye uygulanan yapılandırılmış ve etkili ağ güvenlik kuralları döndürür.</span><span class="sxs-lookup"><span data-stu-id="fb577-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="fb577-109">Bu denetim ve ağ güvenlik grupları ve trafik yükleniyor emin olmak için bir VM üzerinde yapılandırılmış kurallarını tanılamak yararlı bir yetenektir doğru şekilde izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="fb577-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="fb577-110">Bu makalede, Azure CLI kullanarak bir sanal makine için yapılandırılmış ve etkili güvenlik kuralları almak nasıl gösteriyoruz</span><span class="sxs-lookup"><span data-stu-id="fb577-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="fb577-111">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb577-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="fb577-112">Ağ İzleyicisi, CLI desteği şu anda Azure CLI 1.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb577-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fb577-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fb577-113">Before you begin</span></span>

<span data-ttu-id="fb577-114">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="fb577-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="fb577-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="fb577-115">Scenario</span></span>

<span data-ttu-id="fb577-116">Bu makalede ele alınan senaryo, belirli bir sanal makine için yapılandırılmış ve etkili güvenlik kurallarını alır.</span><span class="sxs-lookup"><span data-stu-id="fb577-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="fb577-117">VM Al</span><span class="sxs-lookup"><span data-stu-id="fb577-117">Get a VM</span></span>

<span data-ttu-id="fb577-118">Bir sanal makineyi çalıştırmak için gerekli `vm list` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fb577-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="fb577-119">Aşağıdaki komut bir kaynak grubunda sanal machinese listeler:</span><span class="sxs-lookup"><span data-stu-id="fb577-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="fb577-120">Sanal makine öğrendikten sonra kullanabileceğiniz `vm show` kendi kaynak kimliği almak için cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fb577-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="fb577-121">Güvenlik grubu görünümü alma</span><span class="sxs-lookup"><span data-stu-id="fb577-121">Retrieve security group view</span></span>

<span data-ttu-id="fb577-122">Güvenlik grubu Görünüm sonucu almak için sonraki adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="fb577-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="fb577-123">Ekleme "--json" json sonuçları bayrağı biçimlendirecek.</span><span class="sxs-lookup"><span data-stu-id="fb577-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="fb577-124">Sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="fb577-124">Viewing the results</span></span>

<span data-ttu-id="fb577-125">Döndürülen sonuçlar kısaltılmış yanıtın örnektir.</span><span class="sxs-lookup"><span data-stu-id="fb577-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="fb577-126">Gruplar halinde ayrılmış sanal makine üzerinde etkili ve uygulanan güvenlik kuralları sonuçları göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="fb577-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="fb577-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb577-127">Next steps</span></span>

<span data-ttu-id="fb577-128">Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md) ağ güvenlik grupları doğrulanması otomatikleştirmek öğrenmek için.</span><span class="sxs-lookup"><span data-stu-id="fb577-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="fb577-129">Ağ kaynaklarınıza ziyaret ederek uygulanan güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fb577-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
