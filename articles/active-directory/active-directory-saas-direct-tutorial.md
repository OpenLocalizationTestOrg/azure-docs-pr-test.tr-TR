---
title: "Öğretici: Azure Active Directory Tümleştirme ile doğrudan | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin ve doğrudan Azure Active Directory arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="f9c69-103">Öğretici: Azure Active Directory Tümleştirme ile doğrudan</span><span class="sxs-lookup"><span data-stu-id="f9c69-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="f9c69-104">Bu öğreticide, bilgi nasıl toointegrate doğrudan Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9c69-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9c69-105">Doğrudan Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f9c69-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f9c69-106">Erişim tooDirect sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f9c69-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="f9c69-107">Kullanıcıların tooautomatically get açan tooDirect (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f9c69-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9c69-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f9c69-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f9c69-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9c69-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9c69-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9c69-110">Prerequisites</span></span>

<span data-ttu-id="f9c69-111">Azure AD tümleştirme tooconfigure Direct ile aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9c69-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="f9c69-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f9c69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9c69-113">Bir doğrudan çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f9c69-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9c69-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f9c69-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9c69-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9c69-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9c69-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f9c69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9c69-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9c69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9c69-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f9c69-118">Scenario description</span></span>
<span data-ttu-id="f9c69-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f9c69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9c69-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f9c69-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9c69-121">Doğrudan hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="f9c69-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="f9c69-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f9c69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="f9c69-123">Doğrudan hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="f9c69-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="f9c69-124">Azure AD'ye tooconfigure hello tümleştirme doğrudan tooadd doğrudan hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9c69-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f9c69-125">**tooadd doğrudan hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9c69-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f9c69-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f9c69-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9c69-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f9c69-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f9c69-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9c69-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f9c69-133">Merhaba arama kutusuna yazın **doğrudan**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-133">In hello search box, type **Direct**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="f9c69-135">Merhaba Sonuçlar panelinde seçin **doğrudan**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f9c69-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9c69-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f9c69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9c69-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile doğrudan "Britta Simon." olarak adlandırılan bir test kullanıcı dayalı test etme</span><span class="sxs-lookup"><span data-stu-id="f9c69-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9c69-139">Tek toowork'ın oturum açma hangi hello karşılık gelen, doğrudan tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9c69-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="f9c69-140">Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili kurulan doğrudan gereksinimlerini toobe içinde.</span><span class="sxs-lookup"><span data-stu-id="f9c69-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="f9c69-141">Merhaba hello değeri doğrudan içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f9c69-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f9c69-142">tooconfigure ve test Azure AD çoklu oturum açma Direct ile yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f9c69-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f9c69-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f9c69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f9c69-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f9c69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9c69-145">**[Doğrudan test kullanıcısı oluşturma](#creating-a-direct-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir doğrudan içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f9c69-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9c69-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f9c69-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9c69-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f9c69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9c69-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f9c69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9c69-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma doğrudan uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f9c69-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="f9c69-150">**Azure AD çoklu oturum açma tooconfigure doğrudan ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9c69-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="f9c69-151">Hello hello üzerinde Azure portal'ın **doğrudan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f9c69-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f9c69-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="f9c69-155">Merhaba üzerinde **doğrudan etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="f9c69-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="f9c69-157">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="f9c69-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="f9c69-158">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="f9c69-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="f9c69-160">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL'si:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="f9c69-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="f9c69-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f9c69-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="f9c69-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9c69-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f9c69-165">tooconfigure çoklu oturum açma üzerinde **doğrudan** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[doğrudan destek ekibi](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="f9c69-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="f9c69-166">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f9c69-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f9c69-167">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f9c69-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f9c69-168">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9c69-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9c69-169">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9c69-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9c69-170">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f9c69-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f9c69-172">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9c69-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f9c69-173">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f9c69-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9c69-175">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9c69-177">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9c69-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9c69-179">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f9c69-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9c69-181">a.</span><span class="sxs-lookup"><span data-stu-id="f9c69-181">a.</span></span> <span data-ttu-id="f9c69-182">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9c69-183">b.</span><span class="sxs-lookup"><span data-stu-id="f9c69-183">b.</span></span> <span data-ttu-id="f9c69-184">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f9c69-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9c69-185">c.</span><span class="sxs-lookup"><span data-stu-id="f9c69-185">c.</span></span> <span data-ttu-id="f9c69-186">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f9c69-187">d.</span><span class="sxs-lookup"><span data-stu-id="f9c69-187">d.</span></span> <span data-ttu-id="f9c69-188">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9c69-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="f9c69-189">Doğrudan test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9c69-189">Creating a Direct test user</span></span>

<span data-ttu-id="f9c69-190">Bu bölümde, doğrudan içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9c69-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="f9c69-191">Çalışmak [doğrudan destek ekibi](https://direct4b.com/ja/support.html#inquiry) hello doğrudan platformunda hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="f9c69-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="f9c69-192">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f9c69-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f9c69-193">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f9c69-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f9c69-194">Bu bölümde, erişim tooDirect vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9c69-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f9c69-196">**tooassign Britta Simon tooDirect hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f9c69-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="f9c69-197">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f9c69-199">Merhaba uygulamalar listesinde **doğrudan**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-199">In hello applications list, select **Direct**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="f9c69-201">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f9c69-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f9c69-203">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9c69-203">Click **Add** button.</span></span> <span data-ttu-id="f9c69-204">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9c69-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f9c69-206">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f9c69-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f9c69-207">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9c69-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9c69-208">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f9c69-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9c69-209">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f9c69-209">Testing single sign-on</span></span>

<span data-ttu-id="f9c69-210">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f9c69-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="f9c69-211">İçinde tootest istiyorsanız **IDP başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="f9c69-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="f9c69-212">Merhaba tıkladığınızda **doğrudan** parçasında Merhaba erişim paneli, otomatik olarak oturum açma tooyour alması gereken **doğrudan** uygulama.</span><span class="sxs-lookup"><span data-stu-id="f9c69-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="f9c69-213">İçinde tootest istiyorsanız **SP tarafından başlatılan modu**:</span><span class="sxs-lookup"><span data-stu-id="f9c69-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="f9c69-214">a.</span><span class="sxs-lookup"><span data-stu-id="f9c69-214">a.</span></span> <span data-ttu-id="f9c69-215">Tıklatın hello üzerinde **doğrudan** döşeme hello erişim paneli ve uygulama oturum açma sayfasına yeniden yönlendirilen toohello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f9c69-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="f9c69-216">b.</span><span class="sxs-lookup"><span data-stu-id="f9c69-216">b.</span></span> <span data-ttu-id="f9c69-217">Giriş, `subdomain` görüntülenen hello textbox ve tuşuna '次へ (İleri)' ve otomatik olarak oturum açma tooyour almalısınız **doğrudan** uygulama.</span><span class="sxs-lookup"><span data-stu-id="f9c69-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="f9c69-218">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9c69-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9c69-219">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f9c69-219">Additional resources</span></span>

* [<span data-ttu-id="f9c69-220">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f9c69-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9c69-221">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f9c69-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

