---
title: "Öğretici: Azure Active Directory Tümleştirme Adobe işaretiyle | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma Azure Active Directory ve Adobe oturum arasında bilgi edinin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="17dd3-103">Öğretici: Azure Active Directory Tümleştirme Adobe oturum</span><span class="sxs-lookup"><span data-stu-id="17dd3-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="17dd3-104">Bu öğreticide, bilgi Adobe toointegrate oturum nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="17dd3-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17dd3-105">Adobe oturum Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="17dd3-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17dd3-106">Erişim tooAdobe oturum sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="17dd3-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="17dd3-107">Kullanıcıların tooautomatically get açan tooAdobe oturum (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="17dd3-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17dd3-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="17dd3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17dd3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17dd3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17dd3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="17dd3-110">Prerequisites</span></span>

<span data-ttu-id="17dd3-111">tooconfigure Adobe oturum ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="17dd3-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="17dd3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="17dd3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17dd3-113">Bir Adobe oturum çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="17dd3-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17dd3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="17dd3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17dd3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="17dd3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17dd3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="17dd3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17dd3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17dd3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17dd3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="17dd3-118">Scenario description</span></span>
<span data-ttu-id="17dd3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="17dd3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17dd3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="17dd3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17dd3-121">Adobe oturum hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="17dd3-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="17dd3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="17dd3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="17dd3-123">Adobe oturum hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="17dd3-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="17dd3-124">Azure AD'ye tooconfigure hello tümleştirme, Adobe oturum tooadd Adobe oturum hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17dd3-125">**tooadd Adobe oturum hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17dd3-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17dd3-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17dd3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17dd3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="17dd3-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="17dd3-133">Merhaba arama kutusuna yazın **Adobe oturum**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="17dd3-135">Merhaba Sonuçlar panelinde seçin **Adobe oturum**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="17dd3-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17dd3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="17dd3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17dd3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Adobe işaretiyle test etme</span><span class="sxs-lookup"><span data-stu-id="17dd3-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17dd3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Adobe oturum içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="17dd3-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Adobe oturum hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="17dd3-141">Adobe oturum açma hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="17dd3-142">tooconfigure ve Adobe işaretiyle Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="17dd3-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17dd3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="17dd3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17dd3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="17dd3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17dd3-145">**[Adobe oturum test kullanıcısı oluşturma](#creating-an-adobe-sign-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Adobe oturum içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="17dd3-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17dd3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="17dd3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17dd3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="17dd3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17dd3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="17dd3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17dd3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Adobe oturum uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17dd3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="17dd3-150">**tooconfigure Azure AD çoklu oturum açma Adobe işaretiyle hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17dd3-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="17dd3-151">Hello hello üzerinde Azure portal'ın **Adobe oturum** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="17dd3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="17dd3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="17dd3-155">Merhaba üzerinde **Adobe oturum etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="17dd3-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="17dd3-157">a.</span><span class="sxs-lookup"><span data-stu-id="17dd3-157">a.</span></span> <span data-ttu-id="17dd3-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="17dd3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="17dd3-159">b.</span><span class="sxs-lookup"><span data-stu-id="17dd3-159">b.</span></span> <span data-ttu-id="17dd3-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="17dd3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17dd3-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-161">These values are not real.</span></span> <span data-ttu-id="17dd3-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="17dd3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="17dd3-163">Kişi [Adobe oturum istemci destek ekibi](https://helpx.adobe.com/in/contact/support.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="17dd3-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="17dd3-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="17dd3-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="17dd3-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17dd3-168">Merhaba üzerinde **Adobe oturum yapılandırma** 'yi tıklatın **yapılandırma Adobe oturum** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="17dd3-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="17dd3-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="17dd3-171">Farklı web tarayıcısı penceresinde tooyour Adobe oturum şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="17dd3-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="17dd3-172">Hello üstte Hello menüde'ı tıklatın **hesap**ve ardından, hello sol tarafında hello Gezinti Bölmesi'nde **SAML ayarları** altında **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="17dd3-173">![Hesap](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "hesabı")</span><span class="sxs-lookup"><span data-stu-id="17dd3-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="17dd3-174">Hello SAML Ayarlar bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="17dd3-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="17dd3-175">![SAML ayarları](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="17dd3-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="17dd3-176">a.</span><span class="sxs-lookup"><span data-stu-id="17dd3-176">a.</span></span> <span data-ttu-id="17dd3-177">Olarak **SAML modu**seçin **SAML zorunlu**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="17dd3-178">b.</span><span class="sxs-lookup"><span data-stu-id="17dd3-178">b.</span></span> <span data-ttu-id="17dd3-179">Seçin **EchoSign kimlik bilgilerini kullanarak EchoSign hesap yöneticileri izin toolog**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="17dd3-180">c.</span><span class="sxs-lookup"><span data-stu-id="17dd3-180">c.</span></span> <span data-ttu-id="17dd3-181">Olarak **kullanıcı oluşturma**seçin **otomatik olarak SAML kimliği doğrulanmış kullanıcılar eklemek**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="17dd3-182">Taşıma, aşağıdaki hello gerçekleştirme adımları:</span><span class="sxs-lookup"><span data-stu-id="17dd3-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="17dd3-183">![SAML ayarları](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML ayarları")</span><span class="sxs-lookup"><span data-stu-id="17dd3-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="17dd3-184">a.</span><span class="sxs-lookup"><span data-stu-id="17dd3-184">a.</span></span> <span data-ttu-id="17dd3-185">Yapıştır **SAML varlık kimliği**, hello Azure portalından kopyalanan **IDP varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="17dd3-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="17dd3-186">b.</span><span class="sxs-lookup"><span data-stu-id="17dd3-186">b.</span></span> <span data-ttu-id="17dd3-187">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hello Azure portalından kopyalanan **IDP oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="17dd3-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="17dd3-188">c.</span><span class="sxs-lookup"><span data-stu-id="17dd3-188">c.</span></span> <span data-ttu-id="17dd3-189">Yapıştır **Sign-Out URL**, hello Azure portalından kopyalanan **IDP oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="17dd3-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="17dd3-190">d.</span><span class="sxs-lookup"><span data-stu-id="17dd3-190">d.</span></span> <span data-ttu-id="17dd3-191">İndirilen açmak **Certificate(Base64)** dosyasını Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello Yapıştır **IDP sertifika** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="17dd3-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="17dd3-192">e.</span><span class="sxs-lookup"><span data-stu-id="17dd3-192">e.</span></span> <span data-ttu-id="17dd3-193">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="17dd3-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="17dd3-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17dd3-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="17dd3-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17dd3-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17dd3-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17dd3-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="17dd3-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="17dd3-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="17dd3-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="17dd3-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17dd3-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17dd3-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17dd3-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17dd3-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="17dd3-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17dd3-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="17dd3-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17dd3-209">a.</span><span class="sxs-lookup"><span data-stu-id="17dd3-209">a.</span></span> <span data-ttu-id="17dd3-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17dd3-211">b.</span><span class="sxs-lookup"><span data-stu-id="17dd3-211">b.</span></span> <span data-ttu-id="17dd3-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="17dd3-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17dd3-213">c.</span><span class="sxs-lookup"><span data-stu-id="17dd3-213">c.</span></span> <span data-ttu-id="17dd3-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17dd3-215">d.</span><span class="sxs-lookup"><span data-stu-id="17dd3-215">d.</span></span> <span data-ttu-id="17dd3-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="17dd3-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="17dd3-217">Adobe oturum test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="17dd3-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="17dd3-218">tooenable Azure AD kullanıcıların toolog tooAdobe oturum'da, bunlar Adobe oturum açın sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="17dd3-219">Adobe oturum Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="17dd3-220">API AAD kullanıcı hesapları Adobe oturum tooprovision tarafından sağlanan veya herhangi diğer Adobe oturum kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17dd3-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="17dd3-221">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17dd3-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="17dd3-222">İçinde tooyour oturum **Adobe oturum** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="17dd3-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="17dd3-223">Hello üstte Hello menüde'ı tıklatın **hesap**ve ardından, hello sol tarafında hello Gezinti Bölmesi'nde **kullanıcıları ve grupları**ve ardından **yeni bir kullanıcı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="17dd3-224">![Hesap](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "hesabı")</span><span class="sxs-lookup"><span data-stu-id="17dd3-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="17dd3-225">Merhaba, **yeni kullanıcı oluştur** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="17dd3-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="17dd3-226">![Kullanıcı oluşturma](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="17dd3-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="17dd3-227">a.</span><span class="sxs-lookup"><span data-stu-id="17dd3-227">a.</span></span> <span data-ttu-id="17dd3-228">Türü hello **e-posta adresi**, **ad**, ve **Soyadı** , metin kutuları hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.</span><span class="sxs-lookup"><span data-stu-id="17dd3-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="17dd3-229">b.</span><span class="sxs-lookup"><span data-stu-id="17dd3-229">b.</span></span> <span data-ttu-id="17dd3-230">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="17dd3-231">Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="17dd3-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17dd3-232">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="17dd3-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17dd3-233">Bu bölümde, erişim tooAdobe oturum vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="17dd3-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="17dd3-235">**tooassign Britta Simon tooAdobe oturum, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="17dd3-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="17dd3-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="17dd3-238">Merhaba uygulamalar listesinde **Adobe oturum**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="17dd3-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="17dd3-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="17dd3-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="17dd3-242">Click **Add** button.</span></span> <span data-ttu-id="17dd3-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="17dd3-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="17dd3-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="17dd3-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17dd3-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="17dd3-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17dd3-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="17dd3-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17dd3-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="17dd3-248">Testing single sign-on</span></span>

<span data-ttu-id="17dd3-249">Adobe oturum hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak oturum açma Adobe oturum uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="17dd3-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="17dd3-250">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17dd3-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17dd3-251">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="17dd3-251">Additional resources</span></span>

* [<span data-ttu-id="17dd3-252">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="17dd3-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17dd3-253">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="17dd3-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

