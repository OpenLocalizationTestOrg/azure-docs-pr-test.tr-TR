---
title: "Öğretici: Azure Active Directory Tümleştirme ile CS yıldız | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve CS yıldız arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: d84533e8a7e9bca2f7bdf4be7f3050bca2f18496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="81d5a-103">Öğretici: Azure Active Directory Tümleştirme CS yıldız ile</span><span class="sxs-lookup"><span data-stu-id="81d5a-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="81d5a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile nasıl toointegrate CS yıldız öğrenin.</span><span class="sxs-lookup"><span data-stu-id="81d5a-104">In this tutorial, you learn how toointegrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81d5a-105">CS yıldız Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="81d5a-105">Integrating CS Stars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81d5a-106">Erişimi olan Azure AD'de denetim tooCS yıldız</span><span class="sxs-lookup"><span data-stu-id="81d5a-106">You can control in Azure AD who has access tooCS Stars</span></span>
- <span data-ttu-id="81d5a-107">Kullanıcıların tooautomatically etkinleştirebilirsiniz kendi Azure AD hesapları ile oturum açma tooCS yıldız (çoklu oturum açma) Al</span><span class="sxs-lookup"><span data-stu-id="81d5a-107">You can enable your users tooautomatically get signed-on tooCS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81d5a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="81d5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="81d5a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81d5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81d5a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="81d5a-110">Prerequisites</span></span>

<span data-ttu-id="81d5a-111">tooconfigure CS yıldız ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="81d5a-111">tooconfigure Azure AD integration with CS Stars, you need hello following items:</span></span>

- <span data-ttu-id="81d5a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="81d5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81d5a-113">Bir CS yıldız çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="81d5a-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81d5a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="81d5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81d5a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="81d5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81d5a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="81d5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81d5a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81d5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81d5a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="81d5a-118">Scenario description</span></span>
<span data-ttu-id="81d5a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="81d5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81d5a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="81d5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81d5a-121">CS yıldız hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="81d5a-121">Adding CS Stars from hello gallery</span></span>
2. <span data-ttu-id="81d5a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="81d5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-hello-gallery"></a><span data-ttu-id="81d5a-123">CS yıldız hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="81d5a-123">Adding CS Stars from hello gallery</span></span>
<span data-ttu-id="81d5a-124">Azure AD'ye tooconfigure hello tümleştirme CS yıldız tooadd CS yıldız hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="81d5a-124">tooconfigure hello integration of CS Stars into Azure AD, you need tooadd CS Stars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81d5a-125">**tooadd CS yıldız hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81d5a-125">**tooadd CS Stars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d5a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="81d5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81d5a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81d5a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="81d5a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81d5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="81d5a-133">Merhaba arama kutusuna yazın **CS yıldız**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-133">In hello search box, type **CS Stars**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="81d5a-135">Merhaba Sonuçlar panelinde seçin **CS yıldız**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="81d5a-135">In hello results panel, select **CS Stars**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81d5a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="81d5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81d5a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma CS "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı yıldız ile test etme</span><span class="sxs-lookup"><span data-stu-id="81d5a-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81d5a-139">Tek toowork'ın oturum açma, Azure AD CS yıldız hangi hello karşılık gelen kullanıcı tooa kullanıcıdır tooknow Azure AD gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="81d5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CS Stars is tooa user in Azure AD.</span></span> <span data-ttu-id="81d5a-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı CS yıldız arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="81d5a-140">In other words, a link relationship between an Azure AD user and hello related user in CS Stars needs toobe established.</span></span>

<span data-ttu-id="81d5a-141">CS yıldızları hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="81d5a-141">In CS Stars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="81d5a-142">tooconfigure ve CS yıldız ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="81d5a-142">tooconfigure and test Azure AD single sign-on with CS Stars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81d5a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="81d5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81d5a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="81d5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81d5a-145">**[CS yıldız test kullanıcısı oluşturma](#creating-a-cs-stars-test-user)**  -toohave Britta Simon kullanıcı gösterimidir bağlantılı toohello Azure AD CS yıldız içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="81d5a-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - toohave a counterpart of Britta Simon in CS Stars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="81d5a-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="81d5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81d5a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="81d5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81d5a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="81d5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81d5a-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma CS yıldız uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81d5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="81d5a-150">**tooconfigure Azure AD çoklu oturum açma CS yıldız ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81d5a-150">**tooconfigure Azure AD single sign-on with CS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d5a-151">Merhaba hello üzerinde Azure portal'ın **CS yıldız** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-151">In hello Azure portal, on hello **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="81d5a-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="81d5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="81d5a-155">Merhaba üzerinde **CS yıldız etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="81d5a-155">On hello **CS Stars Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="81d5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="81d5a-157">a.</span></span> <span data-ttu-id="81d5a-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="81d5a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="81d5a-159">b.</span><span class="sxs-lookup"><span data-stu-id="81d5a-159">b.</span></span> <span data-ttu-id="81d5a-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="81d5a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81d5a-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="81d5a-161">These values are not real.</span></span> <span data-ttu-id="81d5a-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="81d5a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="81d5a-163">Kişi [CS yıldız istemci destek ekibi](http://www.marshclearsight.com/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="81d5a-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="81d5a-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="81d5a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="81d5a-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81d5a-166">Click **Save** button.</span></span>

    <span data-ttu-id="81d5a-167">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="81d5a-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="81d5a-168">tooconfigure çoklu oturum açma üzerinde **CS yıldız** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[CS yıldız destek ekibi](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="81d5a-168">tooconfigure single sign-on on **CS Stars** side, you need toosend hello downloaded **Metadata XML** too[CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="81d5a-169">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="81d5a-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81d5a-170">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="81d5a-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81d5a-171">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81d5a-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81d5a-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="81d5a-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="81d5a-173">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="81d5a-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="81d5a-175">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="81d5a-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d5a-176">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="81d5a-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81d5a-178">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81d5a-180">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="81d5a-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81d5a-182">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="81d5a-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81d5a-184">a.</span><span class="sxs-lookup"><span data-stu-id="81d5a-184">a.</span></span> <span data-ttu-id="81d5a-185">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81d5a-186">b.</span><span class="sxs-lookup"><span data-stu-id="81d5a-186">b.</span></span> <span data-ttu-id="81d5a-187">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="81d5a-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81d5a-188">c.</span><span class="sxs-lookup"><span data-stu-id="81d5a-188">c.</span></span> <span data-ttu-id="81d5a-189">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81d5a-190">d.</span><span class="sxs-lookup"><span data-stu-id="81d5a-190">d.</span></span> <span data-ttu-id="81d5a-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81d5a-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="81d5a-192">CS yıldız test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="81d5a-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="81d5a-193">Bu bölümde Hello amacı toocreate Britta Simon CS yıldızları adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="81d5a-193">hello objective of this section is toocreate a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="81d5a-194">tooget CS yıldızları oluşturulan bir kullanıcı, gereksinim duyduğunuz toocontact, [CS yıldız destek ekibi](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="81d5a-194">tooget a user created in CS Stars, you need toocontact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81d5a-195">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="81d5a-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81d5a-196">Bu bölümde, tooCS yıldız erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="81d5a-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCS Stars.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="81d5a-198">**Yıldız, tooassign Britta Simon tooCS gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="81d5a-198">**tooassign Britta Simon tooCS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="81d5a-199">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="81d5a-201">Merhaba uygulamalar listesinde **CS yıldız**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-201">In hello applications list, select **CS Stars**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="81d5a-203">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="81d5a-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="81d5a-205">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="81d5a-205">Click **Add** button.</span></span> <span data-ttu-id="81d5a-206">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="81d5a-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="81d5a-208">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="81d5a-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81d5a-209">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="81d5a-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81d5a-210">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="81d5a-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81d5a-211">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="81d5a-211">Testing single sign-on</span></span>

<span data-ttu-id="81d5a-212">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="81d5a-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="81d5a-213">CS yıldız hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak oturum açma CS yıldız uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="81d5a-213">When you click hello CS Stars tile in hello Access Panel, you should get automatically signed-on tooyour CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="81d5a-214">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="81d5a-214">Additional resources</span></span>

* [<span data-ttu-id="81d5a-215">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="81d5a-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81d5a-216">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="81d5a-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

