---
title: "Öğretici: Azure Active Directory Tümleştirme ile & frankly | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasında ve & frankly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="8d9bd-103">Öğretici: Azure Active Directory Tümleştirme ile & frankly</span><span class="sxs-lookup"><span data-stu-id="8d9bd-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="8d9bd-104">Bu öğreticide, bilgi nasıl toointegrate & frankly Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d9bd-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d9bd-105">Tümleştirme & frankly Azure AD ile ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d9bd-106">Çok & frankly erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8d9bd-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="8d9bd-107">Kullanıcılarınızın tooautomatically alma açan çok & frankly etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="8d9bd-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d9bd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="8d9bd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d9bd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d9bd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d9bd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8d9bd-110">Prerequisites</span></span>

<span data-ttu-id="8d9bd-111">ile tooconfigure Azure AD tümleştirme & frankly, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="8d9bd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="8d9bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d9bd-113">A & frankly çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="8d9bd-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d9bd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d9bd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d9bd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d9bd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d9bd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d9bd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="8d9bd-118">Scenario description</span></span>
<span data-ttu-id="8d9bd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d9bd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d9bd-121">Ekleme & hello galerisinden frankly</span><span class="sxs-lookup"><span data-stu-id="8d9bd-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="8d9bd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8d9bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="8d9bd-123">Ekleme & hello galerisinden frankly</span><span class="sxs-lookup"><span data-stu-id="8d9bd-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="8d9bd-124">& Azure AD içine frankly tooconfigure hello tümleştirmesi, gereksinim duyduğunuz tooadd & frankly listesinden hello galeri tooyour yönetilen SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d9bd-125">**tooadd & frankly Galerisi'nden hello hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8d9bd-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d9bd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d9bd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d9bd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="8d9bd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="8d9bd-133">Merhaba arama kutusuna yazın **& frankly**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-133">In hello search box, type **&frankly**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="8d9bd-135">Merhaba Sonuçlar panelinde seçin **& frankly**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d9bd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="8d9bd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d9bd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile test & frankly "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="8d9bd-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d9bd-139">Tek toowork'ın oturum açma Azure AD ne karşılık gelen kullanıcı hello & frankly tooa kullanıcı Azure AD'de tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="8d9bd-140">Diğer bir deyişle, bir bağlantı arasındaki ilişki bir Azure AD kullanıcısının ve hello ilgili kullanıcı & frankly gereksinimlerini toobe kuruldu.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="8d9bd-141">Merhaba hello değerini de & frankly, Ata **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d9bd-142">tooconfigure ve Azure AD çoklu oturum açma ile & test frankly, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d9bd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d9bd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d9bd-145">**[Oluşturma bir & frankly test kullanıcısı](#creating-a-frankly-test-user)**  -toohave karşılık gelen Britta Simon & frankly diğer bir deyişle bağlantılı toohello Azure AD kullanıcı gösterimi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d9bd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d9bd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d9bd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8d9bd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d9bd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirme ve çoklu oturum açma, yapılandırma & frankly uygulama.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="8d9bd-150">**Azure AD tooconfigure tek ile oturum & frankly, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8d9bd-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d9bd-151">Hello hello üzerinde Azure portal'ın **& frankly** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="8d9bd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="8d9bd-155">Merhaba üzerinde **& frankly etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="8d9bd-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-157">a.</span></span> <span data-ttu-id="8d9bd-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="8d9bd-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="8d9bd-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-159">b.</span></span> <span data-ttu-id="8d9bd-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="8d9bd-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="8d9bd-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="8d9bd-162">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="8d9bd-164">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="8d9bd-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="8d9bd-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-165">These values are not real.</span></span> <span data-ttu-id="8d9bd-166">Bu değerleri ile Merhaba güncelleştirmek gerçek tanımlayıcısı, oturum açma ve yanıt URL'si.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="8d9bd-167">Kişi [andfrankly destek ekibi](mailto:help@andfrankly.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="8d9bd-168">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="8d9bd-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8d9bd-172">tooconfigure çoklu oturum açma üzerinde **& frankly** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[andfrankly destek ekibi](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="8d9bd-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8d9bd-173">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="8d9bd-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d9bd-174">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d9bd-175">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d9bd-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d9bd-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d9bd-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d9bd-177">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="8d9bd-179">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8d9bd-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d9bd-180">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d9bd-182">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d9bd-184">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d9bd-186">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8d9bd-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d9bd-188">a.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-188">a.</span></span> <span data-ttu-id="8d9bd-189">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d9bd-190">b.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-190">b.</span></span> <span data-ttu-id="8d9bd-191">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d9bd-192">c.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-192">c.</span></span> <span data-ttu-id="8d9bd-193">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d9bd-194">d.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-194">d.</span></span> <span data-ttu-id="8d9bd-195">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="8d9bd-196">Oluşturma bir & frankly test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="8d9bd-196">Creating a &frankly test user</span></span>

<span data-ttu-id="8d9bd-197">Bu bölümde, buna & frankly Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="8d9bd-198">Çalışmak [andfrankly destek ekibi](mailto:help@andfrankly.com) tooadd hello kullanıcılar hello & frankly platform.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d9bd-199">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="8d9bd-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d9bd-200">Bu bölümde, çok & frankly erişim vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="8d9bd-202">**tooassign Britta Simon çok & frankly, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="8d9bd-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d9bd-203">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="8d9bd-205">Merhaba uygulamalar listesinde **& frankly**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-205">In hello applications list, select **&frankly**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="8d9bd-207">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="8d9bd-209">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-209">Click **Add** button.</span></span> <span data-ttu-id="8d9bd-210">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="8d9bd-212">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d9bd-213">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d9bd-214">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d9bd-215">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="8d9bd-215">Testing single sign-on</span></span>

<span data-ttu-id="8d9bd-216">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8d9bd-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8d9bd-217">Frankly hello erişim paneli döşeme & hello'a tıklayın, otomatik olarak oturum açma tooyour almalısınız & frankly uygulama</span><span class="sxs-lookup"><span data-stu-id="8d9bd-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d9bd-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8d9bd-218">Additional resources</span></span>

* [<span data-ttu-id="8d9bd-219">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="8d9bd-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d9bd-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="8d9bd-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

