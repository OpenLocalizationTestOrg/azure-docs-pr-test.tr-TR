---
title: "Uygulama Hizmetleri uygulamanız için Facebook kimlik doğrulamasını yapılandırma"
description: "Uygulama Hizmetleri uygulamanız için Facebook kimlik doğrulaması yapılandırma konusunda bilgi edinin."
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
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="59de8-103">App Service uygulamanızı Facebook oturum açma bilgilerini kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59de8-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="59de8-104">Bu konu Azure App Service Facebook kimlik doğrulama sağlayıcısı olarak kullanmak üzere yapılandırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="59de8-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="59de8-105">Bu konudaki yordamı tamamlamak için doğrulanmış e-posta adresi ve cep telefonu numarası olan bir Facebook hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="59de8-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="59de8-106">Yeni bir Facebook hesabı oluşturmak için şu adrese gidin [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="59de8-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="59de8-107"><a name="register"></a>Facebook ile uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="59de8-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="59de8-108">Oturum [Azure portal]ve uygulamanıza gidin.</span><span class="sxs-lookup"><span data-stu-id="59de8-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="59de8-109">Kopyalama, **URL**.</span><span class="sxs-lookup"><span data-stu-id="59de8-109">Copy your **URL**.</span></span> <span data-ttu-id="59de8-110">Facebook Uygulamanızı yapılandırmak için bunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="59de8-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="59de8-111">Başka bir tarayıcı penceresinde gidin [Facebook geliştiriciler] Web sitesi ve, Facebook ile oturum açma hesabı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="59de8-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="59de8-112">(İsteğe bağlı) Zaten kaydolmadıysanız tıklatın **uygulamaları** > **kaydetmek geliştirici olarak**, ardından ilkeyi kabul etmek ve kayıt adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="59de8-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="59de8-113">Tıklatın **uygulamalarım** > **yeni bir uygulama eklemek** > **Web sitesi** > **atlayın ve uygulama kimliği oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="59de8-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="59de8-114">İçinde **görünen adı**, türü, uygulamanız için benzersiz bir ad yazın, **ilgili kişi e-posta**, seçin bir **kategori** uygulamanız için ardından **uygulama kimliği oluşturma**ve güvenlik denetimi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="59de8-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="59de8-115">Bu, yeni Facebook uygulamanız için geliştirici panoya götürür.</span><span class="sxs-lookup"><span data-stu-id="59de8-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="59de8-116">"Facebook Login" altında tıklatın **Get Started**.</span><span class="sxs-lookup"><span data-stu-id="59de8-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="59de8-117">Uygulamanızın eklemek **yeniden yönlendirme URI'si** için **geçerli OAuth yeniden yönlendirme URI'ler**, ardından **Değişiklikleri Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="59de8-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="59de8-118">URI'dir URL yolu ile eklenen, uygulamanızın, yeniden yönlendirme */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="59de8-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="59de8-119">Örneğin, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="59de8-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="59de8-120">HTTPS şeması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="59de8-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="59de8-121">Sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="59de8-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="59de8-122">Üzerinde **uygulama gizli anahtarı** alan, tıklatın **Göster**, istenen yeniden değerlerini not parolanızı sağlayın **uygulama kimliği** ve **uygulama gizli anahtarı** .</span><span class="sxs-lookup"><span data-stu-id="59de8-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="59de8-123">Bunları daha sonra Azure'da Uygulamanızı yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="59de8-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="59de8-124">Uygulama gizli anahtarı bir önemli güvenlik kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="59de8-124">The app secret is an important security credential.</span></span> <span data-ttu-id="59de8-125">Bu gizli kimseyle paylaşmayın değil veya bir istemci uygulama kapsamındaki dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59de8-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="59de8-126">Uygulamayı kaydetmek için kullanılan Facebook uygulaması bir yönetici hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="59de8-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="59de8-127">Bu noktada, yalnızca Yöneticiler bu uygulamasına oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="59de8-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="59de8-128">Diğer Facebook hesaplarının kimliğini doğrulamak için tıklatın **uygulama İnceleme** ve etkinleştirme **olun < uygulamanızın-adı > ortak** Facebook kimlik doğrulaması kullanarak genel genel erişimi etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="59de8-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="59de8-129"><a name="secrets"></a>Uygulamanıza eklemek Facebook bilgileri</span><span class="sxs-lookup"><span data-stu-id="59de8-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="59de8-130">Geri [Azure portal], uygulamanıza gidin.</span><span class="sxs-lookup"><span data-stu-id="59de8-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="59de8-131">Tıklatın **ayarları** > **kimlik doğrulama / yetkilendirme**, emin olun **App Service kimlik doğrulaması** olan **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="59de8-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="59de8-132">Tıklatın **Facebook**, hangi daha önce aldığınız uygulama kimliği ve uygulama gizli anahtarı değerler yapıştırın, isteğe bağlı olarak, uygulamanız tarafından gerekli herhangi bir kapsam etkinleştirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="59de8-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="59de8-133">Varsayılan olarak, App Service kimlik doğrulaması sağlar ancak yetkili erişimi üzere site içeriğini ve API'lerini kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="59de8-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="59de8-134">Kullanıcılar, uygulama kodunuzda yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59de8-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="59de8-135">(İsteğe bağlı) Sitenize yalnızca Facebook tarafından kimliği doğrulanmış kullanıcılar için erişimi kısıtlamak üzere koyulan **isteğin kimliği doğrulanmamış olduğunda gerçekleştirilecek eylem** için **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="59de8-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="59de8-136">Bu, tüm istekleri doğrulanmasını gerektirir ve tüm kimliği doğrulanmamış istekler için Facebook kimlik doğrulaması için yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="59de8-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="59de8-137">Yapılandırma kimlik doğrulaması yapıldığında tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="59de8-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="59de8-138">Şimdi uygulamanıza kimlik doğrulaması için Facebook kullanmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="59de8-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="59de8-139"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="59de8-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="59de8-140">[Facebook geliştiriciler]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="59de8-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="59de8-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="59de8-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="59de8-142">[Azure portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="59de8-142">[Azure portal]: https://portal.azure.com/</span></span>
