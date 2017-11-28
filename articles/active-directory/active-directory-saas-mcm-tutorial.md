---
title: "Öğretici: Azure Active Directory Tümleştirme ile MCM | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile MCM arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 6fbb3c641725bed1e7c73ee78129efb86979839e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="7c26b-103">Öğretici: Azure Active Directory Tümleştirme MCM ile</span><span class="sxs-lookup"><span data-stu-id="7c26b-103">Tutorial: Azure Active Directory integration with MCM</span></span>

<span data-ttu-id="7c26b-104">Bu öğreticide, bilgi nasıl toointegrate MCM Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c26b-104">In this tutorial, you learn how toointegrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c26b-105">MCM Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7c26b-105">Integrating MCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c26b-106">Erişim tooMCM sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c26b-106">You can control in Azure AD who has access tooMCM</span></span>
- <span data-ttu-id="7c26b-107">Kullanıcıların tooautomatically get açan tooMCM (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7c26b-107">You can enable your users tooautomatically get signed-on tooMCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c26b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7c26b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7c26b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c26b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c26b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c26b-110">Prerequisites</span></span>

<span data-ttu-id="7c26b-111">tooconfigure MCM ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c26b-111">tooconfigure Azure AD integration with MCM, you need hello following items:</span></span>

- <span data-ttu-id="7c26b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7c26b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c26b-113">Bir MCM çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7c26b-113">A MCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c26b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7c26b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c26b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c26b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c26b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7c26b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c26b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c26b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c26b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7c26b-118">Scenario description</span></span>
<span data-ttu-id="7c26b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7c26b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c26b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7c26b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c26b-121">Merhaba Galerisi'nden MCM ekleme</span><span class="sxs-lookup"><span data-stu-id="7c26b-121">Adding MCM from hello gallery</span></span>
2. <span data-ttu-id="7c26b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c26b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-hello-gallery"></a><span data-ttu-id="7c26b-123">Merhaba Galerisi'nden MCM ekleme</span><span class="sxs-lookup"><span data-stu-id="7c26b-123">Adding MCM from hello gallery</span></span>
<span data-ttu-id="7c26b-124">Azure AD'ye tooconfigure hello tümleştirme MCM, tooadd MCM hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c26b-124">tooconfigure hello integration of MCM into Azure AD, you need tooadd MCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c26b-125">**tooadd MCM hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c26b-125">**tooadd MCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c26b-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c26b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c26b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c26b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7c26b-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c26b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7c26b-133">Merhaba arama kutusuna yazın **MCM**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-133">In hello search box, type **MCM**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_search.png)

5. <span data-ttu-id="7c26b-135">Merhaba Sonuçlar panelinde seçin **MCM**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7c26b-135">In hello results panel, select **MCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c26b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7c26b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c26b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı MCM sınayın.</span><span class="sxs-lookup"><span data-stu-id="7c26b-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c26b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen MCM içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c26b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MCM is tooa user in Azure AD.</span></span> <span data-ttu-id="7c26b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı MCM hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c26b-140">In other words, a link relationship between an Azure AD user and hello related user in MCM needs toobe established.</span></span>

<span data-ttu-id="7c26b-141">Merhaba hello değeri MCM içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7c26b-141">In MCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7c26b-142">tooconfigure ve MCM ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c26b-142">tooconfigure and test Azure AD single sign-on with MCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c26b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7c26b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c26b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7c26b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c26b-145">**[Test kullanıcı bir MCM oluşturma](#creating-a-mcm-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir MCM içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7c26b-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - toohave a counterpart of Britta Simon in MCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c26b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c26b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c26b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c26b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c26b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7c26b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c26b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma MCM uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7c26b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="7c26b-150">**tooconfigure Azure AD çoklu oturum açma ile MCM, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c26b-150">**tooconfigure Azure AD single sign-on with MCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c26b-151">Hello hello üzerinde Azure portal'ın **MCM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-151">In hello Azure portal, on hello **MCM** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7c26b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7c26b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_samlbase.png)

3. <span data-ttu-id="7c26b-155">Merhaba üzerinde **MCM etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c26b-155">On hello **MCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_url.png)

    <span data-ttu-id="7c26b-157">a.</span><span class="sxs-lookup"><span data-stu-id="7c26b-157">a.</span></span> <span data-ttu-id="7c26b-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://myaba.co.uk/client-access/<companyname>/saml.php`</span><span class="sxs-lookup"><span data-stu-id="7c26b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span></span>

    <span data-ttu-id="7c26b-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c26b-159">b.</span></span> <span data-ttu-id="7c26b-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://myaba.co.uk/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="7c26b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://myaba.co.uk/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c26b-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7c26b-161">These values are not real.</span></span> <span data-ttu-id="7c26b-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7c26b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7c26b-163">Kişi [MCM istemci destek ekibi](http://mcmtechnology.com/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7c26b-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="7c26b-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7c26b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_certificate.png) 

5. <span data-ttu-id="7c26b-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c26b-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mcm-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="7c26b-168">tooconfigure çoklu oturum açma üzerinde **MCM** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[MCM destek ekibi](http://mcmtechnology.com/support/).</span><span class="sxs-lookup"><span data-stu-id="7c26b-168">tooconfigure single sign-on on **MCM** side, you need toosend hello downloaded **Metadata XML** too[MCM support team](http://mcmtechnology.com/support/).</span></span> <span data-ttu-id="7c26b-169">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7c26b-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7c26b-170">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7c26b-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7c26b-171">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7c26b-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7c26b-172">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c26b-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c26b-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c26b-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c26b-174">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7c26b-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7c26b-176">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c26b-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c26b-177">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7c26b-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mcm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c26b-179">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mcm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c26b-181">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c26b-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mcm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c26b-183">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c26b-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mcm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c26b-185">a.</span><span class="sxs-lookup"><span data-stu-id="7c26b-185">a.</span></span> <span data-ttu-id="7c26b-186">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c26b-187">b.</span><span class="sxs-lookup"><span data-stu-id="7c26b-187">b.</span></span> <span data-ttu-id="7c26b-188">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7c26b-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c26b-189">c.</span><span class="sxs-lookup"><span data-stu-id="7c26b-189">c.</span></span> <span data-ttu-id="7c26b-190">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7c26b-191">d.</span><span class="sxs-lookup"><span data-stu-id="7c26b-191">d.</span></span> <span data-ttu-id="7c26b-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c26b-192">Click **Create**.</span></span>
 
### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="7c26b-193">MCM test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c26b-193">Creating a MCM test user</span></span>

<span data-ttu-id="7c26b-194">Bu bölümde, MCM içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c26b-194">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="7c26b-195">Çalışmak [MCM destek ekibi](http://mcmtechnology.com/support/) tooadd hello kullanıcılar hello MCM Platform.</span><span class="sxs-lookup"><span data-stu-id="7c26b-195">Work with [MCM support team](http://mcmtechnology.com/support/) tooadd hello users in hello MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="7c26b-196">API AAD kullanıcı hesaplarının MCM tooprovision tarafından sağlanan veya herhangi diğer MCM kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c26b-196">You can use any other MCM user account creation tools or APIs provided by MCM tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7c26b-197">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7c26b-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7c26b-198">Bu bölümde, erişim tooMCM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c26b-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMCM.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7c26b-200">**tooassign Britta Simon tooMCM hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7c26b-200">**tooassign Britta Simon tooMCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c26b-201">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7c26b-203">Merhaba uygulamalar listesinde **MCM**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-203">In hello applications list, select **MCM**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_app.png) 

3. <span data-ttu-id="7c26b-205">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7c26b-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7c26b-207">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7c26b-207">Click **Add** button.</span></span> <span data-ttu-id="7c26b-208">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c26b-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7c26b-210">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7c26b-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c26b-211">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c26b-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c26b-212">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7c26b-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c26b-213">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7c26b-213">Testing single sign-on</span></span>

<span data-ttu-id="7c26b-214">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7c26b-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7c26b-215">MCM döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma tooyour MCM uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c26b-215">When you click hello MCM tile in hello Access Panel, you should get automatically signed-on tooyour MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c26b-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7c26b-216">Additional resources</span></span>

* [<span data-ttu-id="7c26b-217">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7c26b-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c26b-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7c26b-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_203.png

