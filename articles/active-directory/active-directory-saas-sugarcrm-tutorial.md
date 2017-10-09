---
title: "Öğretici: Azure Active Directory Tümleştirme Sugar CRM ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Sugar CRM arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="b1a9c-103">Öğretici: Sugar CRM Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="b1a9c-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="b1a9c-104">Bu öğreticide, bilgi nasıl toointegrate Sugar CRM Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1a9c-104">In this tutorial, you learn how toointegrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1a9c-105">Sugar CRM Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-105">Integrating Sugar CRM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1a9c-106">Erişim tooSugar CRM sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b1a9c-106">You can control in Azure AD who has access tooSugar CRM</span></span>
- <span data-ttu-id="b1a9c-107">Kullanıcıların tooautomatically get açan tooSugar CRM (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b1a9c-107">You can enable your users tooautomatically get signed-on tooSugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1a9c-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b1a9c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b1a9c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1a9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1a9c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b1a9c-110">Prerequisites</span></span>

<span data-ttu-id="b1a9c-111">Sugar CRM ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-111">tooconfigure Azure AD integration with Sugar CRM, you need hello following items:</span></span>

- <span data-ttu-id="b1a9c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b1a9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1a9c-113">Bir Sugar CRM çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="b1a9c-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1a9c-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1a9c-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1a9c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1a9c-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1a9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1a9c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b1a9c-118">Scenario description</span></span>
<span data-ttu-id="b1a9c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1a9c-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1a9c-121">Sugar CRM hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="b1a9c-121">Adding Sugar CRM from hello gallery</span></span>
2. <span data-ttu-id="b1a9c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b1a9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-hello-gallery"></a><span data-ttu-id="b1a9c-123">Sugar CRM hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="b1a9c-123">Adding Sugar CRM from hello gallery</span></span>
<span data-ttu-id="b1a9c-124">Azure AD'ye tooconfigure hello tümleştirme Sugar CRM tooadd Sugar CRM hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-124">tooconfigure hello integration of Sugar CRM into Azure AD, you need tooadd Sugar CRM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1a9c-125">**tooadd Sugar CRM hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a9c-125">**tooadd Sugar CRM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a9c-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1a9c-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1a9c-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b1a9c-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b1a9c-133">Merhaba arama kutusuna yazın **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-133">In hello search box, type **Sugar CRM**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="b1a9c-135">Merhaba Sonuçlar panelinde seçin **Sugar CRM**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-135">In hello results panel, select **Sugar CRM**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1a9c-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b1a9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1a9c-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Sugar "Britta Simon" adlı bir test kullanıcı tabanlı CRM ile test etme.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1a9c-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Sugar CRM'deki tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sugar CRM is tooa user in Azure AD.</span></span> <span data-ttu-id="b1a9c-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Sugar CRM hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-140">In other words, a link relationship between an Azure AD user and hello related user in Sugar CRM needs toobe established.</span></span>

<span data-ttu-id="b1a9c-141">Sugar CRM hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-141">In Sugar CRM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b1a9c-142">tooconfigure ve Sugar CRM ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-142">tooconfigure and test Azure AD single sign-on with Sugar CRM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1a9c-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1a9c-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1a9c-145">**[Sugar CRM test kullanıcısı oluşturma](#creating-a-sugar-crm-test-user)**  -toohave karşılık gelen, Britta Simon Sugar CRM'deki bağlantılı toohello Azure AD kullanıcı gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - toohave a counterpart of Britta Simon in Sugar CRM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1a9c-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1a9c-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1a9c-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b1a9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1a9c-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Sugar CRM uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="b1a9c-150">**tooconfigure Azure AD çoklu oturum açma Sugar CRM ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a9c-150">**tooconfigure Azure AD single sign-on with Sugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a9c-151">Hello hello üzerinde Azure portal'ın **Sugar CRM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-151">In hello Azure portal, on hello **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b1a9c-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="b1a9c-155">Merhaba üzerinde **Sugar CRM etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-155">On hello **Sugar CRM Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="b1a9c-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="b1a9c-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-158">hello value is not real.</span></span> <span data-ttu-id="b1a9c-159">Güncelleştirme hello değerle hello gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b1a9c-160">Kişi [Sugar CRM istemci destek ekibi](https://support.sugarcrm.com/) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="b1a9c-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="b1a9c-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1a9c-165">Merhaba üzerinde **Sugar CRM Yapılandırma** 'yi tıklatın **yapılandırma Sugar CRM** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-165">On hello **Sugar CRM Configuration** section, click **Configure Sugar CRM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b1a9c-166">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b1a9c-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="b1a9c-168">Farklı web tarayıcısı penceresinde tooyour Sugar CRM şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-168">In a different web browser window, log in tooyour Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="b1a9c-169">Çok Git**yönetici**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-169">Go too**Admin**.</span></span>
   
    <span data-ttu-id="b1a9c-170">![Yönetici](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="b1a9c-171">Merhaba, **Yönetim** 'yi tıklatın **parola yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-171">In hello **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="b1a9c-172">![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="b1a9c-173">Seçin **SAML kimlik doğrulamasını etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="b1a9c-174">![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="b1a9c-175">Merhaba, **SAML kimlik doğrulaması** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-175">In hello **SAML Authentication** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b1a9c-176">![SAML kimlik doğrulaması](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="b1a9c-177">a.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-177">a.</span></span> <span data-ttu-id="b1a9c-178">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-178">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b1a9c-179">b.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-179">b.</span></span> <span data-ttu-id="b1a9c-180">Merhaba, **SLO URL** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-180">In hello **SLO URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b1a9c-181">c.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-181">c.</span></span> <span data-ttu-id="b1a9c-182">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve ardından yapıştırın içine tüm sertifika hello **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-182">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="b1a9c-183">d.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-183">d.</span></span> <span data-ttu-id="b1a9c-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b1a9c-185">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b1a9c-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b1a9c-186">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b1a9c-187">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1a9c-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1a9c-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1a9c-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1a9c-189">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b1a9c-191">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a9c-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a9c-192">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1a9c-194">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1a9c-196">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1a9c-198">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1a9c-200">a.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-200">a.</span></span> <span data-ttu-id="b1a9c-201">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1a9c-202">b.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-202">b.</span></span> <span data-ttu-id="b1a9c-203">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1a9c-204">c.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-204">c.</span></span> <span data-ttu-id="b1a9c-205">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1a9c-206">d.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-206">d.</span></span> <span data-ttu-id="b1a9c-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="b1a9c-208">Sugar CRM test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1a9c-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="b1a9c-209">Sağlanan tooSugar CRM tooSugar CRM, sipariş tooenable Azure AD kullanıcıların toolog içinde olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-209">In order tooenable Azure AD users toolog in tooSugar CRM, they must be provisioned tooSugar CRM.</span></span>

<span data-ttu-id="b1a9c-210">Sugar CRM Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-210">In hello case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="b1a9c-211">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a9c-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a9c-212">İçinde tooyour oturum **Sugar CRM** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-212">Log in tooyour **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="b1a9c-213">Çok Git**yönetici**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-213">Go too**Admin**.</span></span>
   
    <span data-ttu-id="b1a9c-214">![Yönetici](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="b1a9c-215">Merhaba, **Yönetim** 'yi tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-215">In hello **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="b1a9c-216">![Yönetim](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="b1a9c-217">Çok Git**kullanıcılar \> yeni kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-217">Go too**Users \> Create New User**.</span></span>
   
    <span data-ttu-id="b1a9c-218">![Yeni kullanıcı oluşturmak](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "yeni kullanıcı oluşturun")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="b1a9c-219">Merhaba üzerinde **kullanıcı profili** sekmesinde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-219">On hello **User Profile** tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="b1a9c-220">![Yeni kullanıcı](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="b1a9c-221">a.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-221">a.</span></span> <span data-ttu-id="b1a9c-222">Türü hello **kullanıcı adı**, **Soyadı**, ve **e-posta adresi** hello halinde geçerli bir Azure Active Directory kullanıcı, metin kutuları ilgili.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-222">Type hello **user name**, **last name**, and **email address** of a valid Azure Active Directory user into hello related textboxes.</span></span>
  
6. <span data-ttu-id="b1a9c-223">Olarak **durum**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="b1a9c-224">Merhaba parola sekmesinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b1a9c-224">On hello Password tab, perform hello following steps:</span></span>
   
    <span data-ttu-id="b1a9c-225">![Yeni kullanıcı](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="b1a9c-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="b1a9c-226">a.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-226">a.</span></span> <span data-ttu-id="b1a9c-227">Merhaba türü hello parolanıza textbox ilgili.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-227">Type hello password into hello related textbox.</span></span>

    <span data-ttu-id="b1a9c-228">b.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-228">b.</span></span> <span data-ttu-id="b1a9c-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b1a9c-230">API AAD kullanıcı hesaplarının Sugar CRM tooprovision tarafından sağlanan veya herhangi diğer Sugar CRM kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1a9c-231">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b1a9c-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1a9c-232">Bu bölümde, erişim tooSugar CRM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSugar CRM.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b1a9c-234">**tooassign Britta Simon tooSugar, CRM hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b1a9c-234">**tooassign Britta Simon tooSugar CRM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1a9c-235">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b1a9c-237">Merhaba uygulamalar listesinde **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-237">In hello applications list, select **Sugar CRM**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="b1a9c-239">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b1a9c-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-241">Click **Add** button.</span></span> <span data-ttu-id="b1a9c-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b1a9c-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1a9c-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1a9c-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1a9c-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b1a9c-247">Testing single sign-on</span></span>

<span data-ttu-id="b1a9c-248">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-248">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b1a9c-249">Merhaba Sugar CRM hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Sugar CRM uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1a9c-249">When you click hello Sugar CRM tile in hello Access Panel, you should get automatically signed-on tooyour Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1a9c-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b1a9c-250">Additional resources</span></span>

* [<span data-ttu-id="b1a9c-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b1a9c-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1a9c-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b1a9c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

