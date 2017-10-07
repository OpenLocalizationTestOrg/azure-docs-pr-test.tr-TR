---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Twitter kimlik doğrulaması"
description: "Bilgi nasıl uygulama hizmetleri uygulamanız için tooconfigure Twitter kimlik doğrulaması."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="12520-103">Nasıl tooconfigure App Service uygulama toouse Twitter oturum açma</span><span class="sxs-lookup"><span data-stu-id="12520-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="12520-104">Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Twitter bir kimlik doğrulama sağlayıcısı olarak.</span><span class="sxs-lookup"><span data-stu-id="12520-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="12520-105">Bu konudaki toocomplete hello yordamı, bir doğrulanmış e-posta adresi ve telefon numarası olan bir Twitter hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="12520-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="12520-106">Yeni bir Twitter hesabı toocreate Git çok<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="12520-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="12520-107"><a name="register"></a>Twitter ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="12520-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="12520-108">Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="12520-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="12520-109">Kopyalama, **URL**.</span><span class="sxs-lookup"><span data-stu-id="12520-109">Copy your **URL**.</span></span> <span data-ttu-id="12520-110">Twitter uygulamanız bu tooconfigure kullanır.</span><span class="sxs-lookup"><span data-stu-id="12520-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="12520-111">Toohello gidin [Twitter geliştiriciler] Web sitesi, Twitter hesabı kimlik bilgilerinizle oturum açın ve tıklatın **yeni uygulama oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="12520-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="12520-112">Merhaba türü **adı** ve **açıklama** yeni uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="12520-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="12520-113">Uygulamanızın Yapıştır **URL** hello için **Web sitesi** değeri.</span><span class="sxs-lookup"><span data-stu-id="12520-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="12520-114">Ardından, hello **geri çağırma URL'si**, hello Yapıştır **geri çağırma URL'si** daha önce kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="12520-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="12520-115">Merhaba yolunun ile mobil uygulama ağ geçidi budur */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="12520-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="12520-116">Örneğin, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="12520-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="12520-117">Merhaba HTTPS şeması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="12520-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="12520-118">Merhaba alt hello sayfasında hello koşullarını okuyup kabul edin.</span><span class="sxs-lookup"><span data-stu-id="12520-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="12520-119">Ardından **Twitter uygulamanızı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="12520-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="12520-120">Bu kayıtları hello uygulama hello uygulama ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="12520-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="12520-121">Hello tıklatın **ayarları** sekmesi, onay **bu uygulama kullanılan toobe toosign Twitter oturum izin**, ardından **güncelleştirme ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="12520-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="12520-122">Select hello **anahtarları ve erişim belirteçleri** sekmesi. Merhaba değerlerini Not **tüketici anahtarı (API anahtarı)** ve **tüketici gizli anahtarı (API gizli)**.</span><span class="sxs-lookup"><span data-stu-id="12520-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12520-123">Merhaba tüketici gizli bir önemli güvenlik kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="12520-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="12520-124">Bu gizli kimseyle paylaşmayın değil veya uygulamanızla dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12520-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="12520-125"><a name="secrets"></a>Ekleme Twitter bilgi tooyour uygulama</span><span class="sxs-lookup"><span data-stu-id="12520-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="12520-126">Merhaba edilene [Azure portal], tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="12520-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="12520-127">Tıklatın **ayarları**ve ardından **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="12520-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="12520-128">Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, hello anahtar çok kapatma**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="12520-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="12520-129">Tıklatın **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="12520-129">Click **Twitter**.</span></span> <span data-ttu-id="12520-130">Daha önce edindiğiniz değerleri Hello uygulama kimliği ve uygulama gizli anahtarı yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="12520-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="12520-131">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12520-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="12520-132">Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="12520-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="12520-133">Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="12520-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="12520-134">Twitter tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="12520-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="12520-135">Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış kimlik doğrulaması için yeniden yönlendirilen tooTwitter isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="12520-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="12520-136">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12520-136">Click **Save**.</span></span>

<span data-ttu-id="12520-137">Artık uygulamanızı kimlik doğrulaması için hazır toouse Twitter bulunur.</span><span class="sxs-lookup"><span data-stu-id="12520-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="12520-138"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="12520-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter geliştiriciler]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure portal]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
