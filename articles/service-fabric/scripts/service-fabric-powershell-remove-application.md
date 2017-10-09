---
title: "PowerShell komut dosyası örneği - bir kümeden kaldır uygulama aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="07fa4-103">Bir uygulama Service Fabric kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="07fa4-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="07fa4-104">Bu örnek betik çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü hello kümeden kaydını siler ve hello küme görüntü deposundan hello uygulama paketini siler.</span><span class="sxs-lookup"><span data-stu-id="07fa4-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="07fa4-105">Silme hello uygulama örneği, bu uygulama ile ilişkili hizmet örneklerini çalıştıran tüm hello da siler.</span><span class="sxs-lookup"><span data-stu-id="07fa4-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="07fa4-106">Merhaba parametrelerini gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="07fa4-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="07fa4-107">Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07fa4-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="07fa4-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="07fa4-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="07fa4-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="07fa4-109">Script explanation</span></span>

<span data-ttu-id="07fa4-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="07fa4-110">This script uses hello following commands.</span></span> <span data-ttu-id="07fa4-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="07fa4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="07fa4-112">Komut</span><span class="sxs-lookup"><span data-stu-id="07fa4-112">Command</span></span> | <span data-ttu-id="07fa4-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="07fa4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07fa4-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="07fa4-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="07fa4-115">Çalışan bir Service Fabric uygulaması örneği hello kümeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="07fa4-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="07fa4-116">Kaydı ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="07fa4-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="07fa4-117">Bir Service Fabric uygulama türü ve sürümü hello kümeden kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="07fa4-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="07fa4-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="07fa4-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="07fa4-119">Service Fabric uygulama paketi hello görüntü deposundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="07fa4-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="07fa4-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07fa4-120">Next steps</span></span>

<span data-ttu-id="07fa4-121">Merhaba Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="07fa4-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="07fa4-122">Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="07fa4-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
