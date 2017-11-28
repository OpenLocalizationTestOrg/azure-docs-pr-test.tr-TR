---
title: "aaaPublish yerel istemci uygulamaları - Azure AD | Microsoft Docs"
description: "Nasıl tooenable yerel istemci uygulamaları toocommunicate Azure AD uygulama ara sunucusu Bağlayıcısı tooprovide güvenli uzaktan erişim tooyour ile uygulamaları şirket içi kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="c6499-103">Nasıl tooenable yerel istemci uygulamaları toointeract proxy uygulamaları ile</span><span class="sxs-lookup"><span data-stu-id="c6499-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="c6499-104">Toplama tooweb uygulamalarda, Azure Active Directory Uygulama proxy'si kullanılan toopublish yerel istemci uygulamaları da olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6499-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="c6499-105">Web uygulamaları bir tarayıcı erişilen sırada bir aygıtta yüklü olmadığından yerel istemci uygulamaları, web uygulamaları farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="c6499-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="c6499-106">Uygulama proxy'si yerel istemci uygulamalar tarafından verilen standart yetkilendirmek HTTP üstbilgilerinde gönderilen belirteçler kabul Azure AD destekler.</span><span class="sxs-lookup"><span data-stu-id="c6499-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Son kullanıcılar, Azure Active Directory ve yayımlanmış uygulamalar arasındaki ilişki](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="c6499-108">Merhaba mvc'deki kimlik doğrulama ve birçok istemci ortamları, toopublish yerel uygulamaları destekler Azure AD kimlik doğrulama kitaplığı, kullanın.</span><span class="sxs-lookup"><span data-stu-id="c6499-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="c6499-109">Uygulama proxy'si uygun hello [yerel uygulama tooWeb API senaryo](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="c6499-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="c6499-110">Bu makalede hello dört adım toopublish uygulama proxy'si ve hello Azure AD kimlik doğrulama kitaplığı ile yerel bir uygulamaya anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c6499-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="c6499-111">1. adım: uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="c6499-111">Step 1: Publish your application</span></span>
<span data-ttu-id="c6499-112">Başka bir uygulama gibi proxy uygulamanızı yayımlamak ve uygulamanız kullanıcıların tooaccess atayın.</span><span class="sxs-lookup"><span data-stu-id="c6499-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="c6499-113">Daha fazla bilgi için bkz: [uygulama proxy'si ile uygulama yayımlama](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="c6499-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="c6499-114">2. adım: uygulamanızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c6499-114">Step 2: Configure your application</span></span>
<span data-ttu-id="c6499-115">Yerel uygulamanız aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="c6499-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="c6499-116">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6499-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6499-117">Çok gidin**Azure Active Directory** > **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="c6499-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="c6499-118">Seçin **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="c6499-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="c6499-119">Select, uygulamanız için bir ad belirtin **yerel** hello uygulama türü olarak ve uygulamanız için hello yeniden yönlendirme URI'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c6499-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Yeni bir uygulama kaydı oluşturma](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="c6499-121">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="c6499-121">Select **Create**.</span></span>

<span data-ttu-id="c6499-122">Yeni bir uygulama kaydı oluşturma hakkında daha ayrıntılı bilgi için bkz: [uygulamaları Azure Active Directory ile tümleştirme](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c6499-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="c6499-123">3. adım: Grant erişim tooother uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c6499-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="c6499-124">Merhaba yerel uygulama açığa toobe tooother uygulamalar dizininizde etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="c6499-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="c6499-125">Hala **uygulama kayıtlar**, hello az önce oluşturduğunuz yeni yerel uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="c6499-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="c6499-126">Seçin **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="c6499-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="c6499-127">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c6499-127">Select **Add**.</span></span>
4. <span data-ttu-id="c6499-128">Açık hello ilk adım, **bir API seçin**.</span><span class="sxs-lookup"><span data-stu-id="c6499-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="c6499-129">Hello ilk bölümünde yayınlanan hello arama çubuğu toofind hello uygulama proxy'si uygulamayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c6499-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="c6499-130">Bu uygulama seçin ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="c6499-130">Choose that app, then click **Select**.</span></span> 

   ![Merhaba proxy uygulamayı arayın](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="c6499-132">Açık hello ikinci adım, **seçin izinleri**.</span><span class="sxs-lookup"><span data-stu-id="c6499-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="c6499-133">Yerel uygulama erişim tooyour proxy uygulamanızın Hello onay kutusunu toogrant kullanın ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="c6499-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![GRANT erişim tooproxy uygulama](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="c6499-135">Seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="c6499-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="c6499-136">4. adım: hello Active Directory kimlik doğrulama kitaplığı Düzenle</span><span class="sxs-lookup"><span data-stu-id="c6499-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="c6499-137">Merhaba yerel uygulama kodunu metin aşağıdaki hello Active Directory Authentication Library (ADAL) tooinclude hello hello kimlik doğrulaması bağlamında düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="c6499-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="c6499-138">Merhaba değişkenleri hello örnek kodda şu şekilde değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="c6499-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="c6499-139">**Kiracı kimliği** hello Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c6499-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="c6499-140">Çok gidin**Azure Active Directory** > **özellikleri** ve kopyalama hello dizin kimliği.</span><span class="sxs-lookup"><span data-stu-id="c6499-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="c6499-141">**Dış URL** hello Proxy Uygulama girdiğiniz hello ön uç URL'si.</span><span class="sxs-lookup"><span data-stu-id="c6499-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="c6499-142">toofind bu değer, toohello gidin **uygulama proxy'si** hello proxy uygulama bölümü.</span><span class="sxs-lookup"><span data-stu-id="c6499-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="c6499-143">**Uygulama Kimliği** Merhaba yerel uygulama hello üzerinde bulunabilir **özellikleri** hello yerel uygulama sayfası.</span><span class="sxs-lookup"><span data-stu-id="c6499-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="c6499-144">**Merhaba yerel uygulamasının URI'sini yeniden yönlendir** hello üzerinde bulunabilir **yeniden yönlendirme URI'ler** hello yerel uygulama sayfası.</span><span class="sxs-lookup"><span data-stu-id="c6499-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="c6499-145">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c6499-145">See also</span></span>

<span data-ttu-id="c6499-146">Merhaba yerel uygulama akışı hakkında daha fazla bilgi için bkz: [yerel uygulama tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="c6499-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="c6499-147">Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="c6499-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
