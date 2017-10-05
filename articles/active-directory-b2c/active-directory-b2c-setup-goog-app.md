---
title: "Azure Active Directory B2C: Google + yapılandırma | Microsoft Docs"
description: "Tüketiciye hesaplarıyla Google + uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan kaydolma ve oturum açma sağlar."
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="35f30-103">Azure Active Directory B2C: tüketicileri Google + hesapları ile kaydolma ve oturum açma sağlar</span><span class="sxs-lookup"><span data-stu-id="35f30-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="35f30-104">Bir Google + uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="35f30-104">Create a Google+ application</span></span>
<span data-ttu-id="35f30-105">Google + Azure Active Directory (Azure AD) B2C bir kimlik sağlayıcısı olarak kullanmak için bir Google + uygulaması oluşturmak ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35f30-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="35f30-106">Bunu yapmak için bir Google + hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="35f30-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="35f30-107">Bir sahip değilseniz, yerinde edinebilirsiniz [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="35f30-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="35f30-108">Git [Google geliştiriciler konsol](https://console.developers.google.com/) ve Google + hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="35f30-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="35f30-109">Tıklatın **proje oluştur**, girin bir **proje adı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="35f30-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google + - kullanmaya başlama](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + - yeni proje](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="35f30-112">Tıklatın **API Yöneticisi** ve ardından **kimlik bilgileri** sol gezinti bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="35f30-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="35f30-113">Tıklatın **OAuth izni ekran** üst sekmesini.</span><span class="sxs-lookup"><span data-stu-id="35f30-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google + - kimlik bilgileri](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="35f30-115">Seçin veya geçerli bir belirtin **e-posta adresi**, sağlayan bir **ürün adı**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="35f30-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="35f30-117">Tıklatın **yeni kimlik bilgileri** ve ardından **OAuth istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="35f30-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="35f30-119">Altında **uygulama türü**seçin **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="35f30-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="35f30-121">Sağlayan bir **adı** uygulamanız için girin `https://login.microsoftonline.com` içinde **yetkili JavaScript çıkış** alan, ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` içinde **yetkili URI'ler yeniden yönlendirme** alan.</span><span class="sxs-lookup"><span data-stu-id="35f30-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="35f30-122">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="35f30-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="35f30-123">**{Tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="35f30-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="35f30-124">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35f30-124">Click **Create**.</span></span>
   
    ![Google + - istemci kodu oluştur](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="35f30-126">Değerleri kopyalamak **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="35f30-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="35f30-127">Her ikisi de Google + kimlik sağlayıcısı kiracınızda yapılandırmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="35f30-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="35f30-128">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="35f30-128">**Client secret** is an important security credential.</span></span>
   
    ![Google + - gizli](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="35f30-130">Google + kiracınızda kimlik sağlayıcısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="35f30-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="35f30-131">Aşağıdaki adımları izleyin [B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) Azure portalındaki.</span><span class="sxs-lookup"><span data-stu-id="35f30-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="35f30-132">B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="35f30-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="35f30-133">Dikey pencerenin en üstündeki **+Add (+Ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35f30-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="35f30-134">Kolay bir sağlamak **adı** kimlik sağlayıcısı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="35f30-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="35f30-135">Örneğin, "G +" girin.</span><span class="sxs-lookup"><span data-stu-id="35f30-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="35f30-136">Tıklatın **kimlik sağlayıcısı türü**seçin **Google**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="35f30-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="35f30-137">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve istemci Kimliğini ve daha önce oluşturduğunuz Google + uygulamasının istemci parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="35f30-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="35f30-138">Tıklatın **Tamam** ve ardından **oluşturma** Google + yapılandırmanızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="35f30-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

