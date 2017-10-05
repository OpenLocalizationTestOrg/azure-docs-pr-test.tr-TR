---
title: "Azure portalında Service Bus ad alanı oluşturma | Microsoft Docs"
description: "Azure portalını kullanarak bir Service Bus ad alanı oluşturun."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c8654ed547a9001e2e968d2a45d990a73ef27d3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-service-bus-namespace-using-the-azure-portal"></a><span data-ttu-id="fbbf0-103">Azure portalı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbbf0-103">Create a Service Bus namespace using the Azure portal</span></span>

<span data-ttu-id="fbbf0-104">Ad alanı, tüm mesajlaşma bileşenlerini kapsayan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="fbbf0-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="fbbf0-105">Tek bir ad alanında birden fazla kuyruk ve konu bulunabilir ve ad alanları genellikle uygulama kapsayıcıları olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="fbbf0-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="fbbf0-106">Bir Service Bus ad alanı oluşturmak için iki farklı yol vardır:</span><span class="sxs-lookup"><span data-stu-id="fbbf0-106">There are two different ways to create a Service Bus namespace:</span></span>

1. <span data-ttu-id="fbbf0-107">Azure portalı (bu makale)</span><span class="sxs-lookup"><span data-stu-id="fbbf0-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="fbbf0-108">[Resource Manager şablonları][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="fbbf0-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-the-azure-portal"></a><span data-ttu-id="fbbf0-109">Azure portalında bir ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbbf0-109">Create a namespace in the Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="fbbf0-110">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fbbf0-110">Congratulations!</span></span> <span data-ttu-id="fbbf0-111">Bir Service Bus Mesajlaşması ad alanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="fbbf0-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbbf0-112">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fbbf0-112">Next steps</span></span>

<span data-ttu-id="fbbf0-113">Azure Service Bus Mesajlaşmasının daha gelişmiş özelliklerinden bazılarını gösteren [GitHub örneklerimize][github-samples] göz atın.</span><span class="sxs-lookup"><span data-stu-id="fbbf0-113">Check out our [GitHub samples][github-samples], which show some of the more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
