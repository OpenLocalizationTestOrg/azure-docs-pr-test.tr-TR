---
title: "Azure PowerShell Betiği örnek - uygulama bir kümeye dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Service Fabric kümesi için bir uygulamayı dağıtın."
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="eb733-103">Service Fabric kümesi bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="eb733-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="eb733-104">Bu örnek betik bir uygulama paketi bir küme görüntü deposuna kopyalar, kümede uygulama türü kaydeder ve uygulama türünden uygulama örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb733-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span>  <span data-ttu-id="eb733-105">Varsayılan hizmetlerin hedef uygulama türü uygulama bildiriminde tanımlanan yapıyorsanız, bu hizmetleri şu anda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb733-105">If any default services were defined in the application manifest of the target application type, then those services are created at this time.</span></span> <span data-ttu-id="eb733-106">Parametreleri gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb733-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="eb733-107">Gerekirse, ile Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb733-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="eb733-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="eb733-108">Sample script</span></span>

<span data-ttu-id="eb733-109">[!code-powershell[Ana](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "bir küme bir uygulamayı dağıtma")]</span><span class="sxs-lookup"><span data-stu-id="eb733-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="eb733-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="eb733-110">Clean up deployment</span></span> 

<span data-ttu-id="eb733-111">Komut dosyası örneği gerçekleştirildikten sonra komut dosyasını [bir uygulamayı kaldırmak](service-fabric-powershell-remove-application.md) uygulama örneğini kaldırma, uygulama türü kaydını kaldırma ve uygulama paketi görüntü deposundan silmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eb733-111">After the script sample has been run, the script in [Remove an application](service-fabric-powershell-remove-application.md) can be used to remove the application instance, unregister the application type, and delete the application package from the image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="eb733-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="eb733-112">Script explanation</span></span>

<span data-ttu-id="eb733-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb733-113">This script uses the following commands.</span></span> <span data-ttu-id="eb733-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="eb733-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eb733-115">Komut</span><span class="sxs-lookup"><span data-stu-id="eb733-115">Command</span></span> | <span data-ttu-id="eb733-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="eb733-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eb733-117">Kopyalama ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="eb733-117">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="eb733-118">Bir uygulama paketi küme görüntü deposuna kopyalama.</span><span class="sxs-lookup"><span data-stu-id="eb733-118">Copy an application package to the cluster image store.</span></span>  |
|[<span data-ttu-id="eb733-119">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="eb733-119">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="eb733-120">Bir uygulama türü ve sürümü küme üzerinde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="eb733-120">Registers an application type and version on the cluster.</span></span> |
|[<span data-ttu-id="eb733-121">ServiceFabricApplication yeni</span><span class="sxs-lookup"><span data-stu-id="eb733-121">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="eb733-122">Kayıtlı uygulama türünden bir uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb733-122">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb733-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb733-123">Next steps</span></span>

<span data-ttu-id="eb733-124">Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="eb733-124">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="eb733-125">Azure Service Fabric ek Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eb733-125">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
