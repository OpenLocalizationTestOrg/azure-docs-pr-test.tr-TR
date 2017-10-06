---
title: "Azure Active Directory B2C: WeChat yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan WeChat hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="69640-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers WeChat hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="69640-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="69640-104">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="69640-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="69640-105">WeChat uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="69640-105">Create a WeChat application</span></span>

<span data-ttu-id="69640-106">toouse WeChat Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate WeChat uygulama gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="69640-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="69640-107">Bu WeChat hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="69640-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="69640-108">Yoksa, bir mobil uygulamalarını biri aracılığıyla kaydolan veya h numaranızı kullanarak elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69640-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="69640-109">Bundan sonra hesabınızı hello WeChat Geliştirici programla kayıtlı alın.</span><span class="sxs-lookup"><span data-stu-id="69640-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="69640-110">Daha fazla bilgi bulabilirsiniz [burada](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="69640-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="69640-111">WeChat uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="69640-111">Register a WeChat application</span></span>

1. <span data-ttu-id="69640-112">Çok Git[https://open.weixin.qq.com/](https://open.weixin.qq.com/) ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="69640-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="69640-113">Tıklayın**管理中心**(Yönetim Merkezi).</span><span class="sxs-lookup"><span data-stu-id="69640-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="69640-114">Merhaba gerekli adımları tooregister yeni bir uygulama izleyin.</span><span class="sxs-lookup"><span data-stu-id="69640-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="69640-115">İçin**授权回调域**(geri çağırma URL'si) girin `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="69640-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="69640-116">Örneğin, varsa, `tenant_name` contoso.onmicrosoft.com, kümesi hello URL toobe olan `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="69640-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="69640-117">Bul ve kopyalama hello **uygulama kimliği** ve **uygulama anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="69640-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="69640-118">Bu bilgiler daha sonra ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="69640-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="69640-119">Kimlik sağlayıcısı kiracınızda WeChat yapılandırın</span><span class="sxs-lookup"><span data-stu-id="69640-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="69640-120">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="69640-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="69640-121">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="69640-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="69640-122">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="69640-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="69640-123">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="69640-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="69640-124">Örneğin, "WeChat" girin.</span><span class="sxs-lookup"><span data-stu-id="69640-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="69640-125">Tıklatın **kimlik sağlayıcısı türü**seçin **WeChat**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="69640-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="69640-126">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**</span><span class="sxs-lookup"><span data-stu-id="69640-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="69640-127">Merhaba girin **uygulama anahtarı** hello daha önce kopyaladığınız **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="69640-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="69640-128">Merhaba girin **uygulama gizli anahtarı** hello daha önce kopyaladığınız **gizli**.</span><span class="sxs-lookup"><span data-stu-id="69640-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="69640-129">Tıklatın **Tamam** ve ardından **oluşturma** toosave WeChat yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="69640-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

