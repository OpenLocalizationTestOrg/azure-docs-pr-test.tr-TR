---
title: "aaaAzure Service Fabric CLI komut dosyası örneği dağıtma"
description: "Hello Azure Service Fabric CLI kullanarak bir uygulama tooan Azure Service Fabric kümesi dağıtma"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="a2a51-103">Bir uygulama tooa Service Fabric kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="a2a51-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="a2a51-104">Bu örnek betik bir uygulama paketi tooa kümenin görüntü deposu kopyalar, hello kümede hello uygulama türü kaydeder ve hello uygulama türünden uygulama örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a2a51-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="a2a51-105">Varsayılan hizmetlerin de şu anda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a2a51-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="a2a51-106">Gerekirse, hello yükleyin [Service Fabric CLI](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a2a51-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="a2a51-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a2a51-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a2a51-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="a2a51-108">Clean up deployment</span></span>

<span data-ttu-id="a2a51-109">İşiniz bittiğinde, hello [kaldırmak](cli-remove-application.md) betik kullanılan tooremove hello uygulama olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2a51-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="a2a51-110">Merhaba kaldırma komut dosyası hello uygulama örneği siler, hello uygulama türü kaydını siler ve görüntü deposundan hello uygulama paketini siler.</span><span class="sxs-lookup"><span data-stu-id="a2a51-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2a51-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2a51-111">Next steps</span></span>

<span data-ttu-id="a2a51-112">Daha fazla bilgi için bkz: Merhaba [Service Fabric CLI belgelerine](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a2a51-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="a2a51-113">Azure Service Fabric için ek hizmet doku CLI örnek hello bulunabilir [Service Fabric CLI örnekleri](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a2a51-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
