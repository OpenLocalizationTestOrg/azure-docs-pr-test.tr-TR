---
title: "aaaAzure PowerShell komut dosyası örneği - Service Fabric kümesi oluştur | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Service Fabric kümesi oluşturur."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="ad0d8-103">Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="ad0d8-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="ad0d8-104">Bu örnek betik, beş düğümlü bir küme bir X.509 sertifikası ile güvenli bir Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="ad0d8-105">Merhaba komutu otomatik olarak imzalanan bir sertifika oluşturur ve yeni anahtar kasası tooa yükler.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="ad0d8-106">Merhaba sertifika ayrıca kopyalanan tooa yerel dizin yok.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="ad0d8-107">Set hello *-OS* parametresi toochoose hello sürümü Windows veya Linux hello küme düğümleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="ad0d8-108">Merhaba parametrelerini gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="ad0d8-109">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview) ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ad0d8-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="ad0d8-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ad0d8-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="ad0d8-111">Clean up deployment</span></span> 

<span data-ttu-id="ad0d8-112">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, küme ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="ad0d8-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="ad0d8-113">Script explanation</span></span>

<span data-ttu-id="ad0d8-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-114">This script uses hello following commands.</span></span> <span data-ttu-id="ad0d8-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ad0d8-116">Komut</span><span class="sxs-lookup"><span data-stu-id="ad0d8-116">Command</span></span> | <span data-ttu-id="ad0d8-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="ad0d8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad0d8-118">AzureRmServiceFabricCluster yeni</span><span class="sxs-lookup"><span data-stu-id="ad0d8-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="ad0d8-119">Yeni bir Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad0d8-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad0d8-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad0d8-120">Next steps</span></span>

<span data-ttu-id="ad0d8-121">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad0d8-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ad0d8-122">Azure Service Fabric ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ad0d8-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
