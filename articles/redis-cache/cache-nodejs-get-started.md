---
title: "Node.js ile Azure Redis önbelleği aaaHow toouse | Microsoft Docs"
description: "Node.js ve node_redis kullanarak Azure Redis Cache kullanmaya başlama"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="8ced4-103">Nasıl toouse Azure Redis önbelleği Node.js ile</span><span class="sxs-lookup"><span data-stu-id="8ced4-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ced4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8ced4-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="8ced4-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8ced4-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="8ced4-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8ced4-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="8ced4-107">Java</span><span class="sxs-lookup"><span data-stu-id="8ced4-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="8ced4-108">Python</span><span class="sxs-lookup"><span data-stu-id="8ced4-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="8ced4-109">Microsoft tarafından yönetilen tooa güvenli, ayrılmış bir Redis önbelleğine erişim Azure Redis önbelleği izni verir.</span><span class="sxs-lookup"><span data-stu-id="8ced4-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="8ced4-110">Önbelleğinize Microsoft Azure’daki her uygulamadan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="8ced4-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="8ced4-111">Bu konu tooget Azure Redis önbelleği ile çalışmaya nasıl Node.js kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ced4-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="8ced4-112">Node.js ile Azure Redis Cache’in başka bir örneği için, bkz. [Azure Web Sitesinde Socket.IO ile bir Node.js Sohbet Uygulaması Oluşturma](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="8ced4-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ced4-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8ced4-113">Prerequisites</span></span>
<span data-ttu-id="8ced4-114">[node_redis](https://github.com/mranney/node_redis) yükleyin:</span><span class="sxs-lookup"><span data-stu-id="8ced4-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="8ced4-115">Bu öğreticide, [node_redis](https://github.com/mranney/node_redis) kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8ced4-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="8ced4-116">Diğer Node.js istemcileri kullanım örnekleri için hello adresinde listelenmiş hello Node.js istemcileri tek tek belgelerine bakın [Node.js Redis istemcileri](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="8ced4-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="8ced4-117">Azure’da Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ced4-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="8ced4-118">Merhaba ana bilgisayar adı ve erişim anahtarlarını alma</span><span class="sxs-lookup"><span data-stu-id="8ced4-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="8ced4-119">Güvenli bir şekilde SSL kullanarak toohello önbelleği Bağlan</span><span class="sxs-lookup"><span data-stu-id="8ced4-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="8ced4-120">Merhaba son oluşturur [node_redis](https://github.com/mranney/node_redis) tooAzure Redis önbelleği bağlanmak için destek sağlayan SSL kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8ced4-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="8ced4-121">Aşağıdaki örnek hello nasıl tooconnect tooAzure Redis önbelleği kullanılarak izin ver hello SSL uç noktası 6380 gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ced4-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="8ced4-122">Değiştir `<name>` önbelleğiniz hello adıyla ve `<key>` ile ya da birincil veya ikincil anahtarı açıklandığı gibi hello önceki [almak hello ana bilgisayar adı ve erişim anahtarları](#retrieve-the-host-name-and-access-keys) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8ced4-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="8ced4-123">Merhaba SSL olmayan bağlantı noktası yeni Azure Redis önbelleği örnekleri için devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="8ced4-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="8ced4-124">SSL desteği olmayan farklı bir istemci kullanıyorsanız, bkz: [nasıl tooenable hello SSL olmayan bağlantı noktası](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="8ced4-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="8ced4-125">Bir şey ekleme toohello önbellek ve bunu alma</span><span class="sxs-lookup"><span data-stu-id="8ced4-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="8ced4-126">Merhaba aşağıdaki tooconnect tooan Azure Redis nasıl örneği, önbellek depolamak ve öğeyi hello önbellekten örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="8ced4-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="8ced4-127">Redis ile Merhaba kullanmanın diğer örnekler için [node_redis](https://github.com/mranney/node_redis) istemci, bkz: [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="8ced4-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="8ced4-128">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="8ced4-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="8ced4-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ced4-129">Next steps</span></span>
* <span data-ttu-id="8ced4-130">[Önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics) , böylece [İzleyici](cache-how-to-monitor.md) hello önbelleğinizin sistem durumunu.</span><span class="sxs-lookup"><span data-stu-id="8ced4-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="8ced4-131">Okuma hello resmi [Redis belgeleri](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="8ced4-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

