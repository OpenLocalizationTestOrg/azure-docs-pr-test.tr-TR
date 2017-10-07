---
title: "Uygulama Hizmetleri uygulamanız için aaaHow tooconfigure Microsoft Account kimlik doğrulaması"
description: "Bilgi nasıl tooconfigure Microsoft Account kimlik uygulama hizmetleri uygulamanız için."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="72ab5-103">Nasıl tooconfigure App Service uygulama toouse Microsoft Account oturum açma</span><span class="sxs-lookup"><span data-stu-id="72ab5-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="72ab5-104">Bu konu, nasıl gösterir tooconfigure Azure App Service toouse Microsoft Account bir kimlik doğrulama sağlayıcısı olarak.</span><span class="sxs-lookup"><span data-stu-id="72ab5-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="72ab5-105"><a name="register-microsoft-account"></a>Microsoft hesabı ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="72ab5-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="72ab5-106">Toohello üzerinde oturum [Azure portal]ve tooyour uygulama gidin.</span><span class="sxs-lookup"><span data-stu-id="72ab5-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="72ab5-107">Kopyalama, **URL**, daha sonra uygulamanızı tooconfigure Microsoft Account kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="72ab5-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="72ab5-108">Toohello gidin [uygulamalarım] sayfasında hello Microsoft Account Developer Center'da ve oturum Microsoft hesabınızla gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="72ab5-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="72ab5-109">Tıklatın **bir uygulama ekleyin**, bir uygulama adı yazın ve tıklayın **uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="72ab5-110">Merhaba Not **uygulama kimliği**, daha sonra ihtiyacınız olacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="72ab5-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="72ab5-111">"Platformları altında" **eklemek Platform** ve "Web"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="72ab5-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="72ab5-112">"Yeniden yönlendirme URI'ler" tedarik hello uç nokta altında uygulamanız için ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="72ab5-113">URI'dir hello URL hello yolu ile eklenen, uygulamanızın, yeniden yönlendirme */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="72ab5-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="72ab5-114">Örneğin, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="72ab5-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="72ab5-115">Merhaba HTTPS şeması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="72ab5-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="72ab5-116">"Uygulama parolaları" altında tıklatın **yeni bir parola oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="72ab5-117">Görünen hello değeri not edin.</span><span class="sxs-lookup"><span data-stu-id="72ab5-117">Make note of hello value that appears.</span></span> <span data-ttu-id="72ab5-118">Merhaba sayfayı çıktıktan sonra bir yeniden görüntülenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="72ab5-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="72ab5-119">Merhaba, önemli güvenlik kimlik bilgisi paroladır.</span><span class="sxs-lookup"><span data-stu-id="72ab5-119">hello password is an important security credential.</span></span> <span data-ttu-id="72ab5-120">Merhaba parolanızı kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72ab5-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="72ab5-121"><a name="secrets"></a>Microsoft hesabı Ekle bilgi tooyour uygulama hizmeti uygulaması</span><span class="sxs-lookup"><span data-stu-id="72ab5-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="72ab5-122">Merhaba edilene [Azure portal], tooyour uygulama gidin, tıklatın **ayarları** > **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="72ab5-123">Varsa hello kimlik doğrulama / yetkilendirme özelliği etkin değil, bu geçiş **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="72ab5-124">Tıklatın **Microsoft hesabı**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="72ab5-125">Daha önce edindiğiniz hello uygulama kimliği ve parola değerler içinde yapıştırın ve isteğe bağlı olarak uygulamanızın gerektirdiği herhangi bir kapsam etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="72ab5-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="72ab5-126">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72ab5-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="72ab5-127">Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi tooyour site içeriği ve API'leri kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="72ab5-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="72ab5-128">Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="72ab5-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="72ab5-129">Microsoft hesabı tarafından kimliği doğrulanmış (isteğe bağlı) toorestrict erişim tooyour site tooonly kullanıcılar ayarlamak **istek kimliği doğrulanmamış olduğunda eylem tootake** çok**Microsoft Account**.</span><span class="sxs-lookup"><span data-stu-id="72ab5-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="72ab5-130">Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler yönlendirilir tooMicrosoft hesabı için kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="72ab5-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="72ab5-131">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72ab5-131">Click **Save**.</span></span>

<span data-ttu-id="72ab5-132">Artık uygulamanızı kimlik doğrulaması için hazır toouse Microsoft Account bulunur.</span><span class="sxs-lookup"><span data-stu-id="72ab5-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="72ab5-133"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="72ab5-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[uygulamalarım]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure portal]: https://portal.azure.com/
