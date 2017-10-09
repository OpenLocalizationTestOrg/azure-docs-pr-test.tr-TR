---
title: "Azure Active Directory B2C: Facebook yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Facebook hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="ec867-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Facebook hesabıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ec867-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="ec867-104">Bir Facebook uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec867-104">Create a Facebook application</span></span>
<span data-ttu-id="ec867-105">toouse Facebook kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde toocreate bir Facebook uygulaması gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ec867-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="ec867-106">Bu bir Facebook hesap toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec867-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="ec867-107">Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="ec867-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="ec867-108">Toohello Git [geliştiriciler için Facebook](https://developers.facebook.com/) hesap kimlik bilgileri Web sitesi ve, Facebook ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ec867-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="ec867-109">Zaten yapmadıysanız, Facebook geliştirici olarak tooregister gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec867-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="ec867-110">toodo bunu, **kaydetmek** (Merhaba sağ üst köşesinde hello sayfasının), Facebook'ın ilkeleri kabul etmek ve hello kayıt adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="ec867-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="ec867-111">Tıklatın **My uygulamaları** ve ardından **yeni bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="ec867-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="ec867-112">Hello formunda sağlayan bir **görünen adı** ve geçerli bir **ilgili kişi e-posta**.</span><span class="sxs-lookup"><span data-stu-id="ec867-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="ec867-113">Tıklatın **uygulama kimliği oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ec867-113">Click **Create App ID**.</span></span> <span data-ttu-id="ec867-114">Bu tooaccept Facebook platform ilkeleri gerektirir ve bir çevrimiçi güvenlik denetimi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="ec867-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="ec867-115">Merhaba sol sütunda tıklatın **ayarları** ve ardından **temel** zaten seçilmemişse.</span><span class="sxs-lookup"><span data-stu-id="ec867-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="ec867-116">Seçin bir **kategori**.</span><span class="sxs-lookup"><span data-stu-id="ec867-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="ec867-117">Tıklatın **+ Platform eklemek** seçip **Web sitesi**.</span><span class="sxs-lookup"><span data-stu-id="ec867-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - ayarlar](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - ayarları - Web sitesi](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="ec867-120">Girin `https://login.microsoftonline.com/` hello içinde **Site URL'si** alan ve ardından **Değişiklikleri Kaydet** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ec867-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook - Site URL'si](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="ec867-122">Merhaba değerini kopyalayın **uygulama kimliği**.</span><span class="sxs-lookup"><span data-stu-id="ec867-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="ec867-123">Tıklatın **Göster** ve kopyalama hello değerini **uygulama gizli anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="ec867-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="ec867-124">Bunların her ikisi gerekir tooconfigure Facebook kiracınızda kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ec867-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="ec867-125">**Uygulama gizli anahtarı** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ec867-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - uygulama kimliği & uygulama gizli anahtarı](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="ec867-127">Tıklatın **+ ürün ekleme** hello sol gezinti ve ardından hello **Ayarla** için düğmesini **Facebook oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ec867-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - Facebook oturum açma](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="ec867-129">Tıklatın **ayarları** hello sağ nav altında üzerinde **Facebook oturum açma**</span><span class="sxs-lookup"><span data-stu-id="ec867-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook - Facebook oturum açma ayarları](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="ec867-131">Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **geçerli OAuth yeniden yönlendirme URI'ler** hello alanındaki **istemci OAuth ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ec867-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="ec867-132">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ec867-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="ec867-133">Tıklatın **Değişiklikleri Kaydet** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ec867-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook - OAuth yeniden yönlendirme URI'si](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="ec867-135">toomake Facebook uygulamanız toomake ihtiyacınız Azure AD B2C tarafından kullanılabilir, genel olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ec867-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="ec867-136">Tıklayarak bunu yapabilirsiniz **uygulama İnceleme** sol gezinti hello ve kapatma hello geçiş hello hello sayfanın başında çok**Evet** tıklatıp **Onayla**.</span><span class="sxs-lookup"><span data-stu-id="ec867-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - uygulama genel](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="ec867-138">Facebook kimlik sağlayıcısı kiracınızda yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ec867-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="ec867-139">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ec867-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="ec867-140">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="ec867-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="ec867-141">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="ec867-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ec867-142">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="ec867-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="ec867-143">Örneğin, "Facebook" girin.</span><span class="sxs-lookup"><span data-stu-id="ec867-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="ec867-144">Tıklatın **kimlik sağlayıcısı türü**seçin **Facebook**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ec867-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="ec867-145">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello uygulama kimliği ve uygulama gizli anahtarı (Merhaba daha önce oluşturduğunuz Facebook uygulaması) girin hello içinde **istemci kimliği** ve **gizli**sırasıyla alanları.</span><span class="sxs-lookup"><span data-stu-id="ec867-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="ec867-146">Tıklatın **Tamam**ve ardından **oluşturma** toosave Facebook yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="ec867-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="ec867-147">Ekleme bir **kimlik sağlayıcısı** tooyour Kiracı varolan ilkelerinizi değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="ec867-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="ec867-148">Tooupdate, az önce oluşturduğunuz hello kimlik sağlayıcısı dahil ederek ilkelerinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ec867-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>