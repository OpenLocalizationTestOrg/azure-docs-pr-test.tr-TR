---
title: "Azure Active Directory B2C: Microsoft hesabı yapılandırması | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvence altına alınan Microsoft hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="69e45-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Microsoft hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="69e45-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="69e45-104">Bir Microsoft hesabı uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="69e45-104">Create a Microsoft account application</span></span>
<span data-ttu-id="69e45-105">toouse Microsoft hesabı kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde hello doğru parametrelerle tedarik ve toocreate bir Microsoft hesabı uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="69e45-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="69e45-106">Bu Microsoft hesabı toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="69e45-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="69e45-107">Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="69e45-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="69e45-108">Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ve Microsoft hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="69e45-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="69e45-109">Tıklatın **bir uygulama ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="69e45-109">Click **Add an app**.</span></span>
   
    ![Microsoft hesabı - yeni bir uygulama ekleme](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="69e45-111">Sağlayan bir **adı** tıklatın ve uygulama için **uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="69e45-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Microsoft hesabı - uygulama adı](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="69e45-113">Merhaba değerini kopyalayın **uygulama kimliği**. Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="69e45-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Microsoft hesabı - uygulama kimliği](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="69e45-115">Tıklayın **Ekle platform** ve **Web**.</span><span class="sxs-lookup"><span data-stu-id="69e45-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft hesabı - platform ekleme](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft hesabı - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="69e45-118">Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yeniden yönlendirme URI'ler** alan.</span><span class="sxs-lookup"><span data-stu-id="69e45-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="69e45-119">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="69e45-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Microsoft hesabı - yeniden yönlendirme URL'si](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="69e45-121">Tıklayın **yeni bir parola oluşturmak** hello altında **uygulama parolaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="69e45-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="69e45-122">Ekranda görüntülenen hello yeni parolayı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="69e45-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="69e45-123">Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="69e45-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="69e45-124">Bu parolayı bir önemli güvenlik kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="69e45-124">This password is an important security credential.</span></span>
   
    ![Microsoft hesabı - yeni bir parola oluştur](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft hesabı - yeni parola](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="69e45-127">Bildiren hello kutuyu **Live SDK'sı desteği** hello altında **Gelişmiş Seçenekler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="69e45-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="69e45-128">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="69e45-128">Click **Save**.</span></span>
   
    ![Microsoft hesabı - Live SDK'sı desteği](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="69e45-130">Microsoft hesabı kimlik sağlayıcısı kiracınızda yapılandırın</span><span class="sxs-lookup"><span data-stu-id="69e45-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="69e45-131">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="69e45-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="69e45-132">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="69e45-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="69e45-133">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="69e45-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="69e45-134">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="69e45-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="69e45-135">Örneğin, "MSA" girin.</span><span class="sxs-lookup"><span data-stu-id="69e45-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="69e45-136">Tıklatın **kimlik sağlayıcısı türü**seçin **Microsoft hesabı**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="69e45-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="69e45-137">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** hello uygulama kimliği ve hello daha önce oluşturduğunuz Microsoft hesabı uygulama parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="69e45-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="69e45-138">Tıklatın **Tamam** ve ardından **oluşturma** toosave Microsoft hesabı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="69e45-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

