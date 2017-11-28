---
title: "Linux üzerinde çalışan bir Azure web uygulaması oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="48e70-104">Linux üzerinde çalışan bir Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="48e70-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="48e70-105">Web uygulamanızı oluşturmak için Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="48e70-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="48e70-106">Web uygulamanız Linux'ta oluşturmaya başlamadan [Azure portal](https://portal.azure.com) aşağıdaki görüntüde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="48e70-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Azure portalında bir web uygulaması oluşturmaya başla][1]

<span data-ttu-id="48e70-108">Ardından, **Oluştur dikey** aşağıdaki görüntüde gösterildiği gibi açılır:</span><span class="sxs-lookup"><span data-stu-id="48e70-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![Oluşturma dikey penceresi][2]

1. <span data-ttu-id="48e70-110">Web uygulamanızı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="48e70-110">Give your web app a name.</span></span>
2. <span data-ttu-id="48e70-111">Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48e70-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="48e70-112">(Kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="48e70-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="48e70-113">Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48e70-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="48e70-114">(Uygulama hizmeti planı notlara bakın [sınırlamalar bölüm](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="48e70-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="48e70-115">Kullanmak istediğiniz uygulama yığını seçin.</span><span class="sxs-lookup"><span data-stu-id="48e70-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="48e70-116">Node.js, PHP, .net birkaç sürümleri arasında seçim yapabilirsiniz çekirdek ve Ruby.</span><span class="sxs-lookup"><span data-stu-id="48e70-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="48e70-117">Uygulamayı oluşturduktan sonra uygulama yığın uygulama ayarlarından aşağıdaki görüntüde gösterildiği gibi değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48e70-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Uygulama ayarları][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="48e70-119">Web uygulamanızı dağıtın</span><span class="sxs-lookup"><span data-stu-id="48e70-119">Deploy your web app</span></span>
<span data-ttu-id="48e70-120">Seçme **dağıtım seçenekleri** yönetimden portal size uygulamanızı dağıtmak için yerel Git veya GitHub deposunu kullanmak üzere seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="48e70-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="48e70-121">Kalan yönergeleri Linux olmayan web uygulaması için benzer.</span><span class="sxs-lookup"><span data-stu-id="48e70-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="48e70-122">' Ndaki yönergeleri izleyin [yerel Git dağıtımı](app-service-deploy-local-git.md) veya [sürekli dağıtım](app-service-continuous-deployment.md) uygulamanızı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="48e70-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="48e70-123">FTP, uygulamanızın Web sitenize yüklemek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48e70-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="48e70-124">Aşağıdaki görüntüde gösterildiği gibi tanılama günlüklerini bölümünden web uygulamanız için FTP uç noktasını alın:</span><span class="sxs-lookup"><span data-stu-id="48e70-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Tanılama günlükleri][4]

## <a name="next-steps"></a><span data-ttu-id="48e70-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48e70-126">Next steps</span></span>
* [<span data-ttu-id="48e70-127">Linux üzerinde Azure Web uygulaması nedir?</span><span class="sxs-lookup"><span data-stu-id="48e70-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="48e70-128">Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="48e70-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="48e70-129">Azure App Service Web uygulaması Linux'ta Ruby kullanma</span><span class="sxs-lookup"><span data-stu-id="48e70-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="48e70-130">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="48e70-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
