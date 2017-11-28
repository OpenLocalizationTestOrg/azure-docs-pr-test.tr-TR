---
title: "aaaHow toocreate hello Azure portalında bir hizmet veri yolu ad alanı | Microsoft Docs"
description: "Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturun."
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
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="91bca-103">Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91bca-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="91bca-104">Ad alanı, tüm mesajlaşma bileşenlerini kapsayan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="91bca-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="91bca-105">Tek bir ad alanında birden fazla kuyruk ve konu bulunabilir ve ad alanları genellikle uygulama kapsayıcıları olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="91bca-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="91bca-106">İki farklı şekilde toocreate bir hizmet veri yolu ad alanı vardır:</span><span class="sxs-lookup"><span data-stu-id="91bca-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="91bca-107">Azure portalı (bu makale)</span><span class="sxs-lookup"><span data-stu-id="91bca-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="91bca-108">[Resource Manager şablonları][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="91bca-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="91bca-109">Hello Azure portalında bir ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91bca-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="91bca-110">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="91bca-110">Congratulations!</span></span> <span data-ttu-id="91bca-111">Bir Service Bus Mesajlaşması ad alanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="91bca-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91bca-112">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91bca-112">Next steps</span></span>

<span data-ttu-id="91bca-113">Kullanıma bizim [GitHub örnekleri][github-samples], hangi Göster daha gelişmiş özellikler Azure Service Bus Mesajlaşma hizmetinin hello bazıları.</span><span class="sxs-lookup"><span data-stu-id="91bca-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
