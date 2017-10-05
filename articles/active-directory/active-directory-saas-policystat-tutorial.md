---
title: "Öğretici: Azure Active Directory Tümleştirme ile PolicyStat | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile PolicyStat arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="85ea0-103">Öğretici: Azure Active Directory Tümleştirme PolicyStat ile</span><span class="sxs-lookup"><span data-stu-id="85ea0-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="85ea0-104">Bu öğreticide, Azure Active Directory (Azure AD) ile PolicyStat tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="85ea0-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85ea0-105">PolicyStat Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="85ea0-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85ea0-106">PolicyStat erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="85ea0-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="85ea0-107">Otomatik olarak için PolicyStat (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="85ea0-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85ea0-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="85ea0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="85ea0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85ea0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85ea0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85ea0-110">Prerequisites</span></span>

<span data-ttu-id="85ea0-111">Azure AD tümleştirme PolicyStat ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="85ea0-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="85ea0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="85ea0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85ea0-113">Bir PolicyStat çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="85ea0-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85ea0-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="85ea0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85ea0-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="85ea0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85ea0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="85ea0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85ea0-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85ea0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85ea0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="85ea0-118">Scenario description</span></span>
<span data-ttu-id="85ea0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="85ea0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85ea0-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="85ea0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85ea0-121">Galeriden PolicyStat ekleme</span><span class="sxs-lookup"><span data-stu-id="85ea0-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="85ea0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="85ea0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="85ea0-123">Galeriden PolicyStat ekleme</span><span class="sxs-lookup"><span data-stu-id="85ea0-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="85ea0-124">Azure AD PolicyStat tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden PolicyStat eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85ea0-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85ea0-125">**Galeriden PolicyStat eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85ea0-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85ea0-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="85ea0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85ea0-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85ea0-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="85ea0-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85ea0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="85ea0-133">Arama kutusuna **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-133">In the search box, type **PolicyStat**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="85ea0-135">Sonuçlar panelinde seçin **PolicyStat**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85ea0-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85ea0-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="85ea0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85ea0-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PolicyStat sınayın.</span><span class="sxs-lookup"><span data-stu-id="85ea0-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85ea0-139">Tekli çalışmaya oturum için Azure AD PolicyStat karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="85ea0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="85ea0-140">Diğer bir deyişle, bir Azure AD kullanıcısının PolicyStat ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85ea0-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="85ea0-141">PolicyStat içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="85ea0-142">Yapılandırma ve Azure AD çoklu oturum açma PolicyStat ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="85ea0-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85ea0-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="85ea0-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85ea0-145">**[PolicyStat test kullanıcısı oluşturma](#creating-a-policystat-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı PolicyStat sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="85ea0-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85ea0-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="85ea0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85ea0-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="85ea0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85ea0-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma PolicyStat uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="85ea0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="85ea0-150">**Azure AD çoklu oturum açma ile PolicyStat yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85ea0-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="85ea0-151">Azure portalında üzerinde **PolicyStat** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="85ea0-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="85ea0-155">Üzerinde **PolicyStat etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85ea0-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="85ea0-157">a.</span><span class="sxs-lookup"><span data-stu-id="85ea0-157">a.</span></span> <span data-ttu-id="85ea0-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="85ea0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="85ea0-159">b.</span><span class="sxs-lookup"><span data-stu-id="85ea0-159">b.</span></span> <span data-ttu-id="85ea0-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="85ea0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85ea0-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="85ea0-161">These values are not real.</span></span> <span data-ttu-id="85ea0-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="85ea0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="85ea0-163">Kişi [PolicyStat istemci destek ekibi](http://www.policystat.com/support/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="85ea0-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="85ea0-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="85ea0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="85ea0-166">Bu bölümün amacı kullanıcıların PolicyStat için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="85ea0-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="85ea0-167">Özel öznitelik eşlemelerini eklemenizi gerektirir belirli bir biçimde SAML onaylar PolicyStat uygulama bekler, **SAML belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="85ea0-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="85ea0-168">Aşağıdaki ekran görüntüsü, bunun bir örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="85ea0-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="85ea0-169">![Öznitelikleri](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="85ea0-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="85ea0-170">Gerekli öznitelik eşlemelerini eklemek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85ea0-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="85ea0-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="85ea0-171">Attribute Name</span></span>    |   <span data-ttu-id="85ea0-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="85ea0-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="85ea0-173">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="85ea0-173">uid</span></span> | <span data-ttu-id="85ea0-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="85ea0-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="85ea0-175">a.</span><span class="sxs-lookup"><span data-stu-id="85ea0-175">a.</span></span> <span data-ttu-id="85ea0-176">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85ea0-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="85ea0-179">b.</span><span class="sxs-lookup"><span data-stu-id="85ea0-179">b.</span></span> <span data-ttu-id="85ea0-180">İçinde **öznitelik adı** metin kutusuna, türü **uid**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="85ea0-181">c.</span><span class="sxs-lookup"><span data-stu-id="85ea0-181">c.</span></span> <span data-ttu-id="85ea0-182">İçinde **öznitelik değeri** metin kutusuna, select **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="85ea0-183">d.</span><span class="sxs-lookup"><span data-stu-id="85ea0-183">d.</span></span> <span data-ttu-id="85ea0-184">Gelen **posta** listesinde **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="85ea0-185">e.</span><span class="sxs-lookup"><span data-stu-id="85ea0-185">e.</span></span> <span data-ttu-id="85ea0-186">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="85ea0-186">Click **Ok**</span></span>

7. <span data-ttu-id="85ea0-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85ea0-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="85ea0-189">Farklı web tarayıcısı penceresinde PolicyStat şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="85ea0-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="85ea0-190">Tıklatın **yönetici** sekmesini ve ardından **tek oturum açma yapılandırması** sol gezinti bölmesindeki.</span><span class="sxs-lookup"><span data-stu-id="85ea0-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="85ea0-191">![Yönetici menü](./media/active-directory-saas-policystat-tutorial/ic808633.png "yönetici menüsü")</span><span class="sxs-lookup"><span data-stu-id="85ea0-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="85ea0-192">İçinde **Kurulum** bölümünde, select **oturum açmayı etkinleştir tek tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="85ea0-193">![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808634.png "tek oturum açma yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="85ea0-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="85ea0-194">Tıklatın **öznitelikleri yapılandırma**ve ardından **öznitelikleri yapılandırma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85ea0-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="85ea0-195">![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808635.png "tek oturum açma yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="85ea0-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="85ea0-196">a.</span><span class="sxs-lookup"><span data-stu-id="85ea0-196">a.</span></span> <span data-ttu-id="85ea0-197">İçinde **Username özniteliği** metin kutusuna, türü **uid**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="85ea0-198">b.</span><span class="sxs-lookup"><span data-stu-id="85ea0-198">b.</span></span> <span data-ttu-id="85ea0-199">İçinde **ad özniteliği** metin kutusuna, türü **firstname** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="85ea0-200">c.</span><span class="sxs-lookup"><span data-stu-id="85ea0-200">c.</span></span> <span data-ttu-id="85ea0-201">İçinde **son Name özniteliği** metin kutusuna, türü **lastname** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="85ea0-202">d.</span><span class="sxs-lookup"><span data-stu-id="85ea0-202">d.</span></span> <span data-ttu-id="85ea0-203">İçinde **e-posta özniteliği** metin kutusuna, türü **emailaddress** kullanıcının  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="85ea0-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="85ea0-204">e.</span><span class="sxs-lookup"><span data-stu-id="85ea0-204">e.</span></span> <span data-ttu-id="85ea0-205">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="85ea0-206">Tıklatın **bilgisayarınızı IDP meta veri**ve ardından **bilgisayarınızı IDP meta veri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85ea0-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="85ea0-207">![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808636.png "tek oturum açma yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="85ea0-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="85ea0-208">a.</span><span class="sxs-lookup"><span data-stu-id="85ea0-208">a.</span></span> <span data-ttu-id="85ea0-209">İndirilen meta veri dosyanızı açın, içeriği Kopyala ve ardından yapıştırın **bilgisayarınızı kimlik sağlayıcısı meta verileri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="85ea0-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="85ea0-210">b.</span><span class="sxs-lookup"><span data-stu-id="85ea0-210">b.</span></span> <span data-ttu-id="85ea0-211">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="85ea0-212">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="85ea0-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="85ea0-213">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="85ea0-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="85ea0-214">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85ea0-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85ea0-215">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="85ea0-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="85ea0-216">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="85ea0-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="85ea0-218">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85ea0-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85ea0-219">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="85ea0-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85ea0-221">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85ea0-223">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="85ea0-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85ea0-225">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85ea0-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85ea0-227">a.</span><span class="sxs-lookup"><span data-stu-id="85ea0-227">a.</span></span> <span data-ttu-id="85ea0-228">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85ea0-229">b.</span><span class="sxs-lookup"><span data-stu-id="85ea0-229">b.</span></span> <span data-ttu-id="85ea0-230">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="85ea0-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85ea0-231">c.</span><span class="sxs-lookup"><span data-stu-id="85ea0-231">c.</span></span> <span data-ttu-id="85ea0-232">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="85ea0-233">d.</span><span class="sxs-lookup"><span data-stu-id="85ea0-233">d.</span></span> <span data-ttu-id="85ea0-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85ea0-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="85ea0-235">PolicyStat test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="85ea0-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="85ea0-236">Azure AD kullanıcıların PolicyStat oturum etkinleştirmek için bunların PolicyStat sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="85ea0-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="85ea0-237">Yalnızca zaman sağlama kullanıcı PolicyStat destekler.</span><span class="sxs-lookup"><span data-stu-id="85ea0-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="85ea0-238">Yani, kullanıcılar için PolicyStat el ile eklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="85ea0-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="85ea0-239">Kullanıcılar kendi ilk oturum açma SSO aracılığıyla üzerinde otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="85ea0-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="85ea0-240">API Azure AD kullanıcı hesaplarını sağlamak için PolicyStat tarafından sağlanan veya herhangi diğer PolicyStat kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85ea0-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="85ea0-241">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="85ea0-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="85ea0-242">Bu bölümde, Britta PolicyStat için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="85ea0-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="85ea0-244">**PolicyStat için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="85ea0-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="85ea0-245">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="85ea0-247">Uygulamalar listesinde **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-247">In the applications list, select **PolicyStat**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="85ea0-249">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="85ea0-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="85ea0-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85ea0-251">Click **Add** button.</span></span> <span data-ttu-id="85ea0-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85ea0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="85ea0-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="85ea0-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="85ea0-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85ea0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85ea0-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="85ea0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85ea0-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="85ea0-257">Testing single sign-on</span></span>

<span data-ttu-id="85ea0-258">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="85ea0-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85ea0-259">Erişim paneli PolicyStat parçasında tıklattığınızda, otomatik olarak PolicyStat uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="85ea0-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="85ea0-260">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85ea0-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85ea0-261">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="85ea0-261">Additional resources</span></span>

* [<span data-ttu-id="85ea0-262">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="85ea0-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85ea0-263">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="85ea0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

