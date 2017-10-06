---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Google kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Google kimlik doğrulaması."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="e98fc-103">Nasıl tooconfigure App Service uygulama toouse Google oturum açma</span><span class="sxs-lookup"><span data-stu-id="e98fc-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e98fc-104">Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Google kimlik doğrulama sağlayıcısı olarak.</span><span class="sxs-lookup"><span data-stu-id="e98fc-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="e98fc-105">Bu konudaki toocomplete hello yordamı, doğrulanmış e-posta adresine sahip bir Google hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e98fc-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="e98fc-106">Yeni bir Google hesabı toocreate Git çok[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="e98fc-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="e98fc-107"><a name="register"></a>Google ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="e98fc-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="e98fc-108">Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="e98fc-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="e98fc-109">Kopyalama, **URL**, hangi Google uygulamanızı sonraki tooconfigure kullanın.</span><span class="sxs-lookup"><span data-stu-id="e98fc-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="e98fc-110">Toohello gidin [Google API'leri](http://go.microsoft.com/fwlink/p/?LinkId=268303) Web sitesi, Google hesabı kimlik bilgilerinizle oturum tıklatın **proje oluştur**, sağlayın bir **proje adı**, ardından  **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="e98fc-111">Altında **sosyal API'leri** tıklatın **Google + API** ve ardından **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="e98fc-112">Sol gezinti, hello içinde **kimlik bilgileri** > **OAuth izni ekran**seçeneğini belirleyip, **e-posta adresi**, girin bir **Ürünadı**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="e98fc-113">Merhaba, **kimlik bilgileri** sekmesini tıklatın, **kimlik bilgileri oluşturma** > **OAuth istemci kimliği**seçeneğini belirleyip **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="e98fc-114">Yapıştır hello uygulama hizmeti **URL** , daha önce kopyalanır **yetkili JavaScript çıkış**, ardından, yeniden yönlendirme yapıştırın URI **yeniden yönlendirme URI'si yetkili**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="e98fc-115">URI'dir hello URL hello yolu ile eklenen, uygulamanızın yeniden yönlendirme hello */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="e98fc-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="e98fc-116">Örneğin, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="e98fc-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="e98fc-117">Merhaba HTTPS şeması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e98fc-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="e98fc-118">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e98fc-118">Then click **Create**.</span></span>
7. <span data-ttu-id="e98fc-119">Merhaba sonraki ekranda, kimliği ve istemci gizli anahtarı hello istemci hello değerlerini not edin.</span><span class="sxs-lookup"><span data-stu-id="e98fc-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e98fc-120">Merhaba gizli bir önemli güvenlik kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="e98fc-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="e98fc-121">Bu gizli kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e98fc-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="e98fc-122"><a name="secrets"></a>Ekleme Google bilgi tooyour uygulama</span><span class="sxs-lookup"><span data-stu-id="e98fc-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="e98fc-123">Merhaba edilene [Azure portal], tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="e98fc-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="e98fc-124">Tıklatın **ayarları**ve ardından **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="e98fc-125">Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, hello anahtar çok kapatma**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="e98fc-126">Tıklatın **Google**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-126">Click **Google**.</span></span> <span data-ttu-id="e98fc-127">Daha önce edindiğiniz hello uygulama kimliği ve uygulama gizli anahtarı değerler içinde yapıştırın ve isteğe bağlı olarak uygulamanızın gerektirdiği herhangi bir kapsam etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e98fc-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="e98fc-128">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e98fc-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="e98fc-129">Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="e98fc-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="e98fc-130">Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e98fc-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="e98fc-131">Google tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Google**.</span><span class="sxs-lookup"><span data-stu-id="e98fc-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="e98fc-132">Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış kimlik doğrulaması için yeniden yönlendirilen tooGoogle isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="e98fc-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="e98fc-133">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e98fc-133">Click **Save**.</span></span>

<span data-ttu-id="e98fc-134">Artık uygulamanızı kimlik doğrulaması için hazır toouse Google bulunur.</span><span class="sxs-lookup"><span data-stu-id="e98fc-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="e98fc-135"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="e98fc-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure portal]: https://portal.azure.com/

