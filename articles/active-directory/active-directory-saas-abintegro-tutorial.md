---
title: "Öğretici: Azure Active Directory Tümleştirme ile Abintegro | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Abintegro arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 54e2865860940cab0c0ef31a496f42dd55b0e907
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="be883-103">Öğretici: Azure Active Directory Tümleştirme Abintegro ile</span><span class="sxs-lookup"><span data-stu-id="be883-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="be883-104">Bu öğreticide, bilgi nasıl toointegrate Abintegro Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be883-104">In this tutorial, you learn how toointegrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be883-105">Abintegro Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="be883-105">Integrating Abintegro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="be883-106">Erişim tooAbintegro sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="be883-106">You can control in Azure AD who has access tooAbintegro</span></span>
- <span data-ttu-id="be883-107">Kullanıcıların tooautomatically get açan tooAbintegro (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="be883-107">You can enable your users tooautomatically get signed-on tooAbintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be883-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="be883-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="be883-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be883-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be883-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="be883-110">Prerequisites</span></span>

<span data-ttu-id="be883-111">tooconfigure Abintegro ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="be883-111">tooconfigure Azure AD integration with Abintegro, you need hello following items:</span></span>

- <span data-ttu-id="be883-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="be883-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be883-113">Bir Abintegro çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="be883-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be883-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="be883-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be883-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="be883-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be883-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="be883-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be883-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be883-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be883-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="be883-118">Scenario description</span></span>
<span data-ttu-id="be883-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="be883-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be883-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="be883-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be883-121">Merhaba Galerisi'nden Abintegro ekleme</span><span class="sxs-lookup"><span data-stu-id="be883-121">Adding Abintegro from hello gallery</span></span>
2. <span data-ttu-id="be883-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="be883-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-hello-gallery"></a><span data-ttu-id="be883-123">Merhaba Galerisi'nden Abintegro ekleme</span><span class="sxs-lookup"><span data-stu-id="be883-123">Adding Abintegro from hello gallery</span></span>
<span data-ttu-id="be883-124">Azure AD'ye tooconfigure hello tümleştirme Abintegro, tooadd Abintegro hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="be883-124">tooconfigure hello integration of Abintegro into Azure AD, you need tooadd Abintegro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="be883-125">**tooadd Abintegro hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be883-125">**tooadd Abintegro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="be883-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="be883-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be883-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="be883-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="be883-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="be883-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="be883-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be883-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="be883-133">Merhaba arama kutusuna yazın **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="be883-133">In hello search box, type **Abintegro**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="be883-135">Merhaba Sonuçlar panelinde seçin **Abintegro**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="be883-135">In hello results panel, select **Abintegro**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be883-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="be883-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be883-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Abintegro ile test etme</span><span class="sxs-lookup"><span data-stu-id="be883-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be883-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Abintegro içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="be883-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Abintegro is tooa user in Azure AD.</span></span> <span data-ttu-id="be883-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Abintegro hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="be883-140">In other words, a link relationship between an Azure AD user and hello related user in Abintegro needs toobe established.</span></span>

<span data-ttu-id="be883-141">Merhaba hello değeri Abintegro içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="be883-141">In Abintegro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="be883-142">tooconfigure ve Abintegro ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="be883-142">tooconfigure and test Azure AD single sign-on with Abintegro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="be883-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="be883-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="be883-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="be883-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be883-145">**[Bir Abintegro test kullanıcısı oluşturma](#creating-an-abintegro-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Abintegro içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="be883-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - toohave a counterpart of Britta Simon in Abintegro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="be883-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="be883-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be883-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="be883-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be883-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="be883-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be883-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Abintegro uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be883-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="be883-150">**tooconfigure Azure AD çoklu oturum açma ile Abintegro, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be883-150">**tooconfigure Azure AD single sign-on with Abintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="be883-151">Hello hello üzerinde Azure portal'ın **Abintegro** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="be883-151">In hello Azure portal, on hello **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="be883-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="be883-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="be883-155">Merhaba üzerinde **Abintegro etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be883-155">On hello **Abintegro Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="be883-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="be883-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="be883-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="be883-158">This value is not real.</span></span> <span data-ttu-id="be883-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="be883-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="be883-160">Kişi [Abintegro istemci destek ekibi](mailto:support@abintegro.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="be883-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="be883-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be883-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="be883-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be883-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be883-165">tooconfigure çoklu oturum açma üzerinde **Abintegro** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Abintegro destek ekibi](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="be883-165">tooconfigure single sign-on on **Abintegro** side, you need toosend hello downloaded **Metadata XML** too[Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="be883-166">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="be883-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="be883-167">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="be883-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="be883-168">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="be883-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="be883-169">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be883-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be883-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be883-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="be883-171">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="be883-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="be883-173">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be883-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="be883-174">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="be883-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be883-176">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="be883-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be883-178">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="be883-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be883-180">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be883-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be883-182">a.</span><span class="sxs-lookup"><span data-stu-id="be883-182">a.</span></span> <span data-ttu-id="be883-183">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be883-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be883-184">b.</span><span class="sxs-lookup"><span data-stu-id="be883-184">b.</span></span> <span data-ttu-id="be883-185">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="be883-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be883-186">c.</span><span class="sxs-lookup"><span data-stu-id="be883-186">c.</span></span> <span data-ttu-id="be883-187">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="be883-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="be883-188">d.</span><span class="sxs-lookup"><span data-stu-id="be883-188">d.</span></span> <span data-ttu-id="be883-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be883-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="be883-190">Bir Abintegro test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be883-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="be883-191">TooAbintegro sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="be883-191">There is no action item for you tooconfigure user provisioning tooAbintegro.</span></span> <span data-ttu-id="be883-192">Atanmış bir kullanıcı hello erişim paneli kullanılarak Abintegro toolog çalıştığında Abintegro hello kullanıcı var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="be883-192">When an assigned user tries toolog into Abintegro using hello access panel, Abintegro checks whether hello user exists.</span></span>
  
<span data-ttu-id="be883-193">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Abintegro tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="be883-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="be883-194">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="be883-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="be883-195">Bu bölümde, erişim tooAbintegro vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="be883-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbintegro.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="be883-197">**tooassign Britta Simon tooAbintegro hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be883-197">**tooassign Britta Simon tooAbintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="be883-198">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="be883-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="be883-200">Merhaba uygulamalar listesinde **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="be883-200">In hello applications list, select **Abintegro**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="be883-202">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="be883-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="be883-204">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be883-204">Click **Add** button.</span></span> <span data-ttu-id="be883-205">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be883-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="be883-207">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="be883-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="be883-208">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be883-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be883-209">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be883-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be883-210">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="be883-210">Testing single sign-on</span></span>

<span data-ttu-id="be883-211">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="be883-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="be883-212">Merhaba Abintegro hello erişim paneli parçasında tıkladığınızda, oturum açma sayfasına Abintegro uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be883-212">When you click hello Abintegro tile in hello Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="be883-213">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be883-213">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="be883-214">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="be883-214">Additional resources</span></span>

* [<span data-ttu-id="be883-215">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="be883-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be883-216">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="be883-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

