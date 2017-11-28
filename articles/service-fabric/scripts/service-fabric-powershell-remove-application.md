---
title: "Azure PowerShell Betiği örnek - bir kümeden kaldır uygulama | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - uygulama bir Service Fabric kümesinden Kaldır."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 05851132c7e5e5877884d29f04bce6c0717ce411
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="ff0e4-103">Bir uygulama Service Fabric kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="ff0e4-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="ff0e4-104">Bu örnek betik, çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü kümesinden bir küme kaydını siler ve uygulama paketi küme görüntü deposundan siler.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster, and deletes the application package from the cluster image store.</span></span>  <span data-ttu-id="ff0e4-105">Uygulama örneğinin silinmesi da siler çalışan tüm hizmet örnekleri uygulama ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="ff0e4-106">Parametreleri gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="ff0e4-107">Gerekirse, ile Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ff0e4-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ff0e4-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="ff0e4-108">Sample script</span></span>

<span data-ttu-id="ff0e4-109">[!code-powershell[Ana](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "bir uygulamayı kümeden kaldırma")]</span><span class="sxs-lookup"><span data-stu-id="ff0e4-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="ff0e4-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="ff0e4-110">Script explanation</span></span>

<span data-ttu-id="ff0e4-111">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-111">This script uses the following commands.</span></span> <span data-ttu-id="ff0e4-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ff0e4-113">Komut</span><span class="sxs-lookup"><span data-stu-id="ff0e4-113">Command</span></span> | <span data-ttu-id="ff0e4-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="ff0e4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff0e4-115">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="ff0e4-115">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="ff0e4-116">Çalışan bir Service Fabric uygulaması örneği kümeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-116">Removes a running Service Fabric application instance from the cluster.</span></span>  |
| [<span data-ttu-id="ff0e4-117">Kaydı ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="ff0e4-117">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="ff0e4-118">Bir Service Fabric uygulama türü ve sürümü kümesinden bir küme kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-118">Unregisters a Service Fabric application type and version from the cluster.</span></span> |
| [<span data-ttu-id="ff0e4-119">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="ff0e4-119">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="ff0e4-120">Service Fabric uygulama paketi görüntü deposundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ff0e4-120">Removes a Service Fabric application package from the image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="ff0e4-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff0e4-121">Next steps</span></span>

<span data-ttu-id="ff0e4-122">Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ff0e4-122">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="ff0e4-123">Azure Service Fabric ek Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ff0e4-123">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
