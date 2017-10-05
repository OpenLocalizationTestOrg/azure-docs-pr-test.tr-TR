---
title: "Azure Active Directory B2C: LinkedIn yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan LinkedIn hesaplarıyla tüketicileri için kaydolma ve oturum açma sağlayın"
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
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="af6f3-103">Azure Active Directory B2C: Kaydolma ve oturum açma LinkedIn hesaplarıyla tüketicileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="af6f3-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="af6f3-104">Bir LinkedIn uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="af6f3-104">Create a LinkedIn application</span></span>
<span data-ttu-id="af6f3-105">LinkedIn Azure Active Directory (Azure AD) B2C bir kimlik sağlayıcısı olarak kullanmak için bir LinkedIn uygulaması oluşturmak ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="af6f3-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="af6f3-106">Bunu yapmak için bir LinkedIn hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="af6f3-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="af6f3-107">Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="af6f3-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="af6f3-108">Git [LinkedIn geliştiricilerin Web sitesi](https://www.developer.linkedin.com/) ve LinkedIn hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="af6f3-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="af6f3-109">Tıklatın **My uygulamaları** üst menü çubuğu ve ardından **uygulama oluştur**.</span><span class="sxs-lookup"><span data-stu-id="af6f3-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn - yeni uygulama](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="af6f3-111">İçinde **yeni bir uygulama oluşturmak** formunda, ilgili bilgileri doldurun (**şirket adı**, **adı**, **açıklama**, **Uygulama Logo URL'si**, **uygulama kullanımı**, **Web sitesi URL'si**, **iş e-posta** ve **iş telefonu**).</span><span class="sxs-lookup"><span data-stu-id="af6f3-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="af6f3-112">Kabul **LinkedIn API Kullanım Koşulları'nı** tıklatıp **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="af6f3-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - kayıt uygulama](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="af6f3-114">Değerleri kopyalamak **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="af6f3-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="af6f3-115">(Bunları altında bulabilirsiniz **kimlik doğrulaması anahtarları**.) Her ikisi de kiracınızda kimlik sağlayıcısı LinkedIn yapılandırmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="af6f3-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="af6f3-116">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="af6f3-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="af6f3-117">Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` içinde **yönlendirme URL'si yetkili** alan (altında **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="af6f3-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="af6f3-118">Değiştir **{tenant}** , kiracının adlı (örneğin, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="af6f3-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="af6f3-119">Tıklatın **Ekle**ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="af6f3-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="af6f3-120">**{Tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="af6f3-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn - Kurulum uygulama](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="af6f3-122">Kimlik sağlayıcısı kiracınızda LinkedIn yapılandırın</span><span class="sxs-lookup"><span data-stu-id="af6f3-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="af6f3-123">Aşağıdaki adımları izleyin [B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) Azure portalındaki.</span><span class="sxs-lookup"><span data-stu-id="af6f3-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="af6f3-124">B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="af6f3-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="af6f3-125">Dikey pencerenin en üstündeki **+Add (+Ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af6f3-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="af6f3-126">Kolay bir sağlamak **adı** kimlik sağlayıcısı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="af6f3-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="af6f3-127">Örneğin, "LI" girin.</span><span class="sxs-lookup"><span data-stu-id="af6f3-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="af6f3-128">Tıklatın **kimlik sağlayıcısı türü**seçin **LinkedIn**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="af6f3-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="af6f3-129">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve istemci Kimliğini ve daha önce oluşturduğunuz LinkedIn uygulamanın istemci parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="af6f3-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="af6f3-130">Tıklatın **Tamam** ve ardından **oluşturma** LinkedIn yapılandırmanızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="af6f3-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

