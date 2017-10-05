---
title: "Azure PowerShell Betiği örnek - Service Fabric kümesi oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="3a111-103">Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="3a111-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="3a111-104">Bu örnek betik, beş düğümlü bir küme bir X.509 sertifikası ile güvenli bir Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a111-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="3a111-105">Komut otomatik olarak imzalanan bir sertifika oluşturur ve yeni bir anahtar Kasası'na yükler.</span><span class="sxs-lookup"><span data-stu-id="3a111-105">The command creates a self-signed certificate and uploads it to a new key vault.</span></span> <span data-ttu-id="3a111-106">Sertifikanın da yerel bir dizine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="3a111-106">The certificate is also copied to a local directory.</span></span>  <span data-ttu-id="3a111-107">Ayarlama *-OS* parametresini kullanarak Windows veya küme düğümleri üzerinde çalıştırılan Linux sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="3a111-107">Set the *-OS* parameter to choose the version of Windows or Linux that runs on the cluster nodes.</span></span>  <span data-ttu-id="3a111-108">Parametreleri gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3a111-108">Customize the parameters as needed.</span></span>

<span data-ttu-id="3a111-109">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview) ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3a111-109">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3a111-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3a111-110">Sample script</span></span>

<span data-ttu-id="3a111-111">[!code-powershell[Ana](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Service Fabric kümesi oluştur")]</span><span class="sxs-lookup"><span data-stu-id="3a111-111">[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3a111-112">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="3a111-112">Clean up deployment</span></span> 

<span data-ttu-id="3a111-113">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, küme ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3a111-113">After the script sample has been run, the following command can be used to remove the resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3a111-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3a111-114">Script explanation</span></span>

<span data-ttu-id="3a111-115">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a111-115">This script uses the following commands.</span></span> <span data-ttu-id="3a111-116">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="3a111-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3a111-117">Komut</span><span class="sxs-lookup"><span data-stu-id="3a111-117">Command</span></span> | <span data-ttu-id="3a111-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="3a111-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a111-119">AzureRmServiceFabricCluster yeni</span><span class="sxs-lookup"><span data-stu-id="3a111-119">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="3a111-120">Yeni bir Service Fabric kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a111-120">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a111-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a111-121">Next steps</span></span>

<span data-ttu-id="3a111-122">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a111-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3a111-123">Azure Service Fabric ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3a111-123">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
