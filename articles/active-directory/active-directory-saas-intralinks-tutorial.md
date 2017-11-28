---
title: "Öğretici: Azure Active Directory Tümleştirme ile Intralinks | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Intralinks arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="9d805-103">Öğretici: Azure Active Directory Tümleştirme Intralinks ile</span><span class="sxs-lookup"><span data-stu-id="9d805-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="9d805-104">Bu öğreticide, bilgi nasıl toointegrate Intralinks Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d805-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d805-105">Intralinks Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9d805-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d805-106">Erişim tooIntralinks sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9d805-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="9d805-107">Kullanıcıların tooautomatically get açan tooIntralinks (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9d805-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d805-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9d805-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9d805-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d805-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d805-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d805-110">Prerequisites</span></span>

<span data-ttu-id="9d805-111">tooconfigure Intralinks ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d805-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="9d805-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9d805-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d805-113">Bir Intralinks çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="9d805-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d805-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9d805-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d805-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d805-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d805-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9d805-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d805-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d805-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d805-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9d805-118">Scenario description</span></span>
<span data-ttu-id="9d805-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9d805-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d805-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9d805-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d805-121">Merhaba Galerisi'nden Intralinks ekleme</span><span class="sxs-lookup"><span data-stu-id="9d805-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="9d805-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9d805-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="9d805-123">Merhaba Galerisi'nden Intralinks ekleme</span><span class="sxs-lookup"><span data-stu-id="9d805-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="9d805-124">Azure AD'ye tooconfigure hello tümleştirme Intralinks, tooadd Intralinks hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d805-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d805-125">**tooadd Intralinks hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9d805-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d805-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d805-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9d805-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d805-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9d805-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9d805-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9d805-133">Merhaba arama kutusuna yazın **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="9d805-133">In hello search box, type **Intralinks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="9d805-135">Merhaba Sonuçlar panelinde seçin **Intralinks**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9d805-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d805-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9d805-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d805-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Intralinks sınayın.</span><span class="sxs-lookup"><span data-stu-id="9d805-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d805-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Intralinks içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d805-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="9d805-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Intralinks hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d805-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="9d805-141">Merhaba hello değeri Intralinks içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="9d805-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9d805-142">tooconfigure ve Intralinks ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d805-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d805-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="9d805-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d805-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="9d805-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d805-145">**[Bir Intralinks test kullanıcısı oluşturma](#creating-an-intralinks-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Intralinks içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="9d805-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d805-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9d805-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d805-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="9d805-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d805-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9d805-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d805-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Intralinks uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9d805-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="9d805-150">**tooconfigure Azure AD çoklu oturum açma ile Intralinks, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9d805-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d805-151">Hello hello üzerinde Azure portal'ın **Intralinks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9d805-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9d805-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9d805-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="9d805-155">Merhaba üzerinde **Intralinks etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9d805-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="9d805-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="9d805-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d805-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="9d805-158">This value is not real.</span></span> <span data-ttu-id="9d805-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="9d805-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9d805-160">Kişi [Intralinks istemci destek ekibi](https://www.intralinks.com/contact-1) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="9d805-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="9d805-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9d805-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="9d805-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d805-165">tooconfigure çoklu oturum açma üzerinde **Intralinks** yan, indirilen toosend hello ihtiyacınız **meta veri XML** [Intralinks destek ekibi](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="9d805-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="9d805-166">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9d805-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9d805-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9d805-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9d805-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="9d805-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9d805-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d805-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d805-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d805-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d805-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9d805-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9d805-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9d805-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d805-174">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d805-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9d805-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d805-178">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="9d805-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d805-180">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9d805-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d805-182">a.</span><span class="sxs-lookup"><span data-stu-id="9d805-182">a.</span></span> <span data-ttu-id="9d805-183">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d805-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d805-184">b.</span><span class="sxs-lookup"><span data-stu-id="9d805-184">b.</span></span> <span data-ttu-id="9d805-185">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9d805-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d805-186">c.</span><span class="sxs-lookup"><span data-stu-id="9d805-186">c.</span></span> <span data-ttu-id="9d805-187">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9d805-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9d805-188">d.</span><span class="sxs-lookup"><span data-stu-id="9d805-188">d.</span></span> <span data-ttu-id="9d805-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9d805-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="9d805-190">Bir Intralinks test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d805-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="9d805-191">Bu bölümde, Intralinks içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d805-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="9d805-192">Lütfen çalışmak [Intralinks destek ekibi](https://www.intralinks.com/contact-1) tooadd hello kullanıcılar hello Intralinks Platform.</span><span class="sxs-lookup"><span data-stu-id="9d805-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9d805-193">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9d805-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9d805-194">Bu bölümde, erişim tooIntralinks vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d805-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9d805-196">**tooassign Britta Simon tooIntralinks hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9d805-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d805-197">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9d805-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9d805-199">Merhaba uygulamalar listesinde **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="9d805-199">In hello applications list, select **Intralinks**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="9d805-201">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9d805-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9d805-203">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-203">Click **Add** button.</span></span> <span data-ttu-id="9d805-204">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9d805-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9d805-206">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9d805-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d805-207">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9d805-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d805-208">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9d805-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="9d805-209">Intralinks aracılığıyla veya Elite uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="9d805-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="9d805-210">Intralinks kullandığı anlaşma Nexus uygulama hariç tüm diğer Intralinks uygulamalar için aynı SSO kimlik platformu hello.</span><span class="sxs-lookup"><span data-stu-id="9d805-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="9d805-211">Başka bir Intralinks uygulama toouse düşünüyorsanız, bu nedenle daha sonra ilk tooconfigure SSO yukarıda açıklanan hello yordamı kullanarak birincil Intralinks uygulama için gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d805-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="9d805-212">Bundan sonra yordamı tooadd aşağıda hello başka bir Intralinks uygulama kiracınızda hangi birincil bu uygulama için SSO yararlanabilirsiniz izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d805-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="9d805-213">Bu özellik kullanılabilir yalnızca tooAzure AD Premium SKU müşterileri içindir ve ücretsiz veya temel SKU müşteriler için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9d805-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="9d805-214">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="9d805-216">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9d805-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d805-217">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9d805-217">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9d805-219">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9d805-221">Merhaba arama kutusuna yazın **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="9d805-221">In hello search box, type **Intralinks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="9d805-223">Üzerinde **uygulama Intralinks Ekle** hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9d805-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Intralinks aracılığıyla veya Elite uygulama ekleme](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="9d805-225">a.</span><span class="sxs-lookup"><span data-stu-id="9d805-225">a.</span></span> <span data-ttu-id="9d805-226">İçinde **adı** metin kutusuna, uygun Merhaba uygulaması örneğin adını **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="9d805-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="9d805-227">b.</span><span class="sxs-lookup"><span data-stu-id="9d805-227">b.</span></span> <span data-ttu-id="9d805-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="9d805-229">Hello hello üzerinde Azure portal'ın **Intralinks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9d805-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

7. <span data-ttu-id="9d805-231">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **bağlantılı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9d805-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="9d805-233">Merhaba hello SP başlatılan SSO URL'den al [Intralinks takım](https://www.intralinks.com/contact-1) hello diğer Intralinks uygulama ve içinde girin **yapılandırma oturum açma URL'si** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="9d805-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="9d805-235">Merhaba oturum üzerinde URL'si metin kutusuna desen aşağıdaki hello kullanarak kullanıcıların toosign üzerinde tooyour Intralinks uygulamanız tarafından kullanılan hello URL'yi yazın:</span><span class="sxs-lookup"><span data-stu-id="9d805-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="9d805-236">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d805-236">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="9d805-238">Merhaba bölümünde gösterildiği gibi Hello uygulama toouser veya grupları atama ** [atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="9d805-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="9d805-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9d805-239">Testing single sign-on</span></span>

<span data-ttu-id="9d805-240">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9d805-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d805-241">Hello erişim paneli Intralinks döşeme hello tıkladığınızda, otomatik olarak oturum açma Intralinks uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d805-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="9d805-242">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d805-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d805-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9d805-243">Additional resources</span></span>

* [<span data-ttu-id="9d805-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9d805-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d805-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9d805-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

