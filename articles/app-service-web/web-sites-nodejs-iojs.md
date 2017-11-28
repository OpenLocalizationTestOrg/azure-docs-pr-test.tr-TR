---
title: Azure App Service Web Apps ile aaaHow toouse io.js
description: "Bilgi nasıl toouse io.js ile Azure App Service'te bir web uygulaması."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="5e3c6-103">Nasıl Azure App Service Web Apps ile io.js toouse</span><span class="sxs-lookup"><span data-stu-id="5e3c6-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="5e3c6-104">Merhaba popüler düğümü çatalı [io.js] daha açık bir idare modeli, daha hızlı bir yayın döngüsü ve yeni ve Deneysel JavaScript özellikleri daha hızlı benimsenmesi dahil olmak üzere çeşitli farklar tooJoyent'ın Node.js proje özellikleri.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="5e3c6-105">Sırada [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları birçok Node.js sürümleri önceden yüklenmiş olan, aynı zamanda için bir kullanıcı tarafından sağlanan Node.js ikili sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="5e3c6-106">App Service Web Apps üzerinde io.js hello kullanımını etkinleştirme iki yöntem bu makalede ele: hello Azure toouse hello en son kullanılabilir io.js sürümünü otomatik olarak yapılandırır ve genişletilmiş dağıtım betiğini de kullanımı gibi hello io.js ikili el ile karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="5e3c6-107">Bir dağıtım komut dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="5e3c6-107">Using a Deployment Script</span></span>
<span data-ttu-id="5e3c6-108">Bir Node.js uygulaması dağıtımı sırasında App Service Web Apps ortamı hello tooensure'nın düzgün yapılandırıldığından küçük komutlarının sayısı çalışır.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="5e3c6-109">Bir dağıtım komut dosyası kullanarak, bu işlem özelleştirilmiş tooinclude hello indirme ve io.js yapılandırması olabilir.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="5e3c6-110">Merhaba [io.js dağıtım betiği](https://github.com/felixrieseberg/iojs-azure) Github'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="5e3c6-111">web uygulamanızdan tooenable io.js sadece kopyalayın **.deployment**, **deploy.cmd** ve **IISNode.yml** toohello kök uygulama klasörünüzün tooWeb uygulamalar ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="5e3c6-112">Merhaba ilk dosya **.deployment**, Web uygulamaları toorun bildirir **deploy.cmd** dağıtım bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="5e3c6-113">Bu komut dosyasını bir Node.js uygulaması için tüm hello normal adımları çalışır, ancak ayrıca hello io.js en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="5e3c6-114">Son olarak, **IISNode.yml** Web Apps toouse indirilen yalnızca hello io.js önceden yüklenmiş bir Node.js ikili yerine ikili yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="5e3c6-115">io.js ikili tooupdate hello kullanılan, yalnızca uygulamanız dağıtmanız - hello betik her tek seferde hello uygulamanın dağıtıldığını io.js yeni sürümü indirir.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="5e3c6-116">El ile yükleme kullanma</span><span class="sxs-lookup"><span data-stu-id="5e3c6-116">Using Manual Installation</span></span>
<span data-ttu-id="5e3c6-117">Merhaba el ile yüklemesi özel io.js sürümü, yalnızca iki adımı içerir.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="5e3c6-118">İlk olarak, hello karşıdan **win x64** hello doğrudan ikili [io.js dağıtım].</span><span class="sxs-lookup"><span data-stu-id="5e3c6-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="5e3c6-119">Gerekli olan iki dosyalar - **iojs.exe** ve **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="5e3c6-120">Kaydet hem dosyaları, web uygulamanızın tooa klasöre örneğin **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="5e3c6-121">tooconfigure Web Apps toouse **iojs.exe** oluşturmak yerine önceden yüklenmiş bir düğüm sürüm, bir **IISNode.yml** dosya hello uygulamanızı kökünde ve satır aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="5e3c6-122">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5e3c6-122">Next Steps</span></span>
<span data-ttu-id="5e3c6-123">Bu makalede nasıl el ile yükleme yanı sıra dağıtım betikleri toouse io.js her ikisini de kullanarak App Service Web Apps ile sağlanan öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="5e3c6-124">io.js ağır Geliştiriliyor ve Node.js daha sık güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="5e3c6-125">Node.js modüllerini sayısı ile io.js - Lütfen belgelere bakın işe yaramayabilir [github'da io.js] sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="5e3c6-126">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5e3c6-126">What's changed</span></span>
* <span data-ttu-id="5e3c6-127">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5e3c6-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="5e3c6-128">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5e3c6-129">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5e3c6-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js dağıtım]: https://iojs.org/dist/
[github'da io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
