---
title: "Linux üzerinde Azure Web uygulamasında Node.js için aaaUsing PM2 yapılandırma | Microsoft Docs"
description: "Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak"
keywords: "Azure uygulama hizmeti, web uygulaması, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Linux üzerinde Azure Web uygulamasında Node.js için PM2 yapılandırma kullan

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Azure Web uygulaması Linux'ta hello uygulama yığın tooNode.js ayarlarsanız, hello seçeneği tooset Node.js başlangıç dosyasını hello görüntü aşağıdaki gösterildiği gibi alın:

![Node.js başlangıç dosyası ayarlayın][1]

Bu seçenek toodo bir görevleri aşağıdaki hello birini kullanabilirsiniz:

* Node.js uygulamanızı Hello başlangıç komut dosyasını belirtin (örneğin: /bin/server.js).
* Node.js uygulamanız için Hello PM2 yapılandırma dosyası toouse belirtin (örneğin: /foo/process.json).
  
  > [!NOTE]
  > Belirli dosya değiştirildiğinde, Node.js işlemleri toorestart otomatik olarak istiyorsanız, hello PM2 yapılandırmasını kullanın. Aksi takdirde (örneğin, uygulama kodunuzun değiştiğinde) değişiklik bildirimleri aldığında uygulamanızı başlatın olmaz.
  > 
  > 

Merhaba Node.js denetleyebilirsiniz [işlem dosya belgelerine](http://pm2.keymetrics.io/docs/usage/application-declaration/) tüm seçenekleri hello ancak process.json dosyanız kullanmak, bir örnek verilmiştir:

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

Bu yapılandırmada önemli noktalar toonote şunlardır:

* Merhaba "komut dosyası" özelliği, uygulamanızın başlangıç betiği belirtir.
* Merhaba "Instances" özelliği, kaç tane hello düğümü işlem toolaunch örneğinin belirtir. Uygulamanız birden çok çekirdeğe sahip büyük VM'ler üzerinde çalıştırıyorsanız, iyi bir fikir toomaximize olan kaynaklarınızı daha yüksek bir değer burada ayarlayarak.
* Merhaba "izleme" bunlar değiştirdiğinizde toorestart hello düğümü işlemi için istediğiniz tüm dosyaları dizisini belirtir.
* "Watch_options" Merhaba için şu anda toospecify "usePolling" doğru olarak uygulama içeriğinin takılı hello yol nedeniyle gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde Azure Web uygulaması nedir?](app-service-linux-intro.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
