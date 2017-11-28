---
title: "Öğretici: Azure Active Directory Tümleştirme tanı ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve tanı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="0ea78-103">Öğretici: Tanı Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="0ea78-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="0ea78-104">Bu öğreticide, bilgi toointegrate Azure Active Directory (Azure AD) ile nasıl algılar.</span><span class="sxs-lookup"><span data-stu-id="0ea78-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ea78-105">Tanı Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0ea78-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0ea78-106">Erişim tooRecognize sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ea78-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="0ea78-107">Kullanıcıların tooautomatically get açan tooRecognize (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0ea78-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ea78-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0ea78-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0ea78-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ea78-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ea78-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ea78-110">Prerequisites</span></span>

<span data-ttu-id="0ea78-111">tooconfigure Azure AD tümleştirme tanı ile aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea78-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="0ea78-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0ea78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ea78-113">Bir tanı çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0ea78-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ea78-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ea78-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ea78-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea78-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ea78-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0ea78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ea78-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ea78-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ea78-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0ea78-118">Scenario description</span></span>
<span data-ttu-id="0ea78-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0ea78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ea78-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0ea78-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ea78-121">Tanı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0ea78-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="0ea78-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0ea78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="0ea78-123">Tanı hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0ea78-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="0ea78-124">Azure AD'ye tooconfigure hello tümleştirme tanı, tooadd tanı hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ea78-125">**tooadd tanı hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea78-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ea78-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0ea78-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0ea78-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0ea78-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0ea78-133">Merhaba arama kutusuna yazın **tanı**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-133">In hello search box, type **Recognize**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="0ea78-135">Merhaba Sonuçlar panelinde seçin **tanı**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0ea78-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ea78-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0ea78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ea78-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı tanı sınayın.</span><span class="sxs-lookup"><span data-stu-id="0ea78-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ea78-139">Tek toowork'ın oturum açma hangi hello karşılık gelen tanı içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="0ea78-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı tanı hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="0ea78-141">Tanı içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0ea78-142">tooconfigure ve test Azure AD çoklu oturum açma tanı ile yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea78-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0ea78-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0ea78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0ea78-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0ea78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ea78-145">**[Tanı test kullanıcısı oluşturma](#creating-a-recognize-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir tanı içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0ea78-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ea78-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0ea78-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ea78-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0ea78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0ea78-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0ea78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0ea78-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma tanı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0ea78-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="0ea78-150">**tooconfigure Azure AD çoklu oturum açma ile tanı, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea78-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ea78-151">Hello hello üzerinde Azure portal'ın **tanı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0ea78-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0ea78-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="0ea78-155">Merhaba üzerinde **etki alanı tanıması ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ea78-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="0ea78-157">a.</span><span class="sxs-lookup"><span data-stu-id="0ea78-157">a.</span></span> <span data-ttu-id="0ea78-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="0ea78-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="0ea78-159">b.</span><span class="sxs-lookup"><span data-stu-id="0ea78-159">b.</span></span> <span data-ttu-id="0ea78-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="0ea78-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ea78-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-161">These values are not real.</span></span> <span data-ttu-id="0ea78-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="0ea78-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0ea78-163">Kişi [tanıması istemci destek ekibi](mailto:support@recognizeapp.com) oturum açma URL'si almak için tanımlayıcı değeri hello hello öğreticinin ilerleyen bölümlerinde açıklanan SSO ayarları bölümünün gelen hello servis sağlayıcı meta verileri URL'sini açarak alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea78-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="0ea78-164">.</span><span class="sxs-lookup"><span data-stu-id="0ea78-164">.</span></span> 
 
4. <span data-ttu-id="0ea78-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0ea78-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="0ea78-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ea78-169">Merhaba üzerinde **Tanı Yapılandırması** 'yi tıklatın **Yapılandırma tanı** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0ea78-170">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0ea78-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="0ea78-172">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour tanı Kiracı.</span><span class="sxs-lookup"><span data-stu-id="0ea78-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="0ea78-173">Merhaba sağ üst köşesinde, tıklatın **menü**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="0ea78-174">Çok Git**şirket yönetici**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-174">Go too**Company Admin**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="0ea78-176">Merhaba sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="0ea78-178">Aşağıdaki adımları hello gerçekleştirmek **SSO ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="0ea78-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="0ea78-180">a.</span><span class="sxs-lookup"><span data-stu-id="0ea78-180">a.</span></span> <span data-ttu-id="0ea78-181">Olarak **etkinleştirmek SSO**seçin **ON**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="0ea78-182">b.</span><span class="sxs-lookup"><span data-stu-id="0ea78-182">b.</span></span> <span data-ttu-id="0ea78-183">Merhaba, **IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0ea78-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="0ea78-184">c.</span><span class="sxs-lookup"><span data-stu-id="0ea78-184">c.</span></span> <span data-ttu-id="0ea78-185">Merhaba, **Sso hedef url** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0ea78-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="0ea78-186">d.</span><span class="sxs-lookup"><span data-stu-id="0ea78-186">d.</span></span> <span data-ttu-id="0ea78-187">Merhaba, **Slo hedef url** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0ea78-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="0ea78-188">e.</span><span class="sxs-lookup"><span data-stu-id="0ea78-188">e.</span></span> <span data-ttu-id="0ea78-189">İndirilen açmak **sertifika (Base64)** dosyasını Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello Yapıştır **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0ea78-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="0ea78-190">f.</span><span class="sxs-lookup"><span data-stu-id="0ea78-190">f.</span></span> <span data-ttu-id="0ea78-191">Merhaba tıklatın **Ayarları Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="0ea78-192">Merhaba yanında **SSO ayarları** bölümünde, altında hello URL'sini Kopyala **hizmet sağlayıcısı meta veri URL'sini**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="0ea78-194">Açık hello **meta veri URL'sini bağlantı** boş tarayıcı toodownload hello meta veri belgesi altında.</span><span class="sxs-lookup"><span data-stu-id="0ea78-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="0ea78-195">Ardından hello EntityDescriptor value(entityID) hello dosyasından kopyalayın ve yapıştırın **tanımlayıcısı** metin kutusuna **etki alanı tanıması ve URL'leri bölümüne** Azure Portal'daki.</span><span class="sxs-lookup"><span data-stu-id="0ea78-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="0ea78-197">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0ea78-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0ea78-198">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0ea78-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0ea78-199">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ea78-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ea78-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea78-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="0ea78-201">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0ea78-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0ea78-203">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea78-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ea78-204">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ea78-206">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ea78-208">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea78-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ea78-210">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0ea78-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ea78-212">a.</span><span class="sxs-lookup"><span data-stu-id="0ea78-212">a.</span></span> <span data-ttu-id="0ea78-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ea78-214">b.</span><span class="sxs-lookup"><span data-stu-id="0ea78-214">b.</span></span> <span data-ttu-id="0ea78-215">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0ea78-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ea78-216">c.</span><span class="sxs-lookup"><span data-stu-id="0ea78-216">c.</span></span> <span data-ttu-id="0ea78-217">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0ea78-218">d.</span><span class="sxs-lookup"><span data-stu-id="0ea78-218">d.</span></span> <span data-ttu-id="0ea78-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ea78-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="0ea78-220">Tanı test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea78-220">Creating a Recognize test user</span></span>

<span data-ttu-id="0ea78-221">Tanı içine sipariş tooenable Azure AD kullanıcıların toolog bunların tanı sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0ea78-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="0ea78-222">Tanı Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="0ea78-223">Bu uygulama SCIM'yi sağlama desteklemiyor, ancak kullanıcılar sağlayan bir alternatif kullanıcı eşitleme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="0ea78-224">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea78-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ea78-225">Tanı şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0ea78-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="0ea78-226">Merhaba sağ üst köşesinde, tıklatın **menü**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="0ea78-227">Çok Git**şirket yönetici**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="0ea78-228">Merhaba sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="0ea78-229">Aşağıdaki adımları hello gerçekleştirmek **kullanıcı eşitleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="0ea78-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="0ea78-230">![Yeni kullanıcı](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="0ea78-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="0ea78-231">a.</span><span class="sxs-lookup"><span data-stu-id="0ea78-231">a.</span></span> <span data-ttu-id="0ea78-232">Olarak **eşitlemenin etkin**seçin **ON**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="0ea78-233">b.</span><span class="sxs-lookup"><span data-stu-id="0ea78-233">b.</span></span> <span data-ttu-id="0ea78-234">Olarak **Seç eşitleme sağlayıcısı**seçin **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="0ea78-235">c.</span><span class="sxs-lookup"><span data-stu-id="0ea78-235">c.</span></span> <span data-ttu-id="0ea78-236">Tıklatın **kullanıcı eşitleme çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0ea78-237">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0ea78-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0ea78-238">Bu bölümde, erişim tooRecognize vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ea78-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0ea78-240">**tooassign Britta Simon tooRecognize hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0ea78-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ea78-241">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0ea78-243">Merhaba uygulamalar listesinde **tanı**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-243">In hello applications list, select **Recognize**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="0ea78-245">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0ea78-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0ea78-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea78-247">Click **Add** button.</span></span> <span data-ttu-id="0ea78-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea78-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0ea78-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0ea78-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0ea78-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea78-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ea78-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0ea78-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0ea78-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0ea78-253">Testing single sign-on</span></span>

<span data-ttu-id="0ea78-254">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0ea78-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0ea78-255">Merhaba tanı hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour tanı uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea78-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="0ea78-256">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0ea78-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ea78-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0ea78-257">Additional resources</span></span>

* [<span data-ttu-id="0ea78-258">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0ea78-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ea78-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0ea78-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

