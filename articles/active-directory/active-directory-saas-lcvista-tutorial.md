---
title: "Öğretici: Azure Active Directory Tümleştirme ile LCVista | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LCVista arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="c9a41-103">Öğretici: Azure Active Directory Tümleştirme LCVista ile</span><span class="sxs-lookup"><span data-stu-id="c9a41-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="c9a41-104">Bu öğreticide, bilgi nasıl toointegrate LCVista Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9a41-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9a41-105">LCVista Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c9a41-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9a41-106">Erişim tooLCVista sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9a41-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="c9a41-107">Kullanıcıların tooautomatically get açan tooLCVista (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c9a41-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9a41-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c9a41-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9a41-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9a41-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9a41-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c9a41-110">Prerequisites</span></span>

<span data-ttu-id="c9a41-111">tooconfigure LCVista ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c9a41-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="c9a41-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c9a41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9a41-113">Bir LCVista çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="c9a41-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9a41-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c9a41-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9a41-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c9a41-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9a41-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c9a41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9a41-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9a41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9a41-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c9a41-118">Scenario description</span></span>
<span data-ttu-id="c9a41-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c9a41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9a41-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c9a41-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9a41-121">Merhaba Galerisi'nden LCVista ekleme</span><span class="sxs-lookup"><span data-stu-id="c9a41-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="c9a41-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c9a41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="c9a41-123">Merhaba Galerisi'nden LCVista ekleme</span><span class="sxs-lookup"><span data-stu-id="c9a41-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="c9a41-124">Azure AD'ye tooconfigure hello tümleştirme LCVista, tooadd LCVista hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9a41-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9a41-125">**tooadd LCVista hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9a41-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a41-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9a41-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9a41-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c9a41-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c9a41-133">Merhaba arama kutusuna yazın **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-133">In hello search box, type **LCVista**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="c9a41-135">Merhaba Sonuçlar panelinde seçin **LCVista**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c9a41-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9a41-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c9a41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9a41-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı LCVista ile test etme</span><span class="sxs-lookup"><span data-stu-id="c9a41-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c9a41-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LCVista içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9a41-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="c9a41-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LCVista hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9a41-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="c9a41-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LCVista içinde.</span><span class="sxs-lookup"><span data-stu-id="c9a41-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="c9a41-142">tooconfigure ve LCVista ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c9a41-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9a41-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c9a41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9a41-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c9a41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9a41-145">**[LCVista test kullanıcısı oluşturma](#creating-a-lcvista-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LCVista içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c9a41-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9a41-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c9a41-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9a41-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c9a41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9a41-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c9a41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9a41-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LCVista uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c9a41-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="c9a41-150">**tooconfigure Azure AD çoklu oturum açma ile LCVista, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9a41-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a41-151">Hello hello üzerinde Azure portal'ın **LCVista** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c9a41-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c9a41-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="c9a41-155">Merhaba üzerinde **LCVista etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c9a41-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="c9a41-157">a.</span><span class="sxs-lookup"><span data-stu-id="c9a41-157">a.</span></span> <span data-ttu-id="c9a41-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="c9a41-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="c9a41-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9a41-159">b.</span></span> <span data-ttu-id="c9a41-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="c9a41-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="c9a41-161">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c9a41-161">These values are not hello real.</span></span> <span data-ttu-id="c9a41-162">Bu güncelleştirme tanımlayıcısı ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="c9a41-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="c9a41-163">Kişi [LCVista istemci destek ekibi](https://lcvista.com/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="c9a41-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="c9a41-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c9a41-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="c9a41-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="c9a41-168">Merhaba üzerinde **LCVista yapılandırma** 'yi tıklatın **yapılandırma LCVista** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c9a41-169">Kopya hello **SAML varlık kimliği** ve **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c9a41-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="c9a41-171">Üzerinde tooyour LCVista uygulama yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c9a41-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="c9a41-172">Merhaba, **SAML Config** bölümünde, hello denetleyin **etkinleştirmek SAML oturum açma** ve görüntü belirtildiği hello ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="c9a41-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="c9a41-174">a.</span><span class="sxs-lookup"><span data-stu-id="c9a41-174">a.</span></span> <span data-ttu-id="c9a41-175">Yapıştır hello **veren URL'si** hello Azure AD'den kopyalanan **varlık kimliği** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c9a41-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="c9a41-176">b.</span><span class="sxs-lookup"><span data-stu-id="c9a41-176">b.</span></span> <span data-ttu-id="c9a41-177">Yapıştır hello **çoklu oturum açma hizmet URL'si** hello Azure AD'den kopyalanan **URL** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c9a41-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="c9a41-178">c.</span><span class="sxs-lookup"><span data-stu-id="c9a41-178">c.</span></span> <span data-ttu-id="c9a41-179">Meta veriler (Azure Portalı'ndan indirilen XML'den), hello değerini kopyalayın **X509Certificate** hello yapıştırın **x509 sertifika** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c9a41-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="c9a41-180">d.</span><span class="sxs-lookup"><span data-stu-id="c9a41-180">d.</span></span> <span data-ttu-id="c9a41-181">Merhaba, **ad özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="c9a41-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="c9a41-182">e.</span><span class="sxs-lookup"><span data-stu-id="c9a41-182">e.</span></span> <span data-ttu-id="c9a41-183">Merhaba, **son name özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="c9a41-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="c9a41-184">f.</span><span class="sxs-lookup"><span data-stu-id="c9a41-184">f.</span></span> <span data-ttu-id="c9a41-185">Merhaba, **e-posta özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="c9a41-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="c9a41-186">g.</span><span class="sxs-lookup"><span data-stu-id="c9a41-186">g.</span></span> <span data-ttu-id="c9a41-187">Merhaba, **Username özniteliği** metin kutusuna, Yapıştır hello değeri `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="c9a41-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="c9a41-188">e.</span><span class="sxs-lookup"><span data-stu-id="c9a41-188">e.</span></span> <span data-ttu-id="c9a41-189">Tıklatın **kaydetmek** toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="c9a41-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="c9a41-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c9a41-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9a41-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c9a41-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9a41-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9a41-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9a41-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9a41-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9a41-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c9a41-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c9a41-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9a41-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a41-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9a41-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9a41-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9a41-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9a41-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c9a41-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9a41-205">a.</span><span class="sxs-lookup"><span data-stu-id="c9a41-205">a.</span></span> <span data-ttu-id="c9a41-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9a41-207">b.</span><span class="sxs-lookup"><span data-stu-id="c9a41-207">b.</span></span> <span data-ttu-id="c9a41-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c9a41-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9a41-209">c.</span><span class="sxs-lookup"><span data-stu-id="c9a41-209">c.</span></span> <span data-ttu-id="c9a41-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9a41-211">d.</span><span class="sxs-lookup"><span data-stu-id="c9a41-211">d.</span></span> <span data-ttu-id="c9a41-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c9a41-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="c9a41-213">LCVista test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9a41-213">Creating a LCVista test user</span></span>

<span data-ttu-id="c9a41-214">Bu bölümde, LCVista içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9a41-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="c9a41-215">Toocontact gerek [LCVista istemci destek ekibi](https://lcvista.com/contact) hello LCVista uygulama tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="c9a41-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9a41-216">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c9a41-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9a41-217">Bu bölümde, erişim tooLCVista vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9a41-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c9a41-219">**tooassign Britta Simon tooLCVista hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c9a41-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9a41-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c9a41-222">Merhaba uygulamalar listesinde **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-222">In hello applications list, select **LCVista**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="c9a41-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c9a41-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c9a41-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-226">Click **Add** button.</span></span> <span data-ttu-id="c9a41-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9a41-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c9a41-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c9a41-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9a41-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9a41-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9a41-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c9a41-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9a41-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c9a41-232">Testing single sign-on</span></span>

<span data-ttu-id="c9a41-233">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c9a41-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="c9a41-234">Merhaba LCVista kutucuğa tıklayın hello erişim paneli, siz olacaksınız tooOrganization oturum açma sayfası yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="c9a41-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="c9a41-235">Başarılı oturum açma işleminden sonra oturum açma LCVista uygulama tooyour olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c9a41-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="c9a41-236">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c9a41-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9a41-237">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c9a41-237">Additional resources</span></span>

* [<span data-ttu-id="c9a41-238">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c9a41-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9a41-239">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c9a41-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

