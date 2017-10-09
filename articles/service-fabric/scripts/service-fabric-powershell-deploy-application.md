---
title: "PowerShell komut dosyası örneği - aaaAzure uygulama tooa kümesini dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir uygulama tooa Service Fabric kümesi dağıtma."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="676d0-103">Bir uygulama tooa Service Fabric kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="676d0-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="676d0-104">Bu örnek betik bir uygulama paketi tooa kümenin görüntü deposu kopyalar, hello kümede hello uygulama türü kaydeder ve hello uygulama türünden uygulama örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="676d0-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="676d0-105">Varsayılan hizmetlerin hello uygulama bildiriminde hello hedef uygulama türü olarak tanımlanmış olan, bu hizmetleri şu anda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="676d0-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="676d0-106">Merhaba parametrelerini gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="676d0-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="676d0-107">Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="676d0-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="676d0-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="676d0-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="676d0-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="676d0-109">Clean up deployment</span></span> 

<span data-ttu-id="676d0-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komut dosyasında hello [bir uygulamayı kaldırmak](service-fabric-powershell-remove-application.md) kullanılan tooremove hello Uygulama örneğinin olması, hello uygulama türü kaydını kaldırma ve hello uygulama paketi hello görüntü deposundan silin.</span><span class="sxs-lookup"><span data-stu-id="676d0-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="676d0-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="676d0-111">Script explanation</span></span>

<span data-ttu-id="676d0-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="676d0-112">This script uses hello following commands.</span></span> <span data-ttu-id="676d0-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="676d0-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="676d0-114">Komut</span><span class="sxs-lookup"><span data-stu-id="676d0-114">Command</span></span> | <span data-ttu-id="676d0-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="676d0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="676d0-116">Kopyalama ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="676d0-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="676d0-117">Bir uygulama paketi toohello kümenin görüntü deposu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="676d0-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="676d0-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="676d0-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="676d0-119">Bir uygulama türü ve sürümü hello kümede kaydeder.</span><span class="sxs-lookup"><span data-stu-id="676d0-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="676d0-120">ServiceFabricApplication yeni</span><span class="sxs-lookup"><span data-stu-id="676d0-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="676d0-121">Kayıtlı uygulama türünden bir uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="676d0-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="676d0-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="676d0-122">Next steps</span></span>

<span data-ttu-id="676d0-123">Merhaba Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="676d0-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="676d0-124">Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="676d0-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
