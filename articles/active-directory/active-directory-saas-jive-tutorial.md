---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jive | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jive arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: f22bf78a55e8a4a9ea2f0020ef2f535be88b6302
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="a21e2-103">Öğretici: Azure Active Directory Tümleştirme Jive ile</span><span class="sxs-lookup"><span data-stu-id="a21e2-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="a21e2-104">Bu öğreticide, bilgi nasıl toointegrate Jive Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="a21e2-104">In this tutorial, you learn how toointegrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a21e2-105">Jive Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a21e2-105">Integrating Jive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a21e2-106">Erişim tooJive sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a21e2-106">You can control in Azure AD who has access tooJive</span></span>
- <span data-ttu-id="a21e2-107">Kullanıcıların tooautomatically get açan tooJive (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a21e2-107">You can enable your users tooautomatically get signed-on tooJive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a21e2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a21e2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a21e2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla bilgi tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a21e2-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a21e2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a21e2-110">Prerequisites</span></span>

<span data-ttu-id="a21e2-111">tooconfigure Jive ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a21e2-111">tooconfigure Azure AD integration with Jive, you need hello following items:</span></span>

- <span data-ttu-id="a21e2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a21e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a21e2-113">Bir Jive çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="a21e2-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a21e2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a21e2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a21e2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a21e2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a21e2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a21e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a21e2-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a21e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a21e2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a21e2-118">Scenario description</span></span>
<span data-ttu-id="a21e2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a21e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a21e2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a21e2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a21e2-121">Merhaba Galerisi'nden Jive ekleme</span><span class="sxs-lookup"><span data-stu-id="a21e2-121">Adding Jive from hello gallery</span></span>
2. <span data-ttu-id="a21e2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a21e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-hello-gallery"></a><span data-ttu-id="a21e2-123">Merhaba Galerisi'nden Jive ekleme</span><span class="sxs-lookup"><span data-stu-id="a21e2-123">Adding Jive from hello gallery</span></span>
<span data-ttu-id="a21e2-124">Azure AD'ye Jive tooconfigure hello tümleştirilmesi, tooadd Jive hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21e2-124">tooconfigure hello integration of Jive into Azure AD, you need tooadd Jive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a21e2-125">**tooadd Jive hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a21e2-125">**tooadd Jive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a21e2-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a21e2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a21e2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a21e2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a21e2-133">Merhaba arama kutusuna yazın **Jive**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-133">In hello search box, type **Jive**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="a21e2-135">Merhaba Sonuçlar panelinde seçin **Jive**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a21e2-135">In hello results panel, select **Jive**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a21e2-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a21e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a21e2-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Jive ile test etme</span><span class="sxs-lookup"><span data-stu-id="a21e2-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a21e2-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Jive içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21e2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jive is tooa user in Azure AD.</span></span> <span data-ttu-id="a21e2-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Jive hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21e2-140">In other words, a link relationship between an Azure AD user and hello related user in Jive needs toobe established.</span></span>

<span data-ttu-id="a21e2-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Jive içinde.</span><span class="sxs-lookup"><span data-stu-id="a21e2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Jive.</span></span>

<span data-ttu-id="a21e2-142">tooconfigure ve Jive ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a21e2-142">tooconfigure and test Azure AD single sign-on with Jive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a21e2-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a21e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a21e2-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a21e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a21e2-145">**[Jive test kullanıcısı oluşturma](#creating-a-jive-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Jive içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a21e2-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - toohave a counterpart of Britta Simon in Jive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a21e2-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a21e2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a21e2-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a21e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a21e2-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a21e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a21e2-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Jive uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a21e2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="a21e2-150">**Azure AD çoklu oturum açma tooconfigure Jive ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a21e2-150">**tooconfigure Azure AD single sign-on with Jive, perform hello following steps:**</span></span>

1. <span data-ttu-id="a21e2-151">Hello hello üzerinde Azure portal'ın **Jive** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-151">In hello Azure portal, on hello **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a21e2-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a21e2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="a21e2-155">Merhaba üzerinde **Jive etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a21e2-155">On hello **Jive Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="a21e2-157">a.</span><span class="sxs-lookup"><span data-stu-id="a21e2-157">a.</span></span> <span data-ttu-id="a21e2-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="a21e2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="a21e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="a21e2-159">b.</span></span> <span data-ttu-id="a21e2-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="a21e2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a21e2-161">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a21e2-161">These values are not hello real.</span></span> <span data-ttu-id="a21e2-162">Bu değerler, oturum açma hello gerçek URL ve tanımlayıcıdır ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a21e2-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="a21e2-163">Kişi [Jive istemci destek ekibi](https://www.jivesoftware.com/services-support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a21e2-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a21e2-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a21e2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="a21e2-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a21e2-168">tooconfigure çoklu oturum açma üzerinde **Jive** yan yana, oturum açma tooyour Jive Kiracı yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="a21e2-168">tooconfigure single sign-on on **Jive** side, sign-on tooyour Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="a21e2-169">Hello içinde hello üst menüsünde "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="a21e2-169">In hello menu on hello top, Click "**Saml**."</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="a21e2-171">a.</span><span class="sxs-lookup"><span data-stu-id="a21e2-171">a.</span></span> <span data-ttu-id="a21e2-172">Seçin **etkin** hello altında **genel** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-172">Select **Enabled** under hello **General** tab.</span></span>   
    <span data-ttu-id="a21e2-173">b.</span><span class="sxs-lookup"><span data-stu-id="a21e2-173">b.</span></span> <span data-ttu-id="a21e2-174">Merhaba tıklayın "**tüm saml Ayarları Kaydet**" düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-174">Click hello "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="a21e2-175">Toohello gidin "**IDP meta veri**" sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-175">Navigate toohello "**Idp Metadata**" tab.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="a21e2-177">a.</span><span class="sxs-lookup"><span data-stu-id="a21e2-177">a.</span></span> <span data-ttu-id="a21e2-178">İndirilen hello meta veri XML dosyası Hello içeriğini kopyalayın ve hello yapıştırma **kimlik sağlayıcısı (IDP) meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a21e2-178">Copy hello content of hello downloaded metadata XML file, and then paste it into hello **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="a21e2-179">b.</span><span class="sxs-lookup"><span data-stu-id="a21e2-179">b.</span></span> <span data-ttu-id="a21e2-180">Merhaba tıklayın "**tüm saml Ayarları Kaydet**" düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-180">Click hello "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="a21e2-181">Toohello Git "**kullanıcı özniteliği eşleme**" sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-181">Go toohello "**User Attribute Mapping**" tab.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="a21e2-183">a.</span><span class="sxs-lookup"><span data-stu-id="a21e2-183">a.</span></span> <span data-ttu-id="a21e2-184">Merhaba, **e-posta** metin kutusuna, kopyalama ve yapıştırma hello öznitelik adını **posta** değeri.</span><span class="sxs-lookup"><span data-stu-id="a21e2-184">In hello **Email** textbox, copy and paste hello attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="a21e2-185">b.</span><span class="sxs-lookup"><span data-stu-id="a21e2-185">b.</span></span> <span data-ttu-id="a21e2-186">Merhaba, **ad** metin kutusuna, kopyalama ve yapıştırma hello öznitelik adını **givenname** değeri.</span><span class="sxs-lookup"><span data-stu-id="a21e2-186">In hello **First Name** textbox, copy and paste hello attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="a21e2-187">c.</span><span class="sxs-lookup"><span data-stu-id="a21e2-187">c.</span></span> <span data-ttu-id="a21e2-188">Merhaba, **Soyadı** metin kutusuna, kopyalama ve yapıştırma hello öznitelik adını **Soyadı** değeri.</span><span class="sxs-lookup"><span data-stu-id="a21e2-188">In hello **Last Name** textbox, copy and paste hello attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="a21e2-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a21e2-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a21e2-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a21e2-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a21e2-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a21e2-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a21e2-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a21e2-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="a21e2-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a21e2-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a21e2-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a21e2-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a21e2-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a21e2-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a21e2-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a21e2-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a21e2-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a21e2-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a21e2-204">a.</span><span class="sxs-lookup"><span data-stu-id="a21e2-204">a.</span></span> <span data-ttu-id="a21e2-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a21e2-206">b.</span><span class="sxs-lookup"><span data-stu-id="a21e2-206">b.</span></span> <span data-ttu-id="a21e2-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a21e2-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a21e2-208">c.</span><span class="sxs-lookup"><span data-stu-id="a21e2-208">c.</span></span> <span data-ttu-id="a21e2-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a21e2-210">d.</span><span class="sxs-lookup"><span data-stu-id="a21e2-210">d.</span></span> <span data-ttu-id="a21e2-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a21e2-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="a21e2-212">Jive test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a21e2-212">Creating a Jive test user</span></span>

<span data-ttu-id="a21e2-213">Çalışmak [Jive istemci destek ekibi](https://www.jivesoftware.com/services-support/) tooadd hello kullanıcılar hello Jive Platform.</span><span class="sxs-lookup"><span data-stu-id="a21e2-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) tooadd hello users in hello Jive platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a21e2-214">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a21e2-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a21e2-215">Bu bölümde, erişim tooJive vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a21e2-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJive.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a21e2-217">**tooassign Britta Simon tooJive hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a21e2-217">**tooassign Britta Simon tooJive, perform hello following steps:**</span></span>

1. <span data-ttu-id="a21e2-218">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a21e2-220">Merhaba uygulamalar listesinde **Jive**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-220">In hello applications list, select **Jive**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="a21e2-222">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a21e2-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a21e2-224">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a21e2-224">Click **Add** button.</span></span> <span data-ttu-id="a21e2-225">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a21e2-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a21e2-227">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a21e2-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a21e2-228">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a21e2-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a21e2-229">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a21e2-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a21e2-230">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a21e2-230">Testing single sign-on</span></span>

<span data-ttu-id="a21e2-231">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a21e2-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a21e2-232">Merhaba Jive hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Jive uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21e2-232">When you click hello Jive tile in hello Access Panel, you should get automatically signed-on tooyour Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a21e2-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a21e2-233">Additional resources</span></span>

* [<span data-ttu-id="a21e2-234">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a21e2-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a21e2-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a21e2-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a21e2-236">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="a21e2-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

