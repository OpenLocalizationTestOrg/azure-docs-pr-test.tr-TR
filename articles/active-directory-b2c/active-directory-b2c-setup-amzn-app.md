---
title: "Azure Active Directory B2C: Amazon yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Amazon hesaplarıyla tüketiciye kaydolma ve oturum açma sağlar."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="d4dab-103">Azure Active Directory B2C: Kaydolma ve oturum açma Amazon hesaplarıyla tüketicileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="d4dab-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="d4dab-104">Amazon uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4dab-104">Create an Amazon application</span></span>
<span data-ttu-id="d4dab-105">Amazon Azure Active Directory (Azure AD) B2C bir kimlik sağlayıcısı olarak kullanmak için Amazon uygulama oluşturma ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4dab-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="d4dab-106">Bunu yapmak için bir Amazon hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4dab-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="d4dab-107">Bir sahip değilseniz, yerinde edinebilirsiniz [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="d4dab-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="d4dab-108">Git [Amazon Geliştirici Merkezi](https://login.amazon.com/) ve Amazon hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d4dab-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="d4dab-109">Zaten yapmadıysanız, tıklatın **kaydolun**, geliştirici kayıt adımları izleyin ve ilke kabul edin.</span><span class="sxs-lookup"><span data-stu-id="d4dab-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="d4dab-110">Tıklatın **kaydetmek yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-110">Click **Register new application**.</span></span>
   
    ![Amazon Web sitesinde yeni bir uygulama kaydetme](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="d4dab-112">Uygulama bilgilerini sağlayın (**adı**, **açıklama**, ve **gizlilik bildirimi URL'si**) tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Amazon en yeni bir uygulama kaydetmeye yönelik uygulama bilgileri sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="d4dab-114">İçinde **Web ayarları** bölümünde, değerlerini kopyalamayı **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="d4dab-115">(Tıklamanız gerekir **Göster gizli** bu düğmeyi.) Her ikisi de kiracınızda kimlik sağlayıcısı Amazon yapılandırmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4dab-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="d4dab-116">Tıklatın **Düzenle** bölümünün altındaki.</span><span class="sxs-lookup"><span data-stu-id="d4dab-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="d4dab-117">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d4dab-117">**Client Secret** is an important security credential.</span></span>
   
    ![Yeni uygulamanızı Amazon için istemci kimliği ve istemci parolası sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="d4dab-119">Girin `https://login.microsoftonline.com` içinde **izin JavaScript çıkış** alan ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` içinde **dönüş URL'leri izin** alan.</span><span class="sxs-lookup"><span data-stu-id="d4dab-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="d4dab-120">Değiştir **{tenant}** , kiracının adlı (örneğin, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d4dab-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="d4dab-121">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4dab-121">Click **Save**.</span></span> <span data-ttu-id="d4dab-122">**{Tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="d4dab-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Yeni uygulamanızı Amazon için JavaScript kaynakları ve dönüş URL'leri sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d4dab-124">Kimlik sağlayıcısı kiracınızda Amazon yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d4dab-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d4dab-125">Aşağıdaki adımları izleyin [B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) Azure portalındaki.</span><span class="sxs-lookup"><span data-stu-id="d4dab-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="d4dab-126">B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d4dab-127">Dikey pencerenin en üstündeki **+Add (+Ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4dab-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="d4dab-128">Kolay bir sağlamak **adı** kimlik sağlayıcısı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="d4dab-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="d4dab-129">Örneğin, "Amzn" girin.</span><span class="sxs-lookup"><span data-stu-id="d4dab-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="d4dab-130">Tıklatın **kimlik sağlayıcısı türü**seçin **Amazon**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d4dab-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="d4dab-131">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** istemci kimliği ve istemci parolası Amazon uygulamasının daha önce oluşturduğunuz girin.</span><span class="sxs-lookup"><span data-stu-id="d4dab-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="d4dab-132">Tıklatın **Tamam** ve ardından **oluşturma** Amazon yapılandırmanızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="d4dab-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

