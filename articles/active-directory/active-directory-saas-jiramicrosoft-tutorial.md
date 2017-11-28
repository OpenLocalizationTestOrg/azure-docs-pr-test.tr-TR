---
title: "Öğretici: Azure Active Directory Tümleştirme JIRA SAML SSO Microsoft tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Microsoft tarafından JIRA SAML SSO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="e7a9f-103">Öğretici: Microsoft tarafından JIRA SAML SSO Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e7a9f-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="e7a9f-104">Bu öğreticide, bilgi nasıl toointegrate JIRA SAML SSO Microsoft Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7a9f-105">Microsoft tarafından JIRA SAML SSO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7a9f-106">Microsoft tarafından SAML SSO erişimi tooJIRA sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e7a9f-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="e7a9f-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooJIRA SAML SSO (çoklu oturum açma) Microsoft tarafından etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e7a9f-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7a9f-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e7a9f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e7a9f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7a9f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e7a9f-110">Prerequisites</span></span>

<span data-ttu-id="e7a9f-111">Microsoft tarafından JIRA SAML SSO ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="e7a9f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e7a9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7a9f-113">Bir Windows 64-bit sunucuda (şirket içi veya hello bulut Iaas altyapı) yüklü JIRA sunucu uygulaması</span><span class="sxs-lookup"><span data-stu-id="e7a9f-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="e7a9f-114">HTTPS etkinleştirilmiş JIRA sunucusudur</span><span class="sxs-lookup"><span data-stu-id="e7a9f-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="e7a9f-115">Not hello desteklenen sürümleri JIRA eklentisi için varsayılan olarak, aşağıdaki bölümünün içinde açıklanan.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="e7a9f-116">JIRA sunucusudur Internet üzerinden ulaşılabilir özellikle tooAzure AD oturum açma sayfasında kimlik doğrulaması için ve mümkün tooreceive Azure AD'den belirteci hello</span><span class="sxs-lookup"><span data-stu-id="e7a9f-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="e7a9f-117">Yönetici kimlik bilgileri JIRA ayarlanır</span><span class="sxs-lookup"><span data-stu-id="e7a9f-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="e7a9f-118">WebSudo JIRA içinde devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="e7a9f-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="e7a9f-119">Test kullanıcısı Hello JIRA sunucu uygulaması oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="e7a9f-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="e7a9f-120">tootest hello bu öğreticideki adımlar, bir üretim ortamında JIRA birini kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="e7a9f-121">Merhaba tümleştirme ilk geliştirme veya hazırlama ortamı hello uygulamasının ve kullanım hello üretim ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="e7a9f-122">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7a9f-123">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7a9f-124">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="e7a9f-125">JIRA desteklenen sürümleri</span><span class="sxs-lookup"><span data-stu-id="e7a9f-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="e7a9f-126">Şimdi itibariyle JIRA aşağıdaki sürümleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="e7a9f-127">JIRA çekirdek ve yazılım: 6.0 too7.2.0</span><span class="sxs-lookup"><span data-stu-id="e7a9f-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="e7a9f-128">JIRA hizmet masasına: 3.0 too3.2</span><span class="sxs-lookup"><span data-stu-id="e7a9f-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7a9f-129">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e7a9f-129">Scenario description</span></span>
<span data-ttu-id="e7a9f-130">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7a9f-131">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7a9f-132">Microsoft tarafından JIRA SAML SSO hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e7a9f-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="e7a9f-133">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e7a9f-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="e7a9f-134">Microsoft tarafından JIRA SAML SSO hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e7a9f-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="e7a9f-135">Azure AD'ye tooconfigure hello tümleştirme, Microsoft tarafından JIRA SAML SSO tooadd JIRA SAML SSO Microsoft tarafından hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7a9f-136">**tooadd JIRA SAML SSO hello Galerisi'nden Microsoft tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7a9f-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7a9f-137">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7a9f-139">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7a9f-140">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-140">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e7a9f-142">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e7a9f-144">Merhaba arama kutusuna yazın **JIRA SAML SSO Microsoft tarafından**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="e7a9f-146">Merhaba Sonuçlar panelinde seçin **JIRA SAML SSO Microsoft tarafından**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7a9f-148">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e7a9f-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7a9f-149">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma JIRA SAML SSO "Britta Simon." olarak adlandırılan bir test kullanıcıyı temel alarak Microsoft tarafından test etme</span><span class="sxs-lookup"><span data-stu-id="e7a9f-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7a9f-150">Tek toowork'ın oturum açma hangi hello karşılık gelen JIRA SAML SSO Microsoft tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="e7a9f-151">Diğer bir deyişle, bir Azure AD kullanıcı ve Microsoft tarafından JIRA SAML SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="e7a9f-152">Microsoft tarafından JIRA SAML SSO içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7a9f-153">tooconfigure ve Microsoft tarafından JIRA SAML SSO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7a9f-154">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7a9f-155">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7a9f-156">**[Microsoft test kullanıcı tarafından JIRA SAML SSO oluşturma](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave Britta Simon JIRA SAML SSO kullanıcı bağlantılı toohello Azure AD gösterimidir Microsoft tarafından karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7a9f-157">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7a9f-158">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7a9f-159">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e7a9f-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7a9f-160">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Microsoft uygulaması tarafından JIRA SAML SSO yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="e7a9f-161">**Microsoft tarafından JIRA SAML SSO ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7a9f-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7a9f-162">Hello hello üzerinde Azure portal'ın **JIRA SAML SSO Microsoft tarafından** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e7a9f-164">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="e7a9f-166">Merhaba üzerinde **JIRA SAML SSO Microsoft Domain ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="e7a9f-168">a.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-168">a.</span></span> <span data-ttu-id="e7a9f-169">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="e7a9f-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="e7a9f-170">b.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-170">b.</span></span> <span data-ttu-id="e7a9f-171">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="e7a9f-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="e7a9f-172">c.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-172">c.</span></span> <span data-ttu-id="e7a9f-173">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="e7a9f-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7a9f-174">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-174">These values are not real.</span></span> <span data-ttu-id="e7a9f-175">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e7a9f-176">Adlandırılmış bir URL olması durumunda bağlantı noktası isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="e7a9f-177">Bu değerleri hello öğreticinin ilerleyen bölümlerinde açıklanan Jira eklentisi hello yapılandırması sırasında alınır.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="e7a9f-178">toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="e7a9f-179">a.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-179">a.</span></span> <span data-ttu-id="e7a9f-180">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-180">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="e7a9f-182">b.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-182">b.</span></span> <span data-ttu-id="e7a9f-183">Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="e7a9f-185">c.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-185">c.</span></span> <span data-ttu-id="e7a9f-186">Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="e7a9f-188">d.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-188">d.</span></span> <span data-ttu-id="e7a9f-189">Şimdi toohello özellik sayfasında gidin **JIRA SAML SSO Microsoft tarafından** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="e7a9f-191">e.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-191">e.</span></span> <span data-ttu-id="e7a9f-192">Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` ve daha sonra hello eklentisi hello yapılandırması için kullanılan bu değer Not Defteri'nde kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="e7a9f-193">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-193">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7a9f-195">Kişi [Microsoft](mailto:waadpartners@microsoft.com) bilgi hello JIRA eklentisi için aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="e7a9f-196">Müşteri adı:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-196">Customer Name:</span></span>
    *   <span data-ttu-id="e7a9f-197">Birincil etki alanı adı:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-197">Primary domain name:</span></span>
    *   <span data-ttu-id="e7a9f-198">Azure AD Premium: Evet/Hayır (eklentisi kullanılabilir tooall hello müşteri ücretsiz, temel ve Premium SKU olacaktır)</span><span class="sxs-lookup"><span data-stu-id="e7a9f-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="e7a9f-199">Bu tümleştirme kullanarak kullanıcıların sayısı:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="e7a9f-200">JIRA sürümü:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-200">JIRA Version:</span></span>
    *   <span data-ttu-id="e7a9f-201">Açıklama:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-201">Comments:</span></span>

7. <span data-ttu-id="e7a9f-202">Farklı web tarayıcısı penceresinde tooyour JIRA örneğinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="e7a9f-203">Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="e7a9f-205">Eklentiler sekmesi bölümü altında tıklatın **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="e7a9f-207">Microsoft tarafından sağlanan hello eklentisini el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="e7a9f-208">Merhaba eklentisi yüklendikten sonra görünür **kullanıcı yüklü** eklentileri bölümünü **yönetmek eklenti** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="e7a9f-209">Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="e7a9f-210">Yapılandırma sayfasında şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-210">Perform following steps on configuration page:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="e7a9f-212">a.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-212">a.</span></span> <span data-ttu-id="e7a9f-213">İçinde **meta veri URL'sini** hello yapıştırın **meta veri URL'sini** Azure AD'den oluşturulur ve hello tıklatın **gidermek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="e7a9f-214">Merhaba IDP meta veri URL'sini okur ve tüm hello alanları bilgileri doldurur.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="e7a9f-215">Varsayılan SAML kullanıcı kimliği konumu ad tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="e7a9f-216">Bu tooan özniteliği seçeneği değiştirmek ve hello uygun öznitelik adı girin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="e7a9f-217">Yani hata hello meta veri çözümlemede hello uygulamayı karşı eşlenen yalnızca bir sertifika olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="e7a9f-218">Merhaba meta veri çözümleme sırasında birden fazla sertifika varsa yönetici bir hata alır.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="e7a9f-219">b.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-219">b.</span></span> <span data-ttu-id="e7a9f-220">Kopya hello **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** değerleri ve bunları yapıştırın **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** kutularındaki sırasıyla içinde **JIRA SAML SSO Microsoft Domain ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="e7a9f-221">c.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-221">c.</span></span> <span data-ttu-id="e7a9f-222">İçinde **oturum açma düğmesi adı** türü hello adı düğmesine kuruluşunuz hello kullanıcılar toosee oturum açma ekranında istemektedir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="e7a9f-223">d.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-223">d.</span></span> <span data-ttu-id="e7a9f-224">İçinde **SAML kullanıcı kimliği konumları** seçin **kullanıcı kimliğidir hello NameIdentifier öğesinde hello konu deyimi** veya **kullanıcı kimliği olan bir öznitelik öğedeki**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="e7a9f-225">Bu kimliği toobe hello JIRA kullanıcı kimliği var. Merhaba kullanıcı kimliği eşleşmiyorsa, ardından sistemi kullanıcılar toolog izin vermez.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="e7a9f-226">e.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-226">e.</span></span> <span data-ttu-id="e7a9f-227">Seçerseniz **kullanıcı kimliği olan bir öznitelik öğedeki** seçeneği, sonra **öznitelik adı** kullanıcı kimliği beklenirken hello özniteliğinin textbox türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="e7a9f-228">f.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-228">f.</span></span> <span data-ttu-id="e7a9f-229">Azure AD ile Merhaba Federasyon etki alanını (örneğin, ADFS vb.) kullanıyorsanız, üzerinde hello'ı tıklatın **giriş bölgesi bulmayı etkinleştirmek** seçeneği ve hello yapılandırma **etki alanı adı**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="e7a9f-230">g.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-230">g.</span></span> <span data-ttu-id="e7a9f-231">İçinde **etki alanı adı** hello etki alanı adını buraya yazın hello ADFS tabanlı oturum açma durumunda.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="e7a9f-232">h.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-232">h.</span></span> <span data-ttu-id="e7a9f-233">Denetleme **etkinleştirmek tek oturum kapatma** bir kullanıcı oturum açtığında JIRA Azure AD'den toolog çıkışı isterseniz.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="e7a9f-234">ı.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-234">i.</span></span> <span data-ttu-id="e7a9f-235">Tıklatın **kaydetmek** düğmesini toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="e7a9f-236">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e7a9f-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7a9f-237">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7a9f-238">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7a9f-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7a9f-239">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7a9f-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7a9f-240">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e7a9f-242">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7a9f-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7a9f-243">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7a9f-245">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7a9f-247">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7a9f-249">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7a9f-251">a.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-251">a.</span></span> <span data-ttu-id="e7a9f-252">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7a9f-253">b.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-253">b.</span></span> <span data-ttu-id="e7a9f-254">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7a9f-255">c.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-255">c.</span></span> <span data-ttu-id="e7a9f-256">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e7a9f-257">d.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-257">d.</span></span> <span data-ttu-id="e7a9f-258">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="e7a9f-259">Microsoft test kullanıcı tarafından JIRA SAML SSO oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7a9f-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="e7a9f-260">tooenable Azure AD kullanıcıların toolog tooJIRA şirket içi Server'da, bunlar JIRA SAML SSO Microsoft tarafından sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="e7a9f-261">Microsoft tarafından JIRA SAML SSO için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="e7a9f-262">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7a9f-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7a9f-263">İçinde tooyour JIRA şirket içi sunucu yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="e7a9f-264">Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-264">Hover on cog and click hello **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="e7a9f-266">Yeniden yönlendirilen tooAdministrator erişim sayfası tooenter olduğunuz **parola** tıklatıp **Onayla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="e7a9f-268">Altında **kullanıcı yönetimi** bölüm sekmesini tıklatın, **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-268">Under **User management** tab section, click **create user**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="e7a9f-270">Merhaba üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7a9f-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="e7a9f-272">a.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-272">a.</span></span> <span data-ttu-id="e7a9f-273">Merhaba, **e-posta adresi** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e7a9f-274">b.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-274">b.</span></span> <span data-ttu-id="e7a9f-275">Merhaba, **tam adı** metin kutusuna, Britta Simon gibi hello kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="e7a9f-276">c.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-276">c.</span></span> <span data-ttu-id="e7a9f-277">Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e7a9f-278">d.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-278">d.</span></span> <span data-ttu-id="e7a9f-279">Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="e7a9f-280">e.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-280">e.</span></span> <span data-ttu-id="e7a9f-281">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e7a9f-282">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e7a9f-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e7a9f-283">Bu bölümde, Microsoft tarafından SAML SSO erişimi tooJIRA vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e7a9f-285">**tooassign Britta Simon tooJIRA SAML SSO Microsoft tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7a9f-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7a9f-286">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e7a9f-288">Merhaba uygulamalar listesinde **JIRA SAML SSO Microsoft tarafından**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="e7a9f-290">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e7a9f-292">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-292">Click **Add** button.</span></span> <span data-ttu-id="e7a9f-293">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e7a9f-295">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7a9f-296">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7a9f-297">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7a9f-298">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e7a9f-298">Testing single sign-on</span></span>

<span data-ttu-id="e7a9f-299">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7a9f-300">Merhaba JIRA SAML SSO hello erişim paneli Microsoft parçasında tarafından tıkladığınızda, otomatik olarak oturum açma tooyour JIRA SAML SSO Microsoft uygulaması tarafından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7a9f-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="e7a9f-301">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7a9f-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7a9f-302">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e7a9f-302">Additional resources</span></span>

* [<span data-ttu-id="e7a9f-303">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e7a9f-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7a9f-304">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e7a9f-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

