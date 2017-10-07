---
title: "Azure Active Directory B2C: Google + yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvence altına alınan Google + hesapları ile kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="ff1bb-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Google + hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="ff1bb-104">Bir Google + uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff1bb-104">Create a Google+ application</span></span>
<span data-ttu-id="ff1bb-105">toouse Google + Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Google + uygulama gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="ff1bb-106">Bu bir Google + hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="ff1bb-107">Bir sahip değilseniz, yerinde edinebilirsiniz [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="ff1bb-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="ff1bb-108">Toohello Git [Google geliştiriciler konsol](https://console.developers.google.com/) ve Google + hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="ff1bb-109">Tıklatın **proje oluştur**, girin bir **proje adı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google + - kullanmaya başlama](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + - yeni proje](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="ff1bb-112">Tıklatın **API Yöneticisi** ve ardından **kimlik bilgileri** sol gezinti hello içinde.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="ff1bb-113">Merhaba tıklatın **OAuth izni ekran** sekmesini hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google + - kimlik bilgileri](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="ff1bb-115">Seçin veya geçerli bir belirtin **e-posta adresi**, sağlayan bir **ürün adı**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="ff1bb-117">Tıklatın **yeni kimlik bilgileri** ve ardından **OAuth istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="ff1bb-119">Altında **uygulama türü**seçin **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="ff1bb-121">Sağlamak bir **adı** , uygulamanız için girin `https://login.microsoftonline.com` hello içinde **yetkili JavaScript çıkış** alan, ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yetkili URI'leryenidenyönlendirme**alan.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="ff1bb-122">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ff1bb-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="ff1bb-123">Merhaba **{tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="ff1bb-124">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-124">Click **Create**.</span></span>
   
    ![Google + - istemci kodu oluştur](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="ff1bb-126">Merhaba değerlerini kopyalamayı **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="ff1bb-127">Bunların her ikisi gerekir tooconfigure Google + kiracınızda kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="ff1bb-128">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-128">**Client secret** is an important security credential.</span></span>
   
    ![Google + - gizli](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ff1bb-130">Google + kiracınızda kimlik sağlayıcısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff1bb-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ff1bb-131">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ff1bb-132">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ff1bb-133">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ff1bb-134">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ff1bb-135">Örneğin, "G +" girin.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="ff1bb-136">Tıklatın **kimlik sağlayıcısı türü**seçin **Google**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="ff1bb-137">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello daha önce oluşturduğunuz Google + uygulama, hello istemci kimliği ve istemci parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="ff1bb-138">Tıklatın **Tamam** ve ardından **oluşturma** toosave Google + yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

