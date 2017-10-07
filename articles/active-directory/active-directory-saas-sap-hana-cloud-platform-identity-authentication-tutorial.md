---
title: "Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Nasıl tooconfigure çoklu oturum açmayı Azure Active Directory arasında ve SAP HANA bulut platformu kimlik doğrulama öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="0e9af-103">Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="0e9af-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="0e9af-104">Bu öğreticide, nasıl toointegrate SAP öğrenin HANA bulut platformu kimlik doğrulaması Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e9af-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0e9af-105">SAP HANA bulut platformu kimlik doğrulama ana IDP hello gibi Azure AD kullanarak bir proxy IDP tooaccess SAP uygulamaları olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="0e9af-106">SAP HANA bulut platformu kimlik doğrulaması Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0e9af-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e9af-107">Access tooSAP uygulaması olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0e9af-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="0e9af-108">Kullanıcıların tooautomatically get açan tooSAP uygulamaları çoklu oturum açma (SSO) ile Azure AD hesaplarına etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0e9af-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e9af-109">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="0e9af-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="0e9af-110">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e9af-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0e9af-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0e9af-111">Prerequisites</span></span>

<span data-ttu-id="0e9af-112">SAP HANA bulut platformu kimlik doğrulaması ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e9af-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="0e9af-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0e9af-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0e9af-114">A **SAP HANA bulut platformu kimlik doğrulama** SSO abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0e9af-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="0e9af-115">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0e9af-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="0e9af-116">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e9af-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e9af-117">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0e9af-118">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e9af-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e9af-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0e9af-119">Scenario description</span></span>
<span data-ttu-id="0e9af-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="0e9af-121">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0e9af-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e9af-122">SAP HANA bulut platformu kimlik doğrulama hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0e9af-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="0e9af-123">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="0e9af-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="0e9af-124">Merhaba teknik ayrıntılara girmeden önce önemli toounderstand hello kavramları toolook adresindeki oluşturacağız olur.</span><span class="sxs-lookup"><span data-stu-id="0e9af-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="0e9af-125">Merhaba SAP HANA bulut platformu kimlik doğrulaması ve Azure Active Directory Federasyon tooimplement SSO uygulamalar veya SAP uygulamaları ve Hizmetleri SAP HANA bulut Platform kimliği tarafından korunan ile AAD (olarak bir IDP) tarafından korunan hizmetler arasında sağlar Kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="0e9af-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="0e9af-126">Şu anda, SAP HANA bulut platformu kimlik doğrulama bir Proxy Kimlik sağlayıcısı tooSAP uygulamalar olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="0e9af-127">Azure Active Directory kimlik sağlayıcısı bu kurulumunda önde gelen hello sırayla görür.</span><span class="sxs-lookup"><span data-stu-id="0e9af-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="0e9af-128">Aşağıdaki diyagramda hello bunu göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="0e9af-128">hello following diagram illustrates this:</span></span>    

![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="0e9af-130">Bu kurulum ile SAP HANA bulut platformu kimlik doğrulama kiracınızı Azure Active Directory'de güvenilir bir uygulama olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="0e9af-131">Daha sonra tüm SAP uygulamaları ve Hizmetleri bu şekilde aracılığıyla tooprotect istediğiniz hello SAP HANA bulut platformu kimlik doğrulama yönetim konsolunda yapılandırılan!</span><span class="sxs-lookup"><span data-stu-id="0e9af-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="0e9af-132">Bu erişim izni verme tooSAP uygulamalar için yetkilendirme anlamına gelir ve böyle bir kurulum (olarak Azure Active Directory'de karşılıklı tooconfiguring yetkilendirme) için SAP HANA bulut platformu kimlik doğrulama gereksinimlerini tootake yerine Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="0e9af-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="0e9af-133">SAP HANA bulut platformu kimlik doğrulama hello Azure Active Directory Marketi üzerinden bir uygulama olarak yapılandırarak, gerekli bireysel talepler yapılandırma care of tootake gerekmeyen / SAML onaylar ve dönüşümleri gerekli tooproduce bir SAP uygulamaları için geçerli bir kimlik doğrulama belirteci.</span><span class="sxs-lookup"><span data-stu-id="0e9af-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="0e9af-134">Şu anda Web SSO her iki taraf tarafından yalnızca test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="0e9af-135">Uygulama API veya API API iletişimi için gerekli akışları çalışması gerekir, ancak, henüz test edilmemiştir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="0e9af-136">Bunlar bir sonraki etkinliklere bir parçası olarak test edilir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="0e9af-137">SAP HANA bulut platformu kimlik doğrulama hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0e9af-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="0e9af-138">Azure AD'ye tooconfigure hello tümleştirme SAP HANA bulut platformu kimlik doğrulama, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd SAP HANA bulut platformu kimlik doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e9af-139">**SAP HANA bulut platformu kimlik doğrulama hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e9af-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e9af-140">Merhaba, [ **Azure Yönetim Portalı**](https://portal.azure.com), üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0e9af-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e9af-142">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e9af-143">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-143">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0e9af-145">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e9af-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0e9af-147">Merhaba arama kutusuna yazın **SAP HANA bulut platformu kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="0e9af-149">Merhaba Sonuçlar panelinde seçin **SAP HANA bulut platformu kimlik doğrulama**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0e9af-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e9af-151">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0e9af-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0e9af-152">Bu bölümde, yapılandırma ve SAP HANA bulut Platform kimliği "Britta Simon" adlı bir test kullanıcı tabanlı kimlik doğrulaması ile Azure AD SSO test etme.</span><span class="sxs-lookup"><span data-stu-id="0e9af-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e9af-153">SSO toowork için hangi hello karşılık gelen SAP HANA bulut platformu kimlik doğrulama içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="0e9af-154">Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP HANA bulut platformu kimlik doğrulama hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="0e9af-155">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** SAP HANA bulut platformu kimlik doğrulama içinde.</span><span class="sxs-lookup"><span data-stu-id="0e9af-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="0e9af-156">tooconfigure ve SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e9af-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e9af-157">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0e9af-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e9af-158">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0e9af-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e9af-159">**[SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir SAP HANA bulut platformu kimlik doğrulama olarak, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0e9af-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0e9af-160">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0e9af-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e9af-161">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="0e9af-162">Azure AD SSO yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e9af-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="0e9af-163">Bu bölümdeki hello Azure Yönetim Portalı'nda Azure AD SSO'yu etkinleştirmek ve çoklu oturum açma, SAP HANA bulut platformu kimlik doğrulama uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0e9af-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="0e9af-164">SAP HANA bulut platformu kimlik doğrulama uygulaması hello SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0e9af-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0e9af-165">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="0e9af-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0e9af-166">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-166">hello following screenshot shows an example for this.</span></span>

![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="0e9af-168">**SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e9af-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e9af-169">Hello üzerinde hello Azure Yönetim Portalı'nda **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0e9af-171">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0e9af-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın][5]

3. <span data-ttu-id="0e9af-173">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** SAP uygulamanız bir öznitelik örneğin "firstName" görüyorsa iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="0e9af-174">Merhaba SAML belirteci öznitelikleri iletişim kutusunda hello "firstName" özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="0e9af-175">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın][6]

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="0e9af-178">Merhaba, **öznitelik adı** metin kutusuna, türü hello öznitelik adı "ad".</span><span class="sxs-lookup"><span data-stu-id="0e9af-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="0e9af-179">Merhaba gelen **öznitelik değeri** listesinde, select hello öznitelik değeri "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="0e9af-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="0e9af-180">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e9af-180">Click **Ok**.</span></span>

4. <span data-ttu-id="0e9af-181">Merhaba üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulaması etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e9af-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="0e9af-183">Merhaba, **oturum üzerinde URL'si** metin kutusuna, hello oturum hello SAP uygulama için URL'yi yazın.</span><span class="sxs-lookup"><span data-stu-id="0e9af-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="0e9af-184">Merhaba, **tanımlayıcısı** metin kutusuna, düzeni izleyen türü başlangıç değeri:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="0e9af-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="0e9af-185">Bu değer bilmiyorsanız, lütfen hello SAP HANA bulut platformu kimlik doğrulama belgeleri izleyin [Kiracı SAML 2.0 yapılandırma](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="0e9af-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="0e9af-186">Merhaba üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulama Yapılandırması** 'yi tıklatın **SAP HANA bulut platformu kimlik doğrulama** tooopen **oturum açmayapılandırma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="0e9af-187">Ardından, tıklatın **SAML XML meta verilerini** ve hello dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="0e9af-190">Uygulamanız için yapılandırılmış SSO tooget tooSAP HANA bulut Platform kimliği kimlik doğrulama yönetim konsolunda gidin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="0e9af-191">Merhaba URL deseni takip hello sahiptir:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="0e9af-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="0e9af-192">Ardından hello belgelerine SAP HANA bulut platformu kimlik doğrulama üzerinde çok izleyin[SAP HANA bulut platformu kimlik doğrulaması sırasında Kurumsal kimlik sağlayıcısı yapılandırma Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="0e9af-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="0e9af-193">Hello Azure Yönetim Portalı'nda tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e9af-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="0e9af-194">Yalnızca tooadd isterseniz ve SSO'yu etkinleştirmek için başka bir SAP uygulama adımları izleyerek hello devam edin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="0e9af-195">SAP HANA bulut platformu kimlik doğrulama başka bir kopyası hello bölüm "Ekleme SAP HANA bulut platformu kimlik doğrulama hello galerisinden" tooadd altındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="0e9af-196">Merhaba üzerinde hello Azure Yönetim Portalı'nda **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **bağlantılı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Bağlantılı oturum açma özelliğini yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="0e9af-198">Ardından, hello yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="0e9af-199">Merhaba yeni uygulama hello önceki SAP uygulamasının hello SSO yapılandırmasını özelliğinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="0e9af-200">Lütfen emin olun kullanım hello hello SAP HANA bulut Platform kimliği kimlik doğrulama yönetim konsolunu aynı Kurumsal kimlik sağlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="0e9af-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e9af-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e9af-201">Create an Azure AD test user</span></span>
<span data-ttu-id="0e9af-202">Merhaba amacı, bu bölümde toocreate bir sınama kullanıcısı Britta Simon adlı hello yeni Portalı'nda ' dir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0e9af-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e9af-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e9af-205">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0e9af-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e9af-207">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="0e9af-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e9af-209">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e9af-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e9af-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="0e9af-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="0e9af-214">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0e9af-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="0e9af-215">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="0e9af-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e9af-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="0e9af-217">SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e9af-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="0e9af-218">SAP HANA bulut platformu kimlik doğrulaması bir kullanıcı toocreate gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="0e9af-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="0e9af-219">Hello Azure AD kullanıcı deposunda kullanıcılar hello SSO işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e9af-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="0e9af-220">SAP HANA bulut platformu kimlik doğrulama hello Kimlik Federasyonu seçeneğini destekler.</span><span class="sxs-lookup"><span data-stu-id="0e9af-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="0e9af-221">Merhaba Kurumsal kimlik sağlayıcısı tarafından kimliği doğrulanmış hello kullanıcılar hello kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama, yoksa bu seçenek hello uygulama toocheck sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e9af-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="0e9af-222">Merhaba varsayılan ayarı hello Kimlik Federasyonu seçeneği devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="0e9af-223">Kimlik Federasyonu etkinleştirilirse, SAP HANA bulut platformu kimlik doğrulama içeri aktarılan yalnızca hello mümkün tooaccess Merhaba uygulaması kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="0e9af-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="0e9af-224">Nasıl tooenable veya devre dışı bırak SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu bakın SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu etkinleştirme hakkında daha fazla bilgi için [Kimlik Federasyonu yapılandırma Merhaba kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama ile. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="0e9af-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0e9af-225">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="0e9af-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0e9af-226">Bu bölümde, kendi erişim tooSAP HANA bulut platformu kimlik doğrulama vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e9af-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0e9af-228">**tooassign Britta Simon tooSAP HANA bulut platformu kimlik doğrulama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e9af-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e9af-229">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0e9af-231">Merhaba uygulamalar listesinde **SAP HANA bulut platformu kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="0e9af-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0e9af-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0e9af-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e9af-235">Click **Add** button.</span></span> <span data-ttu-id="0e9af-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0e9af-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0e9af-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e9af-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e9af-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e9af-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="0e9af-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="0e9af-241">Test single sign-on</span></span>

<span data-ttu-id="0e9af-242">Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="0e9af-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e9af-243">Merhaba SAP HANA bulut platformu kimlik doğrulama hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SAP HANA bulut platformu kimlik doğrulama uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e9af-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0e9af-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0e9af-244">Additional resources</span></span>

* [<span data-ttu-id="0e9af-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0e9af-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e9af-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0e9af-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png