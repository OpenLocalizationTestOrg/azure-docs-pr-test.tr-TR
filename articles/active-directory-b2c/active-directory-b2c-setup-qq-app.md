---
title: "Azure Active Directory B2C: H yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan h hesaplarıyla tüketiciye kaydolma ve oturum açma sağlar."
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
ms.openlocfilehash: b32e81494b8c84799485f154ae43ad30af394caa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-qq-accounts"></a><span data-ttu-id="1474f-103">Azure Active Directory B2C: Kaydolma ve oturum açma h hesaplarıyla tüketicileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="1474f-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="1474f-104">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="1474f-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="1474f-105">H uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1474f-105">Create a QQ application</span></span>

<span data-ttu-id="1474f-106">H Azure Active Directory (Azure AD) B2C bir kimlik sağlayıcısı olarak kullanmak için h uygulaması oluşturmak ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1474f-106">To use QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a QQ application and supply it with the right parameters.</span></span> <span data-ttu-id="1474f-107">Bunu yapmak için bir h hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1474f-107">You need a QQ account to do this.</span></span> <span data-ttu-id="1474f-108">Yoksa, her seferde alabilirsiniz [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="1474f-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-the-qq-developer-program"></a><span data-ttu-id="1474f-109">H developer program kaydolun</span><span class="sxs-lookup"><span data-stu-id="1474f-109">Register for the QQ developer program</span></span>

1. <span data-ttu-id="1474f-110">Git [h Geliştirici Portalı](http://open.qq.com) ve h hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1474f-110">Go to the [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="1474f-111">Oturum açtıktan sonra Git [http://open.qq.com/reg](http://open.qq.com/reg) kendiniz geliştirici olarak kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="1474f-111">After signing in, go to [http://open.qq.com/reg](http://open.qq.com/reg) to register yourself as a developer.</span></span>
3. <span data-ttu-id="1474f-112">Menüde seçin**个人**(bireysel Geliştirici).</span><span class="sxs-lookup"><span data-stu-id="1474f-112">In the menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="1474f-113">Forma gerekli bilgileri girin ve tıklayın**下一步**(sonraki adım).</span><span class="sxs-lookup"><span data-stu-id="1474f-113">Enter the required information into the form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="1474f-114">E-posta doğrulama işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1474f-114">Complete the email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="1474f-115">Geliştirici olarak kaydolduktan sonra onaylanması birkaç gün beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1474f-115">You will need to wait a few days to be approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="1474f-116">H uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="1474f-116">Register a QQ application</span></span>

1. <span data-ttu-id="1474f-117">Git [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="1474f-117">Go to [https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="1474f-118">Tıklayın**应用管理**(Uygulama Yönetimi).</span><span class="sxs-lookup"><span data-stu-id="1474f-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="1474f-119">Tıklayın**创建应用**(Uygulama Oluştur).</span><span class="sxs-lookup"><span data-stu-id="1474f-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="1474f-120">Gerekli uygulama bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="1474f-120">Enter the necessary app information.</span></span>
5. <span data-ttu-id="1474f-121">Tıklayın**创建应用**(Uygulama Oluştur).</span><span class="sxs-lookup"><span data-stu-id="1474f-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="1474f-122">Gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="1474f-122">Enter the required information.</span></span>
7. <span data-ttu-id="1474f-123">İçin**授权回调域**(geri çağırma URL'si) alanına, `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="1474f-123">For the **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="1474f-124">Örneğin, varsa, `tenant_name` olan contoso.onmicrosoft.com, URL olması için ayarlama `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="1474f-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="1474f-125">Tıklayın**创建应用**(Uygulama Oluştur).</span><span class="sxs-lookup"><span data-stu-id="1474f-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="1474f-126">Onay sayfasında tıklayın**应用管理**(uygulama yönetimi sayfasına dönmek için uygulama yönetimi).</span><span class="sxs-lookup"><span data-stu-id="1474f-126">On the confirmation page, click on **应用管理** (app management) to return to the app management page.</span></span>
10. <span data-ttu-id="1474f-127">Tıklayın**查看**(görüntüleme) az önce oluşturduğunuz uygulama yanındaki.</span><span class="sxs-lookup"><span data-stu-id="1474f-127">Click on **查看** (view) next to the app you just created.</span></span>
11. <span data-ttu-id="1474f-128">Tıklayın**修改**(Düzenle).</span><span class="sxs-lookup"><span data-stu-id="1474f-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="1474f-129">Sayfanın üst kısmından kopyalama **uygulama kimliği** ve **uygulama anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="1474f-129">From the top of the page, copy the **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="1474f-130">Kimlik sağlayıcısı kiracınızda h yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1474f-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="1474f-131">Aşağıdaki adımları izleyin [B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) Azure portalındaki.</span><span class="sxs-lookup"><span data-stu-id="1474f-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="1474f-132">B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="1474f-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="1474f-133">Dikey pencerenin en üstündeki **+Add (+Ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1474f-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="1474f-134">Kolay bir sağlamak **adı** kimlik sağlayıcısı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="1474f-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="1474f-135">Örneğin, "H" girin.</span><span class="sxs-lookup"><span data-stu-id="1474f-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="1474f-136">Tıklatın **kimlik sağlayıcısı türü**seçin **h**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1474f-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="1474f-137">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**</span><span class="sxs-lookup"><span data-stu-id="1474f-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="1474f-138">Girin **uygulama anahtarı** olarak daha önce kopyaladığınız **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="1474f-138">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="1474f-139">Girin **uygulama gizli anahtarı** olarak daha önce kopyaladığınız **gizli**.</span><span class="sxs-lookup"><span data-stu-id="1474f-139">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="1474f-140">Tıklatın **Tamam** ve ardından **oluşturma** h yapılandırmanızı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="1474f-140">Click **OK** and then click **Create** to save your QQ configuration.</span></span>

