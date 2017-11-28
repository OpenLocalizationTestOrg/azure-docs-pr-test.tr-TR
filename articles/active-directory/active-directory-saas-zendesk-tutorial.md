---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zendesk | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zendesk arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="487c0-103">Öğretici: Zendesk Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="487c0-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="487c0-104">Bu öğreticide, bilgi nasıl toointegrate Zendesk Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="487c0-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="487c0-105">Zendesk Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="487c0-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="487c0-106">Erişim tooZendesk sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="487c0-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="487c0-107">Kullanıcıların tooautomatically get açan tooZendesk (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="487c0-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="487c0-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="487c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="487c0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="487c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="487c0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="487c0-110">Prerequisites</span></span>

<span data-ttu-id="487c0-111">tooconfigure Zendesk ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="487c0-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="487c0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="487c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="487c0-113">Bir Zendesk çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="487c0-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="487c0-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="487c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="487c0-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="487c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="487c0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="487c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="487c0-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="487c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="487c0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="487c0-118">Scenario description</span></span>
<span data-ttu-id="487c0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="487c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="487c0-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="487c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="487c0-121">Zendesk hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="487c0-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="487c0-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="487c0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="487c0-123">Zendesk hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="487c0-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="487c0-124">Azure AD'ye tooconfigure hello tümleştirme Zendesk, tooadd Zendesk hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="487c0-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="487c0-125">**tooadd Zendesk hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="487c0-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="487c0-126">Merhaba,  **[Azure Portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="487c0-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="487c0-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="487c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="487c0-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="487c0-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="487c0-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="487c0-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="487c0-133">Merhaba arama kutusuna yazın **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="487c0-133">In hello search box, type **Zendesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="487c0-135">Merhaba Sonuçlar panelinde seçin **Zendesk**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="487c0-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="487c0-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="487c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="487c0-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zendesk sınayın.</span><span class="sxs-lookup"><span data-stu-id="487c0-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="487c0-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Zendesk içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="487c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="487c0-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zendesk hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="487c0-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="487c0-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Zendesk içinde.</span><span class="sxs-lookup"><span data-stu-id="487c0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="487c0-142">tooconfigure ve Zendesk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="487c0-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="487c0-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="487c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="487c0-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="487c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="487c0-145">**[Zendesk test kullanıcısı oluşturma](#creating-a-zendesk-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zendesk içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="487c0-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="487c0-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="487c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="487c0-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="487c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="487c0-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="487c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="487c0-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zendesk uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="487c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="487c0-150">**tooconfigure Azure AD çoklu oturum açma ile Zendesk, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="487c0-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="487c0-151">Hello hello üzerinde Azure portal'ın **Zendesk** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="487c0-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="487c0-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="487c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="487c0-155">Merhaba üzerinde **Zendesk etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="487c0-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="487c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="487c0-157">a.</span></span> <span data-ttu-id="487c0-158">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="487c0-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="487c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="487c0-159">b.</span></span> <span data-ttu-id="487c0-160">Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="487c0-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="487c0-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="487c0-161">These values are not real.</span></span> <span data-ttu-id="487c0-162">Bu değerleri tanımlayıcı URL'si ve oturum açma hello gerçek URL ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="487c0-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="487c0-163">Kişi [Zendesk destek ekibi](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="487c0-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="487c0-164">Zendesk hello SAML onaylar belirli bir biçimde bekliyor.</span><span class="sxs-lookup"><span data-stu-id="487c0-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="487c0-165">Zorunlu SAML özniteliklere vardır ancak özniteliği isteğe bağlı olarak ekleyebileceğiniz **kullanıcı öznitelikleri** bölümü aşağıdaki adımları aşağıdaki hello tarafından:</span><span class="sxs-lookup"><span data-stu-id="487c0-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="487c0-167">a.</span><span class="sxs-lookup"><span data-stu-id="487c0-167">a.</span></span> <span data-ttu-id="487c0-168">Merhaba tıklatın **görüntüleme ve düzenleme tüm diğer özniteliklerle hello** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="487c0-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="487c0-170">b.</span><span class="sxs-lookup"><span data-stu-id="487c0-170">b.</span></span> <span data-ttu-id="487c0-171">Merhaba tıklatın **özniteliği eklemek** tooopen **Ekle özniteliği** iletişim.</span><span class="sxs-lookup"><span data-stu-id="487c0-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="487c0-173">c.</span><span class="sxs-lookup"><span data-stu-id="487c0-173">c.</span></span> <span data-ttu-id="487c0-174">Merhaba, **adı** metin kutusuna, türü hello öznitelik adı (örneğin **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="487c0-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="487c0-175">d.</span><span class="sxs-lookup"><span data-stu-id="487c0-175">d.</span></span> <span data-ttu-id="487c0-176">Merhaba gelen **değeri** listesinde, select hello öznitelik değeri (olarak **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="487c0-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="487c0-177">e.</span><span class="sxs-lookup"><span data-stu-id="487c0-177">e.</span></span> <span data-ttu-id="487c0-178">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="487c0-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="487c0-179">Varsayılan olarak Azure AD'de olmayan uzantı öznitelikleri tooadd öznitelikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="487c0-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="487c0-180">Tıklatın [SAML ayarlanabilir kullanıcı öznitelikleri](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello tam listesi SAML öznitelikleri **Zendesk** kabul eder.</span><span class="sxs-lookup"><span data-stu-id="487c0-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="487c0-181">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="487c0-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="487c0-183">Merhaba üzerinde **Zendesk yapılandırma** 'yi tıklatın **yapılandırma Zendesk** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="487c0-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="487c0-184">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="487c0-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="487c0-186">Farklı web tarayıcısı penceresinde Zendesk şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="487c0-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="487c0-187">Tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="487c0-187">Click **Admin**.</span></span>

9. <span data-ttu-id="487c0-188">Merhaba sol gezinti bölmesinde **ayarları**ve ardından **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="487c0-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="487c0-189">Merhaba üzerinde **güvenlik** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="487c0-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="487c0-190">![Güvenlik](./media/active-directory-saas-zendesk-tutorial/ic773089.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="487c0-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="487c0-191">![Çoklu oturum açma](./media/active-directory-saas-zendesk-tutorial/ic773090.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="487c0-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="487c0-192">a.</span><span class="sxs-lookup"><span data-stu-id="487c0-192">a.</span></span> <span data-ttu-id="487c0-193">Merhaba tıklatın **yönetici & aracıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="487c0-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="487c0-194">b.</span><span class="sxs-lookup"><span data-stu-id="487c0-194">b.</span></span> <span data-ttu-id="487c0-195">Seçin **çoklu oturum açma (SSO) ve SAML**ve ardından **SAML**.</span><span class="sxs-lookup"><span data-stu-id="487c0-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="487c0-196">c.</span><span class="sxs-lookup"><span data-stu-id="487c0-196">c.</span></span> <span data-ttu-id="487c0-197">İçinde **SAML SSO URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="487c0-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="487c0-198">d.</span><span class="sxs-lookup"><span data-stu-id="487c0-198">d.</span></span> <span data-ttu-id="487c0-199">İçinde **uzak oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="487c0-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="487c0-200">e.</span><span class="sxs-lookup"><span data-stu-id="487c0-200">e.</span></span> <span data-ttu-id="487c0-201">İçinde **sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="487c0-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="487c0-202">f.</span><span class="sxs-lookup"><span data-stu-id="487c0-202">f.</span></span> <span data-ttu-id="487c0-203">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="487c0-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="487c0-204">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="487c0-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="487c0-205">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="487c0-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="487c0-207">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="487c0-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="487c0-208">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="487c0-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="487c0-210">Kullanıcıların toodisplay hello listesini Git çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="487c0-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="487c0-212">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="487c0-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="487c0-214">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="487c0-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="487c0-216">a.</span><span class="sxs-lookup"><span data-stu-id="487c0-216">a.</span></span> <span data-ttu-id="487c0-217">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="487c0-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="487c0-218">b.</span><span class="sxs-lookup"><span data-stu-id="487c0-218">b.</span></span> <span data-ttu-id="487c0-219">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="487c0-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="487c0-220">c.</span><span class="sxs-lookup"><span data-stu-id="487c0-220">c.</span></span> <span data-ttu-id="487c0-221">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="487c0-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="487c0-222">d.</span><span class="sxs-lookup"><span data-stu-id="487c0-222">d.</span></span> <span data-ttu-id="487c0-223">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="487c0-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="487c0-224">Zendesk test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="487c0-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="487c0-225">içine tooenable Azure AD kullanıcıların toolog **Zendesk**, içine sağlanmalıdır **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="487c0-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="487c0-226">Merhaba uygulamalarında atanan hello rolüne bağlı olarak, hello beklenen davranıştır:</span><span class="sxs-lookup"><span data-stu-id="487c0-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="487c0-227">**Son kullanıcı** hesapları otomatik olarak oturum açarken sağlandı.</span><span class="sxs-lookup"><span data-stu-id="487c0-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="487c0-228">**Aracı** ve **yönetici** hesapları gereken el ile derlemenizde toobe **Zendesk** oturum açmadan önce.</span><span class="sxs-lookup"><span data-stu-id="487c0-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="487c0-229">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="487c0-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="487c0-230">İçinde tooyour oturum **Zendesk** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="487c0-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="487c0-231">Select hello **müşteri listesi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="487c0-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="487c0-232">Select hello **kullanıcı** sekmesine ve tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="487c0-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="487c0-233">![Kullanıcı Ekle](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="487c0-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="487c0-234">Tooprovision istediğiniz ve ardından var olan bir Azure AD hesabını hello e-posta adresini yazın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="487c0-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="487c0-235">![Yeni kullanıcı](./media/active-directory-saas-zendesk-tutorial/ic773633.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="487c0-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="487c0-236">API AAD kullanıcı hesaplarının Zendesk tooprovision tarafından sağlanan veya herhangi diğer Zendesk kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="487c0-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="487c0-237">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="487c0-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="487c0-238">Bu bölümde, erişim tooZendesk vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="487c0-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="487c0-240">**tooassign Britta Simon tooZendesk hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="487c0-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="487c0-241">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="487c0-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="487c0-243">Merhaba uygulamalar listesinde **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="487c0-243">In hello applications list, select **Zendesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="487c0-245">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="487c0-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="487c0-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="487c0-247">Click **Add** button.</span></span> <span data-ttu-id="487c0-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="487c0-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="487c0-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="487c0-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="487c0-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="487c0-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="487c0-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="487c0-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="487c0-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="487c0-253">Testing single sign-on</span></span>

<span data-ttu-id="487c0-254">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="487c0-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="487c0-255">Merhaba Zendesk hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zendesk uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="487c0-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="487c0-256">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="487c0-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="487c0-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="487c0-257">Additional resources</span></span>

* [<span data-ttu-id="487c0-258">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="487c0-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="487c0-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="487c0-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
