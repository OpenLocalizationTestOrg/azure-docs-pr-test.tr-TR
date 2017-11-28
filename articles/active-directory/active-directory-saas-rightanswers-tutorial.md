---
title: "Öğretici: Azure Active Directory Tümleştirme ile RightAnswers | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile RightAnswers arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 745e7ed5a13291afeed8f48a595e95b27d4b0e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="a18bd-103">Öğretici: Azure Active Directory Tümleştirme RightAnswers ile</span><span class="sxs-lookup"><span data-stu-id="a18bd-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="a18bd-104">Bu öğreticide, bilgi nasıl toointegrate RightAnswers Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a18bd-104">In this tutorial, you learn how toointegrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a18bd-105">RightAnswers Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a18bd-105">Integrating RightAnswers with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a18bd-106">Erişim tooRightAnswers sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a18bd-106">You can control in Azure AD who has access tooRightAnswers</span></span>
- <span data-ttu-id="a18bd-107">Kullanıcıların tooautomatically get açan tooRightAnswers (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a18bd-107">You can enable your users tooautomatically get signed-on tooRightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a18bd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a18bd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a18bd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a18bd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a18bd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a18bd-110">Prerequisites</span></span>

<span data-ttu-id="a18bd-111">tooconfigure RightAnswers ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a18bd-111">tooconfigure Azure AD integration with RightAnswers, you need hello following items:</span></span>

- <span data-ttu-id="a18bd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a18bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a18bd-113">Bir RightAnswers çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a18bd-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a18bd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a18bd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a18bd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a18bd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a18bd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a18bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a18bd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a18bd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a18bd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a18bd-118">Scenario description</span></span>
<span data-ttu-id="a18bd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a18bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a18bd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a18bd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a18bd-121">Merhaba Galerisi'nden RightAnswers ekleme</span><span class="sxs-lookup"><span data-stu-id="a18bd-121">Adding RightAnswers from hello gallery</span></span>
2. <span data-ttu-id="a18bd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a18bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-hello-gallery"></a><span data-ttu-id="a18bd-123">Merhaba Galerisi'nden RightAnswers ekleme</span><span class="sxs-lookup"><span data-stu-id="a18bd-123">Adding RightAnswers from hello gallery</span></span>
<span data-ttu-id="a18bd-124">Azure AD'ye tooconfigure hello tümleştirme RightAnswers, tooadd RightAnswers hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a18bd-124">tooconfigure hello integration of RightAnswers into Azure AD, you need tooadd RightAnswers from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a18bd-125">**tooadd RightAnswers hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a18bd-125">**tooadd RightAnswers from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18bd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a18bd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a18bd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a18bd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a18bd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a18bd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a18bd-133">Merhaba arama kutusuna yazın **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-133">In hello search box, type **RightAnswers**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="a18bd-135">Merhaba Sonuçlar panelinde seçin **RightAnswers**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a18bd-135">In hello results panel, select **RightAnswers**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a18bd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a18bd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a18bd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı RightAnswers ile test etme</span><span class="sxs-lookup"><span data-stu-id="a18bd-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a18bd-139">Tek toowork'ın oturum açma hangi hello karşılık gelen RightAnswers içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a18bd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RightAnswers is tooa user in Azure AD.</span></span> <span data-ttu-id="a18bd-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı RightAnswers hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a18bd-140">In other words, a link relationship between an Azure AD user and hello related user in RightAnswers needs toobe established.</span></span>

<span data-ttu-id="a18bd-141">Merhaba hello değeri RightAnswers içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a18bd-141">In RightAnswers, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a18bd-142">tooconfigure ve RightAnswers ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a18bd-142">tooconfigure and test Azure AD single sign-on with RightAnswers, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a18bd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a18bd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a18bd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a18bd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a18bd-145">**[RightAnswers test kullanıcısı oluşturma](#creating-a-rightanswers-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir RightAnswers içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a18bd-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - toohave a counterpart of Britta Simon in RightAnswers that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a18bd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a18bd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a18bd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a18bd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a18bd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a18bd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a18bd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma RightAnswers uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a18bd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="a18bd-150">**tooconfigure Azure AD çoklu oturum açma ile RightAnswers, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a18bd-150">**tooconfigure Azure AD single sign-on with RightAnswers, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18bd-151">Hello hello üzerinde Azure portal'ın **RightAnswers** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-151">In hello Azure portal, on hello **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a18bd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a18bd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="a18bd-155">Merhaba üzerinde **RightAnswers etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a18bd-155">On hello **RightAnswers Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="a18bd-157">a.</span><span class="sxs-lookup"><span data-stu-id="a18bd-157">a.</span></span> <span data-ttu-id="a18bd-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="a18bd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="a18bd-159">b.</span><span class="sxs-lookup"><span data-stu-id="a18bd-159">b.</span></span> <span data-ttu-id="a18bd-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="a18bd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a18bd-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a18bd-161">These values are not real.</span></span> <span data-ttu-id="a18bd-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a18bd-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a18bd-163">Kişi [RightAnswers istemci destek ekibi](https://www.rightanswers.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a18bd-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a18bd-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a18bd-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="a18bd-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a18bd-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a18bd-168">tooconfigure çoklu oturum açma üzerinde **RightAnswers** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[RightAnswers destek ekibi](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="a18bd-168">tooconfigure single sign-on on **RightAnswers** side, you need toosend hello downloaded **Metadata XML** too[RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="a18bd-169">RightAnswers destek ekibinize toodo hello gerçek SSO yapılandırmasına sahip.</span><span class="sxs-lookup"><span data-stu-id="a18bd-169">Your RightAnswers support team has toodo hello actual SSO configuration.</span></span>
    ><span data-ttu-id="a18bd-170">SSO, aboneliğiniz için etkinleştirildiğinde, bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a18bd-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="a18bd-171">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a18bd-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a18bd-172">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a18bd-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a18bd-173">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a18bd-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a18bd-174">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a18bd-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="a18bd-175">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a18bd-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a18bd-177">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a18bd-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18bd-178">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a18bd-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a18bd-180">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a18bd-182">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a18bd-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a18bd-184">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a18bd-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a18bd-186">a.</span><span class="sxs-lookup"><span data-stu-id="a18bd-186">a.</span></span> <span data-ttu-id="a18bd-187">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a18bd-188">b.</span><span class="sxs-lookup"><span data-stu-id="a18bd-188">b.</span></span> <span data-ttu-id="a18bd-189">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a18bd-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a18bd-190">c.</span><span class="sxs-lookup"><span data-stu-id="a18bd-190">c.</span></span> <span data-ttu-id="a18bd-191">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a18bd-192">d.</span><span class="sxs-lookup"><span data-stu-id="a18bd-192">d.</span></span> <span data-ttu-id="a18bd-193">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a18bd-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="a18bd-194">RightAnswers test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a18bd-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="a18bd-195">tooenable Azure AD kullanıcıların toolog tooRightAnswers bunların RightAnswers sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a18bd-195">tooenable Azure AD users toolog in tooRightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="a18bd-196">Bu yüzden, hiçbir eylem öğesi sağlama RightAnswers, otomatik bir görev olduğunda.</span><span class="sxs-lookup"><span data-stu-id="a18bd-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="a18bd-197">Kullanıcıları otomatik olarak hello ilk tek oturum açma girişimi sırasında gerekirse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a18bd-197">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="a18bd-198">API AAD kullanıcı hesaplarının RightAnswers tooprovision tarafından sağlanan veya herhangi diğer RightAnswers kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a18bd-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a18bd-199">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a18bd-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a18bd-200">Bu bölümde, erişim tooRightAnswers vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a18bd-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightAnswers.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a18bd-202">**tooassign Britta Simon tooRightAnswers hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a18bd-202">**tooassign Britta Simon tooRightAnswers, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18bd-203">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a18bd-205">Merhaba uygulamalar listesinde **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-205">In hello applications list, select **RightAnswers**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="a18bd-207">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a18bd-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a18bd-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a18bd-209">Click **Add** button.</span></span> <span data-ttu-id="a18bd-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a18bd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a18bd-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a18bd-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a18bd-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a18bd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a18bd-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a18bd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a18bd-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a18bd-215">Testing single sign-on</span></span>

<span data-ttu-id="a18bd-216">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="a18bd-216">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="a18bd-217">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a18bd-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="a18bd-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a18bd-218">Additional resources</span></span>

* [<span data-ttu-id="a18bd-219">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a18bd-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a18bd-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a18bd-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

