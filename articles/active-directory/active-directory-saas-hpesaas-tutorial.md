---
title: "Öğretici: Azure Active Directory Tümleştirme ile HPE SaaS | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile HPE SaaS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 7a846fb2298e51d249f4a406527130828bf7bbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="8e626-103">Öğretici: Azure Active Directory Tümleştirme HPE SaaS ile</span><span class="sxs-lookup"><span data-stu-id="8e626-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="8e626-104">Bu öğreticide, bilgi nasıl toointegrate HPE SaaS Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e626-104">In this tutorial, you learn how toointegrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e626-105">Azure AD ile HPE SaaS tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8e626-105">Integrating HPE SaaS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e626-106">Erişim tooHPE SaaS sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8e626-106">You can control in Azure AD who has access tooHPE SaaS</span></span>
- <span data-ttu-id="8e626-107">Kullanıcıların tooautomatically get açan tooHPE SaaS (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8e626-107">You can enable your users tooautomatically get signed-on tooHPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e626-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8e626-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e626-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e626-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e626-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8e626-110">Prerequisites</span></span>

<span data-ttu-id="8e626-111">tooconfigure HPE SaaS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8e626-111">tooconfigure Azure AD integration with HPE SaaS, you need hello following items:</span></span>

- <span data-ttu-id="8e626-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8e626-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e626-113">Bir HPE SaaS çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="8e626-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e626-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8e626-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e626-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8e626-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e626-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8e626-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e626-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e626-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e626-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8e626-118">Scenario description</span></span>
<span data-ttu-id="8e626-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8e626-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e626-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8e626-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e626-121">Merhaba Galerisi'nden HPE SaaS ekleme</span><span class="sxs-lookup"><span data-stu-id="8e626-121">Adding HPE SaaS from hello gallery</span></span>
2. <span data-ttu-id="8e626-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8e626-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-hello-gallery"></a><span data-ttu-id="8e626-123">Merhaba Galerisi'nden HPE SaaS ekleme</span><span class="sxs-lookup"><span data-stu-id="8e626-123">Adding HPE SaaS from hello gallery</span></span>
<span data-ttu-id="8e626-124">Azure AD'ye tooconfigure hello tümleştirme HPE SaaS, tooadd HPE SaaS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e626-124">tooconfigure hello integration of HPE SaaS into Azure AD, you need tooadd HPE SaaS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e626-125">**tooadd HPE SaaS hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8e626-125">**tooadd HPE SaaS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e626-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8e626-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e626-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8e626-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e626-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8e626-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8e626-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8e626-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8e626-133">Merhaba arama kutusuna yazın **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="8e626-133">In hello search box, type **HPE SaaS**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="8e626-135">Merhaba Sonuçlar panelinde seçin **HPE SaaS**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8e626-135">In hello results panel, select **HPE SaaS**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e626-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8e626-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e626-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma HPE "Britta Simon" adlı bir test kullanıcı tabanlı SaaS ile test etme.</span><span class="sxs-lookup"><span data-stu-id="8e626-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e626-139">Tek toowork'ın oturum açma hangi hello karşılık gelen HPE SaaS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e626-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HPE SaaS is tooa user in Azure AD.</span></span> <span data-ttu-id="8e626-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı HPE SaaS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e626-140">In other words, a link relationship between an Azure AD user and hello related user in HPE SaaS needs toobe established.</span></span>

<span data-ttu-id="8e626-141">Merhaba hello değeri HPE SaaS içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="8e626-141">In HPE SaaS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e626-142">tooconfigure ve HPE SaaS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8e626-142">tooconfigure and test Azure AD single sign-on with HPE SaaS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e626-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8e626-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e626-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8e626-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e626-145">**[Bir HPE SaaS test kullanıcısı oluşturma](#creating-an-hpe-saas-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir HPE SaaS içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="8e626-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - toohave a counterpart of Britta Simon in HPE SaaS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e626-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8e626-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e626-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8e626-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e626-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8e626-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e626-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma HPE SaaS uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8e626-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="8e626-150">**tooconfigure Azure AD çoklu oturum açma HPE SaaS ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8e626-150">**tooconfigure Azure AD single sign-on with HPE SaaS, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e626-151">Hello hello üzerinde Azure portal'ın **HPE SaaS** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8e626-151">In hello Azure portal, on hello **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8e626-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8e626-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="8e626-155">Merhaba üzerinde **HPE SaaS etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8e626-155">On hello **HPE SaaS Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="8e626-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e626-157">a.</span></span> <span data-ttu-id="8e626-158">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="8e626-158">In hello **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="8e626-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e626-159">b.</span></span> <span data-ttu-id="8e626-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="8e626-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e626-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8e626-161">These values are not real.</span></span> <span data-ttu-id="8e626-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8e626-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8e626-163">Kişi [HPE SaaS istemci destek ekibi](https://saas.hpe.com/en-us/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="8e626-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="8e626-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8e626-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="8e626-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8e626-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e626-168">tooconfigure çoklu oturum açma üzerinde **HPE SaaS** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[HPE SaaS destek ekibi](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="8e626-168">tooconfigure single sign-on on **HPE SaaS** side, you need toosend hello downloaded **Metadata XML** too[HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="8e626-169">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8e626-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8e626-170">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8e626-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e626-171">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="8e626-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e626-172">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e626-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e626-173">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e626-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e626-174">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="8e626-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8e626-176">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8e626-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e626-177">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8e626-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e626-179">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8e626-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e626-181">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="8e626-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e626-183">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8e626-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e626-185">a.</span><span class="sxs-lookup"><span data-stu-id="8e626-185">a.</span></span> <span data-ttu-id="8e626-186">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e626-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e626-187">b.</span><span class="sxs-lookup"><span data-stu-id="8e626-187">b.</span></span> <span data-ttu-id="8e626-188">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8e626-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e626-189">c.</span><span class="sxs-lookup"><span data-stu-id="8e626-189">c.</span></span> <span data-ttu-id="8e626-190">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8e626-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e626-191">d.</span><span class="sxs-lookup"><span data-stu-id="8e626-191">d.</span></span> <span data-ttu-id="8e626-192">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8e626-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="8e626-193">Bir HPE SaaS test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e626-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="8e626-194">Bu bölümde Hello amacı toocreate HPE SaaS Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="8e626-194">hello objective of this section is toocreate a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="8e626-195">Lütfen çalışmak [HPE SaaS destek ekibi](https://saas.hpe.com/en-us/contact) hello HPE SaaS hesap tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="8e626-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) tooadd hello users in hello HPE SaaS account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e626-196">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8e626-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e626-197">Bu bölümde, erişim tooHPE SaaS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8e626-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHPE SaaS.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8e626-199">**tooassign Britta Simon tooHPE SaaS, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8e626-199">**tooassign Britta Simon tooHPE SaaS, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e626-200">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8e626-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8e626-202">Merhaba uygulamalar listesinde **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="8e626-202">In hello applications list, select **HPE SaaS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="8e626-204">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8e626-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8e626-206">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8e626-206">Click **Add** button.</span></span> <span data-ttu-id="8e626-207">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8e626-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8e626-209">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8e626-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e626-210">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8e626-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e626-211">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8e626-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e626-212">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8e626-212">Testing single sign-on</span></span>

<span data-ttu-id="8e626-213">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="8e626-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e626-214">Merhaba erişim paneli HPE SaaS döşeme hello tıkladığınızda, otomatik olarak oturum açma HPE SaaS uygulamasına tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e626-214">When you click hello HPE SaaS tile in hello Access Panel, you should get automatically signed-on tooyour HPE SaaS application.</span></span>
<span data-ttu-id="8e626-215">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e626-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e626-216">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8e626-216">Additional resources</span></span>

* [<span data-ttu-id="8e626-217">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8e626-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e626-218">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8e626-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

