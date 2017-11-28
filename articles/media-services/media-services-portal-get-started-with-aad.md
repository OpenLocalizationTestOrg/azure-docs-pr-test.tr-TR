---
title: "Azure portalı kullanarak Azure AD kimlik doğrulaması ile çalışmaya başlama | Microsoft Docs"
description: "Azure Media Services API kullanmak için Azure Active Directory (Azure AD) kimlik doğrulaması erişmek için Azure portalını kullanmayı öğrenin."
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
ms.openlocfilehash: 829e0759f8aeb8758f6b8895b88b60b66ffb22ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="41077-103">Azure portalı kullanarak Azure AD kimlik doğrulaması ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="41077-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="41077-104">Azure Media Services API erişmek için Azure Active Directory (Azure AD) kimlik doğrulaması erişmek için Azure portalını kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41077-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41077-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41077-105">Prerequisites</span></span>

- <span data-ttu-id="41077-106">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="41077-106">An Azure account.</span></span> <span data-ttu-id="41077-107">Bir hesabınız yoksa, başlayan bir [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41077-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="41077-108">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="41077-108">A Media Services account.</span></span> <span data-ttu-id="41077-109">Daha fazla bilgi için bkz: [Azure portalını kullanarak Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="41077-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="41077-110">Gözden geçirmeniz emin olun [Azure AD kimlik doğrulamasına genel bakış ile Azure Media Services API erişme](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="41077-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="41077-111">Azure Media Services ile Azure AD kimlik doğrulaması kullandığınızda, iki kimlik doğrulama seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="41077-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="41077-112">**Kullanıcı kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="41077-112">**User authentication**.</span></span> <span data-ttu-id="41077-113">Uygulama etkileşim kurmak için Media Services kaynaklarla kullanan bir kişi kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="41077-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="41077-114">Etkileşimli uygulama önce kullanıcıdan kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="41077-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="41077-115">Kodlama işleri izlemek veya canlı akış için yetkili kullanıcılar tarafından kullanılan bir yönetim konsol uygulaması örneğidir.</span><span class="sxs-lookup"><span data-stu-id="41077-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="41077-116">**Hizmet asıl kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="41077-116">**Service principal authentication**.</span></span> <span data-ttu-id="41077-117">Bir hizmetin kimliğini.</span><span class="sxs-lookup"><span data-stu-id="41077-117">Authenticate a service.</span></span> <span data-ttu-id="41077-118">Bu kimlik doğrulama yöntemini yaygın olarak kullanan uygulamaları arka plan programı services, orta katman Hizmetleri veya zamanlanmış işler çalışan uygulamalar şunlardır: web uygulamaları, işlev uygulamalarının, logic apps, API veya bir mikro hizmet.</span><span class="sxs-lookup"><span data-stu-id="41077-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41077-119">Şu anda, Media Services, Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="41077-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="41077-120">Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="41077-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="41077-121">Azure AD kimlik doğrulama modeline mümkün olan en kısa sürede geçirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="41077-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="41077-122">Kimlik doğrulama yöntemini seçin</span><span class="sxs-lookup"><span data-stu-id="41077-122">Select the authentication method</span></span>

1. <span data-ttu-id="41077-123">İçinde [Azure portal](https://portal.azure.com/), Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="41077-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="41077-124">Medya Hizmetleri API'sine bağlanma seçin.</span><span class="sxs-lookup"><span data-stu-id="41077-124">Select how to connect to the Media Services API.</span></span>

    ![Bağlantı yöntemi sayfası seçin](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="41077-126">Kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="41077-126">User authentication</span></span>

<span data-ttu-id="41077-127">Kullanıcı kimlik doğrulama seçeneğini kullanarak Media Services API'sine bağlanmak için aşağıdaki parametreleri olan bir Azure AD belirteç istemek istemci uygulamanın gerekir:</span><span class="sxs-lookup"><span data-stu-id="41077-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="41077-128">Azure AD Kiracı uç noktası</span><span class="sxs-lookup"><span data-stu-id="41077-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="41077-129">Media Services kaynak URI'si</span><span class="sxs-lookup"><span data-stu-id="41077-129">Media Services resource URI</span></span>
* <span data-ttu-id="41077-130">Media Services (yerel) uygulama istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="41077-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="41077-131">Media Services (yerel) uygulama yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="41077-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="41077-132">Kaynak URI'si REST Media Services için</span><span class="sxs-lookup"><span data-stu-id="41077-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="41077-133">Değerleri bu parametreler için alma **kullanıcı kimlik doğrulaması ile Media Services API** sayfası.</span><span class="sxs-lookup"><span data-stu-id="41077-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![Kullanıcı kimlik doğrulaması sayfası ile bağlanma](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="41077-135">Media Services Microsoft .NET SDK'sını kullanarak Media Services API'sine bağlanıyorsanız, gerekli değerleri, SDK'ın bir parçası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="41077-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="41077-136">Daha fazla bilgi için bkz: [.NET ile Azure Media Services API erişmek için kimlik doğrulamasını kullan Azure AD](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="41077-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="41077-137">Media Services .NET İstemci SDK kullanmıyorsanız, daha önce açıklanan parametreleri kullanarak bir Azure AD belirteç isteği el ile oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="41077-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="41077-138">Daha fazla bilgi için bkz: [Azure AD belirtecini almak için Azure AD kimlik doğrulama kitaplığı kullanmayı](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="41077-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="41077-139">Hizmet sorumlusu kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="41077-139">Service principal authentication</span></span>

<span data-ttu-id="41077-140">Hizmet asıl seçeneğini kullanarak Media Services API'sine bağlanmak için aşağıdaki parametreleri olan bir Azure AD belirteç istemek Orta katmanda uygulamanızı (web API ya da web uygulaması) gerekir:</span><span class="sxs-lookup"><span data-stu-id="41077-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="41077-141">Azure AD Kiracı uç noktası</span><span class="sxs-lookup"><span data-stu-id="41077-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="41077-142">Media Services kaynak URI'si</span><span class="sxs-lookup"><span data-stu-id="41077-142">Media Services resource URI</span></span> 
* <span data-ttu-id="41077-143">Kaynak URI'si REST Media Services için</span><span class="sxs-lookup"><span data-stu-id="41077-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="41077-144">Azure AD uygulama değerleri: **istemci kimliği** ve **istemci parolası**</span><span class="sxs-lookup"><span data-stu-id="41077-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="41077-145">Değerleri bu parametreler için alma **Media Services API hizmet asıl Bağlan** sayfası.</span><span class="sxs-lookup"><span data-stu-id="41077-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="41077-146">Yeni bir oluşturmak için bu sayfayı kullanın Azure AD uygulaması veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="41077-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="41077-147">Azure AD uygulaması seçtikten sonra istemci kimliği (uygulama kimliği) almak ve istemci gizli anahtarı (anahtar) değerlerini oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="41077-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![Hizmet asıl sayfasıyla Bağlan](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="41077-149">Zaman **hizmet sorumlusu** dikey penceresi açıldığında, aşağıdaki ölçütleri karşılaması ilk Azure AD uygulaması seçilir:</span><span class="sxs-lookup"><span data-stu-id="41077-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="41077-150">Kayıtlı olan Azure AD uygulaması.</span><span class="sxs-lookup"><span data-stu-id="41077-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="41077-151">Bu hesapta katkıda bulunan veya Owner Role-Based erişim denetimi iznine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="41077-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="41077-152">Oluşturma veya bir Azure AD uygulaması seçtikten sonra oluşturun ve istemci parolası (anahtar) ve istemci kimliği (uygulama kimliği) kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="41077-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="41077-153">İstemci kimliği ve istemci parolası erişim Bu senaryoda belirtecini almak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="41077-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="41077-154">Etki alanınızda Azure AD uygulamaları oluşturmak için izinlere sahip değilseniz, Azure AD uygulama denetimleri dikey gösterilmez ve bir uyarı iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="41077-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="41077-155">Media Services .NET SDK'sını kullanarak Media Services API'sine bağlanmak istiyorsanız bkz [.NET ile Azure Media Services API erişmek için kimlik doğrulamasını kullan Azure AD](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="41077-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="41077-156">Media Services .NET İstemci SDK kullanmıyorsanız, daha önce açıklanan parametreleri kullanarak bir Azure AD belirteç isteği el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="41077-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="41077-157">Daha fazla bilgi için bkz: [Azure AD belirtecini almak için Azure AD kimlik doğrulama kitaplığı kullanmayı](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="41077-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="41077-158">İstemci Kimliğini ve istemci gizli anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="41077-158">Get the client ID and client secret</span></span>

<span data-ttu-id="41077-159">Var olan bir Azure AD uygulama seçin veya yeni bir tane oluşturmak için seçeneği seçtikten sonra aşağıdaki düğmeler görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="41077-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![İzinler ve Yönet uygulama düğmesi yönetme](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="41077-161">Azure AD uygulaması dikey penceresini açmak için **uygulamasını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="41077-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="41077-162">Üzerinde **uygulamasını Yönet** dikey penceresinde, uygulamanın istemci Kimliğini (uygulama kimliği) alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41077-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="41077-163">İstemci parolası (anahtar) oluşturmak için seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="41077-163">To generate a client secret (key), select **Keys**.</span></span>

![Uygulama dikey penceresinde anahtarlar seçeneğini yönetme](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="41077-165">İzinler ve uygulama yönetme</span><span class="sxs-lookup"><span data-stu-id="41077-165">Manage permissions and the application</span></span>

<span data-ttu-id="41077-166">Azure AD uygulaması seçtikten sonra izinleri ve uygulama yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41077-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="41077-167">Diğer uygulamalara erişmek için Azure AD uygulamanızı ayarlama için tıklatın **izinleri yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="41077-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="41077-168">İçin yönetim görevleri, anahtarları ve yanıt URL'leri değiştirme gibi veya uygulama bildirimi düzenlemek için tıklatın **uygulamasını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="41077-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="41077-169">Listesi veya uygulamanın ayarlarını Düzenle</span><span class="sxs-lookup"><span data-stu-id="41077-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="41077-170">Uygulamanın ayarları ya da bildirim düzenlemek için tıklatın **uygulamasını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="41077-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![Uygulamasını Yönet sayfası](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="41077-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41077-172">Next steps</span></span>

<span data-ttu-id="41077-173">Kullanmaya başlama [dosyaları hesabınıza Yükleniyor](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="41077-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
