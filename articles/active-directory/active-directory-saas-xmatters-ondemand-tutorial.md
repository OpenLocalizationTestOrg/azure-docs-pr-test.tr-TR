---
title: "Öğretici: Azure Active Directory Tümleştirme ile xMatters OnDemand | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile xMatters OnDemand arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="6f933-103">Öğretici: Azure Active Directory Tümleştirme xMatters OnDemand ile</span><span class="sxs-lookup"><span data-stu-id="6f933-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="6f933-104">Bu öğreticide, bilgi nasıl toointegrate xMatters OnDemand Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f933-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f933-105">XMatters OnDemand Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6f933-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f933-106">Erişim tooxMatters OnDemand sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6f933-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="6f933-107">Kullanıcıların tooautomatically get açan tooxMatters OnDemand (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6f933-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f933-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6f933-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6f933-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f933-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f933-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6f933-110">Prerequisites</span></span>

<span data-ttu-id="6f933-111">tooconfigure xMatters OnDemand ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f933-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="6f933-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6f933-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f933-113">Abonelik xMatters OnDemand çoklu oturum açma etkin</span><span class="sxs-lookup"><span data-stu-id="6f933-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f933-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6f933-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f933-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f933-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f933-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6f933-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f933-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f933-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f933-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6f933-118">Scenario description</span></span>
<span data-ttu-id="6f933-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6f933-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f933-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6f933-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f933-121">Merhaba Galerisi'nden xMatters OnDemand ekleme</span><span class="sxs-lookup"><span data-stu-id="6f933-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="6f933-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f933-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="6f933-123">Merhaba Galerisi'nden xMatters OnDemand ekleme</span><span class="sxs-lookup"><span data-stu-id="6f933-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="6f933-124">Azure AD'ye tooconfigure hello tümleştirme xMatters OnDemand, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd xMatters OnDemand gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f933-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f933-125">**tooadd xMatters OnDemand hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f933-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f933-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f933-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f933-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6f933-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f933-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f933-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6f933-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f933-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6f933-133">Merhaba arama kutusuna yazın **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="6f933-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="6f933-135">Merhaba Sonuçlar panelinde seçin **xMatters OnDemand**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6f933-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f933-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f933-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f933-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı OnDemand tabanlı xMatters ile test etme.</span><span class="sxs-lookup"><span data-stu-id="6f933-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f933-139">Tek toowork'ın oturum açma Azure AD tooknow hangi hello gereken xMatters OnDemand karşılık gelen kullanıcı tooa kullanıcı Azure AD içinde değil.</span><span class="sxs-lookup"><span data-stu-id="6f933-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="6f933-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı xMatters hello arasında bir bağlantı ilişkisi OnDemand kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f933-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="6f933-141">Merhaba hello değerini xMatters OnDemand'da, Ata **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6f933-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f933-142">tooconfigure ve xMatters OnDemand ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f933-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f933-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6f933-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f933-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6f933-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f933-145">**[XMatters OnDemand test kullanıcısı oluşturma](#creating-a-xmatters-ondemand-test-user)**  -toohave bir Britta Simon karşılık gelen xMatters kullanıcı bağlantılı toohello Azure AD gösterimidir OnDemand içinde.</span><span class="sxs-lookup"><span data-stu-id="6f933-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f933-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6f933-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f933-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6f933-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f933-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6f933-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f933-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma xMatters OnDemand uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6f933-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="6f933-150">**tooconfigure Azure AD çoklu oturum açma ile xMatters OnDemand, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f933-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f933-151">Hello hello üzerinde Azure portal'ın **xMatters OnDemand** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6f933-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6f933-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6f933-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="6f933-155">Merhaba üzerinde **xMatters OnDemand etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f933-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="6f933-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f933-157">a.</span></span> <span data-ttu-id="6f933-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="6f933-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="6f933-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f933-159">b.</span></span> <span data-ttu-id="6f933-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="6f933-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="6f933-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6f933-161">These values are not real.</span></span> <span data-ttu-id="6f933-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f933-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6f933-163">Kişi [xMatters OnDemand destek ekibi](https://www.xmatters.com/company/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="6f933-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="6f933-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyasını yerel olarak kaydedin **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="6f933-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="6f933-166">Tooforward hello sertifika toohello gerek [xMatters OnDemand destek ekibi](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="6f933-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="6f933-167">Merhaba sertifikanın oturum açma hello tek yapılandırmasını son haline getirmek önce hello xMatters destek ekibi tarafından karşıya toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f933-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="6f933-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f933-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f933-170">Merhaba üzerinde **xMatters OnDemand yapılandırma** 'yi tıklatın **xMatters OnDemand yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6f933-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6f933-171">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6f933-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="6f933-173">Farklı web tarayıcısı penceresinde içinde tooyour XMatters OnDemand şirket site yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="6f933-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="6f933-174">Merhaba üstte Hello araç çubuğunda **yönetici**ve ardından **şirket ayrıntıları** yan sol hello hello gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="6f933-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="6f933-175">![Yönetici](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="6f933-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="6f933-176">Merhaba üzerinde **SAML Yapılandırması** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f933-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6f933-177">![SAML Yapılandırması](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="6f933-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="6f933-178">a.</span><span class="sxs-lookup"><span data-stu-id="6f933-178">a.</span></span> <span data-ttu-id="6f933-179">Seçin **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="6f933-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="6f933-180">b.</span><span class="sxs-lookup"><span data-stu-id="6f933-180">b.</span></span> <span data-ttu-id="6f933-181">Yapıştır **SAML varlık kimliği**, hello hello Azure portal ' Kopyalanan **kimlik sağlayıcı kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f933-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="6f933-182">c.</span><span class="sxs-lookup"><span data-stu-id="6f933-182">c.</span></span> <span data-ttu-id="6f933-183">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello hello Azure portal ' Kopyalanan **üzerinde tek oturum URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f933-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="6f933-184">d.</span><span class="sxs-lookup"><span data-stu-id="6f933-184">d.</span></span> <span data-ttu-id="6f933-185">Yapıştır **Sign-Out URL**, hello hello Azure portal ' Kopyalanan **çoklu oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f933-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="6f933-186">e.</span><span class="sxs-lookup"><span data-stu-id="6f933-186">e.</span></span> <span data-ttu-id="6f933-187">Merhaba üstünde hello şirket Ayrıntıları sayfası tıklayın **Değişiklikleri Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="6f933-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="6f933-188">![Şirket ayrıntıları](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "şirket ayrıntıları")</span><span class="sxs-lookup"><span data-stu-id="6f933-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="6f933-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6f933-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f933-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6f933-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f933-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f933-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f933-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f933-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f933-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6f933-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6f933-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f933-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f933-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f933-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f933-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6f933-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f933-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f933-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f933-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f933-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f933-204">a.</span><span class="sxs-lookup"><span data-stu-id="6f933-204">a.</span></span> <span data-ttu-id="6f933-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f933-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f933-206">b.</span><span class="sxs-lookup"><span data-stu-id="6f933-206">b.</span></span> <span data-ttu-id="6f933-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6f933-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f933-208">c.</span><span class="sxs-lookup"><span data-stu-id="6f933-208">c.</span></span> <span data-ttu-id="6f933-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6f933-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6f933-210">d.</span><span class="sxs-lookup"><span data-stu-id="6f933-210">d.</span></span> <span data-ttu-id="6f933-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f933-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="6f933-212">XMatters OnDemand test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f933-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="6f933-213">TooXMatters OnDemand içinde sipariş tooenable Azure AD kullanıcıların toolog bunların XMatters OnDemand sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6f933-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="6f933-214">XMatters OnDemand Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6f933-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="6f933-215">bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6f933-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="6f933-216">İçinde tooyour oturum **XMatters OnDemand** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="6f933-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="6f933-217">Tıklatın **kullanıcılar** sekmesini ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6f933-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="6f933-218">![Kullanıcıların](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="6f933-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="6f933-219">Merhaba, **kullanıcı ekleme** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f933-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6f933-220">![Kullanıcı ekleme](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="6f933-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="6f933-221">a.</span><span class="sxs-lookup"><span data-stu-id="6f933-221">a.</span></span> <span data-ttu-id="6f933-222">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="6f933-222">Select **Active**.</span></span>

    <span data-ttu-id="6f933-223">b.</span><span class="sxs-lookup"><span data-stu-id="6f933-223">b.</span></span> <span data-ttu-id="6f933-224">Merhaba, **kullanıcı kimliği** metin kutusuna, türü hello kullanıcının kimliği gibi Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6f933-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="6f933-225">c.</span><span class="sxs-lookup"><span data-stu-id="6f933-225">c.</span></span> <span data-ttu-id="6f933-226">Merhaba, **ad** metin kutusuna, adı Britta gibi hello kullanıcı türü.</span><span class="sxs-lookup"><span data-stu-id="6f933-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="6f933-227">d.</span><span class="sxs-lookup"><span data-stu-id="6f933-227">d.</span></span> <span data-ttu-id="6f933-228">Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını Simon gibi.</span><span class="sxs-lookup"><span data-stu-id="6f933-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="6f933-229">e.</span><span class="sxs-lookup"><span data-stu-id="6f933-229">e.</span></span> <span data-ttu-id="6f933-230">Merhaba, **Site** metin kutusu, geçerli bir Azure Enter hello geçerli site tooprovision istediğiniz AD hesabı.</span><span class="sxs-lookup"><span data-stu-id="6f933-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="6f933-231">f.</span><span class="sxs-lookup"><span data-stu-id="6f933-231">f.</span></span> <span data-ttu-id="6f933-232">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f933-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6f933-233">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6f933-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6f933-234">Bu bölümde, erişim tooxMatters OnDemand vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f933-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6f933-236">**tooassign Britta Simon tooxMatters OnDemand, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f933-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f933-237">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f933-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6f933-239">Merhaba uygulamalar listesinde **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="6f933-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="6f933-241">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6f933-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6f933-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f933-243">Click **Add** button.</span></span> <span data-ttu-id="6f933-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f933-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6f933-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6f933-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f933-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f933-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f933-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f933-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f933-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6f933-249">Testing single sign-on</span></span>

<span data-ttu-id="6f933-250">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6f933-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f933-251">Merhaba xMatters hello erişim paneli OnDemand parçasında tıkladığınızda, otomatik olarak oturum açma tooyour xMatters OnDemand uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f933-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="6f933-252">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f933-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f933-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6f933-253">Additional resources</span></span>

* [<span data-ttu-id="6f933-254">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6f933-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f933-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6f933-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

