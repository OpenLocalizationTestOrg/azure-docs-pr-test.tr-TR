---
title: "Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve SAP HANA bulut platformu kimlik doğrulama arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="00686-103">Öğretici: SAP HANA bulut platformu kimlik doğrulama Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="00686-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="00686-104">Bu öğreticide, SAP HANA bulut platformu kimlik doğrulaması Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="00686-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="00686-105">SAP HANA bulut platformu kimlik doğrulama, bir proxy sunucu olarak IDP ana IDP Azure AD kullanarak SAP uygulamalarına erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="00686-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="00686-106">SAP HANA bulut platformu kimlik doğrulaması Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="00686-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00686-107">SAP uygulama erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="00686-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="00686-108">Otomatik olarak uygulamaları çoklu oturum açma (SSO) ile Azure AD hesaplarına SAP açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="00686-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="00686-109">Hesaplarınızı bir merkezi konumda - Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="00686-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="00686-110">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00686-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="00686-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="00686-111">Prerequisites</span></span>

<span data-ttu-id="00686-112">SAP HANA bulut platformu kimlik doğrulaması ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="00686-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="00686-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="00686-113">An Azure AD subscription</span></span>
- <span data-ttu-id="00686-114">A **SAP HANA bulut platformu kimlik doğrulama** SSO abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="00686-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="00686-115">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="00686-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="00686-116">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="00686-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00686-117">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="00686-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="00686-118">Bir Azure AD deneme ortam yoksa, alabileceğiniz bir [bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00686-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00686-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="00686-119">Scenario description</span></span>
<span data-ttu-id="00686-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="00686-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="00686-121">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="00686-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00686-122">Galeriden SAP HANA bulut platformu kimlik doğrulama ekleme</span><span class="sxs-lookup"><span data-stu-id="00686-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="00686-123">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="00686-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="00686-124">Teknik ayrıntılara girmeden önce bakmak oluşturacağız kavramları anlamanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="00686-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="00686-125">SAP HANA bulut platformu kimlik doğrulaması ve Azure Active Directory Federasyon, uygulamalar veya SAP uygulamaları ve Hizmetleri SAP HANA bulut platformu kimlik doğrulama tarafından korunan ile AAD (olarak bir IDP) tarafından korunan hizmetler arasında SSO uygulanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="00686-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="00686-126">Şu anda, SAP HANA bulut platformu kimlik doğrulama SAP uygulamaları için bir Proxy Kimlik sağlayıcısı gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="00686-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="00686-127">Azure Active Directory sırayla bu kurulumunda başında kimlik sağlayıcısı gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="00686-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="00686-128">Aşağıdaki diyagram bu gösterir:</span><span class="sxs-lookup"><span data-stu-id="00686-128">The following diagram illustrates this:</span></span>    

![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="00686-130">Bu kurulum ile SAP HANA bulut platformu kimlik doğrulama kiracınızı Azure Active Directory'de güvenilir bir uygulama olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="00686-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="00686-131">Daha sonra tüm SAP uygulamalar ve hizmetler bu şekilde korumak istediğiniz SAP HANA bulut platformu kimlik doğrulama yönetim konsolunda yapılandırılan!</span><span class="sxs-lookup"><span data-stu-id="00686-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="00686-132">Başka bir deyişle, SAP uygulamaları ve hizmetlerine erişim izni verme için yetkilendirme (yetkilendirme Azure Active Directory'de yapılandırma) aksine Kurulum SAP HANA bulut platformu kimlik doğrulama yerinde yapması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="00686-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="00686-133">SAP HANA bulut platformu kimlik doğrulaması Azure Active Directory Marketi üzerinden bir uygulama olarak yapılandırarak, gerekli bireysel talepler yapılandırmayı dikkatli gerekmez / SAML onaylar ve dönüşümleri gerekli SAP uygulamaları için geçerli bir kimlik doğrulama belirteci üretmek.</span><span class="sxs-lookup"><span data-stu-id="00686-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="00686-134">Şu anda Web SSO her iki taraf tarafından yalnızca test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="00686-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="00686-135">Uygulama API veya API API iletişimi için gerekli akışları çalışması gerekir, ancak, henüz test edilmemiştir.</span><span class="sxs-lookup"><span data-stu-id="00686-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="00686-136">Bunlar bir sonraki etkinliklere bir parçası olarak test edilir.</span><span class="sxs-lookup"><span data-stu-id="00686-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="00686-137">SAP HANA bulut platformu kimlik doğrulama Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="00686-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="00686-138">SAP HANA bulut platformu kimlik doğrulama tümleştirme Azure AD'ye yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden SAP HANA bulut platformu kimlik doğrulama eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00686-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00686-139">**SAP HANA bulut platformu kimlik doğrulama Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="00686-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00686-140">İçinde [ **Azure Yönetim Portalı**](https://portal.azure.com), sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="00686-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00686-142">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="00686-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00686-143">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="00686-143">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="00686-145">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00686-145">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="00686-147">Arama kutusuna **SAP HANA bulut platformu kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="00686-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="00686-149">Sonuçlar panelinde seçin **SAP HANA bulut platformu kimlik doğrulama**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00686-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="00686-151">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="00686-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="00686-152">Bu bölümde, yapılandırma ve SAP HANA bulut Platform kimliği "Britta Simon" adlı bir test kullanıcı tabanlı kimlik doğrulaması ile Azure AD SSO test etme.</span><span class="sxs-lookup"><span data-stu-id="00686-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="00686-153">Çalışmak SSO için Azure AD karşılık gelen kullanıcı SAP HANA bulut platformu kimlik doğrulama için bir kullanıcı Azure AD'de nedir bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="00686-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="00686-154">Diğer bir deyişle, bir Azure AD kullanıcısının SAP HANA bulut platformu kimlik doğrulama ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="00686-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="00686-155">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** SAP HANA bulut platformu kimlik doğrulama içinde.</span><span class="sxs-lookup"><span data-stu-id="00686-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="00686-156">Yapılandırmak ve SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="00686-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00686-157">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="00686-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00686-158">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="00686-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00686-159">**[SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı SAP HANA bulut platformu kimlik doğrulama sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="00686-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="00686-160">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="00686-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00686-161">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="00686-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="00686-162">Azure AD SSO yapılandırma</span><span class="sxs-lookup"><span data-stu-id="00686-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="00686-163">Bu bölümde, Azure Yönetim Portalı'nda Azure AD SSO'yu etkinleştirmek ve çoklu oturum açma, SAP HANA bulut platformu kimlik doğrulama uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="00686-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="00686-164">SAP HANA bulut platformu kimlik doğrulama uygulaması SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="00686-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="00686-165">Bu öznitelik değerlerini yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="00686-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="00686-166">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="00686-166">The following screenshot shows an example for this.</span></span>

![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="00686-168">**SAP HANA bulut platformu kimlik doğrulaması ile Azure AD SSO yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="00686-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="00686-169">Azure Yönetim Portalı'nda üzerinde **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="00686-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="00686-171">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="00686-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın][5]

3. <span data-ttu-id="00686-173">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** SAP uygulamanız bir öznitelik örneğin "firstName" görüyorsa iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="00686-174">SAML belirteci öznitelikleri iletişim kutusunda, "ad" özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="00686-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="00686-175">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın][6]

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="00686-178">İçinde **öznitelik adı** metin kutusuna, öznitelik adı "ad" yazın.</span><span class="sxs-lookup"><span data-stu-id="00686-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="00686-179">Gelen **öznitelik değeri** listesinde, öznitelik değeri "user.givenname" seçin.</span><span class="sxs-lookup"><span data-stu-id="00686-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="00686-180">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="00686-180">Click **Ok**.</span></span>

4. <span data-ttu-id="00686-181">Üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulaması etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="00686-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="00686-183">İçinde **oturum üzerinde URL'si** metin kutusuna, oturum SAP uygulama için URL'yi yazın.</span><span class="sxs-lookup"><span data-stu-id="00686-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="00686-184">İçinde **tanımlayıcısı** metin kutusuna, desen aşağıdaki değeri yazın:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="00686-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="00686-185">Bu değer bilmiyorsanız, lütfen SAP HANA bulut platformu kimlik doğrulama belgeleri izleyin [Kiracı SAML 2.0 yapılandırma](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="00686-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="00686-186">Üzerinde **SAP HANA bulut Platform kimliği kimlik doğrulama Yapılandırması** 'yi tıklatın **SAP HANA bulut platformu kimlik doğrulama** açmak için **yapılandırma oturum açma** iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="00686-187">Ardından, tıklatın **SAML XML meta verilerini** ve dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="00686-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="00686-190">Uygulamanız için yapılandırılmış SSO almak için SAP HANA bulut Platform kimlik kimlik doğrulama yönetim konsoluna gidin.</span><span class="sxs-lookup"><span data-stu-id="00686-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="00686-191">URL aşağıdaki deseni vardır:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="00686-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="00686-192">Ardından, SAP HANA bulut platformu kimlik doğrulama için belgeleri takip [SAP HANA bulut platformu kimlik doğrulaması sırasında Kurumsal kimlik sağlayıcısı yapılandırma Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="00686-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="00686-193">Azure Yönetim Portalı'nda tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00686-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="00686-194">Yalnızca ekleyin ve başka bir SAP uygulama için SSO'yu etkinleştirmek isterseniz, aşağıdaki adımları devam edin.</span><span class="sxs-lookup"><span data-stu-id="00686-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="00686-195">"Ekleme SAP HANA bulut platformu kimlik doğrulama galerisinden" bölümü altındaki adımları yineleyin SAP HANA bulut platformu kimlik doğrulama başka bir örneği eklemek için.</span><span class="sxs-lookup"><span data-stu-id="00686-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="00686-196">Azure Yönetim Portalı'nda üzerinde **SAP HANA bulut platformu kimlik doğrulama** uygulama tümleştirme sayfasını tıklatın **bağlantılı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="00686-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Bağlantılı oturum açma özelliğini yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="00686-198">Yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="00686-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="00686-199">Yeni uygulama önceki SAP uygulaması için SSO yapılandırma özelliğinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="00686-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="00686-200">Lütfen, aynı Kurumsal kimlik sağlayıcıları SAP HANA bulut Platform kimliği kimlik doğrulama yönetim konsolunda kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="00686-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="00686-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="00686-201">Create an Azure AD test user</span></span>
<span data-ttu-id="00686-202">Bu bölümün amacı, Britta Simon adlı yeni Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="00686-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="00686-204">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="00686-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00686-205">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="00686-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00686-207">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="00686-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00686-209">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00686-211">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="00686-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="00686-213">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00686-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="00686-214">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="00686-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="00686-215">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="00686-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="00686-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="00686-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="00686-217">SAP HANA bulut platformu kimlik doğrulama test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="00686-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="00686-218">SAP HANA bulut Platform kimliği kimlik doğrulamasını bir kullanıcı oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="00686-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="00686-219">Azure AD kullanıcı deposunda kullanıcılar SSO işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00686-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="00686-220">SAP HANA bulut platformu kimlik doğrulama Kimlik Federasyonu seçeneğini destekler.</span><span class="sxs-lookup"><span data-stu-id="00686-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="00686-221">Bu seçenek, Kurumsal kimlik sağlayıcısı tarafından kimliği doğrulanmış kullanıcılar kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama içinde olup olmadığını denetlemek için uygulamanın sağlar.</span><span class="sxs-lookup"><span data-stu-id="00686-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="00686-222">Varsayılan ayar, Kimlik Federasyonu seçenek devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="00686-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="00686-223">Kimlik Federasyonu etkinleştirilirse, SAP HANA bulut platformu kimlik doğrulama içeri aktarılan kullanıcıların uygulamaya erişmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00686-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="00686-224">SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu etkinleştirme etkinleştirmek veya SAP HANA bulut platformu kimlik doğrulaması ile Kimlik Federasyonu devre dışı bırakma hakkında daha fazla bilgi için bkz: [Kimlik Federasyonu ile kullanıcı deposu, SAP HANA bulut platformu kimlik doğrulama yapılandırın.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="00686-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="00686-225">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="00686-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="00686-226">Bu bölümde, SAP HANA bulut platformu kimlik doğrulama için kendi erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="00686-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="00686-228">**SAP HANA bulut platformu kimlik doğrulama için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="00686-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="00686-229">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="00686-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="00686-231">Uygulamalar listesinde **SAP HANA bulut platformu kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="00686-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="00686-233">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="00686-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="00686-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00686-235">Click **Add** button.</span></span> <span data-ttu-id="00686-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="00686-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="00686-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00686-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00686-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="00686-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="00686-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="00686-241">Test single sign-on</span></span>

<span data-ttu-id="00686-242">Bu bölümde, erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.</span><span class="sxs-lookup"><span data-stu-id="00686-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="00686-243">Erişim paneli SAP HANA bulut platformu kimlik doğrulama parçasında tıklattığınızda, otomatik olarak SAP HANA bulut platformu kimlik doğrulama uygulamanız açan.</span><span class="sxs-lookup"><span data-stu-id="00686-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="00686-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="00686-244">Additional resources</span></span>

* [<span data-ttu-id="00686-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="00686-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00686-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="00686-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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