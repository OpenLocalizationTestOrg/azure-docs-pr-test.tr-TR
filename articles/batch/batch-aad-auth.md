---
title: "Azure Batch hizmeti çözümleri kimlik doğrulaması için Azure Active Directory kullanmak | Microsoft Docs"
description: "Batch Batch hizmetinde kimlik doğrulaması için Azure AD destekler."
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
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="b7299-103">Toplu hizmet çözümlerine Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b7299-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="b7299-104">Azure Batch destekleyen kimlik doğrulama ile [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7299-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="b7299-105">Azure AD, Microsoft'un çok kiracılı bulut tabanlı dizin ve Kimlik Yönetimi Hizmeti ' dir.</span><span class="sxs-lookup"><span data-stu-id="b7299-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="b7299-106">Azure kendisini müşteriler, hizmet yöneticileri ve kuruluş kullanıcılarının kimliğini doğrulamak için Azure AD kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7299-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="b7299-107">Azure AD kimlik doğrulaması ile Azure Batch kullanırken, aşağıdaki iki yöntemden biriyle doğrulayabilir:</span><span class="sxs-lookup"><span data-stu-id="b7299-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="b7299-108">Kullanarak **tümleşik kimlik doğrulaması** uygulama ile etkileşim bir kullanıcının kimliğini doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="b7299-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="b7299-109">Tümleşik kimlik doğrulaması kullanarak bir uygulama, bir kullanıcının kimlik bilgilerini toplar ve toplu kaynaklarına erişimde kimlik doğrulaması için bu kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7299-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="b7299-110">Kullanarak bir **hizmet sorumlusu** katılımsız uygulama kimliğini doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="b7299-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="b7299-111">Bir hizmet sorumlusu uygulamanın çalışma zamanında kaynaklara erişirken gösterebilmek için bir uygulama için izinler ve ilke tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="b7299-112">Azure AD hakkında daha fazla bilgi için bkz: [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b7299-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="b7299-113">Kimlik doğrulama ve havuzu ayırma modu</span><span class="sxs-lookup"><span data-stu-id="b7299-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="b7299-114">Bir toplu işlem hesabı oluşturduğunuzda, o hesap için oluşturulan havuzlarının burada ayrılmalıdır belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7299-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="b7299-115">Varsayılan toplu işlem hizmeti aboneliğiniz veya bir kullanıcı abonelik havuzları ayırmak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7299-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="b7299-116">Tercih ettiğiniz bu hesaptaki kaynaklarına erişimde kimlik doğrulaması nasıl etkiler.</span><span class="sxs-lookup"><span data-stu-id="b7299-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="b7299-117">**Batch hizmeti abonelik**.</span><span class="sxs-lookup"><span data-stu-id="b7299-117">**Batch service subscription**.</span></span> <span data-ttu-id="b7299-118">Varsayılan olarak, bir toplu işlem hizmeti abonelikte Batch havuzları ayrılır.</span><span class="sxs-lookup"><span data-stu-id="b7299-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="b7299-119">Bu seçeneği seçerseniz, bu hesaptaki kaynaklara erişim biriyle doğrulanabilir [paylaşılan anahtar](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) veya Azure AD ile.</span><span class="sxs-lookup"><span data-stu-id="b7299-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="b7299-120">**Kullanıcı aboneliği.**</span><span class="sxs-lookup"><span data-stu-id="b7299-120">**User subscription.**</span></span> <span data-ttu-id="b7299-121">Belirttiğiniz bir kullanıcı abonelik Batch havuzlarında ayırmak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7299-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="b7299-122">Bu seçeneği seçerseniz, Azure AD ile kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7299-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="b7299-123">Kimlik doğrulaması için uç noktalar</span><span class="sxs-lookup"><span data-stu-id="b7299-123">Endpoints for authentication</span></span>

<span data-ttu-id="b7299-124">Toplu işlem uygulamaları Azure AD ile kimlik doğrulamak için bazı iyi bilinen uç noktaları kodunuzda eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7299-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="b7299-125">Azure AD uç noktası</span><span class="sxs-lookup"><span data-stu-id="b7299-125">Azure AD endpoint</span></span>

<span data-ttu-id="b7299-126">Temel Azure AD yetkilisi uç noktası:</span><span class="sxs-lookup"><span data-stu-id="b7299-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="b7299-127">Azure AD ile kimlik doğrulamak için bu uç noktaya Kiracı kimliği (dizin kimliği) ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7299-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="b7299-128">Kiracı kimliği kimlik doğrulaması için kullanılacak Azure AD kiracısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="b7299-129">Kiracı Kimliği almak için özetlenen adımları izleyin [için Azure Active Directory Kiracı Kimliğinizi alma](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="b7299-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="b7299-130">Bir hizmet sorumlusunu kullanarak kimlik doğrulaması sırasında Kiracı özgü uç noktası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b7299-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="b7299-131">Tümleşik kimlik doğrulaması kullanarak kimlik doğrulaması sırasında isteğe bağlıdır, ancak önerilen Kiracı özgü uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="b7299-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="b7299-132">Ancak, Azure AD ortak uç nokta de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7299-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="b7299-133">Ortak bir uç belirli bir kiracı sağlanmadığında arabirimi toplama genel bir kimlik bilgisi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b7299-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="b7299-134">Ortak uç noktası `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="b7299-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="b7299-135">Azure AD uç noktaları hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="b7299-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="b7299-136">Batch kaynak uç noktası</span><span class="sxs-lookup"><span data-stu-id="b7299-136">Batch resource endpoint</span></span>

<span data-ttu-id="b7299-137">Kullanım **Azure Batch kaynak endpoint** Batch hizmeti isteklerine kimlik doğrulaması için bir belirteç almak için:</span><span class="sxs-lookup"><span data-stu-id="b7299-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="b7299-138">Bir kiracı ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="b7299-138">Register your application with a tenant</span></span>

<span data-ttu-id="b7299-139">Kimlik doğrulaması için Azure AD kullanmanın ilk adımı uygulamanız bir Azure AD kiracısında kaydediyor.</span><span class="sxs-lookup"><span data-stu-id="b7299-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="b7299-140">Uygulamanızı kaydetme, sağlayan Azure çağırabilmeniz için [Active Directory kimlik doğrulama Kitaplığı] [ aad_adal] (ADAL) kodunuzdan.</span><span class="sxs-lookup"><span data-stu-id="b7299-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="b7299-141">ADAL, uygulamanızdan Azure AD ile kimlik doğrulaması için bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="b7299-142">Uygulamanızı kaydetme tümleşik kimlik doğrulaması veya bir hizmet sorumlusu kullanmayı planladığınız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b7299-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="b7299-143">Uygulamanızı kaydederken, Azure AD'ye uygulamanız ile ilgili bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="b7299-144">Ardından Azure AD çalışma zamanında Azure AD ile uygulamanızı ilişkilendirmek için kullandığınız bir uygulama kimliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="b7299-145">Uygulama kimliği hakkında daha fazla bilgi için bkz: [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="b7299-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="b7299-146">Batch uygulamanızı kaydetmek için adımları [bir uygulama ekleme](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) bölümüne [uygulamaları Azure Active Directory ile tümleştirme][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="b7299-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="b7299-147">Yerel bir uygulama olarak, uygulamanızın kaydederseniz için geçerli bir URI belirtebilirsiniz **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="b7299-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="b7299-148">Gerçek bir uç nokta olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b7299-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="b7299-149">Uygulamanızı kaydınız sonra uygulama kimliği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="b7299-149">After you've registered your application, you'll see the application ID:</span></span>

![Batch uygulamanızı Azure AD ile kaydetme](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="b7299-151">Uygulama Azure AD ile kaydetme hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="b7299-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="b7299-152">İçin Active Directory Kiracı Kimliğinizi alma</span><span class="sxs-lookup"><span data-stu-id="b7299-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="b7299-153">Kiracı kimliği uygulamanız için kimlik doğrulama hizmetleri sağlayan Azure AD kiracısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="b7299-154">Kiracı Kimliği almak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7299-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="b7299-155">Azure portalında Active Directory'nizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b7299-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="b7299-156">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-156">Click **Properties**.</span></span>
3. <span data-ttu-id="b7299-157">Dizin kimliği için sağlanan GUID değeri kopyalayın</span><span class="sxs-lookup"><span data-stu-id="b7299-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="b7299-158">Bu değer Kiracı kimliği olarak da adlandırılır</span><span class="sxs-lookup"><span data-stu-id="b7299-158">This value is also called the tenant ID.</span></span>

![Dizin Kimliğini kopyalayın](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="b7299-160">Tümleşik kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="b7299-160">Use integrated authentication</span></span>

<span data-ttu-id="b7299-161">Tümleşik kimlik doğrulaması ile kimlik doğrulaması için Batch hizmeti API'sine bağlanmak için uygulama izinleri vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7299-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="b7299-162">Bu adım, Azure AD ile Batch hizmeti API çağrıları kimliğini doğrulamak, uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="b7299-163">Seçtiğiniz sonra [uygulamanızı kayıtlı](#register-your-application-with-an-azure-ad-tenant), Batch hizmeti erişim vermek için Azure Portalı'nda aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7299-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="b7299-164">Azure portalının sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="b7299-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="b7299-165">Listedeki uygulamanızın uygulama kayıtların adını arayın:</span><span class="sxs-lookup"><span data-stu-id="b7299-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Uygulama adınız arayın](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="b7299-167">Açık **ayarları** dikey penceresinde uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="b7299-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="b7299-168">İçinde **API erişimini** bölümünde, select **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="b7299-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="b7299-169">İçinde **gerekli izinleri** dikey penceresinde tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="b7299-170">1. adımda toplu işlem API'si için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="b7299-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="b7299-171">API'yi bulana kadar aşağıdaki dizelerden her birini arayın:</span><span class="sxs-lookup"><span data-stu-id="b7299-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="b7299-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="b7299-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="b7299-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="b7299-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="b7299-174">Daha yeni Azure AD kiracıları bu adı kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b7299-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="b7299-175">Batch API'sinin kimliği: **ddbf3205-c6bd-46ae-8127-60eb93363864**.</span><span class="sxs-lookup"><span data-stu-id="b7299-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="b7299-176">Toplu işlem API bulduğunuzda, seçin ve **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="b7299-177">2. adımda yanındaki onay kutusunu işaretleyin **erişim Azure Batch hizmeti** tıklatıp **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="b7299-178">Tıklatın **Bitti** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-178">Click the **Done** button.</span></span>

<span data-ttu-id="b7299-179">**Gerekli izinler** API gösterir, Azure AD uygulaması erişimi ADAL ve toplu işlem hizmeti artık dikey.</span><span class="sxs-lookup"><span data-stu-id="b7299-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="b7299-180">Uygulamanızı Azure AD ile ilk kez kaydederken izinler için ADAL otomatik olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="b7299-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![GRANT API izinleri](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="b7299-182">Bir hizmet sorumlusu kullanın</span><span class="sxs-lookup"><span data-stu-id="b7299-182">Use a service principal</span></span> 

<span data-ttu-id="b7299-183">Katılımsız çalışan bir uygulama kimliğini doğrulamak için bir hizmet sorumlusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7299-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="b7299-184">Uygulamanızı kaydınız sonra Azure portalında bir hizmet sorumlusu yapılandırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7299-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="b7299-185">Uygulamanız için gizli bir anahtar isteyin.</span><span class="sxs-lookup"><span data-stu-id="b7299-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="b7299-186">Uygulamanıza bir RBAC rolü atayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="b7299-187">Uygulamanız için gizli bir anahtarı iste</span><span class="sxs-lookup"><span data-stu-id="b7299-187">Request a secret key for your application</span></span>

<span data-ttu-id="b7299-188">Uygulamanızın hizmet sorumlusu ile doğruladığında, Azure AD uygulama kimliği ve gizli bir anahtar gönderir.</span><span class="sxs-lookup"><span data-stu-id="b7299-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="b7299-189">Oluşturun ve kodunuzdan gizli anahtarı kopyalayın gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7299-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="b7299-190">Azure portalında aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7299-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="b7299-191">Azure portalının sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="b7299-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="b7299-192">Listedeki uygulamanızın uygulama kayıtların adını arayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="b7299-193">Görüntü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="b7299-193">Display the **Settings** blade.</span></span> <span data-ttu-id="b7299-194">İçinde **API erişimini** bölümünde, select **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="b7299-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="b7299-195">Bir anahtar oluşturmak için bu anahtar için bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="b7299-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="b7299-196">Ardından bir veya iki yıl anahtarı için bir süre seçin.</span><span class="sxs-lookup"><span data-stu-id="b7299-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="b7299-197">Tıklatın **kaydetmek** oluşturmak ve anahtarı görüntülemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="b7299-198">Anahtar değeri dikey penceresinde çıktıktan sonra yeniden erişebilir açamazsınız güvenli bir yere kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Gizli bir anahtar oluşturun](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="b7299-200">Uygulamanıza bir RBAC rolü atayın</span><span class="sxs-lookup"><span data-stu-id="b7299-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="b7299-201">Hizmet sorumlusu ile kimlik doğrulaması yapmak için uygulamanızı bir RBAC rolü atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7299-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="b7299-202">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="b7299-202">Follow these steps:</span></span>

1. <span data-ttu-id="b7299-203">Uygulamanız tarafından kullanılan toplu işlem hesabı için Azure portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="b7299-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="b7299-204">İçinde **ayarları** select toplu işlem hesabı için dikey **erişim denetimi (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="b7299-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="b7299-205">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="b7299-206">Gelen **rol** açılan listesinde, ya da seçin _katkıda bulunan_ veya _okuyucu_ rolü uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="b7299-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="b7299-207">Bu rolleri hakkında daha fazla bilgi için bkz: [Azure portalında rol tabanlı erişim denetimi ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="b7299-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="b7299-208">İçinde **seçin** alanında, uygulamanızın adı girin.</span><span class="sxs-lookup"><span data-stu-id="b7299-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="b7299-209">Uygulamanızı listeden seçin ve'ı tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="b7299-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="b7299-210">Uygulamanız artık bir RBAC rolü atanmış erişim denetimi ayarlarınızda görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="b7299-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Uygulamanıza bir RBAC rolü atayın](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="b7299-212">İçin Azure Active Directory Kiracı Kimliğinizi alma</span><span class="sxs-lookup"><span data-stu-id="b7299-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="b7299-213">Kiracı kimliği uygulamanız için kimlik doğrulama hizmetleri sağlayan Azure AD kiracısı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7299-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="b7299-214">Kiracı Kimliği almak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7299-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="b7299-215">Azure portalında Active Directory'nizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b7299-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="b7299-216">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-216">Click **Properties**.</span></span>
3. <span data-ttu-id="b7299-217">Dizin kimliği için sağlanan GUID değeri kopyalayın</span><span class="sxs-lookup"><span data-stu-id="b7299-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="b7299-218">Bu değer Kiracı kimliği olarak da adlandırılır</span><span class="sxs-lookup"><span data-stu-id="b7299-218">This value is also called the tenant ID.</span></span>

![Dizin Kimliğini kopyalayın](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="b7299-220">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="b7299-220">Code examples</span></span>

<span data-ttu-id="b7299-221">Bu bölümdeki kod örnekleri, bir hizmet sorumlusu ile tümleşik kimlik doğrulaması kullanarak Azure AD ile kimlik doğrulaması yapmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7299-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="b7299-222">Bu kod örnekleri .NET kullanın, ancak diğer diller için kavramlar benzerdir.</span><span class="sxs-lookup"><span data-stu-id="b7299-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="b7299-223">Azure AD kimlik doğrulama belirtecini bir saat sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="b7299-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="b7299-224">Bir uzun süreli kullanırken **BatchClient** nesne, geçerli bir belirteci her zaman sahip emin olmak için her istek ADAL bir belirteç almak öneririz.</span><span class="sxs-lookup"><span data-stu-id="b7299-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="b7299-225">.NET ile bunun için Azure AD'den belirteç alan bir yöntem yazmak ve bu yönteme geçirin bir **BatchTokenCredentials** temsilci olarak nesne.</span><span class="sxs-lookup"><span data-stu-id="b7299-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="b7299-226">Temsilci yöntemi geçerli bir belirteci sağlandığından emin olmak için her istek Batch hizmeti için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b7299-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="b7299-227">Yeni bir belirteç Azure AD'den alınan için varsayılan olarak ADAL belirteçleri, önbelleğe alır. yalnızca gerekli olduğunda.</span><span class="sxs-lookup"><span data-stu-id="b7299-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="b7299-228">Azure AD'de belirteçleri hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="b7299-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="b7299-229">Kod örneği: Batch .NET ile tümleşik kimlik doğrulaması Azure AD kullanma</span><span class="sxs-lookup"><span data-stu-id="b7299-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="b7299-230">Batch .NET tümleşik kimlik doğrulamasında kullanılacak başvuru [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) paketi ve [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paket.</span><span class="sxs-lookup"><span data-stu-id="b7299-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="b7299-231">Aşağıdakiler dahil `using` deyimlerinde kodunuzu:</span><span class="sxs-lookup"><span data-stu-id="b7299-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="b7299-232">Kiracı kimliğini de dahil olmak üzere, kodunuzu Azure AD uç başvurusu</span><span class="sxs-lookup"><span data-stu-id="b7299-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="b7299-233">Kiracı Kimliği almak için özetlenen adımları izleyin [için Azure Active Directory Kiracı Kimliğinizi alma](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="b7299-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="b7299-234">Başvuru Batch hizmeti kaynak uç noktası:</span><span class="sxs-lookup"><span data-stu-id="b7299-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="b7299-235">Batch hesabınıza başvurusu:</span><span class="sxs-lookup"><span data-stu-id="b7299-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="b7299-236">Uygulamanız için uygulama kimliği (istemci kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7299-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="b7299-237">Uygulama kimliği, Azure portalında uygulama kaydınızı edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="b7299-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="b7299-238">Ayrıca kayıt işlemi sırasında belirtilen URI yeniden yönlendirme kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b7299-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="b7299-239">URI kodunuzda belirtilen yeniden yönlendirme yeniden yönlendirilen uygulamayı kaydolurken sağladığınız URI eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b7299-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="b7299-240">Azure AD'den kimlik doğrulama belirtecini almak üzere geri arama yöntemi yazın.</span><span class="sxs-lookup"><span data-stu-id="b7299-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="b7299-241">**GetAuthenticationTokenAsync** uygulama ile etkileşim bir kullanıcı kimlik doğrulaması için ADAL çağrıları burada gösterilen geri çağırma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b7299-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="b7299-242">**AcquireTokenAsync** ADAL tarafından sağlanan yöntemi (Bu zaten kimlik bilgilerini önbelleğe sürece) kullanıcı bunları sağlar sonra kullanıcıdan kimlik bilgilerini ve uygulama kazançlar ister:</span><span class="sxs-lookup"><span data-stu-id="b7299-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="b7299-243">Oluşturmak bir **BatchTokenCredentials** temsilcisi bir parametre olarak alan nesne.</span><span class="sxs-lookup"><span data-stu-id="b7299-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="b7299-244">Açmak için bu kimlik bilgilerini kullanan bir **BatchClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="b7299-245">Kullanan **BatchClient** nesne Batch hizmeti karşı sonraki işlemleri için:</span><span class="sxs-lookup"><span data-stu-id="b7299-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="b7299-246">Kod örneği: Azure AD hizmet sorumlusu Batch .NET ile kullanma</span><span class="sxs-lookup"><span data-stu-id="b7299-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="b7299-247">Bir hizmet sorumlusu Batch .NET gelen kimlik doğrulaması yapmak için başvuru [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) paketi ve [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) paket.</span><span class="sxs-lookup"><span data-stu-id="b7299-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="b7299-248">Aşağıdakiler dahil `using` deyimlerinde kodunuzu:</span><span class="sxs-lookup"><span data-stu-id="b7299-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="b7299-249">Kiracı kimliğini de dahil olmak üzere, kodunuzu Azure AD uç başvurusu</span><span class="sxs-lookup"><span data-stu-id="b7299-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="b7299-250">Bir hizmet sorumlusu kullanırken, bir kiracı özel uç noktası sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7299-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="b7299-251">Kiracı Kimliği almak için özetlenen adımları izleyin [için Azure Active Directory Kiracı Kimliğinizi alma](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="b7299-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="b7299-252">Başvuru Batch hizmeti kaynak uç noktası:</span><span class="sxs-lookup"><span data-stu-id="b7299-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="b7299-253">Batch hesabınıza başvurusu:</span><span class="sxs-lookup"><span data-stu-id="b7299-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="b7299-254">Uygulamanız için uygulama kimliği (istemci kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7299-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="b7299-255">Uygulama kimliği, Azure portalında uygulama kaydınızı edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="b7299-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="b7299-256">Azure portalından kopyalandığından gizli anahtarı belirtin:</span><span class="sxs-lookup"><span data-stu-id="b7299-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="b7299-257">Azure AD'den kimlik doğrulama belirtecini almak üzere geri arama yöntemi yazın.</span><span class="sxs-lookup"><span data-stu-id="b7299-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="b7299-258">**GetAuthenticationTokenAsync** katılımsız kimlik doğrulaması için ADAL çağrıları burada gösterilen geri çağırma yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b7299-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="b7299-259">Oluşturmak bir **BatchTokenCredentials** temsilcisi bir parametre olarak alan nesne.</span><span class="sxs-lookup"><span data-stu-id="b7299-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="b7299-260">Açmak için bu kimlik bilgilerini kullanan bir **BatchClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b7299-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="b7299-261">Ardından, kullanabileceğiniz **BatchClient** nesne Batch hizmeti karşı sonraki işlemleri için:</span><span class="sxs-lookup"><span data-stu-id="b7299-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b7299-262">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7299-262">Next steps</span></span>

<span data-ttu-id="b7299-263">Azure AD hakkında daha fazla bilgi için bkz: [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b7299-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="b7299-264">ADAL'nin kullanımı gösteren ayrıntılı örnekler kullanılabilir [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=active-directory) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="b7299-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="b7299-265">Hizmet sorumluları hakkında daha fazla bilgi için bkz: [uygulama ve hizmet asıl nesneler Azure Active Directory'de](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="b7299-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="b7299-266">Azure Portalı'nı kullanarak bir hizmet sorumlusu oluşturmak için bkz: [Active Directory kaynaklara erişebilir uygulama ve hizmet sorumlusu oluşturmak için kullanım portal](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b7299-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="b7299-267">Bir hizmet sorumlusu, PowerShell veya Azure CLI ile de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7299-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="b7299-268">Azure AD kullanarak toplu yönetimini uygulama kimliğini doğrulamak için bkz: [Active Directory ile kimlik doğrulaması toplu yönetim çözümleri](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="b7299-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="b7299-269">[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"</span><span class="sxs-lookup"><span data-stu-id="b7299-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="b7299-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"</span><span class="sxs-lookup"><span data-stu-id="b7299-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="b7299-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"</span><span class="sxs-lookup"><span data-stu-id="b7299-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
