---
title: aaaWeb Azure Portal kullanarak uygulama kopyalama
description: "Bilgi nasıl tooclone, Web uygulamaları toonew Azure Portal kullanarak Web uygulamaları."
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="536f0-103">Azure App Service uygulaması kullanarak Azure portalında kopyalama</span><span class="sxs-lookup"><span data-stu-id="536f0-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="536f0-104">özelliği kopyalama hello [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) hello aynı bölgede varolan web uygulamaları yeni oluşturulan tooa uygulamasını farklı bir bölgede ya da de kolayca kopyalama sağlar.</span><span class="sxs-lookup"><span data-stu-id="536f0-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="536f0-105">Bu müşteriler toodeploy uygulamaları birkaç farklı bölgelerdeki hızla ve kolayca olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="536f0-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="536f0-106">Uygulama kopyalama şu anda yalnızca premium katmanı uygulama hizmeti planları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="536f0-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="536f0-107">Merhaba yeni özellik kullandığı aynı hello Web Apps yedekleme özelliği olarak sınırlamalar bakın [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="536f0-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="536f0-108">Mevcut bir uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="536f0-108">Cloning an existing App</span></span>
<span data-ttu-id="536f0-109">hello Hello web uygulaması çalıştıran **Premium** hello web uygulaması için bir kopya toocreate sırada modu.</span><span class="sxs-lookup"><span data-stu-id="536f0-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="536f0-110">Merhaba, [Azure Portal](https://portal.azure.com/), web uygulamanızın dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="536f0-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="536f0-111">Tıklatın **Araçları**.</span><span class="sxs-lookup"><span data-stu-id="536f0-111">Click **Tools**.</span></span> <span data-ttu-id="536f0-112">Ardından hello **Araçları** dikey penceresinde tıklatın **kopya uygulama**.</span><span class="sxs-lookup"><span data-stu-id="536f0-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="536f0-113">Merhaba web uygulaması zaten hello değilse **Premium** modu, uygulama kopyalama hello desteklenen modları belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="536f0-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="536f0-114">Bu noktada, hello seçeneği tooselect sahip **yükseltme**.</span><span class="sxs-lookup"><span data-stu-id="536f0-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="536f0-115">Merhaba, **kopya uygulama** dikey penceresinde hello yeni web uygulaması, kaynak grubu ve uygulama hizmeti planı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="536f0-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="536f0-116">Aynı zamanda hello kullanıcı mümkün toochoose olup olacaktır tooclone kaynak web uygulaması ayarları sayısı veya değil.</span><span class="sxs-lookup"><span data-stu-id="536f0-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="536f0-117">' I tıklattıktan sonra **oluşturma** hello platform hello kaynak web uygulamasının bir kopyasını oluşturma üzerinde çalışmaya başlayacak.</span><span class="sxs-lookup"><span data-stu-id="536f0-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="536f0-118">Var olan bir uygulama tooan uygulama hizmeti ortamı kopyalama</span><span class="sxs-lookup"><span data-stu-id="536f0-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="536f0-119">Merhaba, **kopya uygulama** dikey penceresinde hello müşteri, bir uygulama havuzu var olan uygulama hizmeti ortamı'nda hello seçeneği toochoose olacaktır.</span><span class="sxs-lookup"><span data-stu-id="536f0-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="536f0-120">Geçerli kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="536f0-120">Current Restrictions</span></span>
<span data-ttu-id="536f0-121">Bu özellik şu anda önizlemede değil, zaman içinde tooadd yeni özellikler çalışıyoruz, liste aşağıdaki hello Azure portalında uygulama kopyalama bilinen sınırlamalar hello geçerli desteği hello:</span><span class="sxs-lookup"><span data-stu-id="536f0-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="536f0-122">Azure Traffic Manager ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="536f0-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="536f0-123">Otomatik ölçek ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="536f0-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="536f0-124">Yedekleme zamanlaması ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="536f0-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="536f0-125">VNET ayarlarını klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="536f0-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="536f0-126">App Insights otomatik olarak hello hedef web uygulamasında belirlenmedi</span><span class="sxs-lookup"><span data-stu-id="536f0-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="536f0-127">Kolay kimlik doğrulama ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="536f0-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="536f0-128">Kudu uzantısı değil kopyalanamıyor</span><span class="sxs-lookup"><span data-stu-id="536f0-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="536f0-129">İpucu kuralları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="536f0-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="536f0-130">Veritabanı içeriğini değil kopyalanamıyor</span><span class="sxs-lookup"><span data-stu-id="536f0-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="536f0-131">Başvurular</span><span class="sxs-lookup"><span data-stu-id="536f0-131">References</span></span>
* [<span data-ttu-id="536f0-132">Web uygulaması PowerShell kullanarak kopyalama</span><span class="sxs-lookup"><span data-stu-id="536f0-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="536f0-133">Azure App Service'in web uygulamasında yedekleyin</span><span class="sxs-lookup"><span data-stu-id="536f0-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="536f0-134">Nasıl tooCreate bir uygulama hizmeti ortamı</span><span class="sxs-lookup"><span data-stu-id="536f0-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="536f0-135">App Service Ortamında bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="536f0-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="536f0-136">Giriş tooApp hizmeti ortamı</span><span class="sxs-lookup"><span data-stu-id="536f0-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
