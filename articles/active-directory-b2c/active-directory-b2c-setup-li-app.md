---
title: "Azure Active Directory B2C: LinkedIn yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan LinkedIn hesaplarıyla kaydolma ve oturum açma tooconsumers sağlayın"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="fe4af-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers LinkedIn hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fe4af-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="fe4af-104">Bir LinkedIn uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe4af-104">Create a LinkedIn application</span></span>
<span data-ttu-id="fe4af-105">toouse LinkedIn Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate LinkedIn uygulama gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fe4af-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="fe4af-106">Bu bir LinkedIn hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="fe4af-107">Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="fe4af-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="fe4af-108">Toohello Git [LinkedIn geliştiricilerin Web sitesi](https://www.developer.linkedin.com/) ve LinkedIn hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fe4af-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="fe4af-109">Tıklatın **My uygulamaları** hello üst menü çubuğu ve ardından **uygulama oluştur**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - yeni uygulama](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="fe4af-111">Merhaba, **yeni bir uygulama oluşturmak** formunda, hello ilgili bilgileri doldurun (**şirket adı**, **adı**, **açıklama**, **Uygulama Logo URL'si**, **uygulama kullanımı**, **Web sitesi URL'si**, **iş e-posta** ve **iş telefonu**).</span><span class="sxs-lookup"><span data-stu-id="fe4af-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="fe4af-112">Toohello kabul **LinkedIn API Kullanım Koşulları'nı** tıklatıp **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - kayıt uygulama](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="fe4af-114">Merhaba değerlerini kopyalamayı **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="fe4af-115">(Bunları altında bulabilirsiniz **kimlik doğrulaması anahtarları**.) Bunların her ikisi gerekir tooconfigure LinkedIn kiracınızda kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fe4af-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fe4af-116">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fe4af-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="fe4af-117">Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yönlendirme URL'si yetkili** alan (altında **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="fe4af-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="fe4af-118">Değiştir **{tenant}** , kiracının adlı (örneğin, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="fe4af-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="fe4af-119">Tıklatın **Ekle**ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="fe4af-120">Merhaba **{tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="fe4af-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Kurulum uygulama](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="fe4af-122">Kimlik sağlayıcısı kiracınızda LinkedIn yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fe4af-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="fe4af-123">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="fe4af-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="fe4af-124">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="fe4af-125">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="fe4af-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="fe4af-126">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="fe4af-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="fe4af-127">Örneğin, "LI" girin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="fe4af-128">Tıklatın **kimlik sağlayıcısı türü**seçin **LinkedIn**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="fe4af-129">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello daha önce oluşturduğunuz LinkedIn uygulama, hello istemci kimliği ve istemci parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="fe4af-130">Tıklatın **Tamam** ve ardından **oluşturma** toosave LinkedIn yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="fe4af-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

