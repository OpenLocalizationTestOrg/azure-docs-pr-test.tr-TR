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
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="cd034-104">Linux üzerinde Azure Web uygulamasında Node.js için PM2 yapılandırma kullan</span><span class="sxs-lookup"><span data-stu-id="cd034-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="cd034-105">Azure Web uygulaması Linux'ta hello uygulama yığın tooNode.js ayarlarsanız, hello seçeneği tooset Node.js başlangıç dosyasını hello görüntü aşağıdaki gösterildiği gibi alın:</span><span class="sxs-lookup"><span data-stu-id="cd034-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Node.js başlangıç dosyası ayarlayın][1]

<span data-ttu-id="cd034-107">Bu seçenek toodo bir görevleri aşağıdaki hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cd034-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="cd034-108">Node.js uygulamanızı Hello başlangıç komut dosyasını belirtin (örneğin: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="cd034-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="cd034-109">Node.js uygulamanız için Hello PM2 yapılandırma dosyası toouse belirtin (örneğin: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="cd034-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cd034-110">Belirli dosya değiştirildiğinde, Node.js işlemleri toorestart otomatik olarak istiyorsanız, hello PM2 yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd034-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="cd034-111">Aksi takdirde (örneğin, uygulama kodunuzun değiştiğinde) değişiklik bildirimleri aldığında uygulamanızı başlatın olmaz.</span><span class="sxs-lookup"><span data-stu-id="cd034-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="cd034-112">Merhaba Node.js denetleyebilirsiniz [işlem dosya belgelerine](http://pm2.keymetrics.io/docs/usage/application-declaration/) tüm seçenekleri hello ancak process.json dosyanız kullanmak, bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="cd034-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

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

<span data-ttu-id="cd034-113">Bu yapılandırmada önemli noktalar toonote şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cd034-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="cd034-114">Merhaba "komut dosyası" özelliği, uygulamanızın başlangıç betiği belirtir.</span><span class="sxs-lookup"><span data-stu-id="cd034-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="cd034-115">Merhaba "Instances" özelliği, kaç tane hello düğümü işlem toolaunch örneğinin belirtir.</span><span class="sxs-lookup"><span data-stu-id="cd034-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="cd034-116">Uygulamanız birden çok çekirdeğe sahip büyük VM'ler üzerinde çalıştırıyorsanız, iyi bir fikir toomaximize olan kaynaklarınızı daha yüksek bir değer burada ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="cd034-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="cd034-117">Merhaba "izleme" bunlar değiştirdiğinizde toorestart hello düğümü işlemi için istediğiniz tüm dosyaları dizisini belirtir.</span><span class="sxs-lookup"><span data-stu-id="cd034-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="cd034-118">"Watch_options" Merhaba için şu anda toospecify "usePolling" doğru olarak uygulama içeriğinin takılı hello yol nedeniyle gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd034-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd034-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd034-119">Next steps</span></span>
* [<span data-ttu-id="cd034-120">Linux üzerinde Azure Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="cd034-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="cd034-121">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="cd034-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
