---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Facebook kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Facebook kimlik doğrulaması."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="934ea-103">Nasıl tooconfigure App Service uygulama toouse Facebook oturum açma</span><span class="sxs-lookup"><span data-stu-id="934ea-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="934ea-104">Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Facebook kimlik doğrulama sağlayıcısı olarak.</span><span class="sxs-lookup"><span data-stu-id="934ea-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="934ea-105">Bu konudaki toocomplete hello yordamı, doğrulanmış e-posta adresi ve cep telefonu numarası olan bir Facebook hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="934ea-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="934ea-106">Yeni bir Facebook hesabıyla toocreate Git çok[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="934ea-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="934ea-107"><a name="register"></a>Facebook ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="934ea-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="934ea-108">Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="934ea-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="934ea-109">Kopyalama, **URL**.</span><span class="sxs-lookup"><span data-stu-id="934ea-109">Copy your **URL**.</span></span> <span data-ttu-id="934ea-110">Bu tooconfigure Facebook uygulamanızı kullanır.</span><span class="sxs-lookup"><span data-stu-id="934ea-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="934ea-111">Başka bir tarayıcı penceresinde toohello gidin [Facebook geliştiriciler] Web sitesi ve, Facebook ile oturum açma hesabı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="934ea-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="934ea-112">(İsteğe bağlı) Zaten kaydolmadıysanız tıklatın **uygulamaları** > **kaydetmek geliştirici olarak**, ardından hello İlkesi kabul etmek ve hello kayıt adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="934ea-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="934ea-113">Tıklatın **uygulamalarım** > **yeni bir uygulama eklemek** > **Web sitesi** > **atlayın ve uygulama kimliği oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="934ea-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="934ea-114">İçinde **görünen adı**, türü, uygulamanız için benzersiz bir ad yazın, **ilgili kişi e-posta**, seçin bir **kategori** uygulamanız için ardından **uygulama kimliği oluşturma**ve hello güvenlik denetimi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="934ea-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="934ea-115">Bu yeni Facebook uygulamanız için toohello Geliştirici Pano götürür.</span><span class="sxs-lookup"><span data-stu-id="934ea-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="934ea-116">"Facebook Login" altında tıklatın **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="934ea-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="934ea-117">Uygulamanızın eklemek **yeniden yönlendirme URI'si** çok**geçerli OAuth yeniden yönlendirme URI'ler**, ardından **Değişiklikleri Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="934ea-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="934ea-118">URI'dir hello URL hello yolu ile eklenen, uygulamanızın, yeniden yönlendirme */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="934ea-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="934ea-119">Örneğin, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="934ea-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="934ea-120">Merhaba HTTPS şeması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="934ea-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="934ea-121">Merhaba sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="934ea-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="934ea-122">Hello üzerinde **uygulama gizli anahtarı** alan, tıklatın **Göster**, istenen yeniden hello değerlerini not parolanızı sağlayın **uygulama kimliği** ve **uygulama gizli anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="934ea-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="934ea-123">Bu sonraki tooconfigure Azure'da uygulamanızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="934ea-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="934ea-124">Merhaba uygulama gizli anahtarı bir önemli güvenlik kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="934ea-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="934ea-125">Bu gizli kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="934ea-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="934ea-126">Merhaba kullanılan tooregister Merhaba uygulaması olan Facebook hesabıyla hello uygulamasının bir yöneticidir.</span><span class="sxs-lookup"><span data-stu-id="934ea-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="934ea-127">Bu noktada, yalnızca Yöneticiler bu uygulamasına oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="934ea-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="934ea-128">tooauthenticate diğer Facebook hesapları **uygulama gözden geçirme** ve etkinleştirmek **olun < uygulamanızın-adı > ortak** tooenable genel genel Facebook kimlik doğrulamasını kullanarak erişim.</span><span class="sxs-lookup"><span data-stu-id="934ea-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="934ea-129"><a name="secrets"></a>Ekleme Facebook bilgi tooyour uygulama</span><span class="sxs-lookup"><span data-stu-id="934ea-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="934ea-130">Merhaba edilene [Azure portal], tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="934ea-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="934ea-131">Tıklatın **ayarları** > **kimlik doğrulama / yetkilendirme**, emin olun **App Service kimlik doğrulaması** olan **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="934ea-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="934ea-132">Tıklatın **Facebook**, daha önce edindiğiniz hello uygulama kimliği ve uygulama gizli anahtarı değerler içinde yapıştırın, isteğe bağlı olarak, uygulamanız tarafından gerekli herhangi bir kapsam etkinleştirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="934ea-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="934ea-133">Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="934ea-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="934ea-134">Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="934ea-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="934ea-135">= (İsteğe bağlı) toorestrict erişim tooyour site tooonly Facebook tarafından kimliği doğrulanmış kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="934ea-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="934ea-136">Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış kimlik doğrulaması için yeniden yönlendirilen tooFacebook isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="934ea-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="934ea-137">Yapılandırma kimlik doğrulaması yapıldığında tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="934ea-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="934ea-138">Artık uygulamanızı hazır toouse Facebook kimlik doğrulaması için bulunur.</span><span class="sxs-lookup"><span data-stu-id="934ea-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="934ea-139"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="934ea-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook geliştiriciler]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure portal]: https://portal.azure.com/
