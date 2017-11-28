---
title: "aaaDefinine ve Azure mikro durumunu yönetmek | Microsoft Docs"
description: "Nasıl toodefine ve Service Fabric hizmet durumunda yönetme"
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
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="6b6d6-103">Hizmet durumu</span><span class="sxs-lookup"><span data-stu-id="6b6d6-103">Service state</span></span>
<span data-ttu-id="6b6d6-104">**Hizmet durumu** toohello bellek içi ya da hizmet toofunction gerektirdiğini disk verilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="6b6d6-105">İçerir, örneğin, hello veri yapılarını ve üye değişkenleri hello hizmet okur ve toodo iş yazar.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="6b6d6-106">Merhaba hizmeti nasıl geliştirilmiştir bağlı olarak dosyalara veya diskte depolanan diğer kaynaklara de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="6b6d6-107">Örneğin, bir veritabanı hello dosyaları toostore veri ve işlem günlüklerini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="6b6d6-108">Bir örnek hizmeti olarak şimdi bir hesap makinesi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="6b6d6-109">Temel hesaplayıcı hizmet iki sayıyı alır ve bunların toplamı döndürür.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="6b6d6-110">Bu hesaplamayı gerçekleştiren hiç üye değişkeni veya diğer bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="6b6d6-111">Şimdi düşünün hello aynı hesaplayıcı ancak depolamak ve hello son toplam döndürmek için ek bir yöntem ile hesaplanan.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="6b6d6-112">Bu hizmet durum bilgisi olan sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-112">This service is now stateful.</span></span> <span data-ttu-id="6b6d6-113">Durum bilgisi olan yeni bir toplam hesaplar ve tooreturn hello son hesaplanan toplam söylediğinizde okur toowhen Yazar bazı durumu içerdiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="6b6d6-114">Azure Service Fabric içinde hello ilk hizmeti durumsuz bir hizmet olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="6b6d6-115">Merhaba ikinci hizmeti durum bilgisi olan bir hizmet olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="6b6d6-116">Hizmetinin durumunu saklama</span><span class="sxs-lookup"><span data-stu-id="6b6d6-116">Storing service state</span></span>
<span data-ttu-id="6b6d6-117">Durum ya da externalized veya hello durumu düzenleme hello koduyla birlikte bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="6b6d6-118">Externalization durumunun, genellikle bir dış veritabanı kullanılarak yapılır veya hello ağ üzerinden veya işlemi dışında farklı makinelerde çalıştırır aynı makine hello diğer veri depolayın.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="6b6d6-119">Hesaplayıcı örneğimizde hello veri deposu bir SQL veritabanına veya Azure tablo deposu örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="6b6d6-120">Her istek toocompute hello toplam bu veriler üzerinde bir güncelleştirme gerçekleştirir ve toohello hizmet tooreturn hello değeri sonucu hello deposundan çekilen hello geçerli değeri ister.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="6b6d6-121">Durum ayrıca hello durumu işleyen hello kodu ile birlikte bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="6b6d6-122">Durum bilgisi olan Service Fabric Hizmetleri'nde genellikle bu modeli kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="6b6d6-123">Service Fabric bu durum yüksek oranda kullanılabilir, tutarlı ve sürekli ve hello Hizmetleri bu şekilde yerleşik kolayca ölçeklendirebilirsiniz hello altyapı tooensure sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b6d6-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b6d6-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b6d6-124">Next steps</span></span>
<span data-ttu-id="6b6d6-125">Service Fabric kavramlarla ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="6b6d6-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="6b6d6-126">Service Fabric hizmetlerin kullanılabilirliğini</span><span class="sxs-lookup"><span data-stu-id="6b6d6-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="6b6d6-127">Service Fabric Hizmetleri ölçeklenebilirliği</span><span class="sxs-lookup"><span data-stu-id="6b6d6-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="6b6d6-128">Service Fabric Hizmetleri bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="6b6d6-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="6b6d6-129">Service Fabric güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="6b6d6-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
