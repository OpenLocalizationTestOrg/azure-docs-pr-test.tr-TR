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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Nasıl toouse Azure Redis önbelleği Node.js ile
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Microsoft tarafından yönetilen tooa güvenli, ayrılmış bir Redis önbelleğine erişim Azure Redis önbelleği izni verir. Önbelleğinize Microsoft Azure’daki her uygulamadan erişilebilir.

Bu konu tooget Azure Redis önbelleği ile çalışmaya nasıl Node.js kullanarak gösterir. Node.js ile Azure Redis Cache’in başka bir örneği için, bkz. [Azure Web Sitesinde Socket.IO ile bir Node.js Sohbet Uygulaması Oluşturma](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Ön koşullar
[node_redis](https://github.com/mranney/node_redis) yükleyin:

    npm install redis

Bu öğreticide, [node_redis](https://github.com/mranney/node_redis) kullanılmaktadır. Diğer Node.js istemcileri kullanım örnekleri için hello adresinde listelenmiş hello Node.js istemcileri tek tek belgelerine bakın [Node.js Redis istemcileri](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Azure’da Redis Cache oluşturma
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Merhaba ana bilgisayar adı ve erişim anahtarlarını alma
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Güvenli bir şekilde SSL kullanarak toohello önbelleği Bağlan
Merhaba son oluşturur [node_redis](https://github.com/mranney/node_redis) tooAzure Redis önbelleği bağlanmak için destek sağlayan SSL kullanarak. Aşağıdaki örnek hello nasıl tooconnect tooAzure Redis önbelleği kullanılarak izin ver hello SSL uç noktası 6380 gösterir. Değiştir `<name>` önbelleğiniz hello adıyla ve `<key>` ile ya da birincil veya ikincil anahtarı açıklandığı gibi hello önceki [almak hello ana bilgisayar adı ve erişim anahtarları](#retrieve-the-host-name-and-access-keys) bölümü.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> Merhaba SSL olmayan bağlantı noktası yeni Azure Redis önbelleği örnekleri için devre dışı bırakılır. SSL desteği olmayan farklı bir istemci kullanıyorsanız, bkz: [nasıl tooenable hello SSL olmayan bağlantı noktası](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Bir şey ekleme toohello önbellek ve bunu alma
Merhaba aşağıdaki tooconnect tooan Azure Redis nasıl örneği, önbellek depolamak ve öğeyi hello önbellekten örnek gösterir. Redis ile Merhaba kullanmanın diğer örnekler için [node_redis](https://github.com/mranney/node_redis) istemci, bkz: [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Çıktı:

    OK
    value


## <a name="next-steps"></a>Sonraki adımlar
* [Önbellek tanılamayı etkinleştirin](cache-how-to-monitor.md#enable-cache-diagnostics) , böylece [İzleyici](cache-how-to-monitor.md) hello önbelleğinizin sistem durumunu.
* Okuma hello resmi [Redis belgeleri](http://redis.io/documentation).

