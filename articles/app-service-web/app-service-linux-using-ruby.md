---
title: "Azure App Service Web uygulamasında Linux'ta Ruby aaaUsing | Microsoft Docs"
description: "Azure App Service Web uygulaması Linux'ta Ruby kullanarak."
keywords: "Azure uygulama hizmeti, web uygulaması, SSS, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="5c43f-104">Ruby Linux üzerinde Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="5c43f-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="5c43f-105">Merhaba en son güncelleştirme tooour arka uç ile Söyleniş v.2.3 desteği sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="5c43f-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="5c43f-106">Merhaba yapılandırma ayarı Linux web uygulamanızın tarafından hello uygulama yığınını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c43f-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="5c43f-107">Hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="5c43f-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="5c43f-108">Menüsünden hello yeni hello [Azure portal](https://portal.azure.com), toocreate Linux üzerinde bir Web uygulaması hello Web + mobil seçenek hello görüntü aşağıdaki gösterildiği gibi seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5c43f-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Azure portal hello üzerinde bir web uygulaması oluşturmaya başla][1]

<span data-ttu-id="5c43f-110">Ardından, hello **Oluştur dikey** hello görüntü aşağıdaki gösterildiği gibi açılır:</span><span class="sxs-lookup"><span data-stu-id="5c43f-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Merhaba Oluştur dikey penceresi][2]

1. <span data-ttu-id="5c43f-112">Web uygulamanızı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="5c43f-112">Give your web app a name.</span></span>
2. <span data-ttu-id="5c43f-113">Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c43f-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="5c43f-114">(Merhaba kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="5c43f-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="5c43f-115">Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c43f-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="5c43f-116">(Uygulama hizmeti planı notları hello bkz [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="5c43f-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="5c43f-117">Merhaba Ruby hello yerleşik çalışma zamanı yığınlar seçin.</span><span class="sxs-lookup"><span data-stu-id="5c43f-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="5c43f-118">Söyleniş web uygulamanızı oluşturulan sonra tooit Git veya FTP kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c43f-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="5c43f-119">hakkında daha fazla bilgi toolearn hello denetleyin Söyleniş bir uygulama oluşturmaya [get Başlarken Kılavuzu](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5c43f-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c43f-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c43f-120">Next steps</span></span>
* [<span data-ttu-id="5c43f-121">Linux üzerinde Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="5c43f-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="5c43f-122">Yerel Git dağıtımı tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="5c43f-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="5c43f-123">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="5c43f-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="5c43f-124">Linux üzerinde Azure Web uygulaması ile Söyleniş bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c43f-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png