---
title: aaaDeploy, uygulama tooAzure uygulama FTP/S kullanarak hizmeti | Microsoft Docs
description: "Bilgi nasıl toodeploy uygulama hizmetini kullanarak FTP veya FTPS, uygulama tooAzure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="55fd9-103">Uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="55fd9-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="55fd9-104">Bu makale size nasıl gösterir toouse FTP veya web uygulaması, mobil uygulama arka ucu veya API uygulaması toodeploy çok FTPS[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="55fd9-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="55fd9-105">Uygulamanız için Hello FTP/S uç nokta zaten etkindir.</span><span class="sxs-lookup"><span data-stu-id="55fd9-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="55fd9-106">Herhangi bir yapılandırma gerekli tooenable FTP/S dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="55fd9-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55fd9-107">Biz, sürekli olarak adımları tooimprove Microsoft Azure platformu güvenlik sürüyor.</span><span class="sxs-lookup"><span data-stu-id="55fd9-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="55fd9-108">Devam eden bu çalışmaların bir parçası olarak Web uygulamaları yükseltmesini Almanya merkezi ve Almanya Kuzeydoğu bölgeler için planlanmış bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="55fd9-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="55fd9-109">Bu sırasında Web Apps hello dağıtımlar için düz metin FTP Protokolü kullanımını devre dışı bırakma.</span><span class="sxs-lookup"><span data-stu-id="55fd9-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="55fd9-110">Öneri tooour müşterilerimizin dağıtımlar için tooswitch tooFTPS olur.</span><span class="sxs-lookup"><span data-stu-id="55fd9-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="55fd9-111">Herhangi bir bozulma tooyour hizmeti için 9/5 planlandığı bu yükseltme sırasında bekliyoruz değil.</span><span class="sxs-lookup"><span data-stu-id="55fd9-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="55fd9-112">Değer veriyoruz bu çaba destekler.</span><span class="sxs-lookup"><span data-stu-id="55fd9-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="55fd9-113">1. adım: dağıtım kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="55fd9-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="55fd9-114">tooaccess hello FTP sunucusu, uygulamanız için önce dağıtım kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="55fd9-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="55fd9-115">Dağıtım kimlik bilgilerinizi tooset veya sıfırlama bkz [Azure uygulama hizmeti dağıtım kimlik bilgileri](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="55fd9-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="55fd9-116">Bu öğretici, kullanıcı düzeyinde kimlik bilgilerinin hello kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="55fd9-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="55fd9-117">2. adım: FTP bağlantı bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="55fd9-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="55fd9-118">Merhaba, [Azure portal](https://portal.azure.com), uygulamanızın açmak [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="55fd9-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="55fd9-119">Seçin **genel bakış** hello soldaki menüde sonra hello değerlerini Not **FTP/dağıtım kullanıcı**, **FTP konak adı**, ve **FTPS konak adı**.</span><span class="sxs-lookup"><span data-stu-id="55fd9-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP bağlantı bilgileri](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="55fd9-121">Merhaba **FTP/dağıtım kullanıcı** kullanıcı değeri tarafından görüntülenen hello hello FTP sunucusu için sipariş tooprovide uygun bağlamında hello uygulama adı dahil olmak üzere Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="55fd9-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="55fd9-122">Bulabileceğiniz seçtiğinizde aynı bilgileri hello **özellikleri** hello soldaki menüde.</span><span class="sxs-lookup"><span data-stu-id="55fd9-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="55fd9-123">Ayrıca, hello dağıtım parola hiçbir zaman gösterilir.</span><span class="sxs-lookup"><span data-stu-id="55fd9-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="55fd9-124">Dağıtım parolanızı unutursanız, çok dön[1. adım](#step1) ve dağıtım parolanızı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="55fd9-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="55fd9-125">Adım 3: dosyaları tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="55fd9-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="55fd9-126">FTP istemcisinden ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), vb.), tooconnect tooyour uygulama topladığınız hello bağlantı bilgisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="55fd9-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="55fd9-127">Dosyalarınızı ve bunların ilgili dizin yapısı toohello kopyalama [ **/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure (veya hello **/site/wwwroot/App_Data/işleri/** için dizin Web işleri).</span><span class="sxs-lookup"><span data-stu-id="55fd9-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="55fd9-128">Gözat tooyour uygulamanın URL tooverify hello uygulama düzgün çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="55fd9-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="55fd9-129">Farklı [Git tabanlı dağıtımlar](app-service-deploy-local-git.md), FTP dağıtım dağıtım otomasyonlara aşağıdaki hello desteklemez:</span><span class="sxs-lookup"><span data-stu-id="55fd9-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="55fd9-130">bağımlılık geri yükleme (örneğin, NuGet, NPM, PIP ve oluşturucu otomasyonlara)</span><span class="sxs-lookup"><span data-stu-id="55fd9-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="55fd9-131">.NET ikili dosyalarının derlenmesini</span><span class="sxs-lookup"><span data-stu-id="55fd9-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="55fd9-132">web.config nesil (burada bir [Node.js örnek](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="55fd9-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="55fd9-133">Geri yükleme gerekir, yapı ve bu gerekli dosyalar yerel makinenizde el ile oluşturmak ve bunları uygulamanızı birlikte dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55fd9-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="55fd9-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55fd9-134">Next steps</span></span>

<span data-ttu-id="55fd9-135">Daha gelişmiş dağıtım senaryoları için deneyin [tooAzure Git ile dağıtma](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="55fd9-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="55fd9-136">Git tabanlı dağıtım tooAzure sürüm denetimi, paket geri yüklemesi, MSBuild ve daha fazlasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="55fd9-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="55fd9-137">Daha Fazla Kaynak</span><span class="sxs-lookup"><span data-stu-id="55fd9-137">More Resources</span></span>

* <span data-ttu-id="55fd9-138">[Bir PHP MySQL web uygulaması oluşturun ve FTP dağıtmanızı](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="55fd9-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="55fd9-139">Azure uygulama hizmeti dağıtım kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="55fd9-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
