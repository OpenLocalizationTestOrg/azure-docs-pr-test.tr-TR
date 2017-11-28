---
title: "Azure Service Fabric CLI komut dosyası Kaldır örneği"
description: "Azure Service Fabric CLI kullanarak bir Azure Service Fabric kümesinden bir uygulamayı kaldırma"
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
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="34dcf-103">Bir uygulama Service Fabric kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="34dcf-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="34dcf-104">Bu örnek betik, çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü kümesinden bir küme kaydını siler.</span><span class="sxs-lookup"><span data-stu-id="34dcf-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster.</span></span>  <span data-ttu-id="34dcf-105">Uygulama örneğinin silinmesi da siler çalışan tüm hizmet örnekleri uygulama ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="34dcf-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="34dcf-106">Ardından, uygulama dosyaları görüntü deposundan silinir.</span><span class="sxs-lookup"><span data-stu-id="34dcf-106">Next, the application files are deleted from the image store.</span></span> 

<span data-ttu-id="34dcf-107">Gerekirse, yükleme [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="34dcf-107">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="34dcf-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="34dcf-108">Sample script</span></span>

<span data-ttu-id="34dcf-109">[!code-sh[Ana](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "bir uygulamayı kümeden kaldırma")]</span><span class="sxs-lookup"><span data-stu-id="34dcf-109">[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="34dcf-110">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34dcf-110">Next steps</span></span>

<span data-ttu-id="34dcf-111">Daha fazla bilgi için bkz: [Service Fabric CLI belgelerine](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="34dcf-111">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="34dcf-112">Azure Service Fabric için ek hizmet doku CLI örnek bulunabilir [Service Fabric CLI örnekleri](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="34dcf-112">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
