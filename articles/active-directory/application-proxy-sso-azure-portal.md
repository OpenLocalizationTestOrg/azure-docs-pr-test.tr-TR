---
title: "Azure AD uygulama proxy'si ile uygulamaları için çoklu oturum açma | Microsoft Docs"
description: "Tek oturum açma için yayımlanan şirket içi uygulamalarınızı Azure portalında Azure AD uygulama proxy'si ile açın."
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
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="84070-103">Çoklu oturum açma için uygulama proxy'si ile vaulting parola</span><span class="sxs-lookup"><span data-stu-id="84070-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="84070-104">Azure Active Directory Uygulama proxy'si uzak çalışanlar güvenli bir şekilde bunları çok erişebilmesi için şirket içi uygulamaları yayımlama üretkenlik geliştirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="84070-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="84070-105">Azure portalında, aynı zamanda çoklu oturum açma (SSO) bu uygulamalara ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84070-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="84070-106">Kullanıcılarınız yalnızca Azure AD ile kimlik doğrulaması yapmanız ve yeniden oturum açmak zorunda kalmadan, Kurumsal uygulama erişebilir.</span><span class="sxs-lookup"><span data-stu-id="84070-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="84070-107">Uygulama proxy'si destekleyen birkaç [tek oturum açma modları](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84070-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="84070-108">Parola tabanlı oturum açma kimlik doğrulaması için bir kullanıcı adı/parola bileşimi kullanan uygulamalar için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="84070-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="84070-109">Uygulamanız için parola tabanlı oturum açma yapılandırdığınızda şirket içi uygulamaya bir kez oturum açmak, kullanıcılarınızın sahip.</span><span class="sxs-lookup"><span data-stu-id="84070-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="84070-110">Bundan sonra Azure Active Directory oturum açma bilgileri depolar ve kullanıcılarınızın, uzaktan erişim otomatik olarak uygulamaya sağlar.</span><span class="sxs-lookup"><span data-stu-id="84070-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="84070-111">Zaten varsa yayımlanan ve uygulama proxy'si ile uygulamanızı test.</span><span class="sxs-lookup"><span data-stu-id="84070-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="84070-112">Aksi takdirde, adımları [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md) tekrar buraya gelin.</span><span class="sxs-lookup"><span data-stu-id="84070-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="84070-113">Uygulamanız için vaulting parola ayarlama</span><span class="sxs-lookup"><span data-stu-id="84070-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="84070-114">[Azure Portal](https://portal.azure.com)’da yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84070-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="84070-115">Seçin **Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="84070-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="84070-116">Listeden SSO'su ayarlamak istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="84070-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="84070-117">Seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="84070-117">Select **Single sign-on**.</span></span>

   ![Çoklu oturum açma seçin](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="84070-119">SSO modu için **parola tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="84070-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="84070-120">Oturum açma URL'sini, burada kullanıcılar kullanıcı adı ve şirket ağı dışından uygulamanıza oturum açmak için parola girin, sayfa için URL'yi girin.</span><span class="sxs-lookup"><span data-stu-id="84070-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="84070-121">Bu uygulama proxy'si aracılığıyla uygulama yayımlandığında oluşturduğunuz dış URL olabilir.</span><span class="sxs-lookup"><span data-stu-id="84070-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Parola tabanlı oturum açma seçin ve URL'nizi girin](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="84070-123">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="84070-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="84070-124">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="84070-124">Test your app</span></span>

<span data-ttu-id="84070-125">Uygulamanız için uzaktan erişim için yapılandırılmış dış URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="84070-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="84070-126">Bu uygulama (veya erişimle ayarladığınız test hesabının kimlik bilgilerini) için kimlik bilgilerinizle oturum.</span><span class="sxs-lookup"><span data-stu-id="84070-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="84070-127">Başarıyla oturum açtıktan sonra uygulamayı bırakın ve kimlik bilgilerinizi tekrar girmeden döndürülmesini yapabiliyor olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84070-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="84070-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84070-128">Next steps</span></span>

- <span data-ttu-id="84070-129">Diğer yollarını uygulamak için okuma [uygulama proxy'si ile çoklu oturum açma](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="84070-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="84070-130">Hakkında bilgi edinin [uygulamaları Azure AD uygulama proxy'si ile uzaktan erişim için güvenlik konuları](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="84070-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>