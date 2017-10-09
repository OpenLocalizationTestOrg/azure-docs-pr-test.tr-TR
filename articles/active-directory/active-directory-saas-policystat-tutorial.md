---
title: "Öğretici: Azure Active Directory Tümleştirme ile PolicyStat | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PolicyStat arasında."
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
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="d8fa3-103">Öğretici: Azure Active Directory Tümleştirme PolicyStat ile</span><span class="sxs-lookup"><span data-stu-id="d8fa3-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="d8fa3-104">Bu öğreticide, bilgi nasıl toointegrate PolicyStat Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8fa3-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8fa3-105">PolicyStat Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8fa3-106">Erişim tooPolicyStat sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d8fa3-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="d8fa3-107">Kullanıcıların tooautomatically get açan tooPolicyStat (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d8fa3-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8fa3-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d8fa3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d8fa3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8fa3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8fa3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d8fa3-110">Prerequisites</span></span>

<span data-ttu-id="d8fa3-111">tooconfigure PolicyStat ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="d8fa3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d8fa3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8fa3-113">Bir PolicyStat çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d8fa3-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8fa3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8fa3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8fa3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8fa3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8fa3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8fa3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d8fa3-118">Scenario description</span></span>
<span data-ttu-id="d8fa3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8fa3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8fa3-121">Merhaba Galerisi'nden PolicyStat ekleme</span><span class="sxs-lookup"><span data-stu-id="d8fa3-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="d8fa3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d8fa3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="d8fa3-123">Merhaba Galerisi'nden PolicyStat ekleme</span><span class="sxs-lookup"><span data-stu-id="d8fa3-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="d8fa3-124">Azure AD'ye tooconfigure hello tümleştirme PolicyStat, tooadd PolicyStat hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d8fa3-125">**tooadd PolicyStat hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8fa3-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8fa3-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8fa3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d8fa3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d8fa3-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d8fa3-133">Merhaba arama kutusuna yazın **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-133">In hello search box, type **PolicyStat**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="d8fa3-135">Merhaba Sonuçlar panelinde seçin **PolicyStat**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8fa3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d8fa3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8fa3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PolicyStat sınayın.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8fa3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen PolicyStat içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="d8fa3-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PolicyStat hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="d8fa3-141">Merhaba hello değeri PolicyStat içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d8fa3-142">tooconfigure ve PolicyStat ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d8fa3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d8fa3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8fa3-145">**[PolicyStat test kullanıcısı oluşturma](#creating-a-policystat-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir PolicyStat içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8fa3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8fa3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8fa3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d8fa3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8fa3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma PolicyStat uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="d8fa3-150">**tooconfigure Azure AD çoklu oturum açma ile PolicyStat, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8fa3-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8fa3-151">Hello hello üzerinde Azure portal'ın **PolicyStat** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d8fa3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="d8fa3-155">Merhaba üzerinde **PolicyStat etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="d8fa3-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-157">a.</span></span> <span data-ttu-id="d8fa3-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="d8fa3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="d8fa3-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-159">b.</span></span> <span data-ttu-id="d8fa3-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="d8fa3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8fa3-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-161">These values are not real.</span></span> <span data-ttu-id="d8fa3-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d8fa3-163">Kişi [PolicyStat istemci destek ekibi](http://www.policystat.com/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="d8fa3-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="d8fa3-166">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooPolicyStat Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="d8fa3-167">Merhaba PolicyStat uygulama bekliyor hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, **SAML belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="d8fa3-168">Aşağıdaki ekran görüntüsü hello bunun bir örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="d8fa3-169">![Öznitelikleri](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="d8fa3-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="d8fa3-170">tooadd hello gerekli öznitelik eşlemelerini hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="d8fa3-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="d8fa3-171">Attribute Name</span></span>    |   <span data-ttu-id="d8fa3-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="d8fa3-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="d8fa3-173">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="d8fa3-173">uid</span></span> | <span data-ttu-id="d8fa3-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="d8fa3-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="d8fa3-175">a.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-175">a.</span></span> <span data-ttu-id="d8fa3-176">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="d8fa3-179">b.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-179">b.</span></span> <span data-ttu-id="d8fa3-180">Merhaba, **öznitelik adı** metin kutusuna, türü **uid**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="d8fa3-181">c.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-181">c.</span></span> <span data-ttu-id="d8fa3-182">Merhaba, **öznitelik değeri** metin kutusuna, select **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="d8fa3-183">d.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-183">d.</span></span> <span data-ttu-id="d8fa3-184">Merhaba gelen **posta** listesinde **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="d8fa3-185">e.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-185">e.</span></span> <span data-ttu-id="d8fa3-186">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="d8fa3-186">Click **Ok**</span></span>

7. <span data-ttu-id="d8fa3-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d8fa3-189">Farklı web tarayıcısı penceresinde PolicyStat şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="d8fa3-190">Merhaba tıklatın **yönetici** sekmesini ve ardından **tek oturum açma yapılandırması** sol gezinti bölmesindeki.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="d8fa3-191">![Yönetici menü](./media/active-directory-saas-policystat-tutorial/ic808633.png "yönetici menüsü")</span><span class="sxs-lookup"><span data-stu-id="d8fa3-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="d8fa3-192">Merhaba, **Kurulum** bölümünde, select **oturum açmayı etkinleştir tek tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="d8fa3-193">![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808634.png "tek oturum açma yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="d8fa3-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="d8fa3-194">Tıklatın **öznitelikleri yapılandırma**ve ardından hello **öznitelikleri yapılandırma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d8fa3-195">![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808635.png "tek oturum açma yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="d8fa3-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="d8fa3-196">a.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-196">a.</span></span> <span data-ttu-id="d8fa3-197">Merhaba, **Username özniteliği** metin kutusuna, türü **uid**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="d8fa3-198">b.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-198">b.</span></span> <span data-ttu-id="d8fa3-199">Merhaba, **ad özniteliği** metin kutusuna, türü **firstname** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="d8fa3-200">c.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-200">c.</span></span> <span data-ttu-id="d8fa3-201">Merhaba, **son Name özniteliği** metin kutusuna, türü **lastname** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="d8fa3-202">d.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-202">d.</span></span> <span data-ttu-id="d8fa3-203">Merhaba, **e-posta özniteliği** metin kutusuna, türü **emailaddress** kullanıcının  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d8fa3-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="d8fa3-204">e.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-204">e.</span></span> <span data-ttu-id="d8fa3-205">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="d8fa3-206">Tıklatın **bilgisayarınızı IDP meta veri**ve ardından hello **bilgisayarınızı IDP meta veri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d8fa3-207">![Çoklu oturum açma yapılandırması](./media/active-directory-saas-policystat-tutorial/ic808636.png "tek oturum açma yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="d8fa3-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="d8fa3-208">a.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-208">a.</span></span> <span data-ttu-id="d8fa3-209">İndirilen meta veri dosyası, içerik kopyalama hello açın ve hello yapıştırma **bilgisayarınızı kimlik sağlayıcısı meta verileri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="d8fa3-210">b.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-210">b.</span></span> <span data-ttu-id="d8fa3-211">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d8fa3-212">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d8fa3-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d8fa3-213">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d8fa3-214">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d8fa3-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8fa3-215">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8fa3-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8fa3-216">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d8fa3-218">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8fa3-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8fa3-219">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8fa3-221">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8fa3-223">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8fa3-225">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8fa3-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8fa3-227">a.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-227">a.</span></span> <span data-ttu-id="d8fa3-228">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8fa3-229">b.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-229">b.</span></span> <span data-ttu-id="d8fa3-230">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8fa3-231">c.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-231">c.</span></span> <span data-ttu-id="d8fa3-232">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d8fa3-233">d.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-233">d.</span></span> <span data-ttu-id="d8fa3-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="d8fa3-235">PolicyStat test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8fa3-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="d8fa3-236">PolicyStat içine sipariş tooenable Azure AD kullanıcıların toolog bunların PolicyStat sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="d8fa3-237">Yalnızca zaman sağlama kullanıcı PolicyStat destekler.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="d8fa3-238">Yani, gereksinim tooadd hello kullanıcıları el ile tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="d8fa3-239">Merhaba kullanıcılar kendi ilk oturum açma SSO aracılığıyla üzerinde otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="d8fa3-240">API'leri, Azure AD kullanıcı hesapları PolicyStat tooprovision tarafından sağlanan veya herhangi diğer PolicyStat kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d8fa3-241">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d8fa3-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d8fa3-242">Bu bölümde, erişim tooPolicyStat vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d8fa3-244">**tooassign Britta Simon tooPolicyStat hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8fa3-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8fa3-245">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d8fa3-247">Merhaba uygulamalar listesinde **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="d8fa3-249">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d8fa3-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-251">Click **Add** button.</span></span> <span data-ttu-id="d8fa3-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d8fa3-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d8fa3-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8fa3-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8fa3-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d8fa3-257">Testing single sign-on</span></span>

<span data-ttu-id="d8fa3-258">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d8fa3-259">Merhaba PolicyStat hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour PolicyStat uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8fa3-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="d8fa3-260">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d8fa3-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8fa3-261">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d8fa3-261">Additional resources</span></span>

* [<span data-ttu-id="d8fa3-262">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d8fa3-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8fa3-263">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d8fa3-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

