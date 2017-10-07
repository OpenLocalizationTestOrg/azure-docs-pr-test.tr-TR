---
title: "oturum açma aaaSingle tooapps Azure AD uygulama proxy'si ile | Microsoft Docs"
description: "Yayımlanan şirket içi uygulamalarınızı hello Azure portalında Azure AD uygulama proxy'si için çoklu oturum açmayı etkinleştirin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="7ae8a-103">Çoklu oturum açma için uygulama proxy'si ile vaulting parola</span><span class="sxs-lookup"><span data-stu-id="7ae8a-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="7ae8a-104">Azure Active Directory Uygulama proxy'si uzak çalışanlar güvenli bir şekilde bunları çok erişebilmesi için şirket içi uygulamaları yayımlama üretkenlik geliştirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="7ae8a-105">Hello Azure portalı, çoklu oturum açma (SSO) toothese uygulamaları de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="7ae8a-106">Kullanıcılarınızın Azure AD ile tooauthenticate yeterlidir ve toosign yeniden vermeden kuruluş uygulamanız erişebilir.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="7ae8a-107">Uygulama proxy'si destekleyen birkaç [tek oturum açma modları](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ae8a-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="7ae8a-108">Parola tabanlı oturum açma kimlik doğrulaması için bir kullanıcı adı/parola bileşimi kullanan uygulamalar için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="7ae8a-109">Uygulamanız için parola tabanlı oturum açma yapılandırdığınızda, kullanıcılarınızın bir kez toohello şirket içi uygulama toosign sahip.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="7ae8a-110">Bundan sonra Azure Active Directory hello oturum açma bilgileri depolar ve kullanıcılarınızın, uzaktan erişim otomatik olarak toohello uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="7ae8a-111">Zaten varsa yayımlanan ve uygulama proxy'si ile uygulamanızı test.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="7ae8a-112">Aksi takdirde, başlangıç adımları [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md) tekrar buraya gelin.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="7ae8a-113">Uygulamanız için vaulting parola ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ae8a-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="7ae8a-114">İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="7ae8a-115">Seçin **Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="7ae8a-116">Merhaba listeden hello uygulama SSO tooset yedeklemek istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="7ae8a-117">Seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-117">Select **Single sign-on**.</span></span>

   ![Çoklu oturum açma seçin](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="7ae8a-119">Merhaba SSO modunu seçin **parola tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="7ae8a-120">Merhaba URL'Sİ'ın oturum açma, burada kullanıcılar kendi kullanıcı adı ve parola toosign tooyour uygulama hello şirket ağı dışında girin, başlangıç sayfası için hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="7ae8a-121">Bu hello uygulama proxy'si aracılığıyla hello uygulama yayımlandığında oluşturduğunuz dış URL olabilir.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Parola tabanlı oturum açma seçin ve URL'nizi girin](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="7ae8a-123">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="7ae8a-124">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="7ae8a-124">Test your app</span></span>

<span data-ttu-id="7ae8a-125">Uzaktan erişim tooyour uygulama için yapılandırılan tooexternal URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="7ae8a-126">Bu uygulama için kimlik bilgileri (veya hello hesabının kimlik bilgilerini erişimle ayarladığınız bir test) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="7ae8a-127">Başarıyla oturum açtıktan sonra mümkün tooleave hello uygulama ve kimlik bilgilerinizi tekrar girmeden geri dönün.</span><span class="sxs-lookup"><span data-stu-id="7ae8a-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7ae8a-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7ae8a-128">Next steps</span></span>

- <span data-ttu-id="7ae8a-129">Diğer yolları tooimplement hakkında okuyun [uygulama proxy'si ile çoklu oturum açma](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7ae8a-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="7ae8a-130">Hakkında bilgi edinin [uygulamaları Azure AD uygulama proxy'si ile uzaktan erişim için güvenlik konuları](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="7ae8a-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>