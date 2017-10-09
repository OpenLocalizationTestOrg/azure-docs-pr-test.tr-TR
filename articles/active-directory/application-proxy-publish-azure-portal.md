---
title: Azure AD uygulama proxy'si aaaPublish uygulamalarla | Microsoft Docs
description: "Azure AD uygulama proxy'si ile şirket içi uygulamalar toohello bulut hello Azure portalında yayımlarsınız."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="4791c-103">Azure AD Uygulama Ara Sunucusu ile uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="4791c-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4791c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4791c-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="4791c-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="4791c-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="4791c-106">Azure Active Directory (AD) uygulama proxy'si hello erişilen şirket içi uygulamalar toobe yayımlayarak uzaktan çalışanlar destek yardımcı olan Internet.</span><span class="sxs-lookup"><span data-stu-id="4791c-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="4791c-107">Ağınızın dışından hello Azure portal tooprovide güvenli uzaktan erişim yoluyla bu uygulamaları yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4791c-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="4791c-108">Bu makalede hello adımları toopublish uygulama proxy'si ile bir şirket içi uygulama anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4791c-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="4791c-109">Bu makalede tamamladıktan sonra kullanıcılarınızın olacak mümkün tooaccess uygulamanızı uzaktan olabilir.</span><span class="sxs-lookup"><span data-stu-id="4791c-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="4791c-110">Ve ek özellikler gibi hello uygulama için hazır tooconfigure olacak tek oturum açma, kişiselleştirilmiş bilgileri ve güvenlik gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="4791c-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="4791c-111">Yeni tooApplication Proxy değilseniz, bu özellik ile Merhaba makalesi hakkında daha fazla bilgi [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4791c-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="4791c-112">Uzaktan erişim için şirket içi uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="4791c-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="4791c-113">Bu adımları toopublish uygulamalarınızı uygulama proxy'si ile izleyin.</span><span class="sxs-lookup"><span data-stu-id="4791c-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="4791c-114">Önceden indirilen henüz ve kuruluşunuz için bir bağlayıcı yapılandırılmış, çok gidin[uygulama proxy'si ile başlayın ve hello Bağlayıcısı yüklemeniz](active-directory-application-proxy-enable.md) ilk olarak ve uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="4791c-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="4791c-115">Hello için uygulama proxy'si ilk kez test ediyorsanız parola tabanlı kimlik doğrulaması için ayarlanmış bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="4791c-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="4791c-116">Uygulama proxy'si diğer kimlik doğrulama türlerini destekler, ancak parola tabanlı uygulamalar hello kolay tooget yukarı ve hızlı bir şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="4791c-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="4791c-117">Merhaba içinde bir yönetici olarak oturum açın [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4791c-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4791c-118">Seçin **Azure Active Directory** > **kurumsal uygulamalar** > **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="4791c-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Kurumsal uygulama ekleme](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="4791c-120">Seçin **tüm**seçeneğini belirleyip **şirket içi uygulama**.</span><span class="sxs-lookup"><span data-stu-id="4791c-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Kendi uygulama ekleme](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="4791c-122">Uygulamanız hakkında bilgi aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="4791c-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="4791c-123">**Ad**: hello erişim paneli ve hello Azure portalında görünür hello uygulamanın hello adı.</span><span class="sxs-lookup"><span data-stu-id="4791c-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="4791c-124">**İç URL**: özel ağınızda tooaccess hello uygulamadan kullandığınız URL hello.</span><span class="sxs-lookup"><span data-stu-id="4791c-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="4791c-125">Merhaba rest hello sunucusunun yayımdan olsa hello arka uç sunucu toopublish üzerinde belirli bir yol sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4791c-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="4791c-126">Bu şekilde, farklı siteleri yayımlama hello farklı uygulamalar aynı sunucuya ve her biri kendi adı ve erişim kuralları belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4791c-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="4791c-127">Bir yol yayımlarsanız, tüm hello gerekli görüntüleri, komut dosyalarını ve stil sayfaları, uygulamanız için dahil olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4791c-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="4791c-128">Uygulamanızı https://yourapp/app ise ve https://yourapp/media bulunan görüntüleri kullanır, örneğin, daha sonra https://yourapp/ hello yolu olarak yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4791c-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="4791c-129">Bu iç URL kullanıcılarınızın toobe hello giriş sayfası sahip değil.</span><span class="sxs-lookup"><span data-stu-id="4791c-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="4791c-130">Daha fazla bilgi için bkz: [yayımlanan uygulamalar için özel bir ana sayfa ayarlamak](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="4791c-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="4791c-131">**Dış URL**: Merhaba adresi kullanıcılarınızın tooin sipariş tooaccess hello uygulamadan ağınızın dışından gider.</span><span class="sxs-lookup"><span data-stu-id="4791c-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="4791c-132">Toouse hello varsayılan uygulama proxy'si etki alanı istemiyorsanız, bilgiyi [Azure AD uygulama proxy'si özel etki alanlarında](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="4791c-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="4791c-133">**Ön kimlik doğrulamasını**: nasıl uygulama proxy'si erişim tooyour uygulama vermeden önce kullanıcıların doğrular.</span><span class="sxs-lookup"><span data-stu-id="4791c-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="4791c-134">Azure Active Directory: Uygulama proxy'si kullanıcılar toosign izinlerini hello dizin ve uygulama için kimlik doğrulaması Azure AD ile yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4791c-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="4791c-135">Koşullu erişim ve çok faktörlü kimlik doğrulaması gibi Azure AD güvenlik özelliklerden yararlanabilmeniz hello varsayılan olarak bu seçenek tutmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="4791c-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="4791c-136">Geçiş: Kullanıcıların Azure Active Directory tooaccess Merhaba uygulaması karşı tooauthenticate yok.</span><span class="sxs-lookup"><span data-stu-id="4791c-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="4791c-137">Hala hello arka uç kimlik doğrulaması gereksinimleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4791c-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="4791c-138">**Bağlayıcı grup**: bağlayıcıları işlem hello uzaktan erişim tooyour uygulama ve bağlayıcı grupları, bağlayıcılar ve bölge, ağ veya amacı uygulamaların düzenlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4791c-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="4791c-139">Bağlayıcı gruplarda henüz yoksa, uygulamanız çok atanan**varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="4791c-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Uygulamanızı yapılandırma](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="4791c-141">Gerekirse, ek ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4791c-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="4791c-142">Çoğu uygulama için bu ayarları varsayılan durumlarına tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4791c-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="4791c-143">**Arka uç uygulaması zaman aşımı**: Bu değeri çok ayarlayın**uzun** yalnızca uygulamanızı yavaş tooauthenticate ve bağlanın ise.</span><span class="sxs-lookup"><span data-stu-id="4791c-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="4791c-144">**Üst bilgileri URL'leri**: Bu değer olarak tutun **Evet** hello özgün ana bilgisayar üstbilgisi hello kimlik doğrulama isteği için uygulamanız gereken sürece.</span><span class="sxs-lookup"><span data-stu-id="4791c-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="4791c-145">**Uygulama gövdesindeki URL'leri**: Bu değer olarak tutun **Hayır** kodlanmış HTML bağlantılar tooother şirket içi uygulamalarınız mevcutsa ve özel etki alanlarını kullanmadığınız sürece.</span><span class="sxs-lookup"><span data-stu-id="4791c-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="4791c-146">Daha fazla bilgi için bkz: [bağlantı uygulama proxy'si ile çeviri](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="4791c-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Uygulamanızı yapılandırma](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="4791c-148">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4791c-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="4791c-149">Test kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="4791c-149">Add a test user</span></span> 

<span data-ttu-id="4791c-150">uygulamanız doğru bir şekilde, yayımlanan tootest bir test kullanıcı hesabı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4791c-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="4791c-151">Bu hesap izinleri tooaccess hello uygulamadan olduğunu doğrulayın hello kurumsal ağ içinde.</span><span class="sxs-lookup"><span data-stu-id="4791c-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="4791c-152">Geri hello hızlı başlangıç dikey penceresinde, seçin **test etmek için bir kullanıcı atamak**.</span><span class="sxs-lookup"><span data-stu-id="4791c-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Test etmek için bir kullanıcı atama](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="4791c-154">Merhaba kullanıcıları ve grupları dikey penceresinde, seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4791c-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Bir kullanıcı veya Grup Ekle](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="4791c-156">Merhaba Ekle atama dikey seçin **kullanıcılar ve gruplar** tooadd istediğiniz hello hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="4791c-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="4791c-157">Seçin **atamak**.</span><span class="sxs-lookup"><span data-stu-id="4791c-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="4791c-158">Yayımlanan uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="4791c-158">Test your published app</span></span>

<span data-ttu-id="4791c-159">Tarayıcınızda, gezinme sırasında hello yapılandırılmış toohello dış URL'si adım yayımlama.</span><span class="sxs-lookup"><span data-stu-id="4791c-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="4791c-160">Merhaba Başlangıç ekranına görmeniz gerekir ve mümkün toosign hello test hesabıyla, ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="4791c-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Yayımlanan uygulamanızı test etme](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="4791c-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4791c-162">Next steps</span></span>
- <span data-ttu-id="4791c-163">[Bağlayıcılar karşıdan](active-directory-application-proxy-enable.md) ve [bağlayıcı grupları oluşturma](active-directory-application-proxy-connectors-azure-portal.md) ayrı ağlar ve konumları toopublish uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="4791c-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="4791c-164">[Çoklu oturum açmayı kurduğunuzda](application-proxy-sso-azure-portal.md) yeni yayımlanan uygulamanız için</span><span class="sxs-lookup"><span data-stu-id="4791c-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
