---
title: "Öğretici: Azure Active Directory Tümleştirme Tableau sunucusuyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Tableau sunucusu arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="be011-103">Öğretici: Azure Active Directory Tümleştirme Tableau sunucusuyla</span><span class="sxs-lookup"><span data-stu-id="be011-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="be011-104">Bu öğreticide, bilgi nasıl toointegrate Tableau Server Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be011-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be011-105">Tableau Server Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="be011-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="be011-106">Erişim tooTableau sunucu sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="be011-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="be011-107">Kullanıcıların tooautomatically get açan tooTableau sunucu (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="be011-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be011-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="be011-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="be011-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be011-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be011-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="be011-110">Prerequisites</span></span>

<span data-ttu-id="be011-111">tooconfigure Tableau Server ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="be011-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="be011-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="be011-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be011-113">Bir Tableau Server Çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="be011-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be011-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="be011-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be011-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="be011-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be011-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="be011-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be011-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be011-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be011-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="be011-118">Scenario description</span></span>
<span data-ttu-id="be011-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="be011-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be011-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="be011-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be011-121">Merhaba Galerisi'nden Tableau sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="be011-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="be011-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="be011-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="be011-123">Merhaba Galerisi'nden Tableau sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="be011-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="be011-124">Azure AD'ye tooconfigure hello tümleştirme Tableau sunucusunun tooadd Tableau sunucu hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="be011-125">**tooadd hello Galerisi, Tableau sunucudan hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be011-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="be011-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="be011-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be011-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="be011-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="be011-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="be011-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="be011-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be011-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="be011-133">Merhaba arama kutusuna yazın **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="be011-133">In hello search box, type **Tableau Server**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="be011-135">Merhaba Sonuçlar panelinde seçin **Tableau Server**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="be011-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be011-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="be011-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be011-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tableau "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı sunucu ile test etme</span><span class="sxs-lookup"><span data-stu-id="be011-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be011-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Tableau Server'daki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="be011-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Tableau Server'daki hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="be011-141">Merhaba hello değeri Tableau Server'da atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="be011-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="be011-142">tooconfigure ve Tableau sunucusu ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="be011-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="be011-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="be011-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="be011-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="be011-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be011-145">**[Tableau Server test kullanıcısı oluşturma](#creating-a-tableau-server-test-user)**  -toohave karşılık gelen, Britta Simon Tableau Server'daki kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="be011-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="be011-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="be011-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be011-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="be011-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be011-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="be011-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be011-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Tableau Server uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be011-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="be011-150">**tooconfigure Azure AD çoklu oturum açma Tableau sunucusuyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be011-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="be011-151">Merhaba hello üzerinde Azure portal'ın **Tableau Server** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="be011-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="be011-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="be011-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="be011-155">Merhaba üzerinde **Tableau sunucu etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be011-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="be011-157">a.</span><span class="sxs-lookup"><span data-stu-id="be011-157">a.</span></span> <span data-ttu-id="be011-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="be011-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="be011-159">b.</span><span class="sxs-lookup"><span data-stu-id="be011-159">b.</span></span> <span data-ttu-id="be011-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="be011-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="be011-161">c.</span><span class="sxs-lookup"><span data-stu-id="be011-161">c.</span></span> <span data-ttu-id="be011-162">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="be011-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="be011-163">Merhaba önceki değerleri gerçek değerler değildir.</span><span class="sxs-lookup"><span data-stu-id="be011-163">hello preceding values are not real values.</span></span> <span data-ttu-id="be011-164">Daha sonra hello gerçek URL ve tanımlayıcıdır hello Tableau sunucu yapılandırma sayfasından ile Merhaba değerlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="be011-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="be011-165">Tableau sunucu uygulaması, belirli bir biçimde hello SAML onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="be011-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="be011-166">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be011-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="be011-167">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Kullanıcı öznitelikleri"** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="be011-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="be011-168">Merhaba aşağıdaki ekran gösterilir hello örneğin aynı.</span><span class="sxs-lookup"><span data-stu-id="be011-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="be011-170">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be011-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="be011-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="be011-171">Attribute Name</span></span> | <span data-ttu-id="be011-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="be011-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="be011-173">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="be011-173">username</span></span> | <span data-ttu-id="be011-174">*User.DisplayName*</span><span class="sxs-lookup"><span data-stu-id="be011-174">*user.displayname*</span></span> |

    <span data-ttu-id="be011-175">a.</span><span class="sxs-lookup"><span data-stu-id="be011-175">a.</span></span> <span data-ttu-id="be011-176">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be011-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="be011-179">b.</span><span class="sxs-lookup"><span data-stu-id="be011-179">b.</span></span> <span data-ttu-id="be011-180">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="be011-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="be011-181">c.</span><span class="sxs-lookup"><span data-stu-id="be011-181">c.</span></span> <span data-ttu-id="be011-182">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="be011-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="be011-183">d.</span><span class="sxs-lookup"><span data-stu-id="be011-183">d.</span></span> <span data-ttu-id="be011-184">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="be011-184">Click **Ok**</span></span>


6. <span data-ttu-id="be011-185">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be011-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="be011-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be011-187">Click **Save** button.</span></span>

    <span data-ttu-id="be011-188">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="be011-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="be011-189">Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour Tableau Server Kiracı yönetici olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="be011-190">a.</span><span class="sxs-lookup"><span data-stu-id="be011-190">a.</span></span> <span data-ttu-id="be011-191">Merhaba Tableau sunucu yapılandırmasında hello tıklatın **SAML** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="be011-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="be011-193">b.</span><span class="sxs-lookup"><span data-stu-id="be011-193">b.</span></span> <span data-ttu-id="be011-194">Hello onay kutusunu seçin **kullanım SAML çoklu oturum açma için**.</span><span class="sxs-lookup"><span data-stu-id="be011-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="be011-195">c.</span><span class="sxs-lookup"><span data-stu-id="be011-195">c.</span></span> <span data-ttu-id="be011-196">Tableau sunucu dönüşü URL — http://tableau_server gibi Tableau Server kullanıcıları erişecek URL hello.</span><span class="sxs-lookup"><span data-stu-id="be011-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="be011-197">Http://localhost kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="be011-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="be011-198">Bir URL sondaki eğik çizgi (örneğin, http://tableau_server/) ile kullanılması desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="be011-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="be011-199">Kopya **Tableau sunucu dönüşü URL** tooAzure AD yapıştırın **oturum üzerinde URL'si** metin kutusuna **Tableau sunucu etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="be011-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="be011-200">d.</span><span class="sxs-lookup"><span data-stu-id="be011-200">d.</span></span> <span data-ttu-id="be011-201">SAML varlık kimliği — hello varlık kimliği Tableau sunucu yükleme toohello IDP benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="be011-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="be011-202">Tableau sunucu URL'si yeniden burada isterseniz girebilirsiniz, ancak toobe Tableau sunucu URL'si yok.</span><span class="sxs-lookup"><span data-stu-id="be011-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="be011-203">Kopya **SAML varlık kimliği** tooAzure AD yapıştırın **tanımlayıcısı** metin kutusuna **Tableau sunucu etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="be011-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="be011-204">e.</span><span class="sxs-lookup"><span data-stu-id="be011-204">e.</span></span> <span data-ttu-id="be011-205">Merhaba tıklatın **meta veri dosyası ver** ve hello metin düzenleyicisi uygulamasında açın.</span><span class="sxs-lookup"><span data-stu-id="be011-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="be011-206">Onaylama işlemi tüketici hizmeti URL'si Http Post ve dizin 0 ve kopyalama hello URL ile bulun.</span><span class="sxs-lookup"><span data-stu-id="be011-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="be011-207">Şimdi tooAzure AD Yapıştır **yanıt URL'si** metin kutusuna **Tableau sunucu etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="be011-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="be011-208">f.</span><span class="sxs-lookup"><span data-stu-id="be011-208">f.</span></span> <span data-ttu-id="be011-209">Azure portalından indirdiğiniz, Federasyon meta veri dosyasını bulun ve hello karşıya **SAML IDP meta veri dosyası**.</span><span class="sxs-lookup"><span data-stu-id="be011-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="be011-210">g.</span><span class="sxs-lookup"><span data-stu-id="be011-210">g.</span></span> <span data-ttu-id="be011-211">Merhaba tıklatın **Tamam** hello Tableau sunucu yapılandırması sayfasında düğmesini.</span><span class="sxs-lookup"><span data-stu-id="be011-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="be011-212">Müşteriniz tooupload herhangi bir sertifikayı hello Tableau Server SAML SSO yapılandırmasında ve hello SSO akış dikkate.</span><span class="sxs-lookup"><span data-stu-id="be011-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="be011-213">SAML Tableau sunucuda yapılandırmaya yardımcı sonra lütfen toothis makalesine başvurun [yapılandırma SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="be011-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="be011-214">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="be011-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="be011-215">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="be011-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="be011-216">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be011-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be011-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be011-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="be011-218">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="be011-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="be011-220">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be011-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="be011-221">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="be011-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be011-223">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="be011-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be011-225">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="be011-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be011-227">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be011-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be011-229">a.</span><span class="sxs-lookup"><span data-stu-id="be011-229">a.</span></span> <span data-ttu-id="be011-230">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be011-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be011-231">b.</span><span class="sxs-lookup"><span data-stu-id="be011-231">b.</span></span> <span data-ttu-id="be011-232">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="be011-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be011-233">c.</span><span class="sxs-lookup"><span data-stu-id="be011-233">c.</span></span> <span data-ttu-id="be011-234">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="be011-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="be011-235">d.</span><span class="sxs-lookup"><span data-stu-id="be011-235">d.</span></span> <span data-ttu-id="be011-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be011-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="be011-237">Tableau Server test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be011-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="be011-238">Bu bölümde Hello amacı toocreate Britta Simon Tableau Server'da adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="be011-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="be011-239">Merhaba Tableau Server'daki tüm hello kullanıcılar tooprovision gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="be011-240">Bu kullanıcı adını hello hello Azure AD özel özniteliğinde yapılandırdığınız hello değeri eşleşmelidir **kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="be011-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="be011-241">Merhaba hello tümleştirme eşleme çalışmalıdır doğru ile [yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="be011-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="be011-242">Toocreate kullanıcı el ile ihtiyacınız varsa, kuruluşunuzdaki toocontact hello Tableau Sunucu Yöneticisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="be011-243">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="be011-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="be011-244">Bu bölümde, erişim tooTableau sunucu vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="be011-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="be011-246">**tooassign Britta Simon tooTableau sunucu hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be011-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="be011-247">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="be011-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="be011-249">Merhaba uygulamalar listesinde **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="be011-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="be011-251">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="be011-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="be011-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be011-253">Click **Add** button.</span></span> <span data-ttu-id="be011-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be011-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="be011-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="be011-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="be011-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be011-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be011-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be011-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be011-259">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="be011-259">Testing single sign-on</span></span>

<span data-ttu-id="be011-260">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="be011-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="be011-261">Merhaba Tableau sunucu hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Tableau sunucu uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be011-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="be011-262">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="be011-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="be011-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="be011-263">Additional resources</span></span>

* [<span data-ttu-id="be011-264">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="be011-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be011-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="be011-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

