---
title: "Son kullanıcı kimlik doğrulaması: Data Lake Store Azure Active Directory ile | Microsoft Docs"
description: "Son kullanıcı kimlik doğrulaması Azure Active Directory'yi kullanarak Data Lake Store ile elde öğrenin"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="dfc7f-103">Azure Active Directory kullanarak Data Lake Store ile son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="dfc7f-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfc7f-104">Hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="dfc7f-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="dfc7f-105">Son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="dfc7f-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="dfc7f-106">Azure Data Lake Store, Azure Active Directory kimlik doğrulaması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="dfc7f-107">Azure Data Lake Store veya Azure Data Lake Analytics ile çalışan bir uygulama geliştirme önce ilk uygulamanızı Azure Active Directory (Azure AD) ile kimlik doğrulama yönteminizi karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="dfc7f-108">İki ana seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dfc7f-108">The two main options available are:</span></span>

* <span data-ttu-id="dfc7f-109">Son kullanıcı kimlik doğrulaması (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="dfc7f-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="dfc7f-110">Hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="dfc7f-110">Service-to-service authentication</span></span>

<span data-ttu-id="dfc7f-111">Azure Data Lake Store veya Azure Data Lake Analytics yapılan her isteği iliştirilmiş bir OAuth 2.0 belirteç ile sağlanan uygulamanızda hem bu seçenekleri sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="dfc7f-112">Bu makale konuşmaları konusunda oluşturma bir **son kullanıcı kimlik doğrulaması için Azure AD yerel uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="dfc7f-113">Hizmetten hizmete kimlik doğrulaması için Azure AD uygulama yapılandırma hakkında yönergeler için bkz [hizmeti için kimlik doğrulaması Azure Active Directory kullanarak Data Lake Store ile](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="dfc7f-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfc7f-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dfc7f-114">Prerequisites</span></span>
* <span data-ttu-id="dfc7f-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-115">An Azure subscription.</span></span> <span data-ttu-id="dfc7f-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfc7f-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="dfc7f-117">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="dfc7f-117">Your subscription ID.</span></span> <span data-ttu-id="dfc7f-118">Azure Portalı'ndan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="dfc7f-119">Örneğin, Data Lake Store hesabı dikey penceresinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Abonelik kimliği alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="dfc7f-121">Azure AD etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-121">Your Azure AD domain name.</span></span> <span data-ttu-id="dfc7f-122">Azure portalının sağ üst köşedeki fare gelerek alabilir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="dfc7f-123">Aşağıdaki ekran görüntüsünde etki alanı adıdır **contoso.onmicrosoft.com**, ve köşeli ayraçlar içinde GUID Kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![AAD etki alanı alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="dfc7f-125">Son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="dfc7f-125">End-user authentication</span></span>
<span data-ttu-id="dfc7f-126">Bu, uygulamanızın Azure AD ile oturum açmak için bir son kullanıcı istiyorsanız önerilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="dfc7f-127">Uygulamanız, oturum açmış aynı düzeyde erişim son kullanıcı ile Azure kaynaklarına erişebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="dfc7f-128">Son kullanıcıların kimlik bilgilerini düzenli olarak erişim, uygulamanız için sırayla sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="dfc7f-129">Oturum açma son kullanıcı sahip uygulamanız bir erişim belirteci ve bir yenileme belirteci verilir sonucudur.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="dfc7f-130">Erişim belirteci Data Lake Store veya Data Lake Analytics yapılan her isteği bağlı ve varsayılan olarak bir saat için geçerli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="dfc7f-131">Düzenli olarak kullanılan iki haftaya varsayılan olarak, geçerli olduğundan ve yenileme belirtecini yeni bir erişim belirteci almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="dfc7f-132">Son kullanıcı oturum açma için iki farklı yaklaşım kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="dfc7f-133">OAuth 2.0 açılır kullanma</span><span class="sxs-lookup"><span data-stu-id="dfc7f-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="dfc7f-134">Uygulamanız son kullanıcı kimlik bilgilerini girebilirsiniz bir OAuth 2.0 yetkilendirme açılır tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="dfc7f-135">Bu açılır pencere Azure AD iki öğeli kimlik doğrulamasını (2FA) işlemine gerektiğinde de çalışır.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="dfc7f-136">Bu yöntem henüz Azure AD Authentication Library (ADAL), Python veya Java için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="dfc7f-137">Kullanıcı kimlik bilgilerini doğrudan geçirme</span><span class="sxs-lookup"><span data-stu-id="dfc7f-137">Directly passing in user credentials</span></span>
<span data-ttu-id="dfc7f-138">Uygulamanızı Azure AD'ye doğrudan kullanıcı kimlik bilgilerini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="dfc7f-139">Bu yöntem yalnızca Kuruluş Kimliği kullanıcı hesaplarıyla çalışır; uyumlu değil kişisel ile / "live ID" kullanıcı hesapları da dahil olmak üzere, bitiş @outlook.com veya @live.com.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="dfc7f-140">Ayrıca, bu yöntem, Azure AD iki öğeli kimlik doğrulamasını (2FA) gerektiren kullanıcı hesaplarını ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="dfc7f-141">Bu yaklaşımı kullanmak neler gerekir?</span><span class="sxs-lookup"><span data-stu-id="dfc7f-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="dfc7f-142">Azure AD etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-142">Azure AD domain name.</span></span> <span data-ttu-id="dfc7f-143">Bu, zaten bu makalede önkoşul olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="dfc7f-144">Azure AD **yerel uygulama**</span><span class="sxs-lookup"><span data-stu-id="dfc7f-144">Azure AD **native application**</span></span>
* <span data-ttu-id="dfc7f-145">Azure AD yerel uygulama için uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="dfc7f-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="dfc7f-146">Azure AD yerel uygulama için yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="dfc7f-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="dfc7f-147">Yetki verilmiş izinleri ayarlayın</span><span class="sxs-lookup"><span data-stu-id="dfc7f-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="dfc7f-148">1. adım: Active Directory yerel uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="dfc7f-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="dfc7f-149">Oluşturun ve Azure AD yerel uygulaması son kullanıcı kimlik doğrulaması için Azure Data Lake Azure Active Directory'yi kullanarak Store ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="dfc7f-150">Yönergeler için bkz: [Azure AD uygulaması oluşturmasına](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dfc7f-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="dfc7f-151">Yukarıdaki bağlantıyı kısmındaki yönergeleri izleyerek sırasında seçtiğinizden emin olun **yerel** aşağıdaki ekran görüntüsünde gösterildiği gibi uygulama türü için.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="dfc7f-152">![Web uygulaması oluşturma](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "yerel uygulama oluştur")</span><span class="sxs-lookup"><span data-stu-id="dfc7f-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="dfc7f-153">2. adım: uygulama kimliği alma ve yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="dfc7f-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="dfc7f-154">Bkz: [uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Azure Klasik Portalı'nda istemci kimliği olarak da bilinir) Azure AD yerel uygulamanın uygulama kimliğini almak için.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="dfc7f-155">Yeniden yönlendirme URI'si almak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="dfc7f-156">Azure Portalı'ndan seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz Azure AD yerel uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="dfc7f-157">Gelen **ayarları** uygulama için dikey tıklayın **yeniden yönlendirme URI'ler**.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Get yeniden yönlendirme URI'si](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="dfc7f-159">Görüntülenen değer kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="dfc7f-160">3. adım: İzinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="dfc7f-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="dfc7f-161">Azure Portalı'ndan seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz Azure AD yerel uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="dfc7f-162">Gelen **ayarları** uygulama için dikey tıklayın **gerekli izinleri**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="dfc7f-164">İçinde **API erişimini eklemek** dikey penceresinde tıklatın **bir API seçin**, tıklatın **Azure Data Lake**ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="dfc7f-166">İçinde **eklemek API erişimini** dikey penceresinde tıklatın **izinler seçeneğini belirleyin**, vermek için bu onay kutusunu seçin **tam erişim Data Lake Store'a**ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="dfc7f-168">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-168">Click **Done**.</span></span>

5. <span data-ttu-id="dfc7f-169">İzinleri vermek için son iki adımı yineleyin **Windows Azure Hizmet Yönetimi API'si** de.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="dfc7f-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dfc7f-170">Next steps</span></span>
<span data-ttu-id="dfc7f-171">Bu makalede Azure AD yerel uygulaması oluşturulur ve .NET SDK'sı, Java SDK'sı, REST API vb. kullanarak Yazar istemci uygulamalarınızda gereksinim duyduğunuz bilgileri toplanmaz. İlk Data Lake Store ile kimlik doğrulaması ve depolama üzerinde başka işlemler gerçekleştirmek için Azure AD web uygulaması kullanma hakkında konuşun aşağıdaki makalelere şimdi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfc7f-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="dfc7f-172">.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dfc7f-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="dfc7f-173">Azure Data Lake Java SDK'sını kullanarak Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dfc7f-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="dfc7f-174">Azure Data Lake REST API kullanarak Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dfc7f-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

