---
title: "Öğretici: Azure Active Directory Tümleştirme ile Aha! | Microsoft Belgeleri"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Aha arasında!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="a73cb-104">Öğretici: Azure Active Directory Tümleştirme ile Aha!</span><span class="sxs-lookup"><span data-stu-id="a73cb-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="a73cb-105">Bu öğreticide, bilgi nasıl toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="a73cb-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="a73cb-106">Azure ile Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a73cb-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a73cb-107">AHA tümleştirme!</span><span class="sxs-lookup"><span data-stu-id="a73cb-107">Integrating Aha!</span></span> <span data-ttu-id="a73cb-108">Azure AD ile ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a73cb-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a73cb-109">Erişim tooAha sahip Azure AD'de kontrol edebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="a73cb-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="a73cb-110">Oturum açma, kullanıcıların tooautomatically get tooAha etkinleştirebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="a73cb-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="a73cb-111">(Çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="a73cb-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a73cb-112">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a73cb-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a73cb-113">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a73cb-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a73cb-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a73cb-114">Prerequisites</span></span>

<span data-ttu-id="a73cb-115">tooconfigure Aha ile Azure AD tümleştirme!, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a73cb-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="a73cb-116">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a73cb-116">An Azure AD subscription</span></span>
- <span data-ttu-id="a73cb-117">Bir Aha!</span><span class="sxs-lookup"><span data-stu-id="a73cb-117">An Aha!</span></span> <span data-ttu-id="a73cb-118">Çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a73cb-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a73cb-119">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a73cb-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a73cb-120">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a73cb-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a73cb-121">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a73cb-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a73cb-122">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a73cb-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a73cb-123">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a73cb-123">Scenario description</span></span>
<span data-ttu-id="a73cb-124">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a73cb-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a73cb-125">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a73cb-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a73cb-126">AHA ekleme!</span><span class="sxs-lookup"><span data-stu-id="a73cb-126">Adding Aha!</span></span> <span data-ttu-id="a73cb-127">Merhaba Galeriden</span><span class="sxs-lookup"><span data-stu-id="a73cb-127">from hello gallery</span></span>
2. <span data-ttu-id="a73cb-128">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a73cb-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="a73cb-129">AHA ekleme!</span><span class="sxs-lookup"><span data-stu-id="a73cb-129">Adding Aha!</span></span> <span data-ttu-id="a73cb-130">Merhaba Galeriden</span><span class="sxs-lookup"><span data-stu-id="a73cb-130">from hello gallery</span></span>
<span data-ttu-id="a73cb-131">Merhaba tümleştirilmesi Aha tooconfigure!</span><span class="sxs-lookup"><span data-stu-id="a73cb-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="a73cb-132">Azure AD ile tooadd Aha gerekiyor!</span><span class="sxs-lookup"><span data-stu-id="a73cb-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="a73cb-133">Merhaba galeri tooyour listesinden yönetilen SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="a73cb-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a73cb-134">**tooadd Aha! Merhaba Galerisi'nden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a73cb-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73cb-135">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a73cb-137">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a73cb-138">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-138">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a73cb-140">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a73cb-142">Merhaba arama kutusuna yazın **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-142">In hello search box, type **Aha!**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="a73cb-144">Merhaba Sonuçlar panelinde seçin **Aha!**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a73cb-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a73cb-146">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a73cb-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a73cb-147">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Aha ile test etme!</span><span class="sxs-lookup"><span data-stu-id="a73cb-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="a73cb-148">"Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="a73cb-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a73cb-149">Tek toowork'ın oturum açma Azure AD Aha hangi hello karşılık gelen kullanıcı tooknow gerekiyor!</span><span class="sxs-lookup"><span data-stu-id="a73cb-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="a73cb-150">tooa, Azure AD'de kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a73cb-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="a73cb-151">Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili Aha içinde!</span><span class="sxs-lookup"><span data-stu-id="a73cb-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="a73cb-152">oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a73cb-152">needs toobe established.</span></span>

<span data-ttu-id="a73cb-153">Aha,!, hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a73cb-154">tooconfigure ve test Azure AD çoklu oturum açma Aha ile!, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a73cb-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a73cb-155">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a73cb-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a73cb-156">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a73cb-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a73cb-157">**[Oluşturma bir Aha! test kullanıcısı](#creating-an-aha-test-user)**  -toohave Britta Simon Aha içinde karşılık gelen!</span><span class="sxs-lookup"><span data-stu-id="a73cb-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="a73cb-158">bağlantılı toohello Azure AD kullanıcı gösterimini olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a73cb-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a73cb-159">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a73cb-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a73cb-160">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a73cb-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a73cb-161">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a73cb-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a73cb-162">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirme ve çoklu oturum açma, Aha yapılandırma!</span><span class="sxs-lookup"><span data-stu-id="a73cb-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="a73cb-163">Uygulama.</span><span class="sxs-lookup"><span data-stu-id="a73cb-163">application.</span></span>

<span data-ttu-id="a73cb-164">**Azure AD çoklu oturum açma tooconfigure Aha ile!, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a73cb-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73cb-165">Merhaba hello üzerinde Azure portal'ın **Aha!**</span><span class="sxs-lookup"><span data-stu-id="a73cb-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="a73cb-166">Uygulama Tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-166">application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a73cb-168">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a73cb-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="a73cb-170">Merhaba üzerinde **Aha! Etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a73cb-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="a73cb-172">a.</span><span class="sxs-lookup"><span data-stu-id="a73cb-172">a.</span></span> <span data-ttu-id="a73cb-173">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="a73cb-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="a73cb-174">b.</span><span class="sxs-lookup"><span data-stu-id="a73cb-174">b.</span></span> <span data-ttu-id="a73cb-175">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="a73cb-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a73cb-176">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a73cb-176">These values are not real.</span></span> <span data-ttu-id="a73cb-177">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a73cb-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a73cb-178">Kişi [Aha! İstemci destek ekibi](https://www.aha.io/company/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a73cb-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="a73cb-179">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a73cb-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="a73cb-181">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-181">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a73cb-183">Farklı web tarayıcısı penceresinde tooyour Aha oturum!</span><span class="sxs-lookup"><span data-stu-id="a73cb-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="a73cb-184">Yönetici olarak şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-184">company site as an administrator.</span></span>

7. <span data-ttu-id="a73cb-185">Hello içinde hello üst menüsünde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="a73cb-186">![Ayarları](./media/active-directory-saas-aha-tutorial/IC798950.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="a73cb-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="a73cb-187">Tıklatın **hesap**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-187">Click **Account**.</span></span>
   
    <span data-ttu-id="a73cb-188">![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "profili")</span><span class="sxs-lookup"><span data-stu-id="a73cb-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="a73cb-189">Tıklatın **güvenlik ve çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="a73cb-190">![Güvenlik ve çoklu oturum açma](./media/active-directory-saas-aha-tutorial/IC798952.png "güvenlik ve çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a73cb-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="a73cb-191">İçinde **çoklu oturum açma** bölümünde olarak **kimlik sağlayıcısı**seçin **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="a73cb-192">![Güvenlik ve çoklu oturum açma](./media/active-directory-saas-aha-tutorial/IC798953.png "güvenlik ve çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a73cb-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="a73cb-193">Merhaba üzerinde **çoklu oturum açma** yapılandırma sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a73cb-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="a73cb-194">![Çoklu oturum açma](./media/active-directory-saas-aha-tutorial/IC798954.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a73cb-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="a73cb-195">a.</span><span class="sxs-lookup"><span data-stu-id="a73cb-195">a.</span></span> <span data-ttu-id="a73cb-196">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="a73cb-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="a73cb-197">b.</span><span class="sxs-lookup"><span data-stu-id="a73cb-197">b.</span></span> <span data-ttu-id="a73cb-198">İçin **kullanarak yapılandırma**seçin **meta veri dosyası**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="a73cb-199">c.</span><span class="sxs-lookup"><span data-stu-id="a73cb-199">c.</span></span> <span data-ttu-id="a73cb-200">tooupload, indirilen meta veri dosyası tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="a73cb-201">d.</span><span class="sxs-lookup"><span data-stu-id="a73cb-201">d.</span></span> <span data-ttu-id="a73cb-202">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="a73cb-203">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a73cb-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a73cb-204">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a73cb-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a73cb-205">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a73cb-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a73cb-206">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a73cb-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="a73cb-207">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a73cb-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a73cb-209">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a73cb-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73cb-210">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a73cb-212">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a73cb-214">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a73cb-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a73cb-216">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a73cb-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a73cb-218">a.</span><span class="sxs-lookup"><span data-stu-id="a73cb-218">a.</span></span> <span data-ttu-id="a73cb-219">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a73cb-220">b.</span><span class="sxs-lookup"><span data-stu-id="a73cb-220">b.</span></span> <span data-ttu-id="a73cb-221">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a73cb-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a73cb-222">c.</span><span class="sxs-lookup"><span data-stu-id="a73cb-222">c.</span></span> <span data-ttu-id="a73cb-223">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a73cb-224">d.</span><span class="sxs-lookup"><span data-stu-id="a73cb-224">d.</span></span> <span data-ttu-id="a73cb-225">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a73cb-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="a73cb-226">Oluşturma bir Aha!</span><span class="sxs-lookup"><span data-stu-id="a73cb-226">Creating an Aha!</span></span> <span data-ttu-id="a73cb-227">Test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="a73cb-227">test user</span></span>

<span data-ttu-id="a73cb-228">tooenable Azure AD kullanıcıların toolog tooAha,!, Aha sağlanmalıdır!.</span><span class="sxs-lookup"><span data-stu-id="a73cb-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="a73cb-229">Merhaba durumda Aha,!, otomatik bir görev olduğundan sağlama.</span><span class="sxs-lookup"><span data-stu-id="a73cb-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="a73cb-230">Sizin için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="a73cb-230">There is no action item for you.</span></span>

<span data-ttu-id="a73cb-231">Kullanıcıları otomatik olarak hello ilk tek oturum açma girişimi sırasında gerekirse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a73cb-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="a73cb-232">Diğer bir Aha kullanabilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="a73cb-232">You can use any other Aha!</span></span> <span data-ttu-id="a73cb-233">kullanıcı hesabı oluşturma araçlarını veya Aha tarafından sağlanan API'leri!</span><span class="sxs-lookup"><span data-stu-id="a73cb-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="a73cb-234">tooprovision AAD kullanıcı hesapları.</span><span class="sxs-lookup"><span data-stu-id="a73cb-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a73cb-235">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a73cb-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a73cb-236">Bu bölümde, erişim tooAha vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştir!.</span><span class="sxs-lookup"><span data-stu-id="a73cb-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a73cb-238">**tooassign Britta Simon tooAha!, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a73cb-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="a73cb-239">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a73cb-241">Merhaba uygulamalar listesinde **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-241">In hello applications list, select **Aha!**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="a73cb-243">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a73cb-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a73cb-245">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a73cb-245">Click **Add** button.</span></span> <span data-ttu-id="a73cb-246">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a73cb-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a73cb-248">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a73cb-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a73cb-249">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a73cb-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a73cb-250">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a73cb-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a73cb-251">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a73cb-251">Testing single sign-on</span></span>

<span data-ttu-id="a73cb-252">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="a73cb-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="a73cb-253">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a73cb-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a73cb-254">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a73cb-254">Additional resources</span></span>

* [<span data-ttu-id="a73cb-255">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a73cb-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a73cb-256">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a73cb-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

