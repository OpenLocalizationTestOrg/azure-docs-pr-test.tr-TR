---
title: "Öğretici: Google Apps Azure Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Google Apps arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="bd501-103">Öğretici: Google Apps Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="bd501-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="bd501-104">Bu öğreticide, bilgi nasıl toointegrate Google Apps Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd501-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd501-105">Google Apps Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bd501-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd501-106">Erişim tooGoogle uygulamaları sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bd501-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="bd501-107">Kullanıcıların tooautomatically get açan tooGoogle uygulamalara (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bd501-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd501-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bd501-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd501-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla bilgi tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd501-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd501-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bd501-110">Prerequisites</span></span>

<span data-ttu-id="bd501-111">Google Apps ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd501-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="bd501-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bd501-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd501-113">Bir Google Apps çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="bd501-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd501-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bd501-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd501-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd501-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd501-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bd501-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd501-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd501-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="bd501-118">Video öğretici</span><span class="sxs-lookup"><span data-stu-id="bd501-118">Video tutorial</span></span>
<span data-ttu-id="bd501-119">Nasıl tooEnable çoklu oturum açma tooGoogle uygulamaları 2 dakika içinde:</span><span class="sxs-lookup"><span data-stu-id="bd501-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="bd501-120">Sık Sorulan Sorular</span><span class="sxs-lookup"><span data-stu-id="bd501-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="bd501-121">**S: Azure AD çoklu oturum açma ile uyumlu Chromebooks ve diğer Chrome aygıtları misiniz?**</span><span class="sxs-lookup"><span data-stu-id="bd501-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="bd501-122">A: Evet Chromebook cihazlarını Azure AD kimlik bilgilerini kullanarak içine mümkün toosign kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="bd501-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="bd501-123">Bu bkz [Google Apps destek makalesi](https://support.google.com/chrome/a/answer/6060880) neden hakkında bilgi için kimlik bilgilerini iki kez kullanıcılardan.</span><span class="sxs-lookup"><span data-stu-id="bd501-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="bd501-124">**S: ı çoklu oturum açma etkinleştirirseniz, kullanıcılar olacak kendi Azure AD kimlik bilgilerini toosign Google sınıf, GMail, Google sürücü, YouTube vb. gibi herhangi bir Google ürünü içine mümkün toouse olabilir?**</span><span class="sxs-lookup"><span data-stu-id="bd501-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="bd501-125">A: Evet hangisini seçtiğinize bağlı [hangi Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) tooenable seçin veya kuruluşunuz için devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="bd501-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="bd501-126">**S: Google Apps Kullanıcılarım yalnızca bir kısmı için çoklu oturum açmayı etkinleştir?**</span><span class="sxs-lookup"><span data-stu-id="bd501-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="bd501-127">A: Hayır çoklu oturum açma üzerinde hemen kapatılması, kendi Azure AD kimlik bilgilerine sahip tüm Google Apps kullanıcılar tooauthenticate gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bd501-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="bd501-128">Google Apps birden çok kimlik sağlayıcısı sahip desteklemediğinden hello kimlik sağlayıcısı Google Apps ortamınız için Azure AD ya da olabilir veya Google--ancak ikisini Merhaba, aynı anda.</span><span class="sxs-lookup"><span data-stu-id="bd501-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="bd501-129">**S: bir kullanıcının Windows oturum açtığı, bunlar otomatik olarak tooGoogle uygulamalar için bir parola istendiğinde alma olmadan kimlik doğrulaması olur mu?**</span><span class="sxs-lookup"><span data-stu-id="bd501-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="bd501-130">Y: Bu senaryoyu etkinleştirmek için iki seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="bd501-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="bd501-131">İlk olarak, kullanıcılar Windows 10 cihazlara üzerinden oturum [Azure Active Directory katılım](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd501-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="bd501-132">Alternatif olarak, kullanıcıların etki alanına katılmış tooan şirket içi tek oturum açma tooAzure AD için etkin Active Directory Windows cihazları oturum bir [Active Directory Federasyon Hizmetleri (AD FS)](active-directory-aadconnect-user-signin.md) dağıtım.</span><span class="sxs-lookup"><span data-stu-id="bd501-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="bd501-133">Her iki seçenek tooperform hello hello öğretici tooenable çoklu oturum açma Azure AD arasında aşağıdaki adımlarda gerektirir ve Google Apps.</span><span class="sxs-lookup"><span data-stu-id="bd501-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd501-134">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bd501-134">Scenario description</span></span>
<span data-ttu-id="bd501-135">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bd501-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd501-136">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bd501-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd501-137">Google Apps hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="bd501-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="bd501-138">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bd501-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="bd501-139">Google Apps hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="bd501-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="bd501-140">Azure AD'ye tooconfigure hello tümleştirme Google uygulamaların tooadd Google Apps hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd501-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd501-141">**Google Apps hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bd501-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd501-142">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bd501-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd501-144">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bd501-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd501-145">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bd501-145">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bd501-147">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bd501-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bd501-149">Merhaba arama kutusuna yazın **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="bd501-149">In hello search box, type **Google Apps**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="bd501-151">Merhaba Sonuçlar panelinde seçin **Google Apps**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bd501-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd501-153">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bd501-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd501-154">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Google "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı uygulamalar ile test etme</span><span class="sxs-lookup"><span data-stu-id="bd501-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd501-155">Tek toowork'ın oturum açma hangi hello karşılık gelen Google Apps içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd501-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="bd501-156">Diğer bir deyişle, bir Azure AD kullanıcısının ve Google Apps hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd501-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="bd501-157">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Google Apps içinde.</span><span class="sxs-lookup"><span data-stu-id="bd501-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="bd501-158">tooconfigure ve Google Apps ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd501-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd501-159">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="bd501-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd501-160">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="bd501-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd501-161">**[Google Apps test kullanıcısı oluşturma](#creating-a-google-apps-test-user)**  -toohave Britta Simon Google uygulamalardaki kullanıcı bağlantılı toohello Azure AD gösterimidir, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="bd501-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd501-162">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bd501-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd501-163">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="bd501-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd501-164">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bd501-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd501-165">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, Google Apps uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bd501-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="bd501-166">**tooconfigure Azure AD çoklu oturum açma Google Apps ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bd501-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd501-167">Hello hello üzerinde Azure portal'ın **Google Apps** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bd501-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bd501-169">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bd501-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="bd501-171">Merhaba üzerinde **Google Apps etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bd501-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="bd501-173">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="bd501-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd501-174">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="bd501-174">This value is not real.</span></span> <span data-ttu-id="bd501-175">Merhaba değerini hello gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd501-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="bd501-176">Merhaba başvurun [Google destek ekibi](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="bd501-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="bd501-177">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bd501-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="bd501-179">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bd501-179">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd501-181">Merhaba üzerinde **Google Apps Yapılandırması** 'yi tıklatın **yapılandırma Google Apps** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bd501-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bd501-182">Kopya hello **Sign-Out URL, SAML çoklu oturum açma hizmet URL'si ve değişiklik parola URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="bd501-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="bd501-184">Tarayıcınızda yeni bir sekme açın ve oturum hello [Google Apps Yönetici Konsolu](http://admin.google.com/) yönetici hesabını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="bd501-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="bd501-185">Tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="bd501-185">Click **Security**.</span></span> <span data-ttu-id="bd501-186">Merhaba bağlantısını görmüyorsanız, hello altında gizli olabilir **daha fazla denetim** hello ekranın hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="bd501-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Güvenlik'e tıklayın.][10]

9. <span data-ttu-id="bd501-188">Merhaba üzerinde **güvenlik** sayfasında, **çoklu oturum açmayı kurduğunuzda (SSO).**</span><span class="sxs-lookup"><span data-stu-id="bd501-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![SSO'ı tıklatın.][11]

10. <span data-ttu-id="bd501-190">Yapılandırma değişiklikleri izleyen hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bd501-190">Perform hello following configuration changes:</span></span>
   
    ![SSO yapılandırın][12]
   
    <span data-ttu-id="bd501-192">a.</span><span class="sxs-lookup"><span data-stu-id="bd501-192">a.</span></span> <span data-ttu-id="bd501-193">Seçin **üçüncü taraf kimlik sağlayıcısı ile Kurulum SSO**.</span><span class="sxs-lookup"><span data-stu-id="bd501-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="bd501-194">b.</span><span class="sxs-lookup"><span data-stu-id="bd501-194">b.</span></span> <span data-ttu-id="bd501-195">İçinde **oturum açma sayfası URL'si** alan Google Apps, hello değerini yapıştırın **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bd501-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bd501-196">c.</span><span class="sxs-lookup"><span data-stu-id="bd501-196">c.</span></span> <span data-ttu-id="bd501-197">Merhaba, **oturum kapatma sayfası URL'si** alan Google Apps, hello değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bd501-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bd501-198">d.</span><span class="sxs-lookup"><span data-stu-id="bd501-198">d.</span></span> <span data-ttu-id="bd501-199">Merhaba, **değiştirmek parola URL'si** alan Google Apps, hello değerini yapıştırın **değiştirmek parola URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bd501-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bd501-200">e.</span><span class="sxs-lookup"><span data-stu-id="bd501-200">e.</span></span> <span data-ttu-id="bd501-201">Hello için Google Apps içinde **doğrulama sertifikası**, Azure Portalı'ndan indirilen karşıya yükleme hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="bd501-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="bd501-202">f.</span><span class="sxs-lookup"><span data-stu-id="bd501-202">f.</span></span> <span data-ttu-id="bd501-203">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bd501-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="bd501-204">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bd501-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd501-205">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="bd501-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd501-206">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd501-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd501-207">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd501-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd501-208">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="bd501-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bd501-210">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bd501-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd501-211">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bd501-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd501-213">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bd501-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd501-215">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="bd501-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd501-217">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bd501-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd501-219">a.</span><span class="sxs-lookup"><span data-stu-id="bd501-219">a.</span></span> <span data-ttu-id="bd501-220">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd501-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd501-221">b.</span><span class="sxs-lookup"><span data-stu-id="bd501-221">b.</span></span> <span data-ttu-id="bd501-222">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="bd501-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd501-223">c.</span><span class="sxs-lookup"><span data-stu-id="bd501-223">c.</span></span> <span data-ttu-id="bd501-224">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bd501-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd501-225">d.</span><span class="sxs-lookup"><span data-stu-id="bd501-225">d.</span></span> <span data-ttu-id="bd501-226">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd501-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="bd501-227">Google Apps test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd501-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="bd501-228">Bu bölümde Hello amacı toocreate Britta Simon Google Apps yazılım adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="bd501-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="bd501-229">Google Apps otomatik sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="bd501-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="bd501-230">Bu bölümdeki hiçbir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="bd501-230">There is no action for you in this section.</span></span> <span data-ttu-id="bd501-231">Bir kullanıcı zaten Google Apps yazılımda yoksa, tooaccess Google Apps yazılım çalıştığında yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bd501-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="bd501-232">Bir kullanıcı toocreate el ile gerekiyorsa hello başvurun [Google destek ekibi](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="bd501-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd501-233">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bd501-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd501-234">Bu bölümde, tooGoogle uygulamaları erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd501-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bd501-236">**tooassign Britta Simon tooGoogle uygulamaları hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bd501-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd501-237">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bd501-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bd501-239">Merhaba uygulamalar listesinde **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="bd501-239">In hello applications list, select **Google Apps**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="bd501-241">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bd501-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bd501-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bd501-243">Click **Add** button.</span></span> <span data-ttu-id="bd501-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bd501-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bd501-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bd501-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd501-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bd501-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd501-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bd501-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd501-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bd501-249">Testing single sign-on</span></span>

<span data-ttu-id="bd501-250">Bu bölümde, tek oturum açma ayarlarınızı, açık hello adresinden erişim Paneli'nde tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)hello test hesaba oturum açın ve tıklatın **Google Apps** döşeme hello erişim paneli.</span><span class="sxs-lookup"><span data-stu-id="bd501-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd501-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bd501-251">Additional resources</span></span>

* [<span data-ttu-id="bd501-252">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bd501-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd501-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bd501-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bd501-254">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="bd501-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png