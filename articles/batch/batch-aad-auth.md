---
title: "aaaUse Azure Active Directory tooauthenticate Azure Batch hizmeti çözümleri | Microsoft Docs"
description: "Toplu Azure AD hello Batch hizmeti kimlik doğrulamasını destekler."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="98526-103">Toplu hizmet çözümlerine Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="98526-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="98526-104">Azure Batch destekleyen kimlik doğrulama ile [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98526-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="98526-105">Azure AD, Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti ' dir.</span><span class="sxs-lookup"><span data-stu-id="98526-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="98526-106">Azure kendisi, müşteriler, hizmet yöneticileri ve kuruluş kullanıcıları Azure AD tooauthenticate kullanır.</span><span class="sxs-lookup"><span data-stu-id="98526-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="98526-107">Azure AD kimlik doğrulaması ile Azure Batch kullanırken, aşağıdaki iki yöntemden biriyle doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="98526-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="98526-108">Kullanarak **tümleşik kimlik doğrulaması** tooauthenticate hello uygulama ile etkileşim bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="98526-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="98526-109">Tümleşik kimlik doğrulaması kullanarak bir uygulamayı bir kullanıcının kimlik bilgilerini toplar ve bu kimlik bilgileri tooauthenticate erişim tooBatch kaynakları kullanır.</span><span class="sxs-lookup"><span data-stu-id="98526-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="98526-110">Kullanarak bir **hizmet sorumlusu** tooauthenticate katılımsız bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="98526-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="98526-111">Bir hizmet sorumlusu hello İlkesi ve bir uygulama için izinler çalışma zamanında kaynaklara erişirken sipariş toorepresent hello uygulamada tanımlar.</span><span class="sxs-lookup"><span data-stu-id="98526-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="98526-112">Azure AD hakkında daha fazla toolearn bkz hello [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="98526-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="98526-113">Kimlik doğrulama ve havuzu ayırma modu</span><span class="sxs-lookup"><span data-stu-id="98526-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="98526-114">Bir toplu işlem hesabı oluşturduğunuzda, o hesap için oluşturulan havuzlarının burada ayrılmalıdır belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98526-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="98526-115">Merhaba varsayılan Batch hizmeti aboneliğiniz veya bir kullanıcı abonelik tooallocate havuzları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98526-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="98526-116">Tercih ettiğiniz bu hesaptaki erişim tooresources nasıl kimlik doğrulaması etkiler.</span><span class="sxs-lookup"><span data-stu-id="98526-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="98526-117">**Batch hizmeti abonelik**.</span><span class="sxs-lookup"><span data-stu-id="98526-117">**Batch service subscription**.</span></span> <span data-ttu-id="98526-118">Varsayılan olarak, bir toplu işlem hizmeti abonelikte Batch havuzları ayrılır.</span><span class="sxs-lookup"><span data-stu-id="98526-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="98526-119">Bu seçeneği seçerseniz, size bu hesaptaki erişim tooresources ile ya da doğrulayabilir [paylaşılan anahtar](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) veya Azure AD ile.</span><span class="sxs-lookup"><span data-stu-id="98526-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="98526-120">**Kullanıcı aboneliği.**</span><span class="sxs-lookup"><span data-stu-id="98526-120">**User subscription.**</span></span> <span data-ttu-id="98526-121">Batch havuzları, belirttiğiniz bir kullanıcı aboneliği tooallocate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98526-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="98526-122">Bu seçeneği seçerseniz, Azure AD ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98526-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="98526-123">Kimlik doğrulaması için uç noktalar</span><span class="sxs-lookup"><span data-stu-id="98526-123">Endpoints for authentication</span></span>

<span data-ttu-id="98526-124">Azure AD ile tooauthenticate toplu iş uygulamaları, gereksinim duyduğunuz tooinclude kodunuzda iyi bilinen bazı uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="98526-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="98526-125">Azure AD uç noktası</span><span class="sxs-lookup"><span data-stu-id="98526-125">Azure AD endpoint</span></span>

<span data-ttu-id="98526-126">Merhaba temel Azure AD yetkilisi uç noktası:</span><span class="sxs-lookup"><span data-stu-id="98526-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="98526-127">Azure AD ile tooauthenticate, bu uç noktaya hello Kiracı kimliği (dizin kimliği) ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="98526-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="98526-128">Merhaba Kiracı kimliği hello Azure AD Kiracı toouse kimlik doğrulaması için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="98526-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="98526-129">tooretrieve Kiracı kimliği Merhaba, özetlenen hello adımları [hello Kiracı Kimliği almak için Azure Active Directory'yi](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="98526-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="98526-130">bir hizmet sorumlusunu kullanarak kimlik doğrulaması sırasında hello Kiracı özgü uç noktası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="98526-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="98526-131">tümleşik kimlik doğrulaması kullanarak kimlik doğrulaması sırasında isteğe bağlıdır, ancak önerilen Hello Kiracı özgü uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="98526-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="98526-132">Ancak, hello Azure AD ortak uç nokta de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98526-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="98526-133">Merhaba ortak uç nokta belirli bir kiracı sağlanmadığında arabirimi toplama genel bir kimlik bilgisi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="98526-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="98526-134">Merhaba ortak uç noktası `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="98526-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="98526-135">Azure AD uç noktaları hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="98526-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="98526-136">Batch kaynak uç noktası</span><span class="sxs-lookup"><span data-stu-id="98526-136">Batch resource endpoint</span></span>

<span data-ttu-id="98526-137">Kullanım hello **Azure Batch kaynak endpoint** tooacquire kimlik doğrulaması için bir belirteç isteklerini toohello Batch hizmeti:</span><span class="sxs-lookup"><span data-stu-id="98526-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="98526-138">Bir kiracı ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="98526-138">Register your application with a tenant</span></span>

<span data-ttu-id="98526-139">Azure AD tooauthenticate kullanarak hello ilk adımı uygulamanız bir Azure AD kiracısında kaydediyor.</span><span class="sxs-lookup"><span data-stu-id="98526-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="98526-140">Uygulamanızı kaydetme sağlar toocall hello Azure [Active Directory kimlik doğrulama Kitaplığı] [ aad_adal] (ADAL) kodunuzdan.</span><span class="sxs-lookup"><span data-stu-id="98526-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="98526-141">Merhaba ADAL uygulamanızdan Azure AD ile kimlik doğrulaması için bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="98526-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="98526-142">Uygulamanızı kaydetme toouse tümleşik kimlik doğrulaması veya bir hizmet sorumlusu planlama olup olmadığını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="98526-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="98526-143">Uygulamanızı kaydederken, uygulama tooAzure AD hakkında bilgi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="98526-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="98526-144">Ardından Azure AD uygulama kimliği sağlar çalışma zamanında Azure AD ile uygulamanızı tooassociate kullanın.</span><span class="sxs-lookup"><span data-stu-id="98526-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="98526-145">toolearn hello uygulama kimliği hakkında daha fazla bilgi görmek [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="98526-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="98526-146">tooregister toplu uygulamanızı hello adımları hello içinde [bir uygulama ekleme](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) bölümüne [uygulamaları Azure Active Directory ile tümleştirme][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="98526-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="98526-147">Yerel bir uygulama olarak, uygulamanızın kaydolursanız, hello için geçerli bir URI belirtebilirsiniz **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="98526-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="98526-148">Toobe gerçek bir uç noktası gerekmez.</span><span class="sxs-lookup"><span data-stu-id="98526-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="98526-149">Uygulamanızı kaydınız sonra hello uygulama kimliği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="98526-149">After you've registered your application, you'll see hello application ID:</span></span>

![Batch uygulamanızı Azure AD ile kaydetme](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="98526-151">Uygulama Azure AD ile kaydetme hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="98526-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="98526-152">Active Directory için Hello Kiracı Kimliğinizi alma</span><span class="sxs-lookup"><span data-stu-id="98526-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="98526-153">Merhaba Kiracı kimliği, kimlik doğrulama hizmetleri tooyour uygulamanın sağladığı hello Azure AD kiracısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="98526-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="98526-154">tooget Kiracı kimliği Merhaba, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="98526-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="98526-155">Hello Azure portal, Active Directory seçin.</span><span class="sxs-lookup"><span data-stu-id="98526-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="98526-156">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98526-156">Click **Properties**.</span></span>
3. <span data-ttu-id="98526-157">Merhaba dizin kimliği için sağlanan hello GUID değeri kopyalayın</span><span class="sxs-lookup"><span data-stu-id="98526-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="98526-158">Bu değer hello Kiracı kimliği olarak da adlandırılır</span><span class="sxs-lookup"><span data-stu-id="98526-158">This value is also called hello tenant ID.</span></span>

![Merhaba dizin Kimliğini kopyalayın](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="98526-160">Tümleşik kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="98526-160">Use integrated authentication</span></span>

<span data-ttu-id="98526-161">tooauthenticate ile tümleşik kimlik doğrulaması, uygulama izinleri tooconnect toohello Batch hizmeti API'si toogrant gerekir.</span><span class="sxs-lookup"><span data-stu-id="98526-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="98526-162">Bu adım, uygulama tooauthenticate çağrıları toohello Batch hizmeti API'si Azure AD ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="98526-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="98526-163">Seçtiğiniz sonra [uygulamanızı kayıtlı](#register-your-application-with-an-azure-ad-tenant), hello toohello Batch hizmeti erişim Azure portalı toogrant'nda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="98526-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="98526-164">Merhaba sol gezinti bölmesinde hello Azure portal'ı seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="98526-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="98526-165">Merhaba listesinde uygulamanızın uygulama kayıtların hello adını arayın:</span><span class="sxs-lookup"><span data-stu-id="98526-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Uygulama adınız arayın](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="98526-167">Açık hello **ayarları** dikey penceresinde uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="98526-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="98526-168">Merhaba, **API erişimini** bölümünde, select **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="98526-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="98526-169">Hello içinde **gerekli izinleri** dikey penceresinde hello tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98526-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="98526-170">1. adımda toplu API hello için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="98526-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="98526-171">Arama hello API bulana kadar bu dizelerin her biri için:</span><span class="sxs-lookup"><span data-stu-id="98526-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="98526-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="98526-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="98526-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="98526-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="98526-174">Daha yeni Azure AD kiracıları bu adı kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="98526-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="98526-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** hello toplu API hello kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="98526-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="98526-176">Merhaba toplu API bulduktan sonra onu seçin ve hello tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98526-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="98526-177">2. adımda seç onay kutusunu sonraki çok hello**erişim Azure Batch hizmeti** hello tıklatıp **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98526-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="98526-178">Merhaba tıklatın **Bitti** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98526-178">Click hello **Done** button.</span></span>

<span data-ttu-id="98526-179">Merhaba **gerekli izinler** tooboth ADAL erişmek ve toplu işlem hizmeti API'si Merhaba, Azure AD uygulaması yok gösterir artık dikey.</span><span class="sxs-lookup"><span data-stu-id="98526-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="98526-180">Uygulamanızı Azure AD ile ilk kez kaydederken izinleri tooADAL otomatik olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="98526-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![GRANT API izinleri](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="98526-182">Bir hizmet sorumlusu kullanın</span><span class="sxs-lookup"><span data-stu-id="98526-182">Use a service principal</span></span> 

<span data-ttu-id="98526-183">tooauthenticate katılımsız çalışan bir uygulama, bir hizmet sorumlusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="98526-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="98526-184">Uygulamanızı kaydınız sonra hello Azure portal tooconfigure bir hizmet sorumlusu'nda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="98526-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="98526-185">Uygulamanız için gizli bir anahtar isteyin.</span><span class="sxs-lookup"><span data-stu-id="98526-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="98526-186">RBAC rolü tooyour uygulama atama.</span><span class="sxs-lookup"><span data-stu-id="98526-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="98526-187">Uygulamanız için gizli bir anahtarı iste</span><span class="sxs-lookup"><span data-stu-id="98526-187">Request a secret key for your application</span></span>

<span data-ttu-id="98526-188">Uygulamanızın hizmet sorumlusuyla kimlik doğruladığında, hello uygulama kimliği ve gizli anahtar tooAzure AD gönderir.</span><span class="sxs-lookup"><span data-stu-id="98526-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="98526-189">Toocreate ihtiyacınız ve kodunuzdan hello gizli anahtar toouse kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="98526-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="98526-190">Hello Azure Portalı'nda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="98526-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="98526-191">Merhaba sol gezinti bölmesinde hello Azure portal'ı seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="98526-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="98526-192">Merhaba listesinde uygulamanızın uygulama kayıtların hello adını arayın.</span><span class="sxs-lookup"><span data-stu-id="98526-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="98526-193">Görüntü hello **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="98526-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="98526-194">Merhaba, **API erişimini** bölümünde, select **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="98526-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="98526-195">toocreate bir anahtar hello anahtarı için bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="98526-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="98526-196">Ardından bir veya iki yıllık hello anahtarı için bir süre seçin.</span><span class="sxs-lookup"><span data-stu-id="98526-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="98526-197">Hello tıklatın **kaydetmek** düğmesini toocreate ve başlangıç anahtarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="98526-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="98526-198">Mümkün tooaccess olmayacak şekilde hello anahtar değeri tooa güvenli bir yerde, kopyalayın, sonra yeniden bırakın hello dikey.</span><span class="sxs-lookup"><span data-stu-id="98526-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Gizli bir anahtar oluşturun](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="98526-200">RBAC rolü tooyour uygulama atama</span><span class="sxs-lookup"><span data-stu-id="98526-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="98526-201">tooauthenticate bir hizmet asıl tooassign RBAC rolü tooyour uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="98526-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="98526-202">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="98526-202">Follow these steps:</span></span>

1. <span data-ttu-id="98526-203">Hello Azure portal, uygulamanız tarafından kullanılan toohello toplu işlem hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="98526-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="98526-204">Merhaba, **ayarları** dikey penceresinde hello toplu işlem hesabı için select **erişim denetimi (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="98526-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="98526-205">Merhaba tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98526-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="98526-206">Merhaba gelen **rol** açılan listesinde, her iki hello seçin _katkıda bulunan_ veya _okuyucu_ rolü uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="98526-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="98526-207">Bu rolleri hakkında daha fazla bilgi için bkz: [hello Azure portal'ın rol tabanlı erişim denetimi ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="98526-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="98526-208">Merhaba, **seçin** alanında, uygulamanızın hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="98526-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="98526-209">Uygulamanızı hello listeden seçin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="98526-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="98526-210">Uygulamanız artık bir RBAC rolü atanmış erişim denetimi ayarlarınızda görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="98526-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![RBAC rolü tooyour uygulama atama](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="98526-212">Azure Active Directory için Hello Kiracı Kimliğinizi alma</span><span class="sxs-lookup"><span data-stu-id="98526-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="98526-213">Merhaba Kiracı kimliği, kimlik doğrulama hizmetleri tooyour uygulamanın sağladığı hello Azure AD kiracısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="98526-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="98526-214">tooget Kiracı kimliği Merhaba, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="98526-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="98526-215">Hello Azure portal, Active Directory seçin.</span><span class="sxs-lookup"><span data-stu-id="98526-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="98526-216">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98526-216">Click **Properties**.</span></span>
3. <span data-ttu-id="98526-217">Merhaba dizin kimliği için sağlanan hello GUID değeri kopyalayın</span><span class="sxs-lookup"><span data-stu-id="98526-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="98526-218">Bu değer hello Kiracı kimliği olarak da adlandırılır</span><span class="sxs-lookup"><span data-stu-id="98526-218">This value is also called hello tenant ID.</span></span>

![Merhaba dizin Kimliğini kopyalayın](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="98526-220">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="98526-220">Code examples</span></span>

<span data-ttu-id="98526-221">Bu bölümdeki Hello kod örnekleri tooauthenticate kullanarak Azure AD ile tümleşik kimlik doğrulaması nasıl ve bir hizmet sorumlusu gösterir.</span><span class="sxs-lookup"><span data-stu-id="98526-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="98526-222">Bu kod örnekleri .NET kullanır, ancak hello kavramları diğer diller için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="98526-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="98526-223">Azure AD kimlik doğrulama belirtecini bir saat sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="98526-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="98526-224">Bir uzun süreli kullanırken **BatchClient** nesnesi, bir belirteç almak öneririz ADAL her isteği tooensure özelliğini, her zaman geçerli bir belirteci vardır.</span><span class="sxs-lookup"><span data-stu-id="98526-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="98526-225">tooachieve bu .NET yazma bir yöntemi alır Azure AD'den belirteci hello ve bu yöntem tooa geçirin **BatchTokenCredentials** temsilci olarak nesne.</span><span class="sxs-lookup"><span data-stu-id="98526-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="98526-226">Geçerli bir belirteci sağlanan her isteği toohello Batch hizmeti tooensure üzerinde Hello temsilci yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="98526-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="98526-227">Yeni bir belirteç Azure AD'den alınan için varsayılan olarak ADAL belirteçleri, önbelleğe alır. yalnızca gerekli olduğunda.</span><span class="sxs-lookup"><span data-stu-id="98526-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="98526-228">Azure AD'de belirteçleri hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="98526-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="98526-229">Kod örneği: Batch .NET ile tümleşik kimlik doğrulaması Azure AD kullanma</span><span class="sxs-lookup"><span data-stu-id="98526-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="98526-230">Batch .NET, başvuru hello tümleşik kimlik doğrulamasını ile tooauthenticate [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) paket ve hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paket.</span><span class="sxs-lookup"><span data-stu-id="98526-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="98526-231">Merhaba şunlar `using` deyimlerinde kodunuzu:</span><span class="sxs-lookup"><span data-stu-id="98526-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="98526-232">Başvuru hello Azure AD endpoint hello dahil olmak üzere, kodunuzda Kiracı kimliği.</span><span class="sxs-lookup"><span data-stu-id="98526-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="98526-233">tooretrieve Kiracı kimliği Merhaba, özetlenen hello adımları [hello Kiracı Kimliği almak için Azure Active Directory'yi](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="98526-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="98526-234">Başvuru hello Batch hizmeti kaynak uç noktası:</span><span class="sxs-lookup"><span data-stu-id="98526-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="98526-235">Batch hesabınıza başvurusu:</span><span class="sxs-lookup"><span data-stu-id="98526-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="98526-236">Uygulamanız için Hello uygulama kimliği (istemci kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="98526-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="98526-237">Merhaba uygulama kimliği uygulama kaydınızı hello Azure portalı içinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="98526-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="98526-238">Ayrıca hello yeniden yönlendirme hello kayıt işlemi sırasında belirtilen URI'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="98526-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="98526-239">Merhaba yeniden yönlendirme URI'si kodunuzda belirtilen hello yeniden yönlendirme Merhaba uygulaması kaydolurken sağladığınız URI eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="98526-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="98526-240">Bir geri çağırma yöntemi tooacquire hello kimlik doğrulama belirteci Azure AD'den yazma.</span><span class="sxs-lookup"><span data-stu-id="98526-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="98526-241">Merhaba **GetAuthenticationTokenAsync** burada gösterilen geri çağırma yöntemi hello uygulama ile etkileşim bir kullanıcı ADAL tooauthenticate çağırır.</span><span class="sxs-lookup"><span data-stu-id="98526-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="98526-242">Merhaba **AcquireTokenAsync** yöntemi tarafından ADAL istemleri kullanıcı kimlik bilgilerinin hello ve Merhaba uygulaması ilerler kez hello kullanıcı sağlanan sağlar bunları (Bu zaten kimlik bilgilerini önbelleğe sürece):</span><span class="sxs-lookup"><span data-stu-id="98526-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="98526-243">Oluşturmak bir **BatchTokenCredentials** hello temsilcisi bir parametre olarak alan nesne.</span><span class="sxs-lookup"><span data-stu-id="98526-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="98526-244">Bu kimlik bilgileri tooopen kullanan bir **BatchClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="98526-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="98526-245">Kullanan **BatchClient** nesne hello Batch hizmeti karşı sonraki işlemleri için:</span><span class="sxs-lookup"><span data-stu-id="98526-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="98526-246">Kod örneği: Azure AD hizmet sorumlusu Batch .NET ile kullanma</span><span class="sxs-lookup"><span data-stu-id="98526-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="98526-247">Batch .NET, başvuru hello alanından bir hizmet asıl tooauthenticate [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) paket ve hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paket.</span><span class="sxs-lookup"><span data-stu-id="98526-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="98526-248">Merhaba şunlar `using` deyimlerinde kodunuzu:</span><span class="sxs-lookup"><span data-stu-id="98526-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="98526-249">Başvuru hello Azure AD endpoint hello dahil olmak üzere, kodunuzda Kiracı kimliği.</span><span class="sxs-lookup"><span data-stu-id="98526-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="98526-250">Bir hizmet sorumlusu kullanırken, bir kiracı özel uç noktası sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98526-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="98526-251">tooretrieve Kiracı kimliği Merhaba, özetlenen hello adımları [hello Kiracı Kimliği almak için Azure Active Directory'yi](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="98526-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="98526-252">Başvuru hello Batch hizmeti kaynak uç noktası:</span><span class="sxs-lookup"><span data-stu-id="98526-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="98526-253">Batch hesabınıza başvurusu:</span><span class="sxs-lookup"><span data-stu-id="98526-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="98526-254">Uygulamanız için Hello uygulama kimliği (istemci kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="98526-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="98526-255">Merhaba uygulama kimliği uygulama kaydınızı hello Azure portalı içinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="98526-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="98526-256">Azure portal hello kopyalanan hello gizli anahtarı belirtin:</span><span class="sxs-lookup"><span data-stu-id="98526-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="98526-257">Bir geri çağırma yöntemi tooacquire hello kimlik doğrulama belirteci Azure AD'den yazma.</span><span class="sxs-lookup"><span data-stu-id="98526-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="98526-258">Merhaba **GetAuthenticationTokenAsync** katılımsız kimlik doğrulaması için ADAL çağrıları burada gösterilen geri çağırma yöntemi:</span><span class="sxs-lookup"><span data-stu-id="98526-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="98526-259">Oluşturmak bir **BatchTokenCredentials** hello temsilcisi bir parametre olarak alan nesne.</span><span class="sxs-lookup"><span data-stu-id="98526-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="98526-260">Bu kimlik bilgileri tooopen kullanan bir **BatchClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="98526-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="98526-261">Ardından, kullanabileceğiniz **BatchClient** nesne hello Batch hizmeti karşı sonraki işlemleri için:</span><span class="sxs-lookup"><span data-stu-id="98526-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="98526-262">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98526-262">Next steps</span></span>

<span data-ttu-id="98526-263">Azure AD hakkında daha fazla toolearn bkz hello [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="98526-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="98526-264">Nasıl toouse ADAL kullanılabilir hello gösteren ayrıntılı örnekler [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=active-directory) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="98526-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="98526-265">Hizmet sorumluları hakkında daha fazla toolearn bkz [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="98526-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="98526-266">kullanarak bir hizmet asıl toocreate hello Azure portal, bkz: [portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanmak](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98526-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="98526-267">Bir hizmet sorumlusu, PowerShell veya Azure CLI ile de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98526-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="98526-268">Azure AD kullanarak tooauthenticate toplu yönetim uygulamaları bkz [Active Directory ile kimlik doğrulaması toplu yönetim çözümleri](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="98526-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"
[azure_portal]: http://portal.azure.com
