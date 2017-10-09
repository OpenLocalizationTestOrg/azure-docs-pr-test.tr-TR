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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Nasıl toouse Azure Redis önbelleği Java ile
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Redis önbelleği, Microsoft tarafından yönetilen ayrılmış tooa erişim azure Redis önbelleği sağlar. Önbelleğinize Microsoft Azure’daki her uygulamadan erişilebilir.

Bu konu tooget Azure Redis önbelleği ile çalışmaya nasıl Java kullanarak gösterir.

## <a name="prerequisites"></a>Ön koşullar
[Jedis](https://github.com/xetorthio/jedis) - Redis için Java istemcisi

Bu öğreticide Jedis kullanılmıştır, ancak [http://redis.io/clients](http://redis.io/clients) adresinde listelenmiş herhangi bir Java istemcisini kullanabilirsiniz.

## <a name="create-a-redis-cache-on-azure"></a>Azure’da Redis Cache oluşturma
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Merhaba ana bilgisayar adı ve erişim anahtarlarını alma
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Güvenli bir şekilde SSL kullanarak toohello önbelleği Bağlan
Merhaba son oluşturur [jedis](https://github.com/xetorthio/jedis) tooAzure Redis önbelleği bağlanmak için destek sağlayan SSL kullanarak. Aşağıdaki örnek hello nasıl tooconnect tooAzure Redis önbelleği kullanılarak izin ver hello SSL uç noktası 6380 gösterir. Değiştir `<name>` önbelleğiniz hello adıyla ve `<key>` ile ya da birincil veya ikincil anahtarı açıklandığı gibi hello önceki [almak hello ana bilgisayar adı ve erişim anahtarları](#retrieve-the-host-name-and-access-keys) bölümü.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> Merhaba SSL olmayan bağlantı noktası yeni Azure Redis önbelleği örnekleri için devre dışı bırakılır. SSL desteği olmayan farklı bir istemci kullanıyorsanız, bkz: [nasıl tooenable hello SSL olmayan bağlantı noktası](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Bir şey ekleme toohello önbellek ve bunu alma
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


## <a name="next-steps"></a>Sonraki adımlar
* [Önbellek tanılamayı etkinleştirin](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) , böylece [İzleyici](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello önbelleğinizin sistem durumunu.
* Okuma hello resmi [Redis belgeleri](http://redis.io/documentation).
