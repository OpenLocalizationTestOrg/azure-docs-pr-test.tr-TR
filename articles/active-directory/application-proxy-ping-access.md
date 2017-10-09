---
title: "Azure AD uygulama proxy'si için kimlik doğrulaması ile PingAccess olarak aaaHeader tabanlı | Microsoft Docs"
description: "PingAccess ve uygulama Proxy toosupport üstbilgi tabanlı kimlik doğrulaması ile uygulama yayımlama."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="fd53d-103">Uygulama proxy'si ve PingAccess ile çoklu oturum açma için üstbilgi tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="fd53d-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="fd53d-104">Azure Active Directory Uygulama proxy'si ve PingAccess tooprovide Azure Active Directory erişimi tooeven müşterilerle birlikte daha fazla uygulama ortaklık.</span><span class="sxs-lookup"><span data-stu-id="fd53d-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="fd53d-105">PingAccess genişletir hello [varolan uygulama proxy'si teklifleri](active-directory-application-proxy-get-started.md) üstbilgileri kimlik doğrulaması için kullanmak tooinclude tek oturum açma erişimini tooapplications.</span><span class="sxs-lookup"><span data-stu-id="fd53d-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="fd53d-106">Azure AD için PingAccess nedir?</span><span class="sxs-lookup"><span data-stu-id="fd53d-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="fd53d-107">Azure Active Directory için PingAccess toogive kullanıcıların erişim sağlayan PingAccess ve kimlik doğrulaması için üstbilgiler kullanan tek oturum açma tooapplications bir tekliftir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="fd53d-108">Uygulama proxy'si kullanarak Azure AD tooauthenticate erişimini ve hello bağlayıcı hizmeti trafiğinin geçirme gibi diğer, bu uygulamalar değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="fd53d-109">PingAccess önünde hello uygulamaları bulunur ve Merhaba uygulaması okuyamamasını hello biçiminde hello kimlik doğrulaması alması hello erişim belirteci Azure AD'den bir üstbilgisine çevirir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="fd53d-110">Şirket uygulamalarınızı toouse içinde imzaladığınızda kullanıcılarınız farklı bir şey fark olmaz.</span><span class="sxs-lookup"><span data-stu-id="fd53d-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="fd53d-111">Bunlar hala herhangi bir yerden herhangi bir cihazda çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd53d-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="fd53d-112">Kendi kimlik doğrulama türü ne olursa olsun uzak trafik tooall uygulamaları Hello uygulama proxy'si bağlayıcılar doğrudan olduğundan, bunlar tooload Bakiye devam edeceğiz otomatik olarak, de.</span><span class="sxs-lookup"><span data-stu-id="fd53d-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="fd53d-113">Erişim nasıl sağlarım?</span><span class="sxs-lookup"><span data-stu-id="fd53d-113">How do I get access?</span></span>

<span data-ttu-id="fd53d-114">Bu senaryo, Azure Active Directory PingAccess arasındaki iş ortaklığına aracılığıyla sunulur olduğundan, her iki hizmet için lisans gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="fd53d-115">Ancak, Azure Active Directory Premium abonelikleri too20 uygulamalarını kapsamaktadır temel bir PingAccess lisans içerir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="fd53d-116">20'den fazla üstbilgi tabanlı uygulamalar toopublish gerekiyorsa, PingAccess ek lisans satın alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd53d-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="fd53d-117">Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="fd53d-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="fd53d-118">Azure'da uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="fd53d-118">Publish your application in Azure</span></span>

<span data-ttu-id="fd53d-119">Bu makale, bir uygulamanın bu senaryo için hello ile ilk kez yayımlama kişiler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fd53d-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="fd53d-120">Tooget hem uygulama hem de PingAccess, ayrıca toohello yayımlama adımları çalışmaya nasıl aracılığıyla size yardımcı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fd53d-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="fd53d-121">Her iki hizmet zaten yapılandırdıktan ancak adımları yayımlama hello bir Yenileyici istiyorsanız hello Bağlayıcısı yükleme atlayın ve çok taşıma[, uygulama tooAzure AD uygulama proxy'si ile ekleme](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="fd53d-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="fd53d-122">Bu senaryo Azure AD arasında ortaklık olduğundan ve PingAccess, bazı hello yönergeleri mevcut Ping kimlik site hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="fd53d-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="fd53d-123">Bir uygulama ara sunucusu Bağlayıcısı'nı yüklemek</span><span class="sxs-lookup"><span data-stu-id="fd53d-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="fd53d-124">Zaten uygulama Proxy etkin olması ve yüklü bir bağlayıcı varsa, bu bölüm atlayın ve çok taşıma[, uygulama tooAzure AD uygulama proxy'si ile ekleme](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="fd53d-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="fd53d-125">Merhaba uygulama ara sunucusu Bağlayıcısı olduğu bir Windows Server, uzak çalışanlar tooyour hello trafiğinden yönlendiren hizmeti yayımlanan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="fd53d-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="fd53d-126">Daha ayrıntılı yükleme yönergeleri için bkz: [uygulama ara sunucusunu etkinleştirme hello Azure portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="fd53d-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="fd53d-127">İçinde toohello oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="fd53d-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="fd53d-128">Seçin **Azure Active Directory** > **uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="fd53d-129">Seçin **Bağlayıcısı'nı indir** toostart hello uygulama ara sunucusu Bağlayıcısı indirme.</span><span class="sxs-lookup"><span data-stu-id="fd53d-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="fd53d-130">Merhaba yükleme yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-130">Follow hello installation instructions.</span></span>

   ![Uygulama Ara sunucusunu etkinleştirme ve hello bağlayıcı indirin](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="fd53d-132">Merhaba Bağlayıcısı indirme otomatik olarak etkinleştirmelisiniz uygulama proxy'si değil, seçebilirsiniz, ancak dizininiz için **uygulama ara sunucusunu etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="fd53d-133">Uygulama tooAzure AD uygulama proxy'si ile ekleme</span><span class="sxs-lookup"><span data-stu-id="fd53d-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="fd53d-134">İki Eylemler hello Azure portal tootake ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="fd53d-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="fd53d-135">İlk olarak, uygulamanızın uygulama proxy'si ile toopublish gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="fd53d-136">Ardından, toocollect hello PingAccess adımları sırasında kullanabilirsiniz hello uygulama hakkında bazı bilgiler gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="fd53d-137">Bu adımları toopublish uygulamanızı izleyin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="fd53d-138">1-8, bkz: izlenecek adımların daha ayrıntılı için [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd53d-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="fd53d-139">Merhaba son bölümünde almadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="fd53d-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="fd53d-140">Seçin **Azure Active Directory** > **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="fd53d-141">Seçin **Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="fd53d-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="fd53d-142">Seçin **şirket içi uygulama**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="fd53d-143">Yeni uygulamanızı hakkında bilgi içeren hello gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="fd53d-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="fd53d-144">Yönergeler hello ayarları için aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="fd53d-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="fd53d-145">**İç URL**: normal şekilde hello şirket ağında olduğunuzda, sayfasında toohello uygulamanın oturum geçen hello URL'sini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fd53d-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="fd53d-146">Bu senaryo için hello Bağlayıcısı hello ön sayfa hello uygulamasının olarak tootreat hello PingAccess proxy olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="fd53d-147">Şu biçimi kullanın: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="fd53d-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="fd53d-148">başlangıç bağlantı noktası, varsayılan değer 3000 olmakla birlikte PingAccess yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd53d-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="fd53d-149">**Ön kimlik doğrulama yöntemi**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd53d-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="fd53d-150">**Üstbilgiler URL'de çevir**: Hayır</span><span class="sxs-lookup"><span data-stu-id="fd53d-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="fd53d-151">Bu ilk uygulamanızı ise, bağlantı noktası 3000 toostart kullanın ve tooupdate PingAccess yapılandırmanızı değiştirirseniz, bu ayar geri dönün.</span><span class="sxs-lookup"><span data-stu-id="fd53d-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="fd53d-152">İkinci veya sonraki uygulamanız varsa bu toomatch hello PingAccess içinde yapılandırdığınız dinleyicisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="fd53d-153">Daha fazla bilgi edinmek [PingAccess dinleyicileri](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="fd53d-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="fd53d-154">Seçin **Ekle** hello dikey penceresinde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="fd53d-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="fd53d-155">Uygulamanızı eklenir ve hello Hızlı Başlat menüsü açılır.</span><span class="sxs-lookup"><span data-stu-id="fd53d-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="fd53d-156">Merhaba Hızlı Başlangıç menüsünde seçin **test etmek için bir kullanıcı atamak**ve en az bir kullanıcı toohello uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="fd53d-157">Bu test hesap erişim toohello şirket içi uygulama olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fd53d-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="fd53d-158">Seçin **atamak** toosave hello test kullanıcı ataması.</span><span class="sxs-lookup"><span data-stu-id="fd53d-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="fd53d-159">Merhaba uygulama yönetimi dikey penceresinde, seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="fd53d-160">Seçin **üstbilgi tabanlı oturum açma** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="fd53d-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="fd53d-161">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="fd53d-162">Üstbilgi tabanlı çoklu oturum açma kullanarak, ilk kez kullanıyorsanız tooinstall PingAccess gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="fd53d-163">toomake emin Azure aboneliğinizi otomatik olarak PingAccess yüklemenizi, bu tek oturum açma sayfası toodownload PingAccess kullanım hello bağlantıyı ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="fd53d-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="fd53d-164">Şimdi hello indirme sitesi açmak veya toothis sayfa daha sonra geri dönün.</span><span class="sxs-lookup"><span data-stu-id="fd53d-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![Üstbilgi tabanlı oturum açma seçin](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="fd53d-166">Merhaba kurumsal uygulamalar dikey penceresini kapatın veya tüm hello yolu toohello sol tooreturn toohello Azure Active Directory menüsüne gidin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="fd53d-167">Seçin **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-167">Select **App registrations**.</span></span>

   ![Uygulama kayıtlar seçin](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="fd53d-169">Yeni eklediğiniz, ardından select hello uygulama **yanıt URL'leri**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![Yanıt URL'leri seçin](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="fd53d-171">Merhaba dış URL hello yanıt URL'leri listesindeki bu atanan tooyour uygulamanızı adım 5'te ise toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="fd53d-172">Değilse, şimdi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="fd53d-173">Merhaba uygulama ayarları dikey penceresinde, seçin **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![Gerekli izinleri seçin](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="fd53d-175">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-175">Select **Add**.</span></span> <span data-ttu-id="fd53d-176">Merhaba API seçin **Windows Azure Active Directory**, ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="fd53d-177">Merhaba izinlerini seçin **okuma ve tüm uygulamaları yazma** ve **oturum açın ve kullanıcı profilini okuma**, ardından **seçin** ve **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![İzinleri seçin](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="fd53d-179">Merhaba PingAccess adımlar için bilgi toplama</span><span class="sxs-lookup"><span data-stu-id="fd53d-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="fd53d-180">Uygulama ayarları dikey üzerinde seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-180">On your app settings blade, select **Properties**.</span></span> 

  ![Özellikler'i seçin](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="fd53d-182">Merhaba Kaydet **uygulama kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="fd53d-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="fd53d-183">PingAccess yapılandırdığınızda bu hello istemci kimliği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd53d-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="fd53d-184">Merhaba uygulama ayarları dikey penceresinde, seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-184">On hello app settings blade, select **Keys**.</span></span>

  ![Anahtarları seçin](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="fd53d-186">Bir anahtar açıklama girerek ve sona erme tarihi hello açılan menüden seçerek bir anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fd53d-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="fd53d-187">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-187">Select **Save**.</span></span> <span data-ttu-id="fd53d-188">Bir GUID hello görünür **değeri** alan.</span><span class="sxs-lookup"><span data-stu-id="fd53d-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="fd53d-189">Bu değer şimdi mümkün toosee olmayacak şekilde yeniden sonra bu pencereyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="fd53d-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![Yeni bir anahtar oluşturun](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="fd53d-191">Merhaba uygulama kayıtlar dikey penceresini kapatın veya tüm hello yolu toohello sol tooreturn toohello Azure Active Directory menüsüne gidin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="fd53d-192">Seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-192">Select **Properties**.</span></span>
8. <span data-ttu-id="fd53d-193">Merhaba Kaydet **dizin kimliği** GUID.</span><span class="sxs-lookup"><span data-stu-id="fd53d-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="fd53d-194">İsteğe bağlı - güncelleştirme GraphAPI toosend özel alanlar</span><span class="sxs-lookup"><span data-stu-id="fd53d-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="fd53d-195">Azure AD kimlik doğrulaması için gönderir güvenlik belirteçleri listesi için bkz: [Azure AD belirteç başvurusu](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="fd53d-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="fd53d-196">Diğer belirteçleri gönderir bir özel talep gerekiyorsa, GraphAPI tooset hello uygulama alanını kullanın *acceptMappedClaims* çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="fd53d-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="fd53d-197">Azure AD Graph Explorer'a veya MS Graph toomake bu yapılandırmayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd53d-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="fd53d-198">Bu örnek Graph Explorer'a kullanır:</span><span class="sxs-lookup"><span data-stu-id="fd53d-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="fd53d-199">PingAccess indirin ve uygulamanızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fd53d-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="fd53d-200">Tüm hello Azure Active Directory kurulum adımlarını tamamladığınıza göre PingAccess tooconfiguring üzerinde taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd53d-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="fd53d-201">Merhaba hello PingAccess bu senaryonun parçası için ayrıntılı adımlar devam hello Ping kimlik belgeleri [yapılandırma PingAccess Azure AD için](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="fd53d-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="fd53d-202">Bu adımları, PingAccess hesabı zaten yoksa, alma, hello PingAccess sunucusu yükleme ve hello hello Azure portal ' kopyaladığınız dizini kimliği ile bir Azure AD OIDC sağlayıcı bağlantısı oluşturma hello işleminde size yol.</span><span class="sxs-lookup"><span data-stu-id="fd53d-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="fd53d-203">Ardından, üzerinde PingAccess hello uygulama kimliği ve anahtarı değerlerini toocreate Web oturumu kullanın.</span><span class="sxs-lookup"><span data-stu-id="fd53d-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="fd53d-204">Bundan sonra kimlik eşlemesi ayarlamanız ve bir sanal ana bilgisayar, site ve uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fd53d-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="fd53d-205">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="fd53d-205">Test your app</span></span>

<span data-ttu-id="fd53d-206">Tüm bu adımları tamamladıktan sonra uygulamanızı açık ve çalışıyor olması.</span><span class="sxs-lookup"><span data-stu-id="fd53d-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="fd53d-207">tootest, bir tarayıcı açın ve Azure'da hello uygulama yayımlandığında, oluşturduğunuz toohello dış URL'yi gidin.</span><span class="sxs-lookup"><span data-stu-id="fd53d-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="fd53d-208">Bu, atanan toohello uygulama Hello test hesabıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fd53d-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd53d-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fd53d-209">Next steps</span></span>

- [<span data-ttu-id="fd53d-210">Azure AD için PingAccess yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fd53d-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="fd53d-211">Azure AD uygulama proxy'si nasıl çoklu oturum açma sağlar?</span><span class="sxs-lookup"><span data-stu-id="fd53d-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="fd53d-212">Uygulama proxy'si sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fd53d-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
