---
title: "Azure Active Directory B2C: Amazon yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Amazon hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
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
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="8241e-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Amazon hesabıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8241e-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="8241e-104">Amazon uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="8241e-104">Create an Amazon application</span></span>
<span data-ttu-id="8241e-105">toouse Amazon Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Amazon uygulamanın gereksinim ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8241e-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="8241e-106">Bu bir Amazon hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="8241e-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="8241e-107">Bir sahip değilseniz, yerinde edinebilirsiniz [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="8241e-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="8241e-108">Toohello Git [Amazon Geliştirici Merkezi](https://login.amazon.com/) ve Amazon hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8241e-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="8241e-109">Zaten yapmadıysanız, tıklatın **kaydolun**hello Geliştirici kayıt adımları izleyin ve hello İlkesi kabul edin.</span><span class="sxs-lookup"><span data-stu-id="8241e-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="8241e-110">Tıklatın **kaydetmek yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="8241e-110">Click **Register new application**.</span></span>
   
    ![Yeni bir uygulama hello Amazon Web sitesindeki kaydetme](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="8241e-112">Uygulama bilgilerini sağlayın (**adı**, **açıklama**, ve **gizlilik bildirimi URL'si**) tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8241e-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Amazon en yeni bir uygulama kaydetmeye yönelik uygulama bilgileri sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="8241e-114">Merhaba, **Web ayarları** bölümünde, kopyalama hello değerlerini **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="8241e-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="8241e-115">(Tooclick hello ihtiyacınız **Göster gizli** toosee bu düğmesine tıklayın.) Her ikisine de ihtiyacınız tooconfigure Amazon kiracınızda kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8241e-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="8241e-116">Tıklatın **Düzenle** hello bölümünün hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="8241e-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="8241e-117">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8241e-117">**Client Secret** is an important security credential.</span></span>
   
    ![Yeni uygulamanızı Amazon için istemci kimliği ve istemci parolası sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="8241e-119">Girin `https://login.microsoftonline.com` hello içinde **izin JavaScript çıkış** alan ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **dönüş URL'leri izin** alan.</span><span class="sxs-lookup"><span data-stu-id="8241e-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="8241e-120">Değiştir **{tenant}** , kiracının adlı (örneğin, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="8241e-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="8241e-121">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8241e-121">Click **Save**.</span></span> <span data-ttu-id="8241e-122">Merhaba **{tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="8241e-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Yeni uygulamanızı Amazon için JavaScript kaynakları ve dönüş URL'leri sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="8241e-124">Kimlik sağlayıcısı kiracınızda Amazon yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8241e-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="8241e-125">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8241e-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="8241e-126">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="8241e-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="8241e-127">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="8241e-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="8241e-128">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="8241e-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="8241e-129">Örneğin, "Amzn" girin.</span><span class="sxs-lookup"><span data-stu-id="8241e-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="8241e-130">Tıklatın **kimlik sağlayıcısı türü**seçin **Amazon**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8241e-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="8241e-131">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello daha önce oluşturduğunuz Amazon uygulama, hello istemci kimliği ve istemci parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="8241e-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="8241e-132">Tıklatın **Tamam** ve ardından **oluşturma** toosave Amazon yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="8241e-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

