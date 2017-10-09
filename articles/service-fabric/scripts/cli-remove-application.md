---
title: "aaaAzure Service Fabric CLI komut dosyası örneği Kaldır"
description: "Bir uygulama hello Azure Service Fabric CLI kullanarak bir Azure Service Fabric kümesinden Kaldır"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="7f203-103">Bir uygulama Service Fabric kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="7f203-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="7f203-104">Bu örnek betik, çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü hello kümeden kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="7f203-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="7f203-105">Silme hello uygulama örneği, bu uygulama ile ilişkili hizmet örneklerini çalıştıran tüm hello da siler.</span><span class="sxs-lookup"><span data-stu-id="7f203-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="7f203-106">Ardından, hello uygulama dosyalarını hello görüntü deposundan silinir.</span><span class="sxs-lookup"><span data-stu-id="7f203-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="7f203-107">Gerekirse, hello yükleyin [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7f203-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="7f203-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7f203-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="7f203-109">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f203-109">Next steps</span></span>

<span data-ttu-id="7f203-110">Daha fazla bilgi için bkz: Merhaba [Service Fabric CLI belgelerine](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7f203-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="7f203-111">Azure Service Fabric için ek hizmet doku CLI örnek hello bulunabilir [Service Fabric CLI örnekleri](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7f203-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
