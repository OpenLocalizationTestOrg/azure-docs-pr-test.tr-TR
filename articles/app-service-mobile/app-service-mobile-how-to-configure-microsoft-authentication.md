---
title: "Uygulama Hizmetleri uygulamanız için Microsoft Account kimlik doğrulamasını yapılandırma"
description: "Uygulama Hizmetleri uygulamanız için Microsoft Account kimlik doğrulaması yapılandırma konusunda bilgi edinin."
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
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="f40ca-103">Uygulama hizmeti uygulamanızı Microsoft Account oturum açma kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f40ca-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="f40ca-104">Bu konu Azure App Service'nın Microsoft Account bir kimlik doğrulama sağlayıcısı olarak kullanmak üzere yapılandırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="f40ca-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="f40ca-105"><a name="register-microsoft-account"></a>Microsoft hesabı ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="f40ca-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="f40ca-106">Oturum [Azure portal]ve uygulamanıza gidin.</span><span class="sxs-lookup"><span data-stu-id="f40ca-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="f40ca-107">Kopyalama, **URL**, daha sonra Microsoft Account Uygulamanızı yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f40ca-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="f40ca-108">Gidin [uygulamalarım] sayfasında Microsoft Account Developer Center'da ve oturum Microsoft hesabınızla gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="f40ca-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="f40ca-109">Tıklatın **bir uygulama ekleyin**, bir uygulama adı yazın ve tıklayın **uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="f40ca-110">Not **uygulama kimliği**, daha sonra ihtiyacınız olacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="f40ca-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="f40ca-111">"Platformları altında" **eklemek Platform** ve "Web"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="f40ca-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="f40ca-112">"Yeniden yönlendirme URI'ler" altında uygulamanız için uç noktaya sağlayın, sonra **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f40ca-113">URI'dir URL yolu ile eklenen, uygulamanızın, yeniden yönlendirme */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="f40ca-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="f40ca-114">Örneğin, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="f40ca-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="f40ca-115">HTTPS şeması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f40ca-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="f40ca-116">"Uygulama parolaları" altında tıklatın **yeni bir parola oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="f40ca-117">Görüntülenen değeri not edin.</span><span class="sxs-lookup"><span data-stu-id="f40ca-117">Make note of the value that appears.</span></span> <span data-ttu-id="f40ca-118">Sayfayı çıktıktan sonra bir yeniden görüntülenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="f40ca-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f40ca-119">Parola önemli güvenlik kimlik bilgisi değil.</span><span class="sxs-lookup"><span data-stu-id="f40ca-119">The password is an important security credential.</span></span> <span data-ttu-id="f40ca-120">Parolanızı kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f40ca-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="f40ca-121"><a name="secrets"></a>Uygulama hizmeti uygulamanızı Microsoft hesabı Ekle bilgileri</span><span class="sxs-lookup"><span data-stu-id="f40ca-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="f40ca-122">Geri [Azure portal], uygulamanıza gidin, tıklatın **ayarları** > **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="f40ca-123">Kimlik doğrulama / yetkilendirme özelliği etkin değil, bu geçiş **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="f40ca-124">Tıklatın **Microsoft hesabı**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="f40ca-125">Daha önce aldığınız uygulama kimliği ve parola değerleri yapıştırın ve isteğe bağlı olarak uygulamanızın gerektirdiği herhangi bir kapsam etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f40ca-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="f40ca-126">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f40ca-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="f40ca-127">Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi üzere site içeriğini ve API'lerini kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="f40ca-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="f40ca-128">Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f40ca-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="f40ca-129">(İsteğe bağlı) Sitenize yalnızca Microsoft hesabı tarafından kimliği doğrulanmış kullanıcılar için erişimi kısıtlamak üzere koyulan **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** için **Microsoft Account**.</span><span class="sxs-lookup"><span data-stu-id="f40ca-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="f40ca-130">Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler Microsoft hesabı kimlik doğrulaması için yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f40ca-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="f40ca-131">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f40ca-131">Click **Save**.</span></span>

<span data-ttu-id="f40ca-132">Şimdi uygulamanıza kimlik doğrulaması için Microsoft Account kullanmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="f40ca-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="f40ca-133"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="f40ca-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[uygulamalarım]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure portal]: https://portal.azure.com/
