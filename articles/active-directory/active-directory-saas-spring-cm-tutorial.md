---
title: "Öğretici: Azure Active Directory Tümleştirme ile SpringCM | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SpringCM arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="c5dde-103">Öğretici: Azure Active Directory Tümleştirme SpringCM ile</span><span class="sxs-lookup"><span data-stu-id="c5dde-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="c5dde-104">Bu öğreticide, bilgi nasıl toointegrate SpringCM Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5dde-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5dde-105">SpringCM Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c5dde-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5dde-106">Erişim tooSpringCM sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c5dde-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="c5dde-107">Kullanıcıların tooautomatically get açan tooSpringCM (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c5dde-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5dde-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c5dde-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5dde-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5dde-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5dde-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c5dde-110">Prerequisites</span></span>

<span data-ttu-id="c5dde-111">tooconfigure SpringCM ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c5dde-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="c5dde-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c5dde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5dde-113">Bir SpringCM çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c5dde-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5dde-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c5dde-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5dde-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c5dde-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5dde-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c5dde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5dde-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5dde-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5dde-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c5dde-118">Scenario description</span></span>
<span data-ttu-id="c5dde-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c5dde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5dde-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c5dde-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5dde-121">Merhaba Galerisi'nden SpringCM ekleme</span><span class="sxs-lookup"><span data-stu-id="c5dde-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="c5dde-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c5dde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="c5dde-123">Merhaba Galerisi'nden SpringCM ekleme</span><span class="sxs-lookup"><span data-stu-id="c5dde-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="c5dde-124">Azure AD'ye tooconfigure hello tümleştirme SpringCM, tooadd SpringCM hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5dde-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5dde-125">**tooadd SpringCM hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c5dde-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5dde-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5dde-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5dde-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c5dde-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c5dde-133">Merhaba arama kutusuna yazın **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-133">In hello search box, type **SpringCM**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="c5dde-135">Merhaba Sonuçlar panelinde seçin **SpringCM**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c5dde-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5dde-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c5dde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5dde-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı SpringCM ile test etme</span><span class="sxs-lookup"><span data-stu-id="c5dde-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c5dde-139">Tek toowork'ın oturum açma hangi hello karşılık gelen SpringCM içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5dde-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="c5dde-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı SpringCM hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5dde-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="c5dde-141">Merhaba hello değeri SpringCM içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5dde-142">tooconfigure ve SpringCM ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c5dde-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5dde-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c5dde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5dde-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c5dde-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5dde-145">**[SpringCM test kullanıcısı oluşturma](#creating-a-springcm-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SpringCM içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c5dde-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5dde-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c5dde-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5dde-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c5dde-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5dde-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c5dde-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5dde-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SpringCM uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c5dde-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="c5dde-150">**tooconfigure Azure AD çoklu oturum açma ile SpringCM, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c5dde-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5dde-151">Hello hello üzerinde Azure portal'ın **SpringCM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c5dde-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c5dde-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="c5dde-155">Merhaba üzerinde **SpringCM etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c5dde-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="c5dde-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="c5dde-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5dde-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="c5dde-158">This value is not real.</span></span> <span data-ttu-id="c5dde-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="c5dde-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c5dde-160">Kişi [SpringCM istemci destek ekibi](https://knowledge.springcm.com/support) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="c5dde-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="c5dde-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c5dde-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="c5dde-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5dde-165">Merhaba üzerinde **SpringCM yapılandırma** 'yi tıklatın **yapılandırma SpringCM** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c5dde-166">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c5dde-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="c5dde-168">Farklı web tarayıcısı penceresinde tooyour üzerinde oturum **SpringCM** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="c5dde-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="c5dde-169">Merhaba üstte Hello menüde'ı tıklatın **GİTMEK için**, tıklatın **Tercihler**ve ardından hello **hesap tercihleri** 'yi tıklatın **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="c5dde-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="c5dde-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="c5dde-171">Hello kimlik sağlayıcı yapılandırması Bölümü'da, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c5dde-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c5dde-172">![Kimlik sağlayıcısı Yapılandırması](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "kimlik sağlayıcı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="c5dde-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="c5dde-173">a.</span><span class="sxs-lookup"><span data-stu-id="c5dde-173">a.</span></span> <span data-ttu-id="c5dde-174">tooupload indirilen Azure Active Directory sertifikanızı tıklatın **veren sertifika Seç** veya **değişiklik sertifikayı**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="c5dde-175">b.</span><span class="sxs-lookup"><span data-stu-id="c5dde-175">b.</span></span> <span data-ttu-id="c5dde-176">Yapıştır **SAML varlık kimliği** hello Azure portalından kopyaladığınız değeri **veren** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c5dde-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="c5dde-177">c.</span><span class="sxs-lookup"><span data-stu-id="c5dde-177">c.</span></span> <span data-ttu-id="c5dde-178">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **hizmet sağlayıcısı (SP) başlatılan Endpoint** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c5dde-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="c5dde-179">d.</span><span class="sxs-lookup"><span data-stu-id="c5dde-179">d.</span></span> <span data-ttu-id="c5dde-180">Seçin **SAML etkin** olarak **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="c5dde-181">e.</span><span class="sxs-lookup"><span data-stu-id="c5dde-181">e.</span></span> <span data-ttu-id="c5dde-182">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c5dde-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="c5dde-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c5dde-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5dde-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c5dde-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5dde-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5dde-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5dde-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c5dde-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5dde-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c5dde-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c5dde-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c5dde-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5dde-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5dde-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5dde-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c5dde-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5dde-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c5dde-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5dde-198">a.</span><span class="sxs-lookup"><span data-stu-id="c5dde-198">a.</span></span> <span data-ttu-id="c5dde-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5dde-200">b.</span><span class="sxs-lookup"><span data-stu-id="c5dde-200">b.</span></span> <span data-ttu-id="c5dde-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c5dde-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5dde-202">c.</span><span class="sxs-lookup"><span data-stu-id="c5dde-202">c.</span></span> <span data-ttu-id="c5dde-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5dde-204">d.</span><span class="sxs-lookup"><span data-stu-id="c5dde-204">d.</span></span> <span data-ttu-id="c5dde-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c5dde-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="c5dde-206">SpringCM test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c5dde-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="c5dde-207">tooenable Azure Active Directory Kullanıcıları toolog tooSpringCM bunların SpringCM sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5dde-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="c5dde-208">SpringCM Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c5dde-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="c5dde-209">Daha fazla bilgi için bkz: [oluşturma ve SpringCM kullanıcı düzenleme](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="c5dde-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="c5dde-210">**bir kullanıcı hesabı tooSpringCM tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c5dde-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5dde-211">İçinde tooyour oturum **SpringCM** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="c5dde-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="c5dde-212">Tıklatın **GOTO**ve ardından **adres defteri**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="c5dde-213">![Kullanıcı oluşturma](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="c5dde-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="c5dde-214">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-214">Click **Create User**.</span></span>

4. <span data-ttu-id="c5dde-215">Seçin bir **kullanıcı rolü**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="c5dde-216">Seçin **etkinleştirme e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="c5dde-217">Metin kutuları türü hello ad, Soyadı ve hello tooprovision istediğiniz geçerli bir Azure Active Directory kullanıcı hesabının e-posta adresi ilgili.</span><span class="sxs-lookup"><span data-stu-id="c5dde-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="c5dde-218">Merhaba kullanıcı tooa ekleme **güvenlik grubu**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="c5dde-219">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c5dde-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c5dde-220">API AAD kullanıcı hesaplarının SpringCM tooprovision tarafından sağlanan veya herhangi diğer SpringCM kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5dde-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5dde-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c5dde-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5dde-222">Bu bölümde, erişim tooSpringCM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c5dde-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c5dde-224">**tooassign Britta Simon tooSpringCM hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c5dde-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5dde-225">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c5dde-227">Merhaba uygulamalar listesinde **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-227">In hello applications list, select **SpringCM**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="c5dde-229">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c5dde-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c5dde-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c5dde-231">Click **Add** button.</span></span> <span data-ttu-id="c5dde-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c5dde-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c5dde-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c5dde-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5dde-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c5dde-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5dde-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c5dde-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5dde-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c5dde-237">Testing single sign-on</span></span>

<span data-ttu-id="c5dde-238">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c5dde-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="c5dde-239">Merhaba SpringCM hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SpringCM uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c5dde-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="c5dde-240">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5dde-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c5dde-241">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c5dde-241">Additional resources</span></span>

* [<span data-ttu-id="c5dde-242">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c5dde-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5dde-243">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c5dde-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

