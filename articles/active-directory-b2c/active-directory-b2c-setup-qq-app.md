---
title: "Azure Active Directory B2C: H yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan h hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="d4879-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers h hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d4879-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="d4879-104">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="d4879-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="d4879-105">H uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4879-105">Create a QQ application</span></span>

<span data-ttu-id="d4879-106">toouse h Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate h uygulama gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d4879-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="d4879-107">Bu h hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4879-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="d4879-108">Yoksa, her seferde alabilirsiniz [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="d4879-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="d4879-109">Merhaba h developer program kaydolun</span><span class="sxs-lookup"><span data-stu-id="d4879-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="d4879-110">Toohello Git [h Geliştirici Portalı](http://open.qq.com) ve h hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d4879-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="d4879-111">Oturum açtıktan sonra çok Git[http://open.qq.com/reg](http://open.qq.com/reg) tooregister kendiniz bir geliştirici olarak.</span><span class="sxs-lookup"><span data-stu-id="d4879-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="d4879-112">Merhaba menüde seçin**个人**(bireysel Geliştirici).</span><span class="sxs-lookup"><span data-stu-id="d4879-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="d4879-113">Merhaba forma hello gerekli bilgileri girin ve tıklatın**下一步**(sonraki adım).</span><span class="sxs-lookup"><span data-stu-id="d4879-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="d4879-114">Merhaba e-posta doğrulama işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="d4879-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="d4879-115">Geliştirici olarak kaydolduktan sonra onaylanmış birkaç gün toobe toowait gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4879-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="d4879-116">H uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="d4879-116">Register a QQ application</span></span>

1. <span data-ttu-id="d4879-117">Çok Git[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="d4879-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="d4879-118">Tıklayın**应用管理**(Uygulama Yönetimi).</span><span class="sxs-lookup"><span data-stu-id="d4879-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="d4879-119">Tıklayın**创建应用**(Uygulama Oluştur).</span><span class="sxs-lookup"><span data-stu-id="d4879-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="d4879-120">Merhaba gerekli uygulama bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="d4879-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="d4879-121">Tıklayın**创建应用**(Uygulama Oluştur).</span><span class="sxs-lookup"><span data-stu-id="d4879-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="d4879-122">Merhaba gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="d4879-122">Enter hello required information.</span></span>
7. <span data-ttu-id="d4879-123">Hello için**授权回调域**(geri çağırma URL'si) alanına, `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="d4879-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="d4879-124">Örneğin, varsa, `tenant_name` contoso.onmicrosoft.com, kümesi hello URL toobe olan `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="d4879-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="d4879-125">Tıklayın**创建应用**(Uygulama Oluştur).</span><span class="sxs-lookup"><span data-stu-id="d4879-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="d4879-126">Merhaba onay sayfasında tıklayın**应用管理**(Uygulama Yönetimi) tooreturn toohello Uygulama Yönetimi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="d4879-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="d4879-127">Tıklayın**查看**(Görünüm), yeni oluşturduğunuz sonraki toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="d4879-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="d4879-128">Tıklayın**修改**(Düzenle).</span><span class="sxs-lookup"><span data-stu-id="d4879-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="d4879-129">Merhaba sayfa Hello üstten hello kopyalama **uygulama kimliği** ve **uygulama anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="d4879-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d4879-130">Kimlik sağlayıcısı kiracınızda h yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d4879-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d4879-131">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="d4879-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d4879-132">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="d4879-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d4879-133">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="d4879-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d4879-134">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="d4879-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d4879-135">Örneğin, "H" girin.</span><span class="sxs-lookup"><span data-stu-id="d4879-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="d4879-136">Tıklatın **kimlik sağlayıcısı türü**seçin **h**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d4879-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="d4879-137">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**</span><span class="sxs-lookup"><span data-stu-id="d4879-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="d4879-138">Merhaba girin **uygulama anahtarı** hello daha önce kopyaladığınız **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="d4879-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="d4879-139">Merhaba girin **uygulama gizli anahtarı** hello daha önce kopyaladığınız **gizli**.</span><span class="sxs-lookup"><span data-stu-id="d4879-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="d4879-140">Tıklatın **Tamam** ve ardından **oluşturma** toosave h yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="d4879-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

