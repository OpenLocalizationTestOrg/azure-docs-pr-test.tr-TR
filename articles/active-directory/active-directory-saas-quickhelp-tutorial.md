---
title: "Öğretici: Azure Active Directory Tümleştirme ile QuickHelp | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile QuickHelp arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="fa7dd-103">Öğretici: Azure Active Directory Tümleştirme QuickHelp ile</span><span class="sxs-lookup"><span data-stu-id="fa7dd-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="fa7dd-104">Bu öğreticide, bilgi nasıl toointegrate QuickHelp Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa7dd-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa7dd-105">QuickHelp Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fa7dd-106">Erişim tooQuickHelp sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fa7dd-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="fa7dd-107">Kullanıcıların tooautomatically get açan tooQuickHelp (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fa7dd-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa7dd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="fa7dd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fa7dd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fa7dd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa7dd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fa7dd-110">Prerequisites</span></span>

<span data-ttu-id="fa7dd-111">tooconfigure QuickHelp ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="fa7dd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fa7dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa7dd-113">Bir QuickHelp çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fa7dd-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa7dd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa7dd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa7dd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa7dd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fa7dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa7dd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fa7dd-118">Scenario description</span></span>
<span data-ttu-id="fa7dd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa7dd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa7dd-121">Merhaba Galerisi'nden QuickHelp ekleme</span><span class="sxs-lookup"><span data-stu-id="fa7dd-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="fa7dd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fa7dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="fa7dd-123">Merhaba Galerisi'nden QuickHelp ekleme</span><span class="sxs-lookup"><span data-stu-id="fa7dd-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="fa7dd-124">Azure AD'ye tooconfigure hello tümleştirme QuickHelp, tooadd QuickHelp hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fa7dd-125">**tooadd QuickHelp hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fa7dd-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa7dd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa7dd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fa7dd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fa7dd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fa7dd-133">Merhaba arama kutusuna yazın **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-133">In hello search box, type **QuickHelp**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="fa7dd-135">Merhaba Sonuçlar panelinde seçin **QuickHelp**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa7dd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fa7dd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa7dd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı QuickHelp sınayın.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fa7dd-139">Tek toowork'ın oturum açma hangi hello karşılık gelen QuickHelp içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="fa7dd-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı QuickHelp hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="fa7dd-141">Merhaba hello değeri QuickHelp içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fa7dd-142">tooconfigure ve QuickHelp ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fa7dd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fa7dd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa7dd-145">**[QuickHelp test kullanıcısı oluşturma](#creating-a-quickhelp-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir QuickHelp içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa7dd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa7dd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa7dd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa7dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa7dd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma QuickHelp uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="fa7dd-150">**tooconfigure Azure AD çoklu oturum açma ile QuickHelp, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fa7dd-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa7dd-151">Hello hello üzerinde Azure portal'ın **QuickHelp** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fa7dd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="fa7dd-155">Merhaba üzerinde **QuickHelp etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="fa7dd-157">a.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-157">a.</span></span> <span data-ttu-id="fa7dd-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="fa7dd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="fa7dd-159">b.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-159">b.</span></span> <span data-ttu-id="fa7dd-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="fa7dd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa7dd-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-161">These values are not real.</span></span> <span data-ttu-id="fa7dd-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fa7dd-163">Kişi [QuickHelp istemci destek ekibi](https://support.quickhelp.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="fa7dd-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="fa7dd-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="fa7dd-168">Yönetici olarak oturum açma tooyour QuickHelp şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="fa7dd-169">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][21]

8. <span data-ttu-id="fa7dd-171">Merhaba, **QuickHelp yönetici** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][22]

9. <span data-ttu-id="fa7dd-173">Tıklatın **kimlik doğrulama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="fa7dd-174">Merhaba üzerinde **kimlik doğrulama ayarlarını** sayfasında, aşağıdaki adımları hello gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="fa7dd-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][23]
   
    <span data-ttu-id="fa7dd-176">a.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-176">a.</span></span> <span data-ttu-id="fa7dd-177">Olarak **SSO türü**seçin **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="fa7dd-178">b.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-178">b.</span></span> <span data-ttu-id="fa7dd-179">tooupload, indirilen Azure meta veri dosyası tıklatın **Gözat**, toohello dosya gidin, end'ye tıklayın **meta veriler karşıya**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="fa7dd-180">c.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-180">c.</span></span> <span data-ttu-id="fa7dd-181">Merhaba, **e-posta** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="fa7dd-182">d.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-182">d.</span></span> <span data-ttu-id="fa7dd-183">Merhaba, **ad** metin kutusuna, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="fa7dd-184">e.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-184">e.</span></span> <span data-ttu-id="fa7dd-185">Merhaba, **Soyadı** metin kutusuna, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="fa7dd-186">f.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-186">f.</span></span> <span data-ttu-id="fa7dd-187">Merhaba, **Eylem çubuğu**, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fa7dd-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fa7dd-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fa7dd-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fa7dd-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa7dd-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa7dd-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa7dd-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa7dd-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fa7dd-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fa7dd-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa7dd-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa7dd-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa7dd-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa7dd-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fa7dd-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa7dd-203">a.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-203">a.</span></span> <span data-ttu-id="fa7dd-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa7dd-205">b.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-205">b.</span></span> <span data-ttu-id="fa7dd-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa7dd-207">c.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-207">c.</span></span> <span data-ttu-id="fa7dd-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fa7dd-209">d.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-209">d.</span></span> <span data-ttu-id="fa7dd-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="fa7dd-211">QuickHelp test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa7dd-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="fa7dd-212">Bu bölümde Hello amacı toocreate Britta Simon içinde QuickHelp adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="fa7dd-213">Tek toowork'ın oturum açma, Azure AD hangi hello karşılık gelen kullanıcı QuickHelp tooa kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="fa7dd-214">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı QuickHelp hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="fa7dd-215">Yalnızca zaman sağlama QuickHelp destekler.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="fa7dd-216">Yani, gerekirse, bir kullanıcı hesabı QuickHelp içinde otomatik olarak oluşturulur ve bağlantılı toohello Azure AD hesabının hello hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="fa7dd-217">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fa7dd-218">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fa7dd-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fa7dd-219">Bu bölümde, erişim tooQuickHelp vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fa7dd-221">**tooassign Britta Simon tooQuickHelp hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fa7dd-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="fa7dd-222">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fa7dd-224">Merhaba uygulamalar listesinde **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="fa7dd-226">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fa7dd-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-228">Click **Add** button.</span></span> <span data-ttu-id="fa7dd-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fa7dd-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fa7dd-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa7dd-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa7dd-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fa7dd-234">Testing single sign-on</span></span>

<span data-ttu-id="fa7dd-235">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="fa7dd-236">Merhaba QuickHelp hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour QuickHelp uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa7dd-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fa7dd-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fa7dd-237">Additional resources</span></span>

* [<span data-ttu-id="fa7dd-238">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fa7dd-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa7dd-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fa7dd-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
