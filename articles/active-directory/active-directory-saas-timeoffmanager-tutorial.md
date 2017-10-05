---
title: "Öğretici: Azure Active Directory Tümleştirme ile TimeOffManager | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile TimeOffManager arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="0ea14-103">Öğretici: Azure Active Directory Tümleştirme TimeOffManager ile</span><span class="sxs-lookup"><span data-stu-id="0ea14-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="0ea14-104">Bu öğreticide, Azure Active Directory (Azure AD) ile TimeOffManager tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ea14-105">TimeOffManager Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0ea14-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0ea14-106">TimeOffManager erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ea14-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="0ea14-107">Otomatik olarak için TimeOffManager (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ea14-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ea14-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0ea14-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0ea14-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ea14-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ea14-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ea14-110">Prerequisites</span></span>

<span data-ttu-id="0ea14-111">Azure AD tümleştirme TimeOffManager ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea14-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="0ea14-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0ea14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ea14-113">Bir TimeOffManager çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0ea14-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ea14-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ea14-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ea14-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea14-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ea14-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ea14-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ea14-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ea14-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0ea14-118">Scenario description</span></span>
<span data-ttu-id="0ea14-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ea14-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0ea14-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ea14-121">Galeriden TimeOffManager Ekle</span><span class="sxs-lookup"><span data-stu-id="0ea14-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="0ea14-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0ea14-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="0ea14-123">Galeriden TimeOffManager Ekle</span><span class="sxs-lookup"><span data-stu-id="0ea14-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="0ea14-124">Azure AD TimeOffManager tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden TimeOffManager eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea14-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0ea14-125">**Galeriden TimeOffManager eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea14-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0ea14-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0ea14-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0ea14-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0ea14-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0ea14-133">Arama kutusuna **TimeOffManager**seçin **TimeOffManager** sonuç paneli ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![Galerisi'nden ekleme](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0ea14-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0ea14-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0ea14-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı TimeOffManager sınayın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ea14-137">Tekli çalışmaya oturum için Azure AD TimeOffManager karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="0ea14-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="0ea14-138">Diğer bir deyişle, bir Azure AD kullanıcısının TimeOffManager ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea14-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="0ea14-139">TimeOffManager içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0ea14-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0ea14-140">Yapılandırma ve Azure AD çoklu oturum açma TimeOffManager ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea14-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0ea14-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0ea14-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0ea14-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="0ea14-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ea14-143">**[TimeOffManager test kullanıcısı oluşturma](#create-a-timeoffmanager-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı TimeOffManager sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="0ea14-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ea14-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0ea14-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ea14-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0ea14-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0ea14-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0ea14-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma TimeOffManager uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="0ea14-148">**Azure AD çoklu oturum açma ile TimeOffManager yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea14-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="0ea14-149">Azure portalında üzerinde **TimeOffManager** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0ea14-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="0ea14-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML oturum açma tabanlı](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="0ea14-153">Üzerinde **TimeOffManager etki alanı ve URL'leri** bölümünde, aşağıdaki işlemi gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ea14-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![TimeOffManager etki alanı ve URL'ler bölümü](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="0ea14-155">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="0ea14-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ea14-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="0ea14-156">This value is not real.</span></span> <span data-ttu-id="0ea14-157">Bu değer ile gerçek yanıt URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="0ea14-158">Bu değerden alabilirsiniz **çoklu oturum açma ayarları sayfasında** daha sonra öğreticide veya kişi içinde açıklanan [TimeOffManager destek ekibi](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ea14-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="0ea14-159">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="0ea14-161">Bu bölümün amacı kullanıcıların TimeOffManger için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="0ea14-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="0ea14-162">SAML belirteci öznitelikleri yapılandırmanıza özel öznitelik eşlemelerini ekleyin gerektiren belirli bir biçimde SAML onaylar TimeOffManger uygulamanızı bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0ea14-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="0ea14-163">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ea14-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="0ea14-164">![SAML belirteci öznitelikleri](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml belirteci öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="0ea14-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="0ea14-165">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="0ea14-165">Attribute Name</span></span> | <span data-ttu-id="0ea14-166">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="0ea14-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0ea14-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="0ea14-167">Firstname</span></span> |<span data-ttu-id="0ea14-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0ea14-168">User.givenname</span></span> |
    | <span data-ttu-id="0ea14-169">Soyadı</span><span class="sxs-lookup"><span data-stu-id="0ea14-169">Lastname</span></span> |<span data-ttu-id="0ea14-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="0ea14-170">User.surname</span></span> |
    | <span data-ttu-id="0ea14-171">E-posta</span><span class="sxs-lookup"><span data-stu-id="0ea14-171">Email</span></span> |<span data-ttu-id="0ea14-172">User.Mail</span><span class="sxs-lookup"><span data-stu-id="0ea14-172">User.mail</span></span> |
    
    <span data-ttu-id="0ea14-173">a.</span><span class="sxs-lookup"><span data-stu-id="0ea14-173">a.</span></span>  <span data-ttu-id="0ea14-174">Her veri satırının için yukarıdaki tabloda **kullanıcı özniteliği eklemek**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="0ea14-175">![SAML belirteci öznitelikleri](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml belirteci öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="0ea14-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="0ea14-176">![SAML belirteci öznitelikleri](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml belirteci öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="0ea14-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="0ea14-177">b.</span><span class="sxs-lookup"><span data-stu-id="0ea14-177">b.</span></span>  <span data-ttu-id="0ea14-178">İçinde **öznitelik adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0ea14-179">c.</span><span class="sxs-lookup"><span data-stu-id="0ea14-179">c.</span></span>  <span data-ttu-id="0ea14-180">İçinde **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen öznitelik değerini seçin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="0ea14-181">d.</span><span class="sxs-lookup"><span data-stu-id="0ea14-181">d.</span></span>  <span data-ttu-id="0ea14-182">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="0ea14-183">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-183">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0ea14-185">Üzerinde **TimeOffManager yapılandırma** 'yi tıklatın **yapılandırma TimeOffManager** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0ea14-186">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0ea14-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TimeOffManager yapılandırma bölümü](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="0ea14-188">Farklı web tarayıcısı penceresinde TimeOffManager şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="0ea14-189">Git **hesap \> Hesap seçenekleri \> tek oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="0ea14-190">![Çoklu oturum açma ayarları](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="0ea14-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="0ea14-191">İçinde **çoklu oturum açma ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ea14-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="0ea14-192">![Çoklu oturum açma ayarları](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="0ea14-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="0ea14-193">a.</span><span class="sxs-lookup"><span data-stu-id="0ea14-193">a.</span></span> <span data-ttu-id="0ea14-194">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve sonra tüm sertifika içine yapıştırabilirsiniz **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0ea14-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="0ea14-195">b.</span><span class="sxs-lookup"><span data-stu-id="0ea14-195">b.</span></span> <span data-ttu-id="0ea14-196">İçinde **IDP veren** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0ea14-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="0ea14-197">c.</span><span class="sxs-lookup"><span data-stu-id="0ea14-197">c.</span></span> <span data-ttu-id="0ea14-198">İçinde **IDP uç nokta URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0ea14-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="0ea14-199">d.</span><span class="sxs-lookup"><span data-stu-id="0ea14-199">d.</span></span> <span data-ttu-id="0ea14-200">Olarak **zorunlu SAML**seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="0ea14-201">e.</span><span class="sxs-lookup"><span data-stu-id="0ea14-201">e.</span></span> <span data-ttu-id="0ea14-202">Olarak **otomatik olarak oluşturma kullanıcıların**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="0ea14-203">f.</span><span class="sxs-lookup"><span data-stu-id="0ea14-203">f.</span></span> <span data-ttu-id="0ea14-204">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0ea14-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="0ea14-205">g.</span><span class="sxs-lookup"><span data-stu-id="0ea14-205">g.</span></span> <span data-ttu-id="0ea14-206">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="0ea14-207">İçinde **çoklu oturum açma ayarları** sayfasında, değerini kopyalayın **onaylama tüketici hizmeti URL'si** ve yapıştırın **yanıt URL'si** metin kutusu altında **TimeOffManager Etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="0ea14-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="0ea14-208">![Çoklu oturum açma ayarları](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="0ea14-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="0ea14-209">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0ea14-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0ea14-210">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="0ea14-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0ea14-211">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ea14-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ea14-212">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea14-212">Create an Azure AD test user</span></span>
<span data-ttu-id="0ea14-213">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="0ea14-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0ea14-215">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea14-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0ea14-216">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ea14-218">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların ve grupların tüm kullanıcılar-->](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ea14-220">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="0ea14-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ea14-222">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ea14-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ea14-224">a.</span><span class="sxs-lookup"><span data-stu-id="0ea14-224">a.</span></span> <span data-ttu-id="0ea14-225">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ea14-226">b.</span><span class="sxs-lookup"><span data-stu-id="0ea14-226">b.</span></span> <span data-ttu-id="0ea14-227">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0ea14-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ea14-228">c.</span><span class="sxs-lookup"><span data-stu-id="0ea14-228">c.</span></span> <span data-ttu-id="0ea14-229">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0ea14-230">d.</span><span class="sxs-lookup"><span data-stu-id="0ea14-230">d.</span></span> <span data-ttu-id="0ea14-231">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ea14-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="0ea14-232">TimeOffManager test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea14-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="0ea14-233">Azure AD kullanıcıların TimeOffManager oturum etkinleştirmek için bunlar için TimeOffManager sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0ea14-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="0ea14-234">Yalnızca zaman sağlama kullanıcı TimeOffManager destekler.</span><span class="sxs-lookup"><span data-stu-id="0ea14-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="0ea14-235">Sizin için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="0ea14-235">There is no action item for you.</span></span>  

<span data-ttu-id="0ea14-236">Kullanıcılar, çoklu oturum açma kullanarak ilk oturum açma sırasında otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="0ea14-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="0ea14-237">API Azure AD kullanıcı hesaplarını sağlamak için TimeOffManager tarafından sağlanan veya herhangi diğer TimeOffManager kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea14-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0ea14-238">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="0ea14-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="0ea14-239">Bu bölümde, Britta TimeOffManager için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0ea14-241">**TimeOffManager için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea14-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="0ea14-242">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0ea14-244">Uygulamalar listesinde **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-244">In the applications list, select **TimeOffManager**.</span></span>

    ![Uygulama listesinde TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="0ea14-246">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0ea14-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0ea14-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea14-248">Click **Add** button.</span></span> <span data-ttu-id="0ea14-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea14-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0ea14-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0ea14-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0ea14-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea14-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ea14-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea14-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0ea14-254">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="0ea14-254">Test single sign-on</span></span>

<span data-ttu-id="0ea14-255">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0ea14-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0ea14-256">Erişim paneli TimeOffManager parçasında tıklattığınızda, otomatik olarak TimeOffManager uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="0ea14-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="0ea14-257">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ea14-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ea14-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0ea14-258">Additional resources</span></span>

* [<span data-ttu-id="0ea14-259">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="0ea14-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ea14-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0ea14-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

