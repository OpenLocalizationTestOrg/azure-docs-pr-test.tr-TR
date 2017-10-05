---
title: Node.js ile Azure Redis Cache kullanma | Microsoft v
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
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="588cd-103">Node.js ile Azure Redis Cache kullanma</span><span class="sxs-lookup"><span data-stu-id="588cd-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="588cd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="588cd-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="588cd-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="588cd-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="588cd-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="588cd-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="588cd-107">Java</span><span class="sxs-lookup"><span data-stu-id="588cd-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="588cd-108">Python</span><span class="sxs-lookup"><span data-stu-id="588cd-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="588cd-109">Azure Redis Cache, Microsoft tarafından yönetilen güvenli, ayrılmış bir Redis önbelleğine erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="588cd-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="588cd-110">Önbelleğinize Microsoft Azure’daki her uygulamadan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="588cd-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="588cd-111">Bu konu Node.js kullanarak Azure Redis Cache kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="588cd-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="588cd-112">Node.js ile Azure Redis Cache’in başka bir örneği için, bkz. [Azure Web Sitesinde Socket.IO ile bir Node.js Sohbet Uygulaması Oluşturma](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="588cd-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="588cd-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="588cd-113">Prerequisites</span></span>
<span data-ttu-id="588cd-114">[node_redis](https://github.com/mranney/node_redis) yükleyin:</span><span class="sxs-lookup"><span data-stu-id="588cd-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="588cd-115">Bu öğreticide, [node_redis](https://github.com/mranney/node_redis) kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="588cd-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="588cd-116">Diğer Node.js istemcilerini kullanmaya ilişkin örnekler için [Node.js Redis istemcileri](http://redis.io/clients#nodejs) listesindeki Node.js istemcilerinin kendi belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="588cd-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="588cd-117">Azure’da Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="588cd-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="588cd-118">Ana bilgisayar adını ve erişim anahtarlarını alma</span><span class="sxs-lookup"><span data-stu-id="588cd-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="588cd-119">SSL kullanarak güvenli bir şekilde önbelleğe bağlanma</span><span class="sxs-lookup"><span data-stu-id="588cd-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="588cd-120">[node_redis](https://github.com/mranney/node_redis)’in en son derlemeleri, Azure Redis Cache’e SSL kullanarak bağlanma konusunda destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="588cd-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="588cd-121">Aşağıdaki örnekte, 6380 SSL bitiş noktasını kullanarak Azure Redis Cache’e nasıl bağlanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="588cd-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="588cd-122">Önceki [Ana bilgisayar adını ve erişim anahtarlarını alma](#retrieve-the-host-name-and-access-keys) bölümünde açıklanan şekilde `<name>` öğesini önbelleğinizin adı ile, `<key>` öğesini ise birincil veya ikincil anahtarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="588cd-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="588cd-123">SSL olmayan bağlantı noktası, yeni Azure Redis Cache örnekleri için devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="588cd-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="588cd-124">SSL desteği olmayan farklı bir istemci kullanıyorsanız bkz. [SSL olmayan bağlantı noktasını etkinleştirme](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="588cd-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="588cd-125">Önbelleğe bir şey ekleme ve bunu alma</span><span class="sxs-lookup"><span data-stu-id="588cd-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="588cd-126">Aşağıdaki örnekte, size bir Azure Redis Cache örneğine bağlanma, önbellekte öğe depolama ve önbellekten öğe alma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="588cd-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="588cd-127">Redis’i [node_redis](https://github.com/mranney/node_redis) istemcisiyle kullanmaya ilişkin daha fazla örnek için bkz. [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="588cd-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="588cd-128">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="588cd-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="588cd-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="588cd-129">Next steps</span></span>
* <span data-ttu-id="588cd-130">Önbelleğinizin sistem durumunu [izleyebilmeniz](cache-how-to-monitor.md) için [önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="588cd-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="588cd-131">Resmi [Redis belgeleri](http://redis.io/documentation)ni okuyun.</span><span class="sxs-lookup"><span data-stu-id="588cd-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

