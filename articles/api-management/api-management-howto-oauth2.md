---
title: "Azure API Management'te OAuth 2.0 kullanan aaaAuthorize Geliştirici hesaplarını | Microsoft Docs"
description: "Bilgi nasıl API Management'te OAuth 2.0 kullanan tooauthorize kullanıcılar."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="90140-103">Nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="90140-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="90140-104">Birçok API'lerini destekleyen [OAuth 2.0](http://oauth.net/2/) toosecure API hello ve yalnızca geçerli kullanıcıların erişimi vardır ve yalnızca kaynak toowhich erişebilir bunlar başlıklı emin olun.</span><span class="sxs-lookup"><span data-stu-id="90140-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="90140-105">Sipariş toouse Azure API Management'ın etkileşimli Geliştirici konsolunda gibi API'leri ile tooconfigure sağlayan hello hizmeti API, hizmet örneği toowork OAuth 2.0 ile etkin.</span><span class="sxs-lookup"><span data-stu-id="90140-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="90140-106"><a name="prerequisites"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="90140-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="90140-107">Bu kılavuz size nasıl tooconfigure, API Management hizmet örneği toouse geliştirici için OAuth 2.0 yetkilendirme hesapları, nasıl göstermez gösterir, ancak tooconfigure bir OAuth 2.0 sağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="90140-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="90140-108">Başlangıç adımları benzerdir ve API Management hizmet örneği içinde OAuth 2.0 yapılandırmada kullanılan bilgi gerekli hello parçalarıdır rağmen farklı sağlayıcısıdır her OAuth 2.0 için Hello yapılandırması aynı hello.</span><span class="sxs-lookup"><span data-stu-id="90140-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="90140-109">Bu konuda bir OAuth 2.0 sağlayıcısı olarak Azure Active Directory kullanan örnekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="90140-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="90140-110">Azure Active Directory'yi kullanarak OAuth 2.0 yapılandırma hakkında daha fazla bilgi için bkz: Merhaba [WebApp GraphAPI DotNet] [ WebApp-GraphAPI-DotNet] örnek.</span><span class="sxs-lookup"><span data-stu-id="90140-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="90140-111"><a name="step1"></a>Bir OAuth 2.0 yetkilendirme Sunucusu API yönetimini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90140-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="90140-112">başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="90140-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="90140-114">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="90140-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="90140-115">Tıklatın **güvenlik** hello gelen **API Management** hello sol, tıklatma menüsünden **OAuth 2.0**ve ardından **yetkilendirme Sunucusu Ekle**.</span><span class="sxs-lookup"><span data-stu-id="90140-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="90140-117">' I tıklattıktan sonra **yetkilendirme Sunucusu Ekle**, hello yeni yetkilendirme sunucusu form görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="90140-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Yeni Sunucu][api-management-oauth2-server-1]

<span data-ttu-id="90140-119">Hello bir ad ve isteğe bağlı bir açıklama girin **adı** ve **açıklama** alanları.</span><span class="sxs-lookup"><span data-stu-id="90140-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="90140-120">Bu alanları hello geçerli API Management hizmet örneği içinde kullanılan tooidentify hello OAuth 2.0 yetkilendirme sunucusu ve değerlerine hello OAuth 2.0 sunucudan gelen.</span><span class="sxs-lookup"><span data-stu-id="90140-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="90140-121">Merhaba girin **istemci kayıt sayfası URL'si**.</span><span class="sxs-lookup"><span data-stu-id="90140-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="90140-122">Bu sayfa, kullanıcıların oluşturmak ve kendi hesaplarını yönetme içindir ve kullanılan hello OAuth 2.0 sağlayıcısına bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="90140-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="90140-123">Merhaba **istemci kayıt sayfası URL'si** toohello sayfasında, kullanıcıların noktaları toocreate kullanın ve kullanıcı hesaplarının yönetimini desteklemek için OAuth 2.0 sağlayıcıları kendi hesaplarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="90140-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="90140-124">Bazı kuruluşlar yapılandırmazsanız veya hello OAuth 2.0 sağlayıcı destekliyorsa olsa bile bu işlevi kullanın.</span><span class="sxs-lookup"><span data-stu-id="90140-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="90140-125">OAuth 2.0 sağlayıcınız yapılandırılmış hesaplarının kullanıcı yönetimini yoksa, şirketinizin hello URL veya URL gibi burada yer tutucu URL gibi girin `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="90140-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="90140-126">Merhaba form Hello sonraki bölümü içerir hello **yetki kodu izin türleri**, **yetkilendirme uç noktası URL'si**, ve **yetkilendirme isteği yöntemi** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="90140-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Yeni Sunucu][api-management-oauth2-server-2]

<span data-ttu-id="90140-128">Merhaba belirtin **yetki kodu izin türleri** istenen hello türleri denetleyerek.</span><span class="sxs-lookup"><span data-stu-id="90140-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="90140-129">**Yetkilendirme kodu** varsayılan olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="90140-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="90140-130">Merhaba girin **yetkilendirme uç noktası URL'si**.</span><span class="sxs-lookup"><span data-stu-id="90140-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="90140-131">Azure Active Directory'de, bu URL URL, aşağıdaki benzer toohello olacaktır nerede `<client_id>` uygulama toohello OAuth 2.0 sunucunuzu tanımlayan hello istemci kimliği ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="90140-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="90140-132">Merhaba **yetkilendirme isteği yöntemi** hello yetkilendirme isteği toohello OAuth 2.0 sunucusu nasıl gönderileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="90140-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="90140-133">Varsayılan olarak **almak** seçilir.</span><span class="sxs-lookup"><span data-stu-id="90140-133">By default **GET** is selected.</span></span>

<span data-ttu-id="90140-134">Merhaba sonraki bölümde yaptığı hello **belirteç uç nokta URL'si**, **istemci kimlik doğrulama yöntemleri**, **yöntemi gönderme erişim belirteci**, ve **varsayılan kapsamı** belirtilir.</span><span class="sxs-lookup"><span data-stu-id="90140-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Yeni Sunucu][api-management-oauth2-server-3]

<span data-ttu-id="90140-136">Bir Azure Active Directory OAuth 2.0 sunucusu için hello **belirteç uç nokta URL'si** biçimi, aşağıdaki hello olacaktır nerede `<APPID>` hello biçimi olan `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="90140-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="90140-137">Merhaba için varsayılan ayar **istemci kimlik doğrulama yöntemleri** olan **temel**, ve **yöntemi gönderme erişim belirteci** olan **Authorization Üstbilgisi**.</span><span class="sxs-lookup"><span data-stu-id="90140-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="90140-138">Bu değerleri bu bölümde hello birlikte hello formunun yapılandırılmış **varsayılan kapsamı**.</span><span class="sxs-lookup"><span data-stu-id="90140-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="90140-139">Merhaba **istemci kimlik bilgileri** bölüm içerir hello **istemci kimliği** ve **gizli**, hello oluşturma ve yapılandırma sürecinde, OAuth 2.0 elde hangi Sunucu.</span><span class="sxs-lookup"><span data-stu-id="90140-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="90140-140">Bir kez hello **istemci kimliği** ve **gizli** , hello belirtilen **redirect_uri** hello için **yetkilendirme kodu** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="90140-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="90140-141">Bu URI kullanılan tooconfigure hello yanıt OAuth 2.0 server yapılandırmanızda URL'dir.</span><span class="sxs-lookup"><span data-stu-id="90140-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Yeni Sunucu][api-management-oauth2-server-4]

<span data-ttu-id="90140-143">Varsa **yetki kodu izin türleri** çok ayarlanır**kaynak sahibi parolası**, hello **kaynak sahibi parolası kimlik bilgileri** bölümdür kullanılan toospecify bu kimlik bilgileri; Aksi takdirde boş bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90140-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Yeni Sunucu][api-management-oauth2-server-5]

<span data-ttu-id="90140-145">Merhaba form tamamlandıktan sonra tıklatın **kaydetmek** toosave hello API Management OAuth 2.0 yetkilendirme sunucu yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="90140-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="90140-146">Merhaba sunucu yapılandırması kaydedildikten sonra bu yapılandırma, hello sonraki bölümde gösterildiği gibi API'leri toouse yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90140-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="90140-147"><a name="step2"></a>API toouse OAuth 2.0 kullanıcı yetkilendirme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="90140-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="90140-148">Tıklatın **API'leri** hello gelen **API Management** hello menüsünde sol, istenen hello API hello adına tıklayın,'ı tıklatın **güvenlik**ve ardından hello kutuyu için **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="90140-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Kullanıcı kimlik doğrulaması][api-management-user-authorization]

<span data-ttu-id="90140-150">İstenen select hello **yetkilendirme sunucusu** hello aşağı açılan liste ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="90140-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Kullanıcı kimlik doğrulaması][api-management-user-authorization-save]

## <span data-ttu-id="90140-152"><a name="step3"></a>Test hello OAuth 2.0 kullanıcı yetkilendirme hello Geliştirici Portalı</span><span class="sxs-lookup"><span data-stu-id="90140-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="90140-153">OAuth 2.0 yetkilendirme sunucunuz yapılandırılmış ve bu sunucu, API toouse yapılandırılmış sonra test toohello Geliştirici Portalı giderek ve bir API çağırma.</span><span class="sxs-lookup"><span data-stu-id="90140-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="90140-154">Tıklatın **Geliştirici Portalı** hello sağ üst menüsündeki içinde.</span><span class="sxs-lookup"><span data-stu-id="90140-154">Click **Developer portal** in hello top right menu.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="90140-156">Tıklatın **API'leri** hello üst menü seçip **Echo API'si**.</span><span class="sxs-lookup"><span data-stu-id="90140-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![Echo API’si][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="90140-158">Yapılandırılmış tek bir API veya görünür tooyour hesabı, API'lere tıklamak sizi doğrudan bu API'nin toohello işlemlerine götürür varsa.</span><span class="sxs-lookup"><span data-stu-id="90140-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="90140-159">Select hello **GET kaynağı** işlemi, tıklatın **açık Konsolu**ve ardından **yetkilendirme kodu** hello açılan gelen.</span><span class="sxs-lookup"><span data-stu-id="90140-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Konsolu açma][api-management-open-console]

<span data-ttu-id="90140-161">Zaman **yetkilendirme kodu** olduğunu belirlenirse, bir açılır pencere hello oturum açma formunda hello OAuth 2.0 sağlayıcı ile görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="90140-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="90140-162">Bu örnekte hello oturum açma formu Azure Active Directory tarafından sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="90140-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="90140-163">Açılır pencerelere varsa, gereken devre dışı tooenable istenir hello tarayıcı tarafından bunları.</span><span class="sxs-lookup"><span data-stu-id="90140-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="90140-164">Bunları etkinleştirdikten sonra Seç **yetkilendirme kodu** yeniden ve hello oturum açma formu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="90140-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![Oturum aç][api-management-oauth2-signin]

<span data-ttu-id="90140-166">Oturum açtıktan sonra hello **istek üst** ile doldurulan bir `Authorization : Bearer` hello isteği yetkilendirir üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="90140-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![İstek üstbilgisi belirteci][api-management-request-header-token]

<span data-ttu-id="90140-168">Bu noktada parametreleri kalan hello istenen hello değerlerini yapılandırmak ve hello isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="90140-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="90140-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90140-169">Next steps</span></span>
<span data-ttu-id="90140-170">Merhaba aşağıdaki video ve eşlik eden OAuth 2.0 ve API Management kullanma hakkında daha fazla bilgi için bkz: [makale](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="90140-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

