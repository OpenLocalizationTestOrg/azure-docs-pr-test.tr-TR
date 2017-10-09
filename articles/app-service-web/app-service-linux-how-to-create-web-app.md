---
title: "aaaCreate bir Azure web uygulaması Linux üzerinde çalışan | Microsoft Docs"
description: "Web uygulaması oluşturma için iş akışı Linux Azure Web uygulaması."
keywords: "Azure uygulama hizmeti, web uygulaması, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="82c1f-104">Linux üzerinde çalışan bir Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82c1f-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="82c1f-105">Web uygulamanızı Hello Azure portal toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="82c1f-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="82c1f-106">Web uygulamanız hello Linux'ta oluşturma başlatabilirsiniz [Azure portal](https://portal.azure.com) hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="82c1f-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Azure portal hello üzerinde bir web uygulaması oluşturmaya başla][1]

<span data-ttu-id="82c1f-108">Ardından, hello **Oluştur dikey** hello görüntü aşağıdaki gösterildiği gibi açılır:</span><span class="sxs-lookup"><span data-stu-id="82c1f-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Merhaba Oluştur dikey penceresi][2]

1. <span data-ttu-id="82c1f-110">Web uygulamanızı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="82c1f-110">Give your web app a name.</span></span>
2. <span data-ttu-id="82c1f-111">Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82c1f-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="82c1f-112">(Merhaba kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="82c1f-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="82c1f-113">Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82c1f-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="82c1f-114">(Uygulama hizmeti planı notları hello bkz [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="82c1f-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="82c1f-115">Merhaba uygulamasını seçin toouse düşündüğünüz yığını.</span><span class="sxs-lookup"><span data-stu-id="82c1f-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="82c1f-116">Node.js, PHP, .net birkaç sürümleri arasında seçim yapabilirsiniz çekirdek ve Ruby.</span><span class="sxs-lookup"><span data-stu-id="82c1f-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="82c1f-117">Merhaba uygulama oluşturduktan sonra hello uygulama yığınını hello uygulama ayarlarından hello görüntü aşağıdaki gösterildiği gibi değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82c1f-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Uygulama ayarları][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="82c1f-119">Web uygulamanızı dağıtın</span><span class="sxs-lookup"><span data-stu-id="82c1f-119">Deploy your web app</span></span>
<span data-ttu-id="82c1f-120">Seçme **dağıtım seçenekleri** hello Yönetim Portalı sağlar, uygulamanızın seçeneği toouse yerel Git veya GitHub depo toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="82c1f-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="82c1f-121">bir Linux olmayan web uygulaması için benzer toothose hello yönergeleri Hello kalan var.</span><span class="sxs-lookup"><span data-stu-id="82c1f-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="82c1f-122">Merhaba yönergeleri takip edebilirsiniz [yerel Git dağıtımı](app-service-deploy-local-git.md) veya [sürekli dağıtım](app-service-continuous-deployment.md) toodeploy uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="82c1f-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="82c1f-123">Uygulama tooyour sitenizi FTP tooupload de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82c1f-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="82c1f-124">Merhaba FTP endpoint web uygulamanız için hello tanılama logs bölümü hello görüntü aşağıdaki gösterildiği gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82c1f-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Tanılama günlükleri][4]

## <a name="next-steps"></a><span data-ttu-id="82c1f-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82c1f-126">Next steps</span></span>
* [<span data-ttu-id="82c1f-127">Linux üzerinde Azure Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="82c1f-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="82c1f-128">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="82c1f-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="82c1f-129">Azure App Service Web uygulaması Linux'ta Ruby kullanma</span><span class="sxs-lookup"><span data-stu-id="82c1f-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="82c1f-130">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="82c1f-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
