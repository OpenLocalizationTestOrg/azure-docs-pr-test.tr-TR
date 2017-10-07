---
title: "Öğretici: Azure Active Directory Tümleştirme ile Sprinklr | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Sprinklr arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="a24ae-103">Öğretici: Azure Active Directory Tümleştirme Sprinklr ile</span><span class="sxs-lookup"><span data-stu-id="a24ae-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="a24ae-104">Bu öğreticide, bilgi nasıl toointegrate Sprinklr Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a24ae-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a24ae-105">Sprinklr Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a24ae-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a24ae-106">Erişim tooSprinklr sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a24ae-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="a24ae-107">Kullanıcıların tooautomatically get açan tooSprinklr (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a24ae-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a24ae-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a24ae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a24ae-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a24ae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a24ae-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a24ae-110">Prerequisites</span></span>

<span data-ttu-id="a24ae-111">tooconfigure Sprinklr ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a24ae-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="a24ae-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a24ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a24ae-113">Bir Sprinklr çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a24ae-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a24ae-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a24ae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a24ae-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a24ae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a24ae-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a24ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a24ae-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a24ae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a24ae-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a24ae-118">Scenario description</span></span>
<span data-ttu-id="a24ae-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a24ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a24ae-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a24ae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a24ae-121">Merhaba Galerisi'nden Sprinklr ekleme</span><span class="sxs-lookup"><span data-stu-id="a24ae-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="a24ae-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a24ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="a24ae-123">Merhaba Galerisi'nden Sprinklr ekleme</span><span class="sxs-lookup"><span data-stu-id="a24ae-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="a24ae-124">Azure AD'ye tooconfigure hello tümleştirme Sprinklr, tooadd Sprinklr hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a24ae-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a24ae-125">**tooadd Sprinklr hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a24ae-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a24ae-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a24ae-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a24ae-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a24ae-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a24ae-133">Merhaba arama kutusuna yazın **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-133">In hello search box, type **Sprinklr**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="a24ae-135">Merhaba Sonuçlar panelinde seçin **Sprinklr**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a24ae-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a24ae-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a24ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a24ae-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Sprinklr ile test etme</span><span class="sxs-lookup"><span data-stu-id="a24ae-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a24ae-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Sprinklr içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a24ae-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="a24ae-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Sprinklr hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a24ae-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="a24ae-141">Merhaba hello değeri Sprinklr içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a24ae-142">tooconfigure ve Sprinklr ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a24ae-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a24ae-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a24ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a24ae-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a24ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a24ae-145">**[Sprinklr test kullanıcısı oluşturma](#creating-a-sprinklr-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Sprinklr içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a24ae-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a24ae-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a24ae-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a24ae-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a24ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a24ae-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a24ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a24ae-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Sprinklr uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a24ae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="a24ae-150">**tooconfigure Azure AD çoklu oturum açma ile Sprinklr, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a24ae-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="a24ae-151">Hello hello üzerinde Azure portal'ın **Sprinklr** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a24ae-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a24ae-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="a24ae-155">Merhaba üzerinde **Sprinklr etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a24ae-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="a24ae-157">a.</span><span class="sxs-lookup"><span data-stu-id="a24ae-157">a.</span></span> <span data-ttu-id="a24ae-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a24ae-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="a24ae-159">b.</span><span class="sxs-lookup"><span data-stu-id="a24ae-159">b.</span></span> <span data-ttu-id="a24ae-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a24ae-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a24ae-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a24ae-161">These values are not real.</span></span> <span data-ttu-id="a24ae-162">Merhaba değeri ile Merhaba güncelleştirin gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a24ae-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a24ae-163">Kişi [Sprinklr istemci destek ekibi](https://www.sprinklr.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a24ae-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a24ae-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a24ae-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="a24ae-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a24ae-168">Merhaba üzerinde **Sprinklr yapılandırma** 'yi tıklatın **yapılandırma Sprinklr** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a24ae-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="a24ae-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="a24ae-170">Farklı web tarayıcısı penceresinde tooyour Sprinklr şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a24ae-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="a24ae-171">Çok Git**Yönetim \> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a24ae-172">![Yönetim](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="a24ae-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="a24ae-173">Çok Git**iş ortağı yönetme \> çoklu oturum açma** üzerinde hello sol bölmesinden.</span><span class="sxs-lookup"><span data-stu-id="a24ae-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="a24ae-174">![İş ortağı yönetme](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "iş ortağı yönetme")</span><span class="sxs-lookup"><span data-stu-id="a24ae-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="a24ae-175">Tıklatın **+ çoklu oturum açmaların eklemek**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="a24ae-176">![Çoklu oturum açmaların](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "çoklu oturum açmaların")</span><span class="sxs-lookup"><span data-stu-id="a24ae-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="a24ae-177">Merhaba üzerinde **çoklu oturum açma** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a24ae-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a24ae-178">![Çoklu oturum açmaların](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "çoklu oturum açmaların")</span><span class="sxs-lookup"><span data-stu-id="a24ae-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="a24ae-179">a.</span><span class="sxs-lookup"><span data-stu-id="a24ae-179">a.</span></span> <span data-ttu-id="a24ae-180">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="a24ae-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="a24ae-181">b.</span><span class="sxs-lookup"><span data-stu-id="a24ae-181">b.</span></span> <span data-ttu-id="a24ae-182">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-182">Select **Enabled**.</span></span>

    <span data-ttu-id="a24ae-183">c.</span><span class="sxs-lookup"><span data-stu-id="a24ae-183">c.</span></span> <span data-ttu-id="a24ae-184">Seçin **yeni SSO sertifikayı kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="a24ae-185">e.</span><span class="sxs-lookup"><span data-stu-id="a24ae-185">e.</span></span> <span data-ttu-id="a24ae-186">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a24ae-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="a24ae-187">f.</span><span class="sxs-lookup"><span data-stu-id="a24ae-187">f.</span></span> <span data-ttu-id="a24ae-188">Yapıştır hello **SAML varlık kimliği** hello Azure portalından kopyalandığından değeri **varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a24ae-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="a24ae-189">g.</span><span class="sxs-lookup"><span data-stu-id="a24ae-189">g.</span></span> <span data-ttu-id="a24ae-190">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello Azure portalından kopyalandığından değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a24ae-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a24ae-191">h.</span><span class="sxs-lookup"><span data-stu-id="a24ae-191">h.</span></span> <span data-ttu-id="a24ae-192">Yapıştır hello **Sign-Out URL** hello Azure portalından kopyalandığından değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a24ae-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="a24ae-193">ı.</span><span class="sxs-lookup"><span data-stu-id="a24ae-193">i.</span></span> <span data-ttu-id="a24ae-194">Olarak **SAML kullanıcı kimliği türü**seçin **onaylamayı içeren kullanıcı "s sprinklr.com kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="a24ae-195">j.</span><span class="sxs-lookup"><span data-stu-id="a24ae-195">j.</span></span> <span data-ttu-id="a24ae-196">Olarak **SAML kullanıcı kimliği konumu**seçin **kullanıcı kimliğidir hello ad tanımlayıcısı öğesinde hello konu deyimi**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="a24ae-197">k.</span><span class="sxs-lookup"><span data-stu-id="a24ae-197">k.</span></span> <span data-ttu-id="a24ae-198">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a24ae-198">Click **Save**.</span></span>
       
    <span data-ttu-id="a24ae-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="a24ae-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="a24ae-200">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a24ae-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a24ae-201">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a24ae-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a24ae-202">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a24ae-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a24ae-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a24ae-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a24ae-204">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a24ae-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a24ae-206">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a24ae-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a24ae-207">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a24ae-209">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a24ae-211">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a24ae-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a24ae-213">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a24ae-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a24ae-215">a.</span><span class="sxs-lookup"><span data-stu-id="a24ae-215">a.</span></span> <span data-ttu-id="a24ae-216">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a24ae-217">b.</span><span class="sxs-lookup"><span data-stu-id="a24ae-217">b.</span></span> <span data-ttu-id="a24ae-218">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a24ae-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a24ae-219">c.</span><span class="sxs-lookup"><span data-stu-id="a24ae-219">c.</span></span> <span data-ttu-id="a24ae-220">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a24ae-221">d.</span><span class="sxs-lookup"><span data-stu-id="a24ae-221">d.</span></span> <span data-ttu-id="a24ae-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a24ae-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="a24ae-223">Sprinklr test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a24ae-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="a24ae-224">İçinde tooyour Sprinklr şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a24ae-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="a24ae-225">Çok Git**Yönetim \> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a24ae-226">![Yönetim](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="a24ae-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="a24ae-227">Çok Git**yönetmek istemci \> kullanıcılar** hello sol bölmesinden.</span><span class="sxs-lookup"><span data-stu-id="a24ae-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="a24ae-228">![Ayarları](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="a24ae-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="a24ae-229">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="a24ae-230">![Ayarları](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="a24ae-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="a24ae-231">Merhaba üzerinde **düzenleme kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a24ae-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="a24ae-232">![Kullanıcı düzenleme](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "düzenleme kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="a24ae-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="a24ae-233">a.</span><span class="sxs-lookup"><span data-stu-id="a24ae-233">a.</span></span> <span data-ttu-id="a24ae-234">Merhaba, **e-posta**, **ad** ve **Soyadı** metin kutuları, tooprovision istediğiniz bir Azure AD kullanıcı hesabının türü hello bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a24ae-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="a24ae-235">b.</span><span class="sxs-lookup"><span data-stu-id="a24ae-235">b.</span></span> <span data-ttu-id="a24ae-236">Seçin **parola devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="a24ae-237">c.</span><span class="sxs-lookup"><span data-stu-id="a24ae-237">c.</span></span> <span data-ttu-id="a24ae-238">Seçin **dil**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-238">Select **Language**.</span></span>

    <span data-ttu-id="a24ae-239">d.</span><span class="sxs-lookup"><span data-stu-id="a24ae-239">d.</span></span> <span data-ttu-id="a24ae-240">Seçin **kullanıcı türü**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-240">Select **User Type**.</span></span>

    <span data-ttu-id="a24ae-241">e.</span><span class="sxs-lookup"><span data-stu-id="a24ae-241">e.</span></span> <span data-ttu-id="a24ae-242">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="a24ae-243">**Parola devre dışı** seçili tooenable içinde kullanıcı toolog bir kimlik sağlayıcısı aracılığıyla olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a24ae-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="a24ae-244">Çok Git**rol**ve ardından hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a24ae-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="a24ae-245">![İş ortağı rolleri](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "ortak rolleri")</span><span class="sxs-lookup"><span data-stu-id="a24ae-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="a24ae-246">a.</span><span class="sxs-lookup"><span data-stu-id="a24ae-246">a.</span></span> <span data-ttu-id="a24ae-247">Merhaba gelen **Global** listesinde **tüm\_izinleri**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="a24ae-248">b.</span><span class="sxs-lookup"><span data-stu-id="a24ae-248">b.</span></span> <span data-ttu-id="a24ae-249">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="a24ae-250">API'leri, Azure AD kullanıcı hesapları Sprinklr tooprovision tarafından sağlanan veya herhangi diğer Sprinklr kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a24ae-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a24ae-251">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a24ae-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a24ae-252">Bu bölümde, erişim tooSprinklr vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a24ae-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a24ae-254">**tooassign Britta Simon tooSprinklr hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a24ae-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="a24ae-255">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a24ae-257">Merhaba uygulamalar listesinde **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="a24ae-259">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a24ae-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a24ae-261">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a24ae-261">Click **Add** button.</span></span> <span data-ttu-id="a24ae-262">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a24ae-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a24ae-264">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a24ae-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a24ae-265">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a24ae-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a24ae-266">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a24ae-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a24ae-267">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a24ae-267">Testing single sign-on</span></span>

<span data-ttu-id="a24ae-268">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a24ae-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a24ae-269">Merhaba Sprinklr hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Sprinklr uygulama hello erişim paneli hakkında daha fazla bilgi almak, bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a24ae-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a24ae-270">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a24ae-270">Additional resources</span></span>

* [<span data-ttu-id="a24ae-271">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a24ae-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a24ae-272">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a24ae-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

