---
title: "Definine ve Azure mikro durumunu yönetmek | Microsoft Docs"
description: "Tanımlayın ve Service Fabric hizmet durumunda yönetme"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="351bd-103">Hizmet durumu</span><span class="sxs-lookup"><span data-stu-id="351bd-103">Service state</span></span>
<span data-ttu-id="351bd-104">**Hizmet durumu** bellekte veya işlevi için bir hizmet gerektiren disk verilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="351bd-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="351bd-105">Bu, örneğin, hizmet okur ve çalışmak yazan üye değişkenleri ve veri yapıları içerir.</span><span class="sxs-lookup"><span data-stu-id="351bd-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="351bd-106">Hizmet nasıl geliştirilmiştir bağlı olarak dosyalara veya diskte depolanan diğer kaynaklara de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="351bd-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="351bd-107">Örneğin, dosyaları, veri ve işlem günlüklerini depolamak için bir veritabanı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="351bd-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="351bd-108">Bir örnek hizmeti olarak şimdi bir hesap makinesi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="351bd-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="351bd-109">Temel hesaplayıcı hizmet iki sayıyı alır ve bunların toplamı döndürür.</span><span class="sxs-lookup"><span data-stu-id="351bd-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="351bd-110">Bu hesaplamayı gerçekleştiren hiç üye değişkeni veya diğer bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="351bd-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="351bd-111">Şimdi aynı hesaplayıcı düşünün, ancak depolamak ve son toplam döndürmek için ek bir yöntem ile hesaplanan.</span><span class="sxs-lookup"><span data-stu-id="351bd-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="351bd-112">Bu hizmet durum bilgisi olan sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="351bd-112">This service is now stateful.</span></span> <span data-ttu-id="351bd-113">Durum bilgisi olan yeni bir toplam hesaplar ve son hesaplanan toplam döndürülecek söylediğinizde okur yükleyen Yazar bazı durumu içerdiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="351bd-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="351bd-114">Azure Service Fabric içinde ilk hizmeti durumsuz bir hizmet olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="351bd-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="351bd-115">İkinci hizmeti durum bilgisi olan bir hizmet olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="351bd-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="351bd-116">Hizmetinin durumunu saklama</span><span class="sxs-lookup"><span data-stu-id="351bd-116">Storing service state</span></span>
<span data-ttu-id="351bd-117">Durum ya da externalized veya durumu düzenleme kod ile birlikte bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="351bd-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="351bd-118">Externalization durumunun genellikle dış veritabanı veya ağ üzerinden veya aynı makine üzerindeki işlemi dışında farklı makinelerde çalışan başka bir veri deposunda kullanılarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="351bd-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="351bd-119">Hesaplayıcı Örneğimizde, veri deposunda bir SQL veritabanına veya Azure tablo deposu örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="351bd-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="351bd-120">Toplam işlem için her istek bu veriler üzerinde bir güncelleştirme gerçekleştirir ve değeri sonucu deposundan çekilen geçerli değeri döndürmek için hizmete ister.</span><span class="sxs-lookup"><span data-stu-id="351bd-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="351bd-121">Durum ayrıca durumu işleyen kodu ile birlikte bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="351bd-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="351bd-122">Durum bilgisi olan Service Fabric Hizmetleri'nde genellikle bu modeli kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="351bd-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="351bd-123">Service Fabric bu durum yüksek oranda kullanılabilir, tutarlı ve dayanıklı olduğundan ve Hizmetleri bu şekilde yerleşik kolayca ölçeklendirebilirsiniz emin olmak için altyapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="351bd-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="351bd-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="351bd-124">Next steps</span></span>
<span data-ttu-id="351bd-125">Service Fabric kavramları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="351bd-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="351bd-126">Service Fabric hizmetlerin kullanılabilirliğini</span><span class="sxs-lookup"><span data-stu-id="351bd-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="351bd-127">Service Fabric Hizmetleri ölçeklenebilirliği</span><span class="sxs-lookup"><span data-stu-id="351bd-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="351bd-128">Service Fabric Hizmetleri bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="351bd-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="351bd-129">Service Fabric güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="351bd-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
