---
title: "Son kullanıcı kimlik doğrulaması: Data Lake Store Azure Active Directory ile | Microsoft Docs"
description: "Bilgi nasıl Azure Active Directory kullanarak Data Lake Store ile tooachieve son kullanıcı kimlik doğrulaması"
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
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="8d1cc-103">Azure Active Directory kullanarak Data Lake Store ile son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8d1cc-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d1cc-104">Hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8d1cc-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="8d1cc-105">Son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8d1cc-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="8d1cc-106">Azure Data Lake Store, Azure Active Directory kimlik doğrulaması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="8d1cc-107">Azure Data Lake Store veya Azure Data Lake Analytics ile çalışan bir uygulama geliştirme önce ilk tooauthenticate yönteminizi karar vermeniz gerekir uygulamanızı Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d1cc-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8d1cc-108">Merhaba iki ana seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8d1cc-108">hello two main options available are:</span></span>

* <span data-ttu-id="8d1cc-109">Son kullanıcı kimlik doğrulaması (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="8d1cc-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="8d1cc-110">Hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8d1cc-110">Service-to-service authentication</span></span>

<span data-ttu-id="8d1cc-111">Ekli tooeach yapılan istek tooAzure Data Lake Store veya Azure Data Lake Analytics alır bir OAuth 2.0 belirteç ile sağlanan uygulamanızda hem bu seçenekleri sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="8d1cc-112">Bu makale konuşmaları konusunda oluşturma bir **son kullanıcı kimlik doğrulaması için Azure AD yerel uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="8d1cc-113">Hizmetten hizmete kimlik doğrulaması için Azure AD uygulama yapılandırma hakkında yönergeler için bkz [hizmeti için kimlik doğrulaması Azure Active Directory kullanarak Data Lake Store ile](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8d1cc-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d1cc-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8d1cc-114">Prerequisites</span></span>
* <span data-ttu-id="8d1cc-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-115">An Azure subscription.</span></span> <span data-ttu-id="8d1cc-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d1cc-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="8d1cc-117">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="8d1cc-117">Your subscription ID.</span></span> <span data-ttu-id="8d1cc-118">Hello Azure Portal ' alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="8d1cc-119">Örneğin, hello Data Lake Store hesabı dikey penceresinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Abonelik kimliği alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="8d1cc-121">Azure AD etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-121">Your Azure AD domain name.</span></span> <span data-ttu-id="8d1cc-122">Vurgulama hello fare hello sağ üst köşesindeki hello Azure Portal tarafından alabilir.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="8d1cc-123">Aşağıdaki Hello ekran görüntüsünde hello etki alanı adıdır **contoso.onmicrosoft.com**, ve hello GUID köşeli ayraçlar içinde hello Kiracı kimliği.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![AAD etki alanı alma](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="8d1cc-125">Son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8d1cc-125">End-user authentication</span></span>
<span data-ttu-id="8d1cc-126">Azure AD ile tooyour uygulamada bir son kullanıcı toolog isterseniz, önerilen yaklaşımı hello budur.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="8d1cc-127">Uygulamanızın mümkün tooaccess hello Azure kaynaklarıyla olacaktır aynı erişim düzeyini oturum hello son kullanıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="8d1cc-128">Son kullanıcıların kimlik bilgilerini düzenli aralıklarla uygulama toomaintain erişiminizi sırayla tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="8d1cc-129">Merhaba son kullanıcı oturum açma sahip hello uygulamanız bir erişim belirteci ve bir yenileme belirteci verilir sonucudur.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="8d1cc-130">ekli tooeach isteği tooData Lake Store veya Data Lake Analytics yapılan Hello erişim belirtecini alır ve varsayılan olarak bir saat için geçerli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="8d1cc-131">Merhaba yenileme belirteci yeni bir erişim belirteci ve düzenli olarak kullandıysanız için geçerli varsayılan olarak, tootwo hafta yukarı kullanılan tooobtain olabilir.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="8d1cc-132">Son kullanıcı oturum açma için iki farklı yaklaşım kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="8d1cc-133">Merhaba OAuth 2.0 açılır kullanma</span><span class="sxs-lookup"><span data-stu-id="8d1cc-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="8d1cc-134">Uygulamanızın hangi hello son kullanıcı kimlik bilgilerini girebilirsiniz bir OAuth 2.0 yetkilendirme açılır tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="8d1cc-135">Bu açılır pencere hello Azure AD iki öğeli kimlik doğrulamasını (2FA) işlemiyle gerektiğinde de çalışır.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="8d1cc-136">Bu yöntem henüz hello Azure AD Authentication Library (ADAL) Python veya Java için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="8d1cc-137">Kullanıcı kimlik bilgilerini doğrudan geçirme</span><span class="sxs-lookup"><span data-stu-id="8d1cc-137">Directly passing in user credentials</span></span>
<span data-ttu-id="8d1cc-138">Uygulamanızın doğrudan kullanıcı kimlik bilgilerini tooAzure AD sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="8d1cc-139">Bu yöntem yalnızca Kuruluş Kimliği kullanıcı hesaplarıyla çalışır; uyumlu değil kişisel ile / "live ID" kullanıcı hesapları da dahil olmak üzere, bitiş @outlook.com veya @live.com. Ayrıca, bu yöntem, Azure AD iki öğeli kimlik doğrulamasını (2FA) gerektiren kullanıcı hesaplarını ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="8d1cc-140">Ne bu yaklaşım toouse ihtiyacım?</span><span class="sxs-lookup"><span data-stu-id="8d1cc-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="8d1cc-141">Azure AD etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-141">Azure AD domain name.</span></span> <span data-ttu-id="8d1cc-142">Bu, zaten bu makalenin hello önkoşul olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="8d1cc-143">Azure AD **yerel uygulama**</span><span class="sxs-lookup"><span data-stu-id="8d1cc-143">Azure AD **native application**</span></span>
* <span data-ttu-id="8d1cc-144">Hello Azure AD yerel uygulama için uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="8d1cc-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="8d1cc-145">Azure AD yerel uygulaması hello için yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="8d1cc-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="8d1cc-146">Yetki verilmiş izinleri ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8d1cc-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="8d1cc-147">1. adım: Active Directory yerel uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d1cc-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="8d1cc-148">Oluşturun ve Azure AD yerel uygulaması son kullanıcı kimlik doğrulaması için Azure Data Lake Azure Active Directory'yi kullanarak Store ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="8d1cc-149">Yönergeler için bkz: [Azure AD uygulaması oluşturmasına](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8d1cc-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="8d1cc-150">Bağlantı yukarıdaki hello Hello yönergeleri aşağıdaki hatayla seçtiğinizden emin olun **yerel** hello ekran görüntüsünde gösterildiği gibi uygulama türü için.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="8d1cc-151">![Web uygulaması oluşturma](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "yerel uygulama oluştur")</span><span class="sxs-lookup"><span data-stu-id="8d1cc-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="8d1cc-152">2. adım: uygulama kimliği alma ve yeniden yönlendirme URI'si</span><span class="sxs-lookup"><span data-stu-id="8d1cc-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="8d1cc-153">Bkz: [hello uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) (Merhaba Klasik Azure portalı hello istemci kimliği olarak da bilinir) tooretrieve hello uygulamanın uygulama kimliğini hello Azure AD yerel.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="8d1cc-154">tooretrieve hello yeniden yönlendirme URI'si, hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="8d1cc-155">Hello Azure Portalı ' seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz hello Azure AD yerel uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="8d1cc-156">Merhaba gelen **ayarları** Merhaba uygulaması için dikey tıklayın **yeniden yönlendirme URI'ler**.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Get yeniden yönlendirme URI'si](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="8d1cc-158">Görüntülenen hello değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="8d1cc-159">3. adım: İzinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="8d1cc-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="8d1cc-160">Hello Azure Portalı ' seçin **Azure Active Directory**, tıklatın **uygulama kayıtlar**ve ardından bulmak ve yeni oluşturduğunuz hello Azure AD yerel uygulama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="8d1cc-161">Merhaba gelen **ayarları** Merhaba uygulaması için dikey tıklayın **gerekli izinleri**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="8d1cc-163">Merhaba, **eklemek API erişimini** dikey penceresinde'ı tıklatın **bir API seçin**, tıklatın **Azure Data Lake**ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="8d1cc-165">Merhaba, **API erişimini eklemek** dikey penceresinde tıklatın **izinler seçeneğini belirleyin**, Seç onay kutusunu toogive hello **tooData Lake Store tam erişim**ve ardından **seçin **.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![istemci kimliği](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="8d1cc-167">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-167">Click **Done**.</span></span>

5. <span data-ttu-id="8d1cc-168">Yineleme hello en son iki adımı toogrant izinlerini **Windows Azure Hizmet Yönetimi API'si** de.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8d1cc-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d1cc-169">Next steps</span></span>
<span data-ttu-id="8d1cc-170">Bu makalede Azure AD yerel uygulaması oluşturulur ve hello bilgileri istemci uygulamalarınızı .NET SDK'sı, Java SDK'sı, REST API vb. kullanarak yazmanız gerekir. Şimdi toouse hello Azure AD web uygulama toofirst Data Lake Store ile nasıl kimlik doğrulaması hakkında konuşun ve hello deposu üzerinde başka işlemler gerçekleştirmek makaleler aşağıdaki toohello devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d1cc-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="8d1cc-171">.NET SDK'yı kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8d1cc-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="8d1cc-172">Azure Data Lake Java SDK'sını kullanarak Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8d1cc-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="8d1cc-173">Azure Data Lake REST API kullanarak Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8d1cc-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

