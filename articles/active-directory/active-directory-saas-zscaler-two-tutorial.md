---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler iki | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler iki arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: dcd13d399f093f24a945f234401cd5b7e527ed34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="dffde-103">Öğretici: Azure Active Directory Tümleştirme ile Zscaler iki</span><span class="sxs-lookup"><span data-stu-id="dffde-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="dffde-104">Bu öğreticide, bilgi nasıl toointegrate Zscaler iki Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dffde-104">In this tutorial, you learn how toointegrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dffde-105">Zscaler iki Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="dffde-105">Integrating Zscaler Two with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dffde-106">Erişim tooZscaler iki sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="dffde-106">You can control in Azure AD who has access tooZscaler Two</span></span>
- <span data-ttu-id="dffde-107">Kullanıcıların tooautomatically get açan tooZscaler iki etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="dffde-107">You can enable your users tooautomatically get signed-on tooZscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dffde-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="dffde-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dffde-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dffde-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dffde-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dffde-110">Prerequisites</span></span>

<span data-ttu-id="dffde-111">tooconfigure Zscaler iki ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dffde-111">tooconfigure Azure AD integration with Zscaler Two, you need hello following items:</span></span>

- <span data-ttu-id="dffde-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="dffde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dffde-113">Bir Zscaler iki çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="dffde-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dffde-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="dffde-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dffde-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="dffde-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dffde-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="dffde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dffde-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dffde-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dffde-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="dffde-118">Scenario description</span></span>
<span data-ttu-id="dffde-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="dffde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dffde-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="dffde-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dffde-121">Zscaler iki hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="dffde-121">Adding Zscaler Two from hello gallery</span></span>
2. <span data-ttu-id="dffde-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="dffde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-hello-gallery"></a><span data-ttu-id="dffde-123">Zscaler iki hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="dffde-123">Adding Zscaler Two from hello gallery</span></span>
<span data-ttu-id="dffde-124">Azure AD'ye tooconfigure hello tümleştirme Zscaler iki, hello galeri tooyour yönetilen SaaS uygulamaları listesinden Zscaler iki tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="dffde-124">tooconfigure hello integration of Zscaler Two into Azure AD, you need tooadd Zscaler Two from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dffde-125">**tooadd Zscaler iki hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dffde-125">**tooadd Zscaler Two from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffde-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dffde-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dffde-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="dffde-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dffde-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="dffde-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="dffde-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dffde-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="dffde-133">Merhaba arama kutusuna yazın **Zscaler iki**.</span><span class="sxs-lookup"><span data-stu-id="dffde-133">In hello search box, type **Zscaler Two**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. <span data-ttu-id="dffde-135">Merhaba Sonuçlar panelinde seçin **Zscaler iki**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dffde-135">In hello results panel, select **Zscaler Two**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dffde-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="dffde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dffde-138">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açma Zscaler "Britta Simon" adlı bir test kullanıcı tabanlı iki sınayın.</span><span class="sxs-lookup"><span data-stu-id="dffde-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dffde-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler iki içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="dffde-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Two is tooa user in Azure AD.</span></span> <span data-ttu-id="dffde-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Zscaler iki arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="dffde-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Two needs toobe established.</span></span>

<span data-ttu-id="dffde-141">İki Zscaler içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="dffde-141">In Zscaler Two, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dffde-142">tooconfigure ve Zscaler iki ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="dffde-142">tooconfigure and test Azure AD single sign-on with Zscaler Two, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dffde-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="dffde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dffde-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="dffde-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="dffde-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="dffde-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="dffde-146">**[Zscaler iki test kullanıcısı oluşturma](#creating-a-zscaler-two-test-user)**  -toohave Britta Simon Zscaler bağlantılı toohello Azure AD kullanıcı gösterimi olan iki içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="dffde-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - toohave a counterpart of Britta Simon in Zscaler Two that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="dffde-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dffde-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="dffde-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="dffde-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dffde-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dffde-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dffde-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler iki uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dffde-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="dffde-151">**tooconfigure Azure AD çoklu oturum açma ile Zscaler iki hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dffde-151">**tooconfigure Azure AD single sign-on with Zscaler Two, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffde-152">Hello hello üzerinde Azure portal'ın **Zscaler iki** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="dffde-152">In hello Azure portal, on hello **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="dffde-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dffde-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. <span data-ttu-id="dffde-156">Merhaba üzerinde **Zscaler iki etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-156">On hello **Zscaler Two Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="dffde-158">Merhaba oturum açma URL'si metin kutusuna, kullanıcıların toosign üzerinde tooyour tarafından ZScaler iki uygulama kullanılan hello URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="dffde-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dffde-159">Bu değeri hello ile tooupdate sahip gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="dffde-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="dffde-160">Kişi [Zscaler iki istemci destek ekibi](https://www.zscaler.com/company/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="dffde-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="dffde-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dffde-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. <span data-ttu-id="dffde-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dffde-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dffde-165">Merhaba üzerinde **Zscaler iki yapılandırma** 'yi tıklatın **Zscaler iki yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="dffde-165">On hello **Zscaler Two Configuration** section, click **Configure Zscaler Two** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dffde-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="dffde-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. <span data-ttu-id="dffde-168">Farklı web tarayıcısı penceresinde tooyour ZScaler iki şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dffde-168">In a different web browser window, log in tooyour ZScaler Two company site as an administrator.</span></span>

8. <span data-ttu-id="dffde-169">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="dffde-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="dffde-170">![Yönetim](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="dffde-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="dffde-171">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="dffde-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="dffde-172">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="dffde-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="dffde-173">Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="dffde-174">![Kimlik doğrulama](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="dffde-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="dffde-175">a.</span><span class="sxs-lookup"><span data-stu-id="dffde-175">a.</span></span> <span data-ttu-id="dffde-176">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="dffde-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="dffde-177">b.</span><span class="sxs-lookup"><span data-stu-id="dffde-177">b.</span></span> <span data-ttu-id="dffde-178">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="dffde-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="dffde-179">Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="dffde-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="dffde-180">![Çoklu oturum açma](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="dffde-180">![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="dffde-181">a.</span><span class="sxs-lookup"><span data-stu-id="dffde-181">a.</span></span> <span data-ttu-id="dffde-182">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="dffde-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="dffde-183">b.</span><span class="sxs-lookup"><span data-stu-id="dffde-183">b.</span></span> <span data-ttu-id="dffde-184">Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="dffde-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="dffde-185">c.</span><span class="sxs-lookup"><span data-stu-id="dffde-185">c.</span></span> <span data-ttu-id="dffde-186">tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="dffde-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="dffde-187">d.</span><span class="sxs-lookup"><span data-stu-id="dffde-187">d.</span></span> <span data-ttu-id="dffde-188">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="dffde-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="dffde-189">Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="dffde-190">![Yönetim](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="dffde-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="dffde-191">a.</span><span class="sxs-lookup"><span data-stu-id="dffde-191">a.</span></span> <span data-ttu-id="dffde-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dffde-192">Click **Save**.</span></span>

    <span data-ttu-id="dffde-193">b.</span><span class="sxs-lookup"><span data-stu-id="dffde-193">b.</span></span> <span data-ttu-id="dffde-194">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="dffde-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="dffde-195">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dffde-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="dffde-196">Internet Explorer'da tooconfigure hello proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="dffde-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="dffde-197">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="dffde-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="dffde-198">Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="dffde-199">![Internet Seçenekleri](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="dffde-199">![Internet Options](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="dffde-200">Merhaba tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="dffde-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="dffde-201">![Bağlantıları](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="dffde-201">![Connections](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="dffde-202">Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="dffde-203">Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="dffde-204">![Proxy sunucusu](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="dffde-204">![Proxy server](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="dffde-205">a.</span><span class="sxs-lookup"><span data-stu-id="dffde-205">a.</span></span> <span data-ttu-id="dffde-206">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="dffde-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="dffde-207">b.</span><span class="sxs-lookup"><span data-stu-id="dffde-207">b.</span></span> <span data-ttu-id="dffde-208">Başlangıç adresi metin kutusuna yazın **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="dffde-208">In hello Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="dffde-209">c.</span><span class="sxs-lookup"><span data-stu-id="dffde-209">c.</span></span> <span data-ttu-id="dffde-210">Başlangıç bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="dffde-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="dffde-211">d.</span><span class="sxs-lookup"><span data-stu-id="dffde-211">d.</span></span> <span data-ttu-id="dffde-212">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="dffde-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="dffde-213">e.</span><span class="sxs-lookup"><span data-stu-id="dffde-213">e.</span></span> <span data-ttu-id="dffde-214">Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="dffde-215">Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="dffde-216">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="dffde-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dffde-217">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="dffde-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dffde-218">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dffde-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dffde-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dffde-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="dffde-220">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="dffde-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="dffde-222">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dffde-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffde-223">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dffde-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dffde-225">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="dffde-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dffde-227">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dffde-229">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dffde-231">a.</span><span class="sxs-lookup"><span data-stu-id="dffde-231">a.</span></span> <span data-ttu-id="dffde-232">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dffde-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dffde-233">b.</span><span class="sxs-lookup"><span data-stu-id="dffde-233">b.</span></span> <span data-ttu-id="dffde-234">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="dffde-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dffde-235">c.</span><span class="sxs-lookup"><span data-stu-id="dffde-235">c.</span></span> <span data-ttu-id="dffde-236">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="dffde-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dffde-237">d.</span><span class="sxs-lookup"><span data-stu-id="dffde-237">d.</span></span> <span data-ttu-id="dffde-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dffde-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="dffde-239">Zscaler iki test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dffde-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="dffde-240">tooenable Azure AD kullanıcıların toolog tooZScaler iki, sağlanan tooZScaler iki olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dffde-240">tooenable Azure AD users toolog in tooZScaler Two, they must be provisioned tooZScaler Two.</span></span> <span data-ttu-id="dffde-241">ZScaler iki, Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="dffde-241">In hello case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="dffde-242">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="dffde-243">İçinde tooyour oturum **Zscaler iki** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="dffde-243">Log in tooyour **Zscaler Two** tenant.</span></span>

2. <span data-ttu-id="dffde-244">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="dffde-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="dffde-245">![Yönetim](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="dffde-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="dffde-246">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="dffde-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="dffde-247">![Ekleme](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="dffde-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="dffde-248">Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dffde-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="dffde-249">![Ekleme](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="dffde-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="dffde-250">Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="dffde-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="dffde-251">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="dffde-251">![Add User](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="dffde-252">a.</span><span class="sxs-lookup"><span data-stu-id="dffde-252">a.</span></span> <span data-ttu-id="dffde-253">Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** geçerli bir Azure AD hesabının tooprovision istiyor.</span><span class="sxs-lookup"><span data-stu-id="dffde-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="dffde-254">b.</span><span class="sxs-lookup"><span data-stu-id="dffde-254">b.</span></span> <span data-ttu-id="dffde-255">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dffde-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="dffde-256">API'leri, Azure AD kullanıcı hesapları ZScaler iki tooprovision tarafından sağlanan veya herhangi diğer ZScaler iki kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dffde-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dffde-257">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="dffde-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dffde-258">Bu bölümde, erişim tooZscaler iki vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="dffde-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Two.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="dffde-260">**tooassign Britta Simon tooZscaler iki hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="dffde-260">**tooassign Britta Simon tooZscaler Two, perform hello following steps:**</span></span>

1. <span data-ttu-id="dffde-261">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="dffde-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="dffde-263">Merhaba uygulamalar listesinde **Zscaler iki**.</span><span class="sxs-lookup"><span data-stu-id="dffde-263">In hello applications list, select **Zscaler Two**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. <span data-ttu-id="dffde-265">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="dffde-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="dffde-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dffde-267">Click **Add** button.</span></span> <span data-ttu-id="dffde-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="dffde-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="dffde-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dffde-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dffde-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="dffde-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dffde-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="dffde-273">Testing single sign-on</span></span>

<span data-ttu-id="dffde-274">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="dffde-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dffde-275">Zscaler iki hello erişim paneli döşeme hello tıkladığınızda, otomatik olarak oturum açma Zscaler iki uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dffde-275">When you click hello Zscaler Two tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Two application.</span></span>
<span data-ttu-id="dffde-276">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dffde-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dffde-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="dffde-277">Additional resources</span></span>

* [<span data-ttu-id="dffde-278">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="dffde-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dffde-279">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="dffde-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png

