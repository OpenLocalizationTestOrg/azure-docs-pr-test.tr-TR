---
title: "Öğretici: Azure Active Directory Tümleştirme Confluence SAML SSO Microsoft tarafından | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Microsoft tarafından Confluence SAML SSO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="23b9f-103">Öğretici: Microsoft tarafından Confluence SAML SSO Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="23b9f-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="23b9f-104">Bu öğreticide, bilgi nasıl toointegrate Confluence SAML SSO Microsoft Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23b9f-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23b9f-105">Microsoft tarafından Confluence SAML SSO Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="23b9f-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="23b9f-106">Microsoft tarafından SAML SSO erişimi tooConfluence sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="23b9f-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="23b9f-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooConfluence SAML SSO (çoklu oturum açma) Microsoft tarafından etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="23b9f-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23b9f-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="23b9f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="23b9f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23b9f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23b9f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="23b9f-110">Prerequisites</span></span>

<span data-ttu-id="23b9f-111">Microsoft tarafından Confluence SAML SSO ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="23b9f-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="23b9f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="23b9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23b9f-113">Bir Windows 64-bit sunucuda (şirket içi veya hello bulut Iaas altyapı) yüklü confluence sunucu uygulaması</span><span class="sxs-lookup"><span data-stu-id="23b9f-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="23b9f-114">HTTPS etkinleştirilmiş confluence sunucusudur</span><span class="sxs-lookup"><span data-stu-id="23b9f-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="23b9f-115">Not hello desteklenen sürümleri Confluence eklentisi için varsayılan olarak, aşağıdaki bölümünün içinde açıklanan.</span><span class="sxs-lookup"><span data-stu-id="23b9f-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="23b9f-116">Confluence sunucusudur Internet üzerinden ulaşılabilir özellikle tooAzure AD oturum açma sayfasında kimlik doğrulaması için ve mümkün tooreceive Azure AD'den belirteci hello</span><span class="sxs-lookup"><span data-stu-id="23b9f-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="23b9f-117">Yönetici kimlik bilgileri Confluence ayarlanır</span><span class="sxs-lookup"><span data-stu-id="23b9f-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="23b9f-118">WebSudo Confluence içinde devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="23b9f-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="23b9f-119">Test kullanıcısı Hello Confluence sunucu uygulaması oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="23b9f-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="23b9f-120">tootest hello bu öğreticideki adımlar, bir üretim ortamında Confluence birini kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="23b9f-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="23b9f-121">Merhaba tümleştirme ilk geliştirme veya hazırlama ortamı hello uygulamasının ve kullanım hello üretim ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="23b9f-122">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="23b9f-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23b9f-123">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23b9f-124">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23b9f-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="23b9f-125">Confluence desteklenen sürümleri</span><span class="sxs-lookup"><span data-stu-id="23b9f-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="23b9f-126">Şimdi itibariyle Confluence aşağıdaki sürümleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="23b9f-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="23b9f-127">Confluence: 5.0 too5.10</span><span class="sxs-lookup"><span data-stu-id="23b9f-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23b9f-128">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="23b9f-128">Scenario description</span></span>
<span data-ttu-id="23b9f-129">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23b9f-130">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="23b9f-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23b9f-131">Microsoft tarafından Confluence SAML SSO hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="23b9f-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="23b9f-132">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="23b9f-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="23b9f-133">Microsoft tarafından Confluence SAML SSO hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="23b9f-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="23b9f-134">Azure AD'ye tooconfigure hello tümleştirme, Microsoft tarafından Confluence SAML SSO tooadd Confluence SAML SSO Microsoft tarafından hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="23b9f-135">**tooadd Confluence SAML SSO hello Galerisi'nden Microsoft tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23b9f-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="23b9f-136">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23b9f-138">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="23b9f-139">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-139">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="23b9f-141">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="23b9f-143">Merhaba arama kutusuna yazın **Confluence SAML SSO Microsoft tarafından**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="23b9f-145">Merhaba Sonuçlar panelinde seçin **Confluence SAML SSO Microsoft tarafından**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="23b9f-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23b9f-147">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="23b9f-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23b9f-148">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Confluence SAML SSO "Britta Simon" adlı bir test kullanıcıyı temel alarak Microsoft tarafından test etme.</span><span class="sxs-lookup"><span data-stu-id="23b9f-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23b9f-149">Tek toowork'ın oturum açma hangi hello karşılık gelen Confluence SAML SSO Microsoft tarafından tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="23b9f-150">Diğer bir deyişle, bir Azure AD kullanıcı ve Microsoft tarafından Confluence SAML SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="23b9f-151">Microsoft tarafından Confluence SAML SSO içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="23b9f-152">tooconfigure ve Microsoft tarafından Confluence SAML SSO ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="23b9f-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="23b9f-153">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="23b9f-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="23b9f-154">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="23b9f-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23b9f-155">**[Microsoft test kullanıcı tarafından Confluence SAML SSO oluşturma](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave Britta Simon Confluence SAML SSO kullanıcı bağlantılı toohello Azure AD gösterimidir Microsoft tarafından karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="23b9f-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="23b9f-156">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="23b9f-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23b9f-157">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="23b9f-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23b9f-158">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23b9f-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23b9f-159">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Microsoft uygulaması tarafından Confluence SAML SSO yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="23b9f-160">**Microsoft tarafından Confluence SAML SSO ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23b9f-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="23b9f-161">Hello hello üzerinde Azure portal'ın **Confluence SAML SSO Microsoft tarafından** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="23b9f-163">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="23b9f-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="23b9f-165">Merhaba üzerinde **Confluence SAML SSO Microsoft Domain ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23b9f-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="23b9f-167">a.</span><span class="sxs-lookup"><span data-stu-id="23b9f-167">a.</span></span> <span data-ttu-id="23b9f-168">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="23b9f-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="23b9f-169">b.</span><span class="sxs-lookup"><span data-stu-id="23b9f-169">b.</span></span> <span data-ttu-id="23b9f-170">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="23b9f-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="23b9f-171">c.</span><span class="sxs-lookup"><span data-stu-id="23b9f-171">c.</span></span> <span data-ttu-id="23b9f-172">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="23b9f-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23b9f-173">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-173">These values are not real.</span></span> <span data-ttu-id="23b9f-174">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="23b9f-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="23b9f-175">Adlandırılmış bir URL olması durumunda bağlantı noktası isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="23b9f-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="23b9f-176">Bu değerleri hello öğreticinin ilerleyen bölümlerinde açıklanan Confluence eklentisi hello yapılandırması sırasında alınır.</span><span class="sxs-lookup"><span data-stu-id="23b9f-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="23b9f-177">toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23b9f-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="23b9f-178">a.</span><span class="sxs-lookup"><span data-stu-id="23b9f-178">a.</span></span> <span data-ttu-id="23b9f-179">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-179">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="23b9f-181">b.</span><span class="sxs-lookup"><span data-stu-id="23b9f-181">b.</span></span> <span data-ttu-id="23b9f-182">Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="23b9f-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="23b9f-184">c.</span><span class="sxs-lookup"><span data-stu-id="23b9f-184">c.</span></span> <span data-ttu-id="23b9f-185">Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="23b9f-187">d.</span><span class="sxs-lookup"><span data-stu-id="23b9f-187">d.</span></span> <span data-ttu-id="23b9f-188">Şimdi toohello özellik sayfasında gidin **Confluence SAML SSO Microsoft tarafından** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="23b9f-190">e.</span><span class="sxs-lookup"><span data-stu-id="23b9f-190">e.</span></span> <span data-ttu-id="23b9f-191">Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` ve daha sonra hello eklentisi hello yapılandırması için kullanılan bu değer Not Defteri'nde kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="23b9f-192">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-192">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23b9f-194">Kişi [Microsoft](mailto:waadpartners@microsoft.com) bilgi hello Confluence eklentisi için aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="23b9f-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="23b9f-195">Müşteri adı:</span><span class="sxs-lookup"><span data-stu-id="23b9f-195">Customer Name:</span></span>
    *   <span data-ttu-id="23b9f-196">Birincil etki alanı adı:</span><span class="sxs-lookup"><span data-stu-id="23b9f-196">Primary domain name:</span></span>
    *   <span data-ttu-id="23b9f-197">Azure AD Premium: Evet/Hayır (eklentisi kullanılabilir tooall hello müşteri ücretsiz, temel ve Premium SKU olacaktır)</span><span class="sxs-lookup"><span data-stu-id="23b9f-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="23b9f-198">Bu tümleştirme kullanarak kullanıcıların sayısı:</span><span class="sxs-lookup"><span data-stu-id="23b9f-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="23b9f-199">Confluence sürümü:</span><span class="sxs-lookup"><span data-stu-id="23b9f-199">Confluence Version:</span></span>
    *   <span data-ttu-id="23b9f-200">Açıklama:</span><span class="sxs-lookup"><span data-stu-id="23b9f-200">Comments:</span></span>

7. <span data-ttu-id="23b9f-201">Farklı web tarayıcısı penceresinde tooyour Confluence örneğinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="23b9f-202">Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="23b9f-204">Eklentiler sekmesi bölümü altında tıklatın **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="23b9f-206">Microsoft tarafından sağlanan hello eklentisini el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="23b9f-207">Merhaba eklentisi yüklendikten sonra görünür **kullanıcı yüklü** eklentileri bölümünü **yönetmek eklenti** bölümü.</span><span class="sxs-lookup"><span data-stu-id="23b9f-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="23b9f-208">Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.</span><span class="sxs-lookup"><span data-stu-id="23b9f-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="23b9f-209">Yapılandırma sayfasında şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23b9f-209">Perform following steps on configuration page:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="23b9f-211">a.</span><span class="sxs-lookup"><span data-stu-id="23b9f-211">a.</span></span> <span data-ttu-id="23b9f-212">İçinde **meta veri URL'sini** hello yapıştırın **meta veri URL'sini** Azure AD'den oluşturulur ve hello tıklatın **gidermek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="23b9f-213">Merhaba IDP meta veri URL'sini okur ve tüm hello alanları bilgileri doldurur.</span><span class="sxs-lookup"><span data-stu-id="23b9f-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="23b9f-214">Varsayılan SAML kullanıcı kimliği konumu ad tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="23b9f-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="23b9f-215">Bu tooan özniteliği seçeneği değiştirmek ve hello uygun öznitelik adı girin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="23b9f-216">Yani hata hello meta veri çözümlemede hello uygulamayı karşı eşlenen yalnızca bir sertifika olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="23b9f-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="23b9f-217">Merhaba meta veri çözümleme sırasında birden fazla sertifika varsa yönetici bir hata alır.</span><span class="sxs-lookup"><span data-stu-id="23b9f-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="23b9f-218">b.</span><span class="sxs-lookup"><span data-stu-id="23b9f-218">b.</span></span> <span data-ttu-id="23b9f-219">Kopya hello **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** değerleri ve bunları yapıştırın **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** kutularındaki sırasıyla içinde **Confluence SAML SSO Microsoft Domain ve URL'leri**  Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="23b9f-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="23b9f-220">c.</span><span class="sxs-lookup"><span data-stu-id="23b9f-220">c.</span></span> <span data-ttu-id="23b9f-221">İçinde **oturum açma düğmesi adı** türü hello adı düğmesine kuruluşunuz hello kullanıcılar toosee oturum açma ekranında istemektedir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="23b9f-222">d.</span><span class="sxs-lookup"><span data-stu-id="23b9f-222">d.</span></span> <span data-ttu-id="23b9f-223">İçinde **SAML kullanıcı kimliği konumları** seçin **kullanıcı kimliğidir hello NameIdentifier öğesinde hello konu deyimi** veya **kullanıcı kimliği olan bir öznitelik öğedeki**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="23b9f-224">Bu kimliği toobe hello Confluence kullanıcı kimliği var. Merhaba kullanıcı kimliği eşleşmiyorsa, ardından sistemi kullanıcılar toolog izin vermez.</span><span class="sxs-lookup"><span data-stu-id="23b9f-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="23b9f-225">e.</span><span class="sxs-lookup"><span data-stu-id="23b9f-225">e.</span></span> <span data-ttu-id="23b9f-226">Seçerseniz **kullanıcı kimliği olan bir öznitelik öğedeki** seçeneği, sonra **öznitelik adı** kullanıcı kimliği beklenirken hello özniteliğinin textbox türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="23b9f-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="23b9f-227">f.</span><span class="sxs-lookup"><span data-stu-id="23b9f-227">f.</span></span> <span data-ttu-id="23b9f-228">Azure AD ile Merhaba Federasyon etki alanını (örneğin, ADFS vb.) kullanıyorsanız, üzerinde hello'ı tıklatın **giriş bölgesi bulmayı etkinleştirmek** seçeneği ve hello yapılandırma **etki alanı adı**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="23b9f-229">g.</span><span class="sxs-lookup"><span data-stu-id="23b9f-229">g.</span></span> <span data-ttu-id="23b9f-230">İçinde **etki alanı adı** hello etki alanı adını buraya yazın hello ADFS tabanlı oturum açma durumunda.</span><span class="sxs-lookup"><span data-stu-id="23b9f-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="23b9f-231">h.</span><span class="sxs-lookup"><span data-stu-id="23b9f-231">h.</span></span> <span data-ttu-id="23b9f-232">Denetleme **etkinleştirmek tek oturum kapatma** bir kullanıcı oturum açtığında Confluence Azure AD'den toolog çıkışı isterseniz.</span><span class="sxs-lookup"><span data-stu-id="23b9f-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="23b9f-233">ı.</span><span class="sxs-lookup"><span data-stu-id="23b9f-233">i.</span></span> <span data-ttu-id="23b9f-234">Tıklatın **kaydetmek** düğmesini toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="23b9f-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="23b9f-235">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="23b9f-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="23b9f-236">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="23b9f-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="23b9f-237">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23b9f-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23b9f-238">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="23b9f-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="23b9f-239">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="23b9f-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="23b9f-241">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23b9f-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="23b9f-242">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23b9f-244">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23b9f-246">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="23b9f-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23b9f-248">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23b9f-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23b9f-250">a.</span><span class="sxs-lookup"><span data-stu-id="23b9f-250">a.</span></span> <span data-ttu-id="23b9f-251">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23b9f-252">b.</span><span class="sxs-lookup"><span data-stu-id="23b9f-252">b.</span></span> <span data-ttu-id="23b9f-253">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="23b9f-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23b9f-254">c.</span><span class="sxs-lookup"><span data-stu-id="23b9f-254">c.</span></span> <span data-ttu-id="23b9f-255">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="23b9f-256">d.</span><span class="sxs-lookup"><span data-stu-id="23b9f-256">d.</span></span> <span data-ttu-id="23b9f-257">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="23b9f-258">Microsoft test kullanıcı tarafından Confluence SAML SSO oluşturma</span><span class="sxs-lookup"><span data-stu-id="23b9f-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="23b9f-259">tooenable Azure AD kullanıcıların toolog içi sunucuda tooConfluence bunlar Confluence SAML SSO Microsoft tarafından sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="23b9f-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="23b9f-260">Microsoft tarafından Confluence SAML SSO için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="23b9f-261">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23b9f-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="23b9f-262">Tooyour Confluence içi sunucuda, yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="23b9f-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="23b9f-263">Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-263">Hover on cog and click hello **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="23b9f-265">Kullanıcılar bölümü altında tıklatın **kullanıcıları eklemek** sekmesi. Merhaba üzerinde **"Bir kullanıcı Ekle"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="23b9f-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="23b9f-267">a.</span><span class="sxs-lookup"><span data-stu-id="23b9f-267">a.</span></span> <span data-ttu-id="23b9f-268">Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının Britta Simon gibi türü hello e-posta.</span><span class="sxs-lookup"><span data-stu-id="23b9f-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="23b9f-269">b.</span><span class="sxs-lookup"><span data-stu-id="23b9f-269">b.</span></span> <span data-ttu-id="23b9f-270">Merhaba, **tam adı** metin kutusuna, türü hello kullanıcının tam adını Britta Simon gibi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="23b9f-271">c.</span><span class="sxs-lookup"><span data-stu-id="23b9f-271">c.</span></span> <span data-ttu-id="23b9f-272">Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="23b9f-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="23b9f-273">d.</span><span class="sxs-lookup"><span data-stu-id="23b9f-273">d.</span></span> <span data-ttu-id="23b9f-274">Merhaba, **parola** metin kutusuna, Britta Simon hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="23b9f-275">e.</span><span class="sxs-lookup"><span data-stu-id="23b9f-275">e.</span></span> <span data-ttu-id="23b9f-276">Tıklatın **parolayı onayla** hello parolayı yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="23b9f-277">f.</span><span class="sxs-lookup"><span data-stu-id="23b9f-277">f.</span></span> <span data-ttu-id="23b9f-278">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="23b9f-279">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="23b9f-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="23b9f-280">Bu bölümde, Microsoft tarafından SAML SSO erişimi tooConfluence vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="23b9f-282">**tooassign Britta Simon tooConfluence SAML SSO Microsoft tarafından hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="23b9f-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="23b9f-283">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="23b9f-285">Merhaba uygulamalar listesinde **Confluence SAML SSO Microsoft tarafından**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="23b9f-287">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="23b9f-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="23b9f-289">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="23b9f-289">Click **Add** button.</span></span> <span data-ttu-id="23b9f-290">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="23b9f-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="23b9f-292">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="23b9f-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="23b9f-293">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="23b9f-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23b9f-294">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="23b9f-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23b9f-295">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="23b9f-295">Testing single sign-on</span></span>

<span data-ttu-id="23b9f-296">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="23b9f-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="23b9f-297">Merhaba Confluence SAML SSO hello erişim paneli Microsoft parçasında tarafından tıkladığınızda, otomatik olarak oturum açma tooyour Confluence SAML SSO Microsoft uygulaması tarafından almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23b9f-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="23b9f-298">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23b9f-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23b9f-299">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="23b9f-299">Additional resources</span></span>

* [<span data-ttu-id="23b9f-300">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="23b9f-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23b9f-301">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="23b9f-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

