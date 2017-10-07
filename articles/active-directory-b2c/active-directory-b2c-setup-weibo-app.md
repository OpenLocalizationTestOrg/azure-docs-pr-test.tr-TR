---
title: "Azure Active Directory B2C: Weibo yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Weibo hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="bffd0-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Weibo hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bffd0-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="bffd0-104">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="bffd0-104">This feature is in preview.</span></span> <span data-ttu-id="bffd0-105">Bu kimlik sağlayıcısı, üretim ortamınızda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bffd0-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="bffd0-106">Weibo uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="bffd0-106">Create a Weibo application</span></span>

<span data-ttu-id="bffd0-107">toouse Weibo Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Weibo uygulama gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bffd0-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="bffd0-108">Bu Weibo hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="bffd0-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="bffd0-109">Yoksa, her seferde alabilirsiniz [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="bffd0-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="bffd0-110">Merhaba Weibo developer program kaydolun</span><span class="sxs-lookup"><span data-stu-id="bffd0-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="bffd0-111">Toohello Git [Weibo Geliştirici Portalı](http://open.weibo.com/) ve Weibo hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bffd0-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="bffd0-112">Oturum açtıktan sonra görünen adınızı hello sağ üst köşedeki tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bffd0-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="bffd0-113">Merhaba açılır menüde seçin**编辑开发者信息**(Geliştirici bilgilerini Düzenle).</span><span class="sxs-lookup"><span data-stu-id="bffd0-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="bffd0-114">Merhaba forma hello gerekli bilgileri girin ve tıklatın**提交**(Gönder).</span><span class="sxs-lookup"><span data-stu-id="bffd0-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="bffd0-115">Merhaba e-posta doğrulama işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="bffd0-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="bffd0-116">Toohello Git [kimlik doğrulama sayfasında](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="bffd0-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="bffd0-117">Merhaba forma hello gerekli bilgileri girin ve tıklatın**提交**(Gönder).</span><span class="sxs-lookup"><span data-stu-id="bffd0-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="bffd0-118">Weibo uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="bffd0-118">Register a Weibo application</span></span>

1. <span data-ttu-id="bffd0-119">Toohello Git [yeni Weibo uygulama kayıt sayfasına](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="bffd0-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="bffd0-120">Merhaba gerekli uygulama bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="bffd0-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="bffd0-121">Tıklatın**创建**(Oluştur).</span><span class="sxs-lookup"><span data-stu-id="bffd0-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="bffd0-122">Merhaba değerlerini kopyalamayı **uygulama anahtarı** ve **uygulama gizli anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="bffd0-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="bffd0-123">Bu daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="bffd0-123">You will need this later.</span></span>
5. <span data-ttu-id="bffd0-124">Gerekli hello fotoğrafı karşıya ve hello gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="bffd0-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="bffd0-125">Tıklatın**保存以上信息**(Kaydet).</span><span class="sxs-lookup"><span data-stu-id="bffd0-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="bffd0-126">Tıklatın**高级信息**(Gelişmiş).</span><span class="sxs-lookup"><span data-stu-id="bffd0-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="bffd0-127">Tıklatın**编辑**(düzenleme) sonraki toohello alanı OAuth2.0 için**授权设置**(yeniden yönlendirme URL'si).</span><span class="sxs-lookup"><span data-stu-id="bffd0-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="bffd0-128">Girin `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` OAuth2.0 için**授权设置**(yeniden yönlendirme URL'si).</span><span class="sxs-lookup"><span data-stu-id="bffd0-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="bffd0-129">Örneğin, varsa, `tenant_name` contoso.onmicrosoft.com, kümesi hello URL toobe olan `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="bffd0-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="bffd0-130">Tıklatın**提交**(Gönder).</span><span class="sxs-lookup"><span data-stu-id="bffd0-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="bffd0-131">Kimlik sağlayıcısı kiracınızda Weibo yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bffd0-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="bffd0-132">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="bffd0-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="bffd0-133">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="bffd0-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="bffd0-134">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="bffd0-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="bffd0-135">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="bffd0-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="bffd0-136">Örneğin, "Weibo" girin.</span><span class="sxs-lookup"><span data-stu-id="bffd0-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="bffd0-137">Tıklatın **kimlik sağlayıcısı türü**seçin **Weibo**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bffd0-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="bffd0-138">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**</span><span class="sxs-lookup"><span data-stu-id="bffd0-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="bffd0-139">Merhaba girin **uygulama anahtarı** hello daha önce kopyaladığınız **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="bffd0-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="bffd0-140">Merhaba girin **uygulama gizli anahtarı** hello daha önce kopyaladığınız **gizli**.</span><span class="sxs-lookup"><span data-stu-id="bffd0-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="bffd0-141">Tıklatın **Tamam** ve ardından **oluşturma** toosave Weibo yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="bffd0-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

