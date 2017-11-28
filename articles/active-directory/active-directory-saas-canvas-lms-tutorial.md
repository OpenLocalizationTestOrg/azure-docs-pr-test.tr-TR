---
title: "Öğretici: Azure Active Directory Tümleştirme tuvale Lms ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve tuvale LMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="cc6ea-103">Öğretici: Tuvale LMS Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="cc6ea-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="cc6ea-104">Bu öğreticide, bilgi nasıl toointegrate tuvale Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc6ea-105">Tuvale Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc6ea-106">Erişim tooCanvas sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cc6ea-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="cc6ea-107">Kullanıcıların tooautomatically get açan tooCanvas (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cc6ea-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc6ea-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cc6ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cc6ea-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc6ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc6ea-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc6ea-110">Prerequisites</span></span>

<span data-ttu-id="cc6ea-111">tooconfigure tuvali ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="cc6ea-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cc6ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc6ea-113">Bir tuval çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="cc6ea-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc6ea-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc6ea-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc6ea-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc6ea-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc6ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc6ea-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cc6ea-118">Scenario description</span></span>
<span data-ttu-id="cc6ea-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc6ea-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc6ea-121">Tuvale hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cc6ea-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="cc6ea-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cc6ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="cc6ea-123">Tuvale hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cc6ea-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="cc6ea-124">Azure AD'ye tooconfigure hello tümleştirme tuvalin tooadd tuvale hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc6ea-125">**tooadd hello galeri tuvalden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc6ea-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc6ea-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc6ea-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc6ea-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cc6ea-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cc6ea-133">Merhaba arama kutusuna yazın **tuvale**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-133">In hello search box, type **Canvas**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="cc6ea-135">Merhaba Sonuçlar panelinde seçin **tuvale**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc6ea-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cc6ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc6ea-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı tuvali ile test etme</span><span class="sxs-lookup"><span data-stu-id="cc6ea-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc6ea-139">Tek toowork'ın oturum açma, Azure AD'de tuvalin hangi hello karşılık gelen kullanıcı tooa kullanıcıdır tooknow Azure AD gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="cc6ea-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı tuvale hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="cc6ea-141">Tuvalde, hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc6ea-142">tooconfigure ve tuvali ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc6ea-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc6ea-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc6ea-145">**[Tuvale test kullanıcısı oluşturma](#creating-a-canvas-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir tuvale içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc6ea-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc6ea-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc6ea-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc6ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc6ea-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma tuvale uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="cc6ea-150">**tooconfigure Azure AD çoklu oturum açma tuvali hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc6ea-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc6ea-151">Merhaba hello üzerinde Azure portal'ın **tuvale** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cc6ea-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="cc6ea-155">Merhaba üzerinde **tuvale etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="cc6ea-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-157">a.</span></span> <span data-ttu-id="cc6ea-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="cc6ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="cc6ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-159">b.</span></span> <span data-ttu-id="cc6ea-160">Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="cc6ea-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc6ea-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-161">These values are not real.</span></span> <span data-ttu-id="cc6ea-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc6ea-163">Kişi [tuvale istemci destek ekibi](https://community.canvaslms.com/community/help) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="cc6ea-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="cc6ea-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc6ea-168">Merhaba üzerinde **tuvale yapılandırma** 'yi tıklatın **yapılandırma tuvale** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc6ea-169">Kopya hello **değişiklik parola URL'si, Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cc6ea-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="cc6ea-171">Farklı web tarayıcısı penceresinde tooyour tuvale şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="cc6ea-172">Çok Git**kurslar \> yönetilen hesapları \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="cc6ea-173">![Tuvale](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "tuvali")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="cc6ea-174">Merhaba soldaki Hello Gezinti Bölmesi'nde seçin **kimlik doğrulaması**ve ardından **ekleme yeni SAML Config**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="cc6ea-175">![Kimlik doğrulama](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="cc6ea-176">Merhaba geçerli tümleştirme sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc6ea-177">![Geçerli tümleştirme](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "geçerli tümleştirme")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="cc6ea-178">a.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-178">a.</span></span> <span data-ttu-id="cc6ea-179">İçinde **IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cc6ea-180">b.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-180">b.</span></span> <span data-ttu-id="cc6ea-181">İçinde **günlük üzerinde URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="cc6ea-182">c.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-182">c.</span></span> <span data-ttu-id="cc6ea-183">İçinde **oturum kapatma URL'sini** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cc6ea-184">d.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-184">d.</span></span> <span data-ttu-id="cc6ea-185">İçinde **değişiklik parola bağlantısı** metin kutusuna, Yapıştır hello değerini **değişiklik parola URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="cc6ea-186">e.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-186">e.</span></span> <span data-ttu-id="cc6ea-187">İçinde **sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="cc6ea-188">f.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-188">f.</span></span> <span data-ttu-id="cc6ea-189">Merhaba gelen **oturum açma özniteliği** listesinde **NameID**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="cc6ea-190">g.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-190">g.</span></span> <span data-ttu-id="cc6ea-191">Merhaba gelen **tanımlayıcı biçimi** listesinde **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="cc6ea-192">h.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-192">h.</span></span> <span data-ttu-id="cc6ea-193">Tıklatın **kimlik doğrulama ayarlarını Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="cc6ea-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cc6ea-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc6ea-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc6ea-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc6ea-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc6ea-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc6ea-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc6ea-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cc6ea-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc6ea-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc6ea-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc6ea-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc6ea-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc6ea-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc6ea-209">a.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-209">a.</span></span> <span data-ttu-id="cc6ea-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc6ea-211">b.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-211">b.</span></span> <span data-ttu-id="cc6ea-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc6ea-213">c.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-213">c.</span></span> <span data-ttu-id="cc6ea-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cc6ea-215">d.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-215">d.</span></span> <span data-ttu-id="cc6ea-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="cc6ea-217">Tuvale test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc6ea-217">Creating a Canvas test user</span></span>

<span data-ttu-id="cc6ea-218">tooenable Azure AD kullanıcıların toolog tooCanvas bunlar tuvale sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="cc6ea-219">Tuvale durumunda, kullanıcı sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="cc6ea-220">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc6ea-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc6ea-221">İçinde tooyour oturum **tuvale** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="cc6ea-222">Çok Git**kurslar \> yönetilen hesapları \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="cc6ea-223">![Tuvale](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "tuvali")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="cc6ea-224">**Kullanıcılar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-224">Click **Users**.</span></span>
   
   <span data-ttu-id="cc6ea-225">![Kullanıcıların](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="cc6ea-226">Tıklatın **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="cc6ea-227">![Kullanıcıların](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="cc6ea-228">Yeni kullanıcı iletişim Sayfa Ekle Hello üzerinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc6ea-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="cc6ea-229">![Kullanıcı ekleme](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="cc6ea-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="cc6ea-230">a.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-230">a.</span></span> <span data-ttu-id="cc6ea-231">Merhaba, **tam adı** metin kutusuna, bir kullanıcı gibi hello adını girin **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="cc6ea-232">b.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-232">b.</span></span> <span data-ttu-id="cc6ea-233">Merhaba, **e-posta** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cc6ea-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="cc6ea-234">c.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-234">c.</span></span> <span data-ttu-id="cc6ea-235">Merhaba, **oturum açma** metin kutusuna, hello kullanıcının Azure AD e-posta adresi gibi girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cc6ea-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="cc6ea-236">d.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-236">d.</span></span> <span data-ttu-id="cc6ea-237">Seçin **bu hesap oluşturma hakkında e-posta hello kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="cc6ea-238">e.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-238">e.</span></span> <span data-ttu-id="cc6ea-239">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="cc6ea-240">API AAD kullanıcı hesapları tuvale tooprovision tarafından sağlanan veya herhangi diğer tuvale kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cc6ea-241">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cc6ea-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cc6ea-242">Bu bölümde, erişim tooCanvas vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cc6ea-244">**tooassign Britta Simon tooCanvas hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cc6ea-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc6ea-245">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cc6ea-247">Merhaba uygulamalar listesinde **tuvale**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-247">In hello applications list, select **Canvas**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="cc6ea-249">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cc6ea-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-251">Click **Add** button.</span></span> <span data-ttu-id="cc6ea-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cc6ea-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc6ea-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc6ea-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc6ea-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cc6ea-257">Testing single sign-on</span></span>

<span data-ttu-id="cc6ea-258">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc6ea-259">Hello tuvale hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour tuvale uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc6ea-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="cc6ea-260">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc6ea-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc6ea-261">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cc6ea-261">Additional resources</span></span>

* [<span data-ttu-id="cc6ea-262">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cc6ea-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc6ea-263">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cc6ea-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

