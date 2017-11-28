---
title: "PowerShell komut dosyası örneği - aaaAzure yükseltme Service Fabric uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yükseltme Service Fabric uygulaması."
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="3fc8a-103">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="3fc8a-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="3fc8a-104">Bu örnek betik çalışan Service Fabric uygulaması örneği tooversion 1.3.0 yükseltir.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="3fc8a-105">Hello betik hello yeni uygulama paketi toohello küme görüntü deposuna kopyalar hello uygulama türü kaydeder, izlenen yükseltme başlar ve hello yükseltme tamamlanana veya geri alındığında kadar sürekli olarak hello yükseltme durumunu denetler.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="3fc8a-106">Merhaba parametrelerini gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="3fc8a-107">Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3fc8a-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3fc8a-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3fc8a-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="3fc8a-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3fc8a-109">Script explanation</span></span>

<span data-ttu-id="3fc8a-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-110">This script uses hello following commands.</span></span> <span data-ttu-id="3fc8a-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3fc8a-112">Komut</span><span class="sxs-lookup"><span data-stu-id="3fc8a-112">Command</span></span> | <span data-ttu-id="3fc8a-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="3fc8a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3fc8a-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="3fc8a-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="3fc8a-115">Merhaba Service Fabric kümesi tüm hello uygulamalarında veya belirli bir uygulama alır.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="3fc8a-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="3fc8a-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="3fc8a-117">Service Fabric uygulama yükseltme Hello durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="3fc8a-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="3fc8a-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="3fc8a-119">Merhaba Service Fabric kümesi üzerinde kayıtlı hello Service Fabric uygulama türlerini alır.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="3fc8a-120">Kaydı ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="3fc8a-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="3fc8a-121">Service Fabric uygulama türü kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="3fc8a-122">Kopyalama ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="3fc8a-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="3fc8a-123">Kopya bir Service Fabric uygulama paketi toohello görüntüsünü depolayın.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="3fc8a-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="3fc8a-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="3fc8a-125">Service Fabric uygulama türü kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="3fc8a-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="3fc8a-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="3fc8a-127">Bir Service Fabric uygulaması toohello belirtilen uygulama türü sürümü yükseltir.</span><span class="sxs-lookup"><span data-stu-id="3fc8a-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3fc8a-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fc8a-128">Next steps</span></span>

<span data-ttu-id="3fc8a-129">Merhaba Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="3fc8a-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="3fc8a-130">Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3fc8a-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
