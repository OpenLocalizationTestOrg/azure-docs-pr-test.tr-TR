---
title: "Azure Portal kullanarak Web uygulaması kopyalama"
description: "Web uygulamalarınızı Azure Portal kullanarak yeni Web uygulamaları için kopyalama öğrenin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="b5ccc-103">Azure App Service uygulaması kullanarak Azure portalında kopyalama</span><span class="sxs-lookup"><span data-stu-id="b5ccc-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="b5ccc-104">Kopyalama özelliği [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kolayca kopyalama varolan sağlar web uygulamaları için farklı bir bölgede ya da aynı bölgede yeni oluşturulan bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="b5ccc-105">Bu uygulama sayısı farklı bölgeler arasında hızlı ve kolay bir şekilde dağıtmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="b5ccc-106">Uygulama kopyalama şu anda yalnızca premium katmanı uygulama hizmeti planları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="b5ccc-107">Yeni özellik aynı sınırlamalar Web Apps yedekleme özelliği kullanan, bkz: [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b5ccc-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="b5ccc-108">Mevcut bir uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="b5ccc-108">Cloning an existing App</span></span>
<span data-ttu-id="b5ccc-109">Web uygulamasının çalışır durumda **Premium** web uygulaması için bir kopya oluşturmak için sırayla modu.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="b5ccc-110">İçinde [Azure Portal](https://portal.azure.com/), web uygulamanızın dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="b5ccc-111">Tıklatın **Araçları**.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-111">Click **Tools**.</span></span> <span data-ttu-id="b5ccc-112">Ardından **Araçları** dikey penceresinde tıklatın **kopya uygulama**.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="b5ccc-113">Web uygulaması zaten değilse **Premium** modu, uygulama kopyalama desteklenen modları belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="b5ccc-114">Bu noktada, seçmek için seçeneğiniz **yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="b5ccc-115">İçinde **kopya uygulama** dikey penceresinde yeni web uygulaması, kaynak grubu ve uygulama hizmeti planı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="b5ccc-116">Ayrıca kullanıcı kaynak web uygulaması ayarları sayısı kopyalamak isteyip istemediğinizi seçin kuramaz veya değil.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="b5ccc-117">' I tıklattıktan sonra **oluşturma** platform kaynak web uygulamasının bir kopyasını oluşturma üzerinde çalışmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="b5ccc-118">Bir uygulama hizmeti ortamı var olan bir uygulamaya kopyalama</span><span class="sxs-lookup"><span data-stu-id="b5ccc-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="b5ccc-119">İçinde **kopya uygulama** dikey müşteri var olan uygulama hizmeti ortamı'nda bir uygulama havuzu seçmek için seçeneği vardır.</span><span class="sxs-lookup"><span data-stu-id="b5ccc-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="b5ccc-120">Geçerli kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="b5ccc-120">Current Restrictions</span></span>
<span data-ttu-id="b5ccc-121">Bu özellik şu anda önizlemede değil, zaman içinde yeni özellikler eklemek için çalışıyoruz, aşağıdaki listede olan uygulama Azure Portalı'nda kopyalama bilinen kısıtlamalar geçerli desteği:</span><span class="sxs-lookup"><span data-stu-id="b5ccc-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="b5ccc-122">Azure Traffic Manager ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="b5ccc-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="b5ccc-123">Otomatik ölçek ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="b5ccc-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="b5ccc-124">Yedekleme zamanlaması ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="b5ccc-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="b5ccc-125">VNET ayarlarını klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="b5ccc-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="b5ccc-126">App Insights otomatik olarak hedef web uygulamasında belirlenmedi</span><span class="sxs-lookup"><span data-stu-id="b5ccc-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="b5ccc-127">Kolay kimlik doğrulama ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="b5ccc-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="b5ccc-128">Kudu uzantısı değil kopyalanamıyor</span><span class="sxs-lookup"><span data-stu-id="b5ccc-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="b5ccc-129">İpucu kuralları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="b5ccc-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="b5ccc-130">Veritabanı içeriğini değil kopyalanamıyor</span><span class="sxs-lookup"><span data-stu-id="b5ccc-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="b5ccc-131">Başvurular</span><span class="sxs-lookup"><span data-stu-id="b5ccc-131">References</span></span>
* [<span data-ttu-id="b5ccc-132">Web uygulaması PowerShell kullanarak kopyalama</span><span class="sxs-lookup"><span data-stu-id="b5ccc-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="b5ccc-133">Azure App Service'in web uygulamasında yedekleyin</span><span class="sxs-lookup"><span data-stu-id="b5ccc-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="b5ccc-134">App Service Ortamı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ccc-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="b5ccc-135">App Service Ortamında bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ccc-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="b5ccc-136">App Service Ortamı’na giriş</span><span class="sxs-lookup"><span data-stu-id="b5ccc-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
