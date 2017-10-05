---
title: "Azure Active Directory B2C: Weibo yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Weibo hesaplarıyla tüketiciye kaydolma ve oturum açma sağlar."
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
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="3aec6-103">Azure Active Directory B2C: Kaydolma ve oturum açma Weibo hesaplarıyla tüketicileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="3aec6-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="3aec6-104">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="3aec6-104">This feature is in preview.</span></span> <span data-ttu-id="3aec6-105">Bu kimlik sağlayıcısı, üretim ortamınızda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="3aec6-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="3aec6-106">Weibo uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3aec6-106">Create a Weibo application</span></span>

<span data-ttu-id="3aec6-107">Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı Weibo kullanmak için Weibo uygulama oluşturabilir ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aec6-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="3aec6-108">Bunu yapmak için bir Weibo hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aec6-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="3aec6-109">Yoksa, her seferde alabilirsiniz [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="3aec6-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="3aec6-110">Weibo developer program kaydolun</span><span class="sxs-lookup"><span data-stu-id="3aec6-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="3aec6-111">Git [Weibo Geliştirici Portalı](http://open.weibo.com/) ve Weibo hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3aec6-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="3aec6-112">Oturum açtıktan sonra görünen adınızı sağ üst köşedeki tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3aec6-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="3aec6-113">Açılır listede seçin**编辑开发者信息**(Geliştirici bilgilerini Düzenle).</span><span class="sxs-lookup"><span data-stu-id="3aec6-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="3aec6-114">Forma gerekli bilgileri girin ve tıklayın**提交**(Gönder).</span><span class="sxs-lookup"><span data-stu-id="3aec6-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="3aec6-115">E-posta doğrulama işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="3aec6-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="3aec6-116">Git [kimlik doğrulama sayfasında](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="3aec6-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="3aec6-117">Forma gerekli bilgileri girin ve tıklayın**提交**(Gönder).</span><span class="sxs-lookup"><span data-stu-id="3aec6-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="3aec6-118">Weibo uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="3aec6-118">Register a Weibo application</span></span>

1. <span data-ttu-id="3aec6-119">Git [yeni Weibo uygulama kayıt sayfasına](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="3aec6-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="3aec6-120">Gerekli uygulama bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="3aec6-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="3aec6-121">Tıklatın**创建**(Oluştur).</span><span class="sxs-lookup"><span data-stu-id="3aec6-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="3aec6-122">Değerleri kopyalamak **uygulama anahtarı** ve **uygulama gizli anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="3aec6-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="3aec6-123">Bu daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="3aec6-123">You will need this later.</span></span>
5. <span data-ttu-id="3aec6-124">Gerekli fotoğrafı karşıya ve gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="3aec6-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="3aec6-125">Tıklatın**保存以上信息**(Kaydet).</span><span class="sxs-lookup"><span data-stu-id="3aec6-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="3aec6-126">Tıklatın**高级信息**(Gelişmiş).</span><span class="sxs-lookup"><span data-stu-id="3aec6-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="3aec6-127">Tıklatın**编辑**(OAuth2.0 için alanın yanındaki Düzenle)**授权设置**(yeniden yönlendirme URL'si).</span><span class="sxs-lookup"><span data-stu-id="3aec6-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="3aec6-128">Girin `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` OAuth2.0 için**授权设置**(yeniden yönlendirme URL'si).</span><span class="sxs-lookup"><span data-stu-id="3aec6-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="3aec6-129">Örneğin, varsa, `tenant_name` olan contoso.onmicrosoft.com, URL olması için ayarlama `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="3aec6-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="3aec6-130">Tıklatın**提交**(Gönder).</span><span class="sxs-lookup"><span data-stu-id="3aec6-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="3aec6-131">Kimlik sağlayıcısı kiracınızda Weibo yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3aec6-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="3aec6-132">Aşağıdaki adımları izleyin [B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) Azure portalındaki.</span><span class="sxs-lookup"><span data-stu-id="3aec6-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="3aec6-133">B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="3aec6-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="3aec6-134">Dikey pencerenin en üstündeki **+Add (+Ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3aec6-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="3aec6-135">Kolay bir sağlamak **adı** kimlik sağlayıcısı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="3aec6-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="3aec6-136">Örneğin, "Weibo" girin.</span><span class="sxs-lookup"><span data-stu-id="3aec6-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="3aec6-137">Tıklatın **kimlik sağlayıcısı türü**seçin **Weibo**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3aec6-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="3aec6-138">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**</span><span class="sxs-lookup"><span data-stu-id="3aec6-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="3aec6-139">Girin **uygulama anahtarı** olarak daha önce kopyaladığınız **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="3aec6-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="3aec6-140">Girin **uygulama gizli anahtarı** olarak daha önce kopyaladığınız **gizli**.</span><span class="sxs-lookup"><span data-stu-id="3aec6-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="3aec6-141">Tıklatın **Tamam** ve ardından **oluşturma** Weibo yapılandırmanızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="3aec6-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

