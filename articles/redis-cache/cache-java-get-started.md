---
title: "Java ile Azure Redis önbelleği aaaHow toouse | Microsoft Docs"
description: "Java kullanarak Azure Redis Cache kullanmaya başlama"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="976a3-103">Nasıl toouse Azure Redis önbelleği Java ile</span><span class="sxs-lookup"><span data-stu-id="976a3-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="976a3-104">.NET</span><span class="sxs-lookup"><span data-stu-id="976a3-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="976a3-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="976a3-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="976a3-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="976a3-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="976a3-107">Java</span><span class="sxs-lookup"><span data-stu-id="976a3-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="976a3-108">Python</span><span class="sxs-lookup"><span data-stu-id="976a3-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="976a3-109">Redis önbelleği, Microsoft tarafından yönetilen ayrılmış tooa erişim azure Redis önbelleği sağlar.</span><span class="sxs-lookup"><span data-stu-id="976a3-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="976a3-110">Önbelleğinize Microsoft Azure’daki her uygulamadan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="976a3-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="976a3-111">Bu konu tooget Azure Redis önbelleği ile çalışmaya nasıl Java kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="976a3-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="976a3-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="976a3-112">Prerequisites</span></span>
<span data-ttu-id="976a3-113">[Jedis](https://github.com/xetorthio/jedis) - Redis için Java istemcisi</span><span class="sxs-lookup"><span data-stu-id="976a3-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="976a3-114">Bu öğreticide Jedis kullanılmıştır, ancak [http://redis.io/clients](http://redis.io/clients) adresinde listelenmiş herhangi bir Java istemcisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="976a3-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="976a3-115">Azure’da Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="976a3-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="976a3-116">Merhaba ana bilgisayar adı ve erişim anahtarlarını alma</span><span class="sxs-lookup"><span data-stu-id="976a3-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="976a3-117">Güvenli bir şekilde SSL kullanarak toohello önbelleği Bağlan</span><span class="sxs-lookup"><span data-stu-id="976a3-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="976a3-118">Merhaba son oluşturur [jedis](https://github.com/xetorthio/jedis) tooAzure Redis önbelleği bağlanmak için destek sağlayan SSL kullanarak.</span><span class="sxs-lookup"><span data-stu-id="976a3-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="976a3-119">Aşağıdaki örnek hello nasıl tooconnect tooAzure Redis önbelleği kullanılarak izin ver hello SSL uç noktası 6380 gösterir.</span><span class="sxs-lookup"><span data-stu-id="976a3-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="976a3-120">Değiştir `<name>` önbelleğiniz hello adıyla ve `<key>` ile ya da birincil veya ikincil anahtarı açıklandığı gibi hello önceki [almak hello ana bilgisayar adı ve erişim anahtarları](#retrieve-the-host-name-and-access-keys) bölümü.</span><span class="sxs-lookup"><span data-stu-id="976a3-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="976a3-121">Merhaba SSL olmayan bağlantı noktası yeni Azure Redis önbelleği örnekleri için devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="976a3-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="976a3-122">SSL desteği olmayan farklı bir istemci kullanıyorsanız, bkz: [nasıl tooenable hello SSL olmayan bağlantı noktası](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="976a3-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="976a3-123">Bir şey ekleme toohello önbellek ve bunu alma</span><span class="sxs-lookup"><span data-stu-id="976a3-123">Add something toohello cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="976a3-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="976a3-124">Next steps</span></span>
* <span data-ttu-id="976a3-125">[Önbellek tanılamayı etkinleştirin](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) , böylece [İzleyici](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello önbelleğinizin sistem durumunu.</span><span class="sxs-lookup"><span data-stu-id="976a3-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="976a3-126">Okuma hello resmi [Redis belgeleri](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="976a3-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
