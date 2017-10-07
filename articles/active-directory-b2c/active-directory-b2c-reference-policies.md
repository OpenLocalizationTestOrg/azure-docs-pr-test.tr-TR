---
title: "Azure Active Directory B2C: Yerleşik ilkeleri | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C hello Genişletilebilir ilke çerçevesini ve nasıl toocreate çeşitli ilke türleri"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="59f9d-103">Azure Active Directory B2C: Yerleşik ilkeleri</span><span class="sxs-lookup"><span data-stu-id="59f9d-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="59f9d-104">Azure Active Directory (Azure AD) B2C Hello Genişletilebilir ilke çerçevesini hello çekirdek hello hizmet gücünü ' dir.</span><span class="sxs-lookup"><span data-stu-id="59f9d-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="59f9d-105">İlkeleri tam olarak açıklayan tüketici kimlik deneyimi gibi kaydolma, oturum açma ve profil düzenleme.</span><span class="sxs-lookup"><span data-stu-id="59f9d-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="59f9d-106">Örneğin, bir kayıt ilkesi toocontrol davranışları hello aşağıdaki ayarları yapılandırarak sağlar:</span><span class="sxs-lookup"><span data-stu-id="59f9d-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="59f9d-107">Tüketiciler toosign Merhaba uygulaması için kullanabileceğiniz türü (facebook sosyal hesapları) veya e-posta adresleri gibi yerel hesap</span><span class="sxs-lookup"><span data-stu-id="59f9d-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="59f9d-108">Öznitelikler (örneğin, ad, posta kodu ve ayakkabı boyutu) toobe hello tüketiciden kayıt sırasında toplanan</span><span class="sxs-lookup"><span data-stu-id="59f9d-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="59f9d-109">Azure çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="59f9d-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="59f9d-110">Merhaba görünümüne tüm kayıt sayfaları</span><span class="sxs-lookup"><span data-stu-id="59f9d-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="59f9d-111">Çalıştırma hello İlkesi tamamlandığında uygulama hello (hangi bir belirteç talep olarak bildirimleri) bilgilerini alır</span><span class="sxs-lookup"><span data-stu-id="59f9d-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="59f9d-112">Kiracınızda farklı türlerde birden çok ilke oluşturup, bunları gerektiği gibi uygulamalarınızda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59f9d-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="59f9d-113">İlkeler, uygulamalar arasında yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59f9d-113">Policies can be reused across applications.</span></span> <span data-ttu-id="59f9d-114">Bu esneklik, geliştiricilerin toodefine sağlar ve tüketici kimlik deneyimi ile en az veya herhangi bir değişiklik tootheir kodu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59f9d-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="59f9d-115">İlkeleri basit Geliştirici arabirimi aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59f9d-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="59f9d-116">Uygulamanız (bir ilke parametre hello istekte geçirme) standart bir HTTP kimlik doğrulaması isteği kullanarak bir ilke tetikler ve yanıt olarak özelleştirilmiş bir belirteç alır.</span><span class="sxs-lookup"><span data-stu-id="59f9d-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="59f9d-117">Örneğin, bir kayıt ilkesi çağırma istekleri ve oturum açma ilke çağırmak istekleri arasındaki tek fark hello hello "p" sorgu dizesi parametresi kullanılır hello ilkesi adı şudur:</span><span class="sxs-lookup"><span data-stu-id="59f9d-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="59f9d-118">Hello ilkesi çerçevesi hakkında daha fazla bilgi için bkz: [bu blog gönderisine Azure AD B2C üzerinde hello Enterprise Mobility and Security Blog hakkında](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="59f9d-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="59f9d-119">Bir kayıt veya oturum açma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="59f9d-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="59f9d-120">Bu ilke, her iki tüketici kaydolma ve oturum açma deneyimlerini tek bir yapılandırmasına sahip işler.</span><span class="sxs-lookup"><span data-stu-id="59f9d-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="59f9d-121">Tüketiciler, yoldan hello sağ (kaydolma veya oturum açma) hello bağlam bağlı olarak gerektiriyordu.</span><span class="sxs-lookup"><span data-stu-id="59f9d-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="59f9d-122">Ayrıca, Merhaba uygulaması başarılı oturum ups veya oturum açma işlemleri almaz belirteçleri Merhaba içeriğine anlatır.  Hello kaydolma veya oturum açma ilkesi için bir kod örneğidir [kullanılabilir burada](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="59f9d-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="59f9d-123">Kayıt İlkesi ve oturum açma ilkesi bu ilkeyi kullanmak maskelenmesi önerilen olur.</span><span class="sxs-lookup"><span data-stu-id="59f9d-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="59f9d-124">Kayıt ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="59f9d-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="59f9d-125">Bir oturum açma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="59f9d-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="59f9d-126">İlke düzenleme profil oluşturma</span><span class="sxs-lookup"><span data-stu-id="59f9d-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="59f9d-127">Bir parola sıfırlama ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="59f9d-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="59f9d-128">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="59f9d-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="59f9d-129">Bir kayıt veya oturum açma ilkesi bir parola sıfırlama İlkesi ile nasıl bağlanır?</span><span class="sxs-lookup"><span data-stu-id="59f9d-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="59f9d-130">Bir oturum açma veya kaydolma ilkesiyle (yerel hesaplar için) oluşturduğunuzda, gördüğünüz bir **unuttunuz parola?** hello deneyimi'nın ilk sayfasında hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="59f9d-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="59f9d-131">Bu bağlantıyı tıklatarak otomatik olarak tetikleyici bir parola sıfırlama İlkesi değil.</span><span class="sxs-lookup"><span data-stu-id="59f9d-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="59f9d-132">Bunun yerine, hata kodu hello  **`AADB2C90118`**  tooyour uygulamasına döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59f9d-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="59f9d-133">Uygulamanızın, belirli parolası sıfırlama ilkesini harekete geçirerek, bu hata kodu toohandle gerekir.</span><span class="sxs-lookup"><span data-stu-id="59f9d-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="59f9d-134">Daha fazla bilgi için bir [ilkeleri bağlama hello yaklaşımı gösteren örnek](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="59f9d-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="59f9d-135">Bir kayıt veya oturum açma ilkesi veya bir kayıt ilkesi ve bir oturum açma ilkesi kullanmalıyım?</span><span class="sxs-lookup"><span data-stu-id="59f9d-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="59f9d-136">Bir kayıt ilkesi ve bir oturum açma ilkesi bir kayıt veya oturum açma ilkesi kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="59f9d-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="59f9d-137">Hello kaydolma veya oturum açma ilkesi hello oturum açma ilkesinden daha fazla özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="59f9d-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="59f9d-138">Ayrıca toouse sayfası kullanıcı arabirimini özelleştirme sağlar ve yerelleştirme için daha iyi destek vardır.</span><span class="sxs-lookup"><span data-stu-id="59f9d-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="59f9d-139">oturum açma Hello İlkesi ilkelerinizi toolocalize gerekmiyorsa, yalnızca markalama için ikincil özelleştirme özellikleri gerekir ve parola istediğiniz önerilir yerleşik sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="59f9d-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59f9d-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59f9d-140">Next steps</span></span>
* [<span data-ttu-id="59f9d-141">Belirteç, oturum ve tek oturum açma yapılandırması</span><span class="sxs-lookup"><span data-stu-id="59f9d-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="59f9d-142">E-posta doğrulama tüketici kaydolma sırasında devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="59f9d-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

