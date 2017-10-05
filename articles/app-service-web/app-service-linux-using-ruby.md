---
title: "Azure App Service Web uygulaması Linux'ta Ruby kullanarak | Microsoft Docs"
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
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="21f91-104">Ruby Linux üzerinde Web uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="21f91-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="21f91-105">Bizim arka uç için en son güncelleştirme ile Söyleniş v.2.3 desteği sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="21f91-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="21f91-106">Linux web uygulamanızın yapılandırma ayarlayarak, uygulama yığınını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f91-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="21f91-107">Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="21f91-107">Using the Azure portal</span></span> ##

<span data-ttu-id="21f91-108">Yeni menüsünden [Azure portal](https://portal.azure.com), aşağıdaki görüntüde gösterildiği gibi Web + Mobil Seçenek'dan Linux üzerinde bir Web uygulaması oluşturmayı seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21f91-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Azure portalında bir web uygulaması oluşturmaya başla][1]

<span data-ttu-id="21f91-110">Ardından, **Oluştur dikey** aşağıdaki görüntüde gösterildiği gibi açılır:</span><span class="sxs-lookup"><span data-stu-id="21f91-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![Oluşturma dikey penceresi][2]

1. <span data-ttu-id="21f91-112">Web uygulamanızı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="21f91-112">Give your web app a name.</span></span>
2. <span data-ttu-id="21f91-113">Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f91-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="21f91-114">(Kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="21f91-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="21f91-115">Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f91-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="21f91-116">(Uygulama hizmeti planı notlara bakın [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="21f91-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="21f91-117">Söyleniş yerleşik çalışma zamanı yığınlar seçin.</span><span class="sxs-lookup"><span data-stu-id="21f91-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="21f91-118">Söyleniş web uygulamanızı oluşturulan sonra Git veya FTP kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f91-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="21f91-119">Söyleniş uygulama oluşturma hakkında daha fazla bilgi edinmek için [get Başlarken Kılavuzu](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="21f91-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="21f91-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21f91-120">Next steps</span></span>
* [<span data-ttu-id="21f91-121">Linux üzerinde Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="21f91-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="21f91-122">Azure App Service için Yerel Git Dağıtımı</span><span class="sxs-lookup"><span data-stu-id="21f91-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="21f91-123">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="21f91-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="21f91-124">Linux üzerinde Azure Web uygulaması ile Söyleniş bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f91-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png