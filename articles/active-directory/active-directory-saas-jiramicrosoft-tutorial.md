---
title: "Öğretici: Azure Active Directory Tümleştirme JIRA SAML SSO Microsoft tarafından | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Microsoft tarafından JIRA SAML SSO arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="649ce-103">Öğretici: Microsoft tarafından JIRA SAML SSO Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="649ce-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="649ce-104">Bu öğreticide, Microsoft tarafından JIRA SAML SSO Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="649ce-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="649ce-105">Microsoft tarafından JIRA SAML SSO Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="649ce-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="649ce-106">Microsoft tarafından JIRA SAML SSO erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="649ce-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="649ce-107">Azure AD hesaplarına otomatik olarak JIRA SAML SSO (çoklu oturum açma) Microsoft tarafından açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="649ce-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="649ce-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="649ce-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="649ce-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="649ce-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="649ce-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="649ce-110">Prerequisites</span></span>

<span data-ttu-id="649ce-111">Microsoft tarafından JIRA SAML SSO ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="649ce-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="649ce-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="649ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="649ce-113">Bir Windows 64-bit sunucuda (şirket içi veya Bulut Iaas altyapı) yüklü JIRA sunucu uygulaması</span><span class="sxs-lookup"><span data-stu-id="649ce-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="649ce-114">HTTPS etkinleştirilmiş JIRA sunucusudur</span><span class="sxs-lookup"><span data-stu-id="649ce-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="649ce-115">Aşağıdaki bölümüne JIRA eklentisi için desteklenen sürümleri bahsedilen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="649ce-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="649ce-116">JIRA sunucu kimlik doğrulaması için Azure AD oturum açma sayfasına özellikle Internet üzerinden erişilebildiğinden ve Azure AD'den belirteç alamaz gerekir</span><span class="sxs-lookup"><span data-stu-id="649ce-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="649ce-117">Yönetici kimlik bilgileri JIRA ayarlanır</span><span class="sxs-lookup"><span data-stu-id="649ce-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="649ce-118">WebSudo JIRA içinde devre dışı bırakıldı</span><span class="sxs-lookup"><span data-stu-id="649ce-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="649ce-119">JIRA sunucu uygulamasından oluşturulan test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="649ce-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="649ce-120">Bu öğreticide adımları test etmek için bir üretim ortamında JIRA birini kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="649ce-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="649ce-121">Geliştirme veya uygulamanın hazırlama ortamında tümleştirme önce test ve üretim ortamına kullanın.</span><span class="sxs-lookup"><span data-stu-id="649ce-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="649ce-122">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="649ce-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="649ce-123">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="649ce-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="649ce-124">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="649ce-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="649ce-125">JIRA desteklenen sürümleri</span><span class="sxs-lookup"><span data-stu-id="649ce-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="649ce-126">Şimdi itibariyle JIRA aşağıdaki sürümleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="649ce-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="649ce-127">JIRA çekirdek ve yazılım: 6.0 için 7.2.0</span><span class="sxs-lookup"><span data-stu-id="649ce-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="649ce-128">JIRA hizmet masasına: 3.0 3.2 için</span><span class="sxs-lookup"><span data-stu-id="649ce-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="649ce-129">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="649ce-129">Scenario description</span></span>
<span data-ttu-id="649ce-130">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="649ce-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="649ce-131">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="649ce-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="649ce-132">Microsoft tarafından JIRA SAML SSO Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="649ce-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="649ce-133">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="649ce-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="649ce-134">Microsoft tarafından JIRA SAML SSO Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="649ce-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="649ce-135">Azure AD JIRA SAML SSO Microsoft tarafından tümleştirilmesi yapılandırmak için Microsoft tarafından JIRA SAML SSO Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="649ce-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="649ce-136">**Microsoft tarafından JIRA SAML SSO Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="649ce-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="649ce-137">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="649ce-139">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="649ce-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="649ce-140">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="649ce-140">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="649ce-142">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="649ce-144">Arama kutusuna **JIRA SAML SSO Microsoft tarafından**.</span><span class="sxs-lookup"><span data-stu-id="649ce-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="649ce-146">Sonuçlar panelinde seçin **JIRA SAML SSO Microsoft tarafından**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="649ce-148">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="649ce-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="649ce-149">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma JIRA SAML SSO "Britta Simon." olarak adlandırılan bir test kullanıcıyı temel alarak Microsoft tarafından test etme</span><span class="sxs-lookup"><span data-stu-id="649ce-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="649ce-150">Tekli çalışmaya oturum için Azure AD ne karşılık gelen JIRA SAML SSO Microsoft tarafından bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="649ce-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="649ce-151">Diğer bir deyişle, bir Azure AD kullanıcısının ve Microsoft tarafından JIRA SAML SSO ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="649ce-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="649ce-152">Microsoft tarafından JIRA SAML SSO içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="649ce-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="649ce-153">Yapılandırma ve Azure AD çoklu oturum açma JIRA SAML SSO Microsoft tarafından test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="649ce-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="649ce-154">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="649ce-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="649ce-155">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="649ce-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="649ce-156">**[Microsoft test kullanıcı tarafından JIRA SAML SSO oluşturma](#creating-a-jira-saml-sso-by-microsoft-test-user)**  - Britta Simon, karşılık gelen JIRA SAML SSO kullanıcı Azure AD gösterimini bağlantılı Microsoft tarafından sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="649ce-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="649ce-157">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="649ce-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="649ce-158">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="649ce-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="649ce-159">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="649ce-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="649ce-160">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Microsoft uygulaması tarafından JIRA SAML SSO yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="649ce-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="649ce-161">**Microsoft tarafından JIRA SAML SSO ile Azure AD çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="649ce-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="649ce-162">Azure portalında üzerinde **JIRA SAML SSO Microsoft tarafından** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="649ce-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="649ce-164">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="649ce-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="649ce-166">Üzerinde **JIRA SAML SSO Microsoft Domain ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="649ce-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="649ce-168">a.</span><span class="sxs-lookup"><span data-stu-id="649ce-168">a.</span></span> <span data-ttu-id="649ce-169">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="649ce-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="649ce-170">b.</span><span class="sxs-lookup"><span data-stu-id="649ce-170">b.</span></span> <span data-ttu-id="649ce-171">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="649ce-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="649ce-172">c.</span><span class="sxs-lookup"><span data-stu-id="649ce-172">c.</span></span> <span data-ttu-id="649ce-173">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="649ce-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="649ce-174">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="649ce-174">These values are not real.</span></span> <span data-ttu-id="649ce-175">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="649ce-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="649ce-176">Adlandırılmış bir URL olması durumunda bağlantı noktası isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="649ce-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="649ce-177">Öğreticide daha sonra açıklanan Jira eklentisi yapılandırma sırasında bu değerleri alma.</span><span class="sxs-lookup"><span data-stu-id="649ce-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="649ce-178">Oluşturulacak **meta veri** url, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="649ce-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="649ce-179">a.</span><span class="sxs-lookup"><span data-stu-id="649ce-179">a.</span></span> <span data-ttu-id="649ce-180">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="649ce-180">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="649ce-182">b.</span><span class="sxs-lookup"><span data-stu-id="649ce-182">b.</span></span> <span data-ttu-id="649ce-183">Tıklatın **uç noktaları** açmak için **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="649ce-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="649ce-185">c.</span><span class="sxs-lookup"><span data-stu-id="649ce-185">c.</span></span> <span data-ttu-id="649ce-186">Kopyalamak için Kopyala düğmesini tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="649ce-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="649ce-188">d.</span><span class="sxs-lookup"><span data-stu-id="649ce-188">d.</span></span> <span data-ttu-id="649ce-189">Şimdi özellik sayfasına gidin **JIRA SAML SSO Microsoft tarafından** ve kopyalama **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="649ce-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="649ce-191">e.</span><span class="sxs-lookup"><span data-stu-id="649ce-191">e.</span></span> <span data-ttu-id="649ce-192">Oluştur **meta veri URL'sini** şu biçimi kullanarak: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` ve daha sonra eklentiyi yapılandırma için kullanılan bu değer Not Defteri'nde kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="649ce-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="649ce-193">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-193">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="649ce-195">Kişi [Microsoft](mailto:waadpartners@microsoft.com) JIRA eklentisi için aşağıdaki bilgileri ile.</span><span class="sxs-lookup"><span data-stu-id="649ce-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="649ce-196">Müşteri adı:</span><span class="sxs-lookup"><span data-stu-id="649ce-196">Customer Name:</span></span>
    *   <span data-ttu-id="649ce-197">Birincil etki alanı adı:</span><span class="sxs-lookup"><span data-stu-id="649ce-197">Primary domain name:</span></span>
    *   <span data-ttu-id="649ce-198">Azure AD Premium: Evet/Hayır (eklentisi kullanılabilir tüm müşteri ücretsiz, basit ve Premium SKU için)</span><span class="sxs-lookup"><span data-stu-id="649ce-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="649ce-199">Bu tümleştirme kullanarak kullanıcıların sayısı:</span><span class="sxs-lookup"><span data-stu-id="649ce-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="649ce-200">JIRA sürümü:</span><span class="sxs-lookup"><span data-stu-id="649ce-200">JIRA Version:</span></span>
    *   <span data-ttu-id="649ce-201">Açıklama:</span><span class="sxs-lookup"><span data-stu-id="649ce-201">Comments:</span></span>

7. <span data-ttu-id="649ce-202">Farklı web tarayıcısı penceresinde JIRA Örneğiniz için yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="649ce-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="649ce-203">Dişlisine üzerine gelin ve tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="649ce-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="649ce-205">Eklentiler sekmesi bölümü altında tıklatın **eklentileri yönetme**.</span><span class="sxs-lookup"><span data-stu-id="649ce-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="649ce-207">Microsoft tarafından sağlanan eklentisini el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="649ce-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="649ce-208">Eklenti yüklendikten sonra görünür **kullanıcı yüklü** eklentileri bölümünü **yönetmek eklenti** bölümü.</span><span class="sxs-lookup"><span data-stu-id="649ce-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="649ce-209">Tıklatın **yapılandırma** yeni eklenti yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="649ce-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="649ce-210">Yapılandırma sayfasında şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="649ce-210">Perform following steps on configuration page:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="649ce-212">a.</span><span class="sxs-lookup"><span data-stu-id="649ce-212">a.</span></span> <span data-ttu-id="649ce-213">İçinde **meta veri URL'sini** Yapıştır **meta veri URL'sini** Azure AD'den oluşturulur ve tıklatın **gidermek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="649ce-214">IDP meta veri URL'sini okur ve tüm alanları bilgileri doldurur.</span><span class="sxs-lookup"><span data-stu-id="649ce-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="649ce-215">Varsayılan SAML kullanıcı kimliği konumu ad tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="649ce-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="649ce-216">Bu öznitelik seçeneği ile değiştirin ve uygun öznitelik adını girin.</span><span class="sxs-lookup"><span data-stu-id="649ce-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="649ce-217">Yani hata meta verileri çözümlenmesinde uygulamayı karşı eşlenen yalnızca bir sertifika olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="649ce-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="649ce-218">Meta Veri Çözümleme sırasında birden fazla sertifika varsa yönetici bir hata alır.</span><span class="sxs-lookup"><span data-stu-id="649ce-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="649ce-219">b.</span><span class="sxs-lookup"><span data-stu-id="649ce-219">b.</span></span> <span data-ttu-id="649ce-220">Kopya **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** değerleri ve bunları yapıştırın **tanımlayıcı, yanıt URL'si ve oturum açma URL'si** kutularındaki sırasıyla söz **JIRA SAML SSO Microsoft Domain ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="649ce-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="649ce-221">c.</span><span class="sxs-lookup"><span data-stu-id="649ce-221">c.</span></span> <span data-ttu-id="649ce-222">İçinde **oturum açma düğmesi adı** , kuruluşunuzda kullanıcıların oturum açma ekranında düğmesinin adını yazın.</span><span class="sxs-lookup"><span data-stu-id="649ce-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="649ce-223">d.</span><span class="sxs-lookup"><span data-stu-id="649ce-223">d.</span></span> <span data-ttu-id="649ce-224">İçinde **SAML kullanıcı kimliği konumları** seçin **kullanıcı kimliğidir konu deyimi NameIdentifier öğesinde** veya **kullanıcı kimliği olan bir öznitelik öğedeki**.</span><span class="sxs-lookup"><span data-stu-id="649ce-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="649ce-225">Bu kimliği JIRA kullanıcı kimliği olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="649ce-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="649ce-226">Kullanıcı Kimliği eşleşmiyorsa, ardından sistemi oturum açmak kullanıcılar izin vermez.</span><span class="sxs-lookup"><span data-stu-id="649ce-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="649ce-227">e.</span><span class="sxs-lookup"><span data-stu-id="649ce-227">e.</span></span> <span data-ttu-id="649ce-228">Seçerseniz **kullanıcı kimliği olan bir öznitelik öğedeki** seçeneği, ardından **öznitelik adı** metin kullanıcı kimliği beklenirken özniteliğin adını yazın.</span><span class="sxs-lookup"><span data-stu-id="649ce-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="649ce-229">f.</span><span class="sxs-lookup"><span data-stu-id="649ce-229">f.</span></span> <span data-ttu-id="649ce-230">Azure AD ile Federasyon etki alanını (örneğin, ADFS vb.) kullanıyorsanız, tıklayın **giriş bölgesi bulmayı etkinleştirmek** seçeneği ve yapılandırma **etki alanı adı**.</span><span class="sxs-lookup"><span data-stu-id="649ce-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="649ce-231">g.</span><span class="sxs-lookup"><span data-stu-id="649ce-231">g.</span></span> <span data-ttu-id="649ce-232">İçinde **etki alanı adı** ADFS tabanlı oturum açma durumunda burada etki alanı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="649ce-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="649ce-233">h.</span><span class="sxs-lookup"><span data-stu-id="649ce-233">h.</span></span> <span data-ttu-id="649ce-234">Denetleme **etkinleştirmek tek oturum kapatma** bir kullanıcı oturum açtığında JIRA Azure AD'den oturumunuzu etmek istiyor.</span><span class="sxs-lookup"><span data-stu-id="649ce-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="649ce-235">ı.</span><span class="sxs-lookup"><span data-stu-id="649ce-235">i.</span></span> <span data-ttu-id="649ce-236">' I tıklatın **kaydetmek** düğmesini tıklatarak ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="649ce-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="649ce-237">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="649ce-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="649ce-238">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="649ce-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="649ce-239">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="649ce-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="649ce-240">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="649ce-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="649ce-241">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="649ce-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="649ce-243">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="649ce-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="649ce-244">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="649ce-246">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="649ce-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="649ce-248">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="649ce-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="649ce-250">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="649ce-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="649ce-252">a.</span><span class="sxs-lookup"><span data-stu-id="649ce-252">a.</span></span> <span data-ttu-id="649ce-253">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="649ce-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="649ce-254">b.</span><span class="sxs-lookup"><span data-stu-id="649ce-254">b.</span></span> <span data-ttu-id="649ce-255">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="649ce-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="649ce-256">c.</span><span class="sxs-lookup"><span data-stu-id="649ce-256">c.</span></span> <span data-ttu-id="649ce-257">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="649ce-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="649ce-258">d.</span><span class="sxs-lookup"><span data-stu-id="649ce-258">d.</span></span> <span data-ttu-id="649ce-259">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="649ce-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="649ce-260">Microsoft test kullanıcı tarafından JIRA SAML SSO oluşturma</span><span class="sxs-lookup"><span data-stu-id="649ce-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="649ce-261">JIRA şirket içi sunucuya oturum açmak Azure AD kullanıcıları etkinleştirmek için bunların JIRA SAML SSO Microsoft tarafından sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="649ce-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="649ce-262">Microsoft tarafından JIRA SAML SSO için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="649ce-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="649ce-263">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="649ce-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="649ce-264">JIRA şirket içi sunucunuza yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="649ce-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="649ce-265">Dişlisine üzerine gelin ve tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="649ce-265">Hover on cog and click the **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="649ce-267">Girmek için yönetici erişimi sayfasına yönlendirilirsiniz **parola** tıklatıp **Onayla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="649ce-269">Altında **kullanıcı yönetimi** bölüm sekmesini tıklatın, **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="649ce-269">Under **User management** tab section, click **create user**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="649ce-271">Üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="649ce-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="649ce-273">a.</span><span class="sxs-lookup"><span data-stu-id="649ce-273">a.</span></span> <span data-ttu-id="649ce-274">İçinde **e-posta adresi** metin kutusuna, kullanıcının e-posta adresi türü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="649ce-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="649ce-275">b.</span><span class="sxs-lookup"><span data-stu-id="649ce-275">b.</span></span> <span data-ttu-id="649ce-276">İçinde **tam adı** metin kutusuna, Britta Simon gibi kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="649ce-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="649ce-277">c.</span><span class="sxs-lookup"><span data-stu-id="649ce-277">c.</span></span> <span data-ttu-id="649ce-278">İçinde **kullanıcıadı** metin kutusu, kullanıcı e-posta türünü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="649ce-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="649ce-279">d.</span><span class="sxs-lookup"><span data-stu-id="649ce-279">d.</span></span> <span data-ttu-id="649ce-280">İçinde **parola** metin kutusuna, kullanıcının parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="649ce-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="649ce-281">e.</span><span class="sxs-lookup"><span data-stu-id="649ce-281">e.</span></span> <span data-ttu-id="649ce-282">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="649ce-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="649ce-283">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="649ce-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="649ce-284">Bu bölümde, Microsoft tarafından JIRA SAML SSO için erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="649ce-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="649ce-286">**Microsoft tarafından JIRA SAML SSO Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="649ce-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="649ce-287">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="649ce-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="649ce-289">Uygulamalar listesinde **JIRA SAML SSO Microsoft tarafından**.</span><span class="sxs-lookup"><span data-stu-id="649ce-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="649ce-291">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="649ce-291">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="649ce-293">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="649ce-293">Click **Add** button.</span></span> <span data-ttu-id="649ce-294">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="649ce-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="649ce-296">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="649ce-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="649ce-297">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="649ce-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="649ce-298">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="649ce-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="649ce-299">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="649ce-299">Testing single sign-on</span></span>

<span data-ttu-id="649ce-300">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="649ce-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="649ce-301">Erişim paneli Microsoft parçasında tarafından JIRA SAML SSO tıklattığınızda, otomatik olarak, JIRA SAML SSO Microsoft uygulaması tarafından açan.</span><span class="sxs-lookup"><span data-stu-id="649ce-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="649ce-302">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="649ce-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="649ce-303">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="649ce-303">Additional resources</span></span>

* [<span data-ttu-id="649ce-304">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="649ce-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="649ce-305">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="649ce-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

