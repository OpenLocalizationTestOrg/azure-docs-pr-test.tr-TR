---
title: "Azure Ağ İzleyicisi güvenlik grubu görünümü - Azure CLI 1.0 ile aaaAnalyze ağ güvenliği | Microsoft Docs"
description: "Bu makalede, Azure CLI 1.0 toouse tooanalyze sanal bir güvenlik grubu görünümü ile güvenliği nasıl makineleri anlatmaktadır."
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="2ca76-103">Güvenlik grubu Azure CLI 1.0 kullanarak görünümü ile sanal makine güvenliğinizi Çözümle</span><span class="sxs-lookup"><span data-stu-id="2ca76-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2ca76-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ca76-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="2ca76-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2ca76-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="2ca76-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2ca76-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="2ca76-107">REST API</span><span class="sxs-lookup"><span data-stu-id="2ca76-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="2ca76-108">Güvenlik grubu görünümü uygulanan tooa sanal makine yapılandırılmış ve etkili ağ güvenlik kuralları döndürür.</span><span class="sxs-lookup"><span data-stu-id="2ca76-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="2ca76-109">Bu özellik kullanışlı tooaudit ve ağ güvenlik grupları tanılama ve bir VM tooensure trafiğinde yapılandırılmış kuralları yükleniyor doğru şekilde izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="2ca76-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="2ca76-110">Bu makalede, tooretrieve hello nasıl yapılandırılacağı ve Azure CLI kullanarak etkin güvenlik kuralları tooa sanal makine gösteriyoruz</span><span class="sxs-lookup"><span data-stu-id="2ca76-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="2ca76-111">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ca76-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="2ca76-112">Ağ İzleyicisi, CLI desteği şu anda Azure CLI 1.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ca76-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2ca76-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="2ca76-113">Before you begin</span></span>

<span data-ttu-id="2ca76-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="2ca76-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="2ca76-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="2ca76-115">Scenario</span></span>

<span data-ttu-id="2ca76-116">Bu makalede ele alınan hello senaryo yapılandırılmış hello ve belirli bir sanal makine için etkili güvenlik kurallarını alır.</span><span class="sxs-lookup"><span data-stu-id="2ca76-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="2ca76-117">VM Al</span><span class="sxs-lookup"><span data-stu-id="2ca76-117">Get a VM</span></span>

<span data-ttu-id="2ca76-118">Gerekli toorun hello bir sanal makinedir `vm list` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2ca76-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="2ca76-119">Merhaba aşağıdaki komut bir kaynak grubunda hello sanal machinese listeler:</span><span class="sxs-lookup"><span data-stu-id="2ca76-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="2ca76-120">Merhaba sanal makine öğrendikten sonra hello kullanabilirsiniz `vm show` cmdlet tooget kendi kaynak kimliği:</span><span class="sxs-lookup"><span data-stu-id="2ca76-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="2ca76-121">Güvenlik grubu görünümü alma</span><span class="sxs-lookup"><span data-stu-id="2ca76-121">Retrieve security group view</span></span>

<span data-ttu-id="2ca76-122">Merhaba sonraki tooretrieve hello güvenlik grubu Görünüm sonucu adımdır.</span><span class="sxs-lookup"><span data-stu-id="2ca76-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="2ca76-123">Ekleme hello "--json" bayrağı json hello sonuçlarında biçimlendirecek.</span><span class="sxs-lookup"><span data-stu-id="2ca76-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="2ca76-124">Merhaba sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2ca76-124">Viewing hello results</span></span>

<span data-ttu-id="2ca76-125">Merhaba aşağıdaki kısaltılmış bir yanıt döndürdü hello sonuçlarının bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="2ca76-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="2ca76-126">Merhaba sonuçları tüm hello etkili ve uygulanan güvenlik kuralları hello sanal makineye gruplar halinde ayrıntılarıyla Göster **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, ve  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="2ca76-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2ca76-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ca76-127">Next steps</span></span>

<span data-ttu-id="2ca76-128">Ziyaret [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md) toolearn nasıl tooautomate doğrulama ağ güvenlik grupları.</span><span class="sxs-lookup"><span data-stu-id="2ca76-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="2ca76-129">Şu adresi ziyaret ederek uygulanan tooyour ağ kaynaklarına olan hello güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2ca76-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
