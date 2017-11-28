---
title: "Öğretici: Azure Active Directory Tümleştirme ile EverBridge | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile EverBridge arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="6e7d2-103">Öğretici: Azure Active Directory Tümleştirme EverBridge ile</span><span class="sxs-lookup"><span data-stu-id="6e7d2-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="6e7d2-104">Bu öğreticide, bilgi nasıl toointegrate EverBridge Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e7d2-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e7d2-105">EverBridge Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e7d2-106">Erişim tooEverBridge sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6e7d2-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="6e7d2-107">Kullanıcıların tooautomatically get açan tooEverBridge (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6e7d2-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e7d2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6e7d2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6e7d2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e7d2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e7d2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6e7d2-110">Prerequisites</span></span>

<span data-ttu-id="6e7d2-111">tooconfigure EverBridge ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="6e7d2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6e7d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e7d2-113">Bir EverBridge çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="6e7d2-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e7d2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e7d2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e7d2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e7d2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e7d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e7d2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6e7d2-118">Scenario description</span></span>
<span data-ttu-id="6e7d2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e7d2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e7d2-121">Merhaba Galerisi'nden EverBridge ekleme</span><span class="sxs-lookup"><span data-stu-id="6e7d2-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="6e7d2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6e7d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="6e7d2-123">Merhaba Galerisi'nden EverBridge ekleme</span><span class="sxs-lookup"><span data-stu-id="6e7d2-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="6e7d2-124">Azure AD'ye tooconfigure hello tümleştirme EverBridge, tooadd EverBridge hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e7d2-125">**tooadd EverBridge hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6e7d2-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7d2-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e7d2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e7d2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6e7d2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6e7d2-133">Merhaba arama kutusuna yazın **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-133">In hello search box, type **EverBridge**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="6e7d2-135">Merhaba Sonuçlar panelinde seçin **EverBridge**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e7d2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6e7d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e7d2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı EverBridge sınayın.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e7d2-139">Tek toowork'ın oturum açma hangi hello karşılık gelen EverBridge içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="6e7d2-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı EverBridge hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="6e7d2-141">Merhaba hello değeri EverBridge içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6e7d2-142">tooconfigure ve EverBridge ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e7d2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e7d2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e7d2-145">**[Bir EverBridge test kullanıcısı oluşturma](#creating-an-everbridge-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir EverBridge içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e7d2-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e7d2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e7d2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6e7d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e7d2-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma EverBridge uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="6e7d2-150">**tooconfigure Azure AD çoklu oturum açma ile EverBridge, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6e7d2-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7d2-151">Hello hello üzerinde Azure portal'ın **EverBridge** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6e7d2-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="6e7d2-155">Merhaba üzerinde **EverBridge etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="6e7d2-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-157">a.</span></span> <span data-ttu-id="6e7d2-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="6e7d2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="6e7d2-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-159">b.</span></span> <span data-ttu-id="6e7d2-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="6e7d2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e7d2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-161">These values are not real.</span></span> <span data-ttu-id="6e7d2-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6e7d2-163">Kişi [EverBridge destek ekibi](mailto:support@everbridge.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="6e7d2-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="6e7d2-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e7d2-168">Merhaba üzerinde **EverBridge yapılandırma** 'yi tıklatın **yapılandırma EverBridge** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6e7d2-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6e7d2-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="6e7d2-171">Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour Everbridge Kiracı yönetici olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="6e7d2-172">Hello'nde hello üstte, hello menüsünü **ayarları** sekmesinde ve seçin **çoklu oturum açma** altında **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="6e7d2-174">a.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-174">a.</span></span> <span data-ttu-id="6e7d2-175">Merhaba, **adı** metin kutusuna, tür hello tanımlayıcı sağlayıcı adını (örneğin: şirketinizin adını).</span><span class="sxs-lookup"><span data-stu-id="6e7d2-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="6e7d2-176">b.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-176">b.</span></span> <span data-ttu-id="6e7d2-177">Merhaba, **API adı** metin kutusuna, API tür hello adı.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="6e7d2-178">c.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-178">c.</span></span> <span data-ttu-id="6e7d2-179">Tıklatın **Dosya Seç** Azure Portalı'ndan indirilen düğmesi tooupload hello meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="6e7d2-180">d.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-180">d.</span></span> <span data-ttu-id="6e7d2-181">Hello SAML kimlik konumu, seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="6e7d2-182">e.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-182">e.</span></span> <span data-ttu-id="6e7d2-183">Merhaba, **kimlik sağlayıcısı oturum açma URL'si** metin kutusuna, Azure AD'den SAML SSO URL Yapıştır hello değeri.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="6e7d2-185">f.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-185">f.</span></span> <span data-ttu-id="6e7d2-186">Merhaba hizmet sağlayıcısı tarafından başlatılan bağlama istek içinde seçin **HTTP yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="6e7d2-187">g.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-187">g.</span></span> <span data-ttu-id="6e7d2-188">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="6e7d2-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="6e7d2-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6e7d2-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6e7d2-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6e7d2-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e7d2-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e7d2-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e7d2-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e7d2-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6e7d2-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6e7d2-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7d2-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e7d2-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e7d2-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e7d2-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6e7d2-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e7d2-204">a.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-204">a.</span></span> <span data-ttu-id="6e7d2-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e7d2-206">b.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-206">b.</span></span> <span data-ttu-id="6e7d2-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e7d2-208">c.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-208">c.</span></span> <span data-ttu-id="6e7d2-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e7d2-210">d.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-210">d.</span></span> <span data-ttu-id="6e7d2-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="6e7d2-212">Bir EverBridge test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e7d2-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="6e7d2-213">Bu bölümde, Everbridge içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="6e7d2-214">Çalışmak [EverBridge destek ekibi](mailto:support@everbridge.com) tooadd hello kullanıcılar hello Everbridge Platform.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6e7d2-215">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6e7d2-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6e7d2-216">Bu bölümde, erişim tooEverBridge vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6e7d2-218">**tooassign Britta Simon tooEverBridge hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6e7d2-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e7d2-219">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6e7d2-221">Merhaba uygulamalar listesinde **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-221">In hello applications list, select **EverBridge**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="6e7d2-223">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6e7d2-225">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-225">Click **Add** button.</span></span> <span data-ttu-id="6e7d2-226">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6e7d2-228">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e7d2-229">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e7d2-230">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e7d2-231">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6e7d2-231">Testing single sign-on</span></span>

<span data-ttu-id="6e7d2-232">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e7d2-233">Merhaba Everbridge hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Everbridge uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e7d2-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e7d2-234">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6e7d2-234">Additional resources</span></span>

* [<span data-ttu-id="6e7d2-235">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6e7d2-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e7d2-236">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6e7d2-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

