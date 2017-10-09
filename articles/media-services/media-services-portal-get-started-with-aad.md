---
title: "aaaGet hello Azure portal kullanarak Azure AD kimlik doğrulamasıyla çalışmaya | Microsoft Docs"
description: "Nasıl toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) kimlik doğrulama tooconsume hello Azure Media Services API öğrenin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="9327e-103">Hello Azure portal kullanarak Azure AD kimlik doğrulaması ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9327e-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="9327e-104">Azure Media Services API toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) kimlik doğrulama tooaccess nasıl hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9327e-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9327e-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9327e-105">Prerequisites</span></span>

- <span data-ttu-id="9327e-106">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="9327e-106">An Azure account.</span></span> <span data-ttu-id="9327e-107">Bir hesabınız yoksa, başlayan bir [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9327e-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="9327e-108">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="9327e-108">A Media Services account.</span></span> <span data-ttu-id="9327e-109">Daha fazla bilgi için bkz: [hello Azure portal kullanarak Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="9327e-110">Merhaba gözden emin olun [Azure AD kimlik doğrulamasına genel bakış ile Azure Media Services API erişme](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="9327e-111">Azure Media Services ile Azure AD kimlik doğrulaması kullandığınızda, iki kimlik doğrulama seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="9327e-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="9327e-112">**Kullanıcı kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="9327e-112">**User authentication**.</span></span> <span data-ttu-id="9327e-113">Media Services kaynaklarla hello uygulama toointeract kullanan bir kişi kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="9327e-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="9327e-114">Merhaba etkileşimli uygulaması ilk hello kullanıcıdan kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="9327e-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="9327e-115">Bir örnek yetkili kullanıcıların toomonitor kodlama işlemler tarafından kullanılan bir yönetim konsol uygulaması ya da canlı akış.</span><span class="sxs-lookup"><span data-stu-id="9327e-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="9327e-116">**Hizmet asıl kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="9327e-116">**Service principal authentication**.</span></span> <span data-ttu-id="9327e-117">Bir hizmetin kimliğini.</span><span class="sxs-lookup"><span data-stu-id="9327e-117">Authenticate a service.</span></span> <span data-ttu-id="9327e-118">Bu kimlik doğrulama yöntemini yaygın olarak kullanan uygulamaları arka plan programı services, orta katman Hizmetleri veya zamanlanmış işler çalışan uygulamalar şunlardır: web uygulamaları, işlev uygulamalarının, logic apps, API veya bir mikro hizmet.</span><span class="sxs-lookup"><span data-stu-id="9327e-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9327e-119">Şu anda, Media Services hello Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="9327e-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="9327e-120">Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="9327e-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="9327e-121">Mümkün olan en kısa sürede toohello Azure AD kimlik doğrulama modeli geçirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="9327e-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="9327e-122">Merhaba kimlik doğrulama yöntemini seçin</span><span class="sxs-lookup"><span data-stu-id="9327e-122">Select hello authentication method</span></span>

1. <span data-ttu-id="9327e-123">Merhaba, [Azure portal](https://portal.azure.com/), Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="9327e-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="9327e-124">Select nasıl tooconnect toohello Media Services API.</span><span class="sxs-lookup"><span data-stu-id="9327e-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Bağlantı yöntemi sayfası seçin](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="9327e-126">Kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="9327e-126">User authentication</span></span>

<span data-ttu-id="9327e-127">kullanarak tooconnect toohello Media Services API Merhaba kullanıcı kimlik doğrulaması seçeneği, hello istemci uygulamanın toorequest şu parametreler hello sahip bir Azure AD belirteci gerekir:</span><span class="sxs-lookup"><span data-stu-id="9327e-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="9327e-128">Azure AD Kiracı uç noktası</span><span class="sxs-lookup"><span data-stu-id="9327e-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="9327e-129">Media Services kaynak URI'si</span><span class="sxs-lookup"><span data-stu-id="9327e-129">Media Services resource URI</span></span>
* <span data-ttu-id="9327e-130">Media Services (yerel) uygulama istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="9327e-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="9327e-131">Media Services (yerel) uygulama yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="9327e-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="9327e-132">Kaynak URI'si REST Media Services için</span><span class="sxs-lookup"><span data-stu-id="9327e-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="9327e-133">Bu parametrelerin hello üzerinde hello değerleri alabilirsiniz **kullanıcı kimlik doğrulaması ile Media Services API** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9327e-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Kullanıcı kimlik doğrulaması sayfası ile bağlanma](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="9327e-135">Hello Media Services Microsoft .NET SDK kullanarak toohello Media Services API bağlanıyorsanız hello değerleri kullanılabilir tooyou hello SDK bir parçası olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9327e-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="9327e-136">Daha fazla bilgi için bkz: [kullanım Azure AD kimlik doğrulama tooaccess hello .NET ile Azure Media Services API](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="9327e-137">Merhaba Media Services .NET İstemci SDK kullanmıyorsanız, daha önce bahsedilen hello parametrelerini kullanarak bir Azure AD belirteç isteği el ile oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="9327e-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="9327e-138">Daha fazla bilgi için bkz: [nasıl toouse hello Azure AD kimlik doğrulama kitaplığı tooget hello Azure AD belirteci](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="9327e-139">Hizmet sorumlusu kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="9327e-139">Service principal authentication</span></span>

<span data-ttu-id="9327e-140">Hizmet asıl seçeneğini kullanarak tooconnect toohello Media Services API Merhaba, orta katman uygulamanızın (web API ya da web uygulaması) toorequest şu parametreler hello sahip bir Azure AD belirteci gerekir:</span><span class="sxs-lookup"><span data-stu-id="9327e-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="9327e-141">Azure AD Kiracı uç noktası</span><span class="sxs-lookup"><span data-stu-id="9327e-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="9327e-142">Media Services kaynak URI'si</span><span class="sxs-lookup"><span data-stu-id="9327e-142">Media Services resource URI</span></span> 
* <span data-ttu-id="9327e-143">Kaynak URI'si REST Media Services için</span><span class="sxs-lookup"><span data-stu-id="9327e-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="9327e-144">Azure AD uygulama değerleri: Merhaba **istemci kimliği** ve **istemci parolası**</span><span class="sxs-lookup"><span data-stu-id="9327e-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="9327e-145">Bu parametrelerin hello üzerinde hello değerleri alabilirsiniz **tooMedia Hizmetleri API ile hizmet sorumlusu bağlanmak** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9327e-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="9327e-146">Bu sayfa toocreate yeni bir Azure kullanın AD uygulaması veya tooselect mevcut bir.</span><span class="sxs-lookup"><span data-stu-id="9327e-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="9327e-147">Hello Azure AD uygulaması seçtikten sonra hello istemci kimliği (uygulama kimliği) almak ve hello istemci gizli anahtarı (anahtar) değerlerini oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="9327e-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Hizmet asıl sayfasıyla Bağlan](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="9327e-149">Ne zaman hello **hizmet sorumlusu** dikey penceresi açıldığında, hello aşağıdaki ölçütleri karşılayan hello ilk Azure AD uygulaması seçili:</span><span class="sxs-lookup"><span data-stu-id="9327e-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="9327e-150">Kayıtlı olan Azure AD uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9327e-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="9327e-151">Katkıda bulunan veya Owner Role-Based erişim denetimi izinleri hello hesabında içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9327e-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="9327e-152">Oluşturma veya bir Azure AD uygulaması seçtikten sonra oluşturun ve istemci parolası (anahtar) kopyalayın ve istemci kimliği (uygulama kimliği) hello.</span><span class="sxs-lookup"><span data-stu-id="9327e-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="9327e-153">Bu senaryoda gerekli tooget hello erişim belirteci Hello istemci gizli anahtarı ve istemci kimliği var.</span><span class="sxs-lookup"><span data-stu-id="9327e-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="9327e-154">Etki alanınızda izinleri toocreate Azure AD uygulamalarınız yoksa, hello Azure AD uygulama denetimleri hello dikey gösterilmez ve bir uyarı iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9327e-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="9327e-155">Media Services API toohello hello Media Services .NET SDK kullanarak bağlanıyorsanız, bkz: [kullanım Azure AD kimlik doğrulama tooaccess hello .NET ile Azure Media Services API](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="9327e-156">Merhaba Media Services .NET İstemci SDK kullanmıyorsanız, daha önce bahsedilen hello parametrelerini kullanarak bir Azure AD belirteç isteği el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9327e-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="9327e-157">Daha fazla bilgi için bkz: [nasıl toouse hello Azure AD kimlik doğrulama kitaplığı tooget hello Azure AD belirteci](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="9327e-158">Merhaba istemci kimliği ve istemci parolası mı almak</span><span class="sxs-lookup"><span data-stu-id="9327e-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="9327e-159">Yeni bir tane var olan Azure AD uygulaması veya select hello seçeneği toocreate seçtikten sonra aşağıdaki düğmeler hello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="9327e-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![İzinler ve Yönet uygulama düğmesi yönetme](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="9327e-161">tooopen hello Azure AD uygulaması dikey penceresinde tıklatın **uygulamasını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9327e-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="9327e-162">Merhaba üzerinde **uygulamasını Yönet** dikey penceresinde hello uygulamanın istemci Kimliğini (uygulama kimliği) alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9327e-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="9327e-163">bir istemci parolası (anahtar), select toogenerate **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="9327e-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Uygulama dikey penceresinde anahtarlar seçeneğini yönetme](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="9327e-165">İzinler ve hello uygulama yönetme</span><span class="sxs-lookup"><span data-stu-id="9327e-165">Manage permissions and hello application</span></span>

<span data-ttu-id="9327e-166">Hello Azure AD uygulaması seçtikten sonra hello uygulama ve izinleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9327e-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="9327e-167">tooset diğer uygulamaları, Azure AD uygulama tooaccess tıklatın **izinleri yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="9327e-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="9327e-168">İçin yönetim görevleri, anahtarları ve yanıt URL'leri ya da tooedit hello uygulamanın bildirim değiştirme gibi tıklatın **uygulamasını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9327e-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="9327e-169">Merhaba uygulamanın ayarlarını düzenleyin veya bildirimi</span><span class="sxs-lookup"><span data-stu-id="9327e-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="9327e-170">tooedit hello uygulamanın ayarları veya bildirimi tıklatın **uygulamasını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9327e-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Uygulamasını Yönet sayfası](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="9327e-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9327e-172">Next steps</span></span>

<span data-ttu-id="9327e-173">Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="9327e-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
