---
title: "Öğretici: Azure Active Directory Tümleştirme Zscaler Beta ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler Beta arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="e1720-103">Öğretici: Azure Active Directory Tümleştirme Zscaler Beta ile</span><span class="sxs-lookup"><span data-stu-id="e1720-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="e1720-104">Bu öğreticide, bilgi nasıl toointegrate Zscaler Beta Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1720-104">In this tutorial, you learn how toointegrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1720-105">Zscaler Beta Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1720-105">Integrating Zscaler Beta with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1720-106">Erişim tooZscaler Beta sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1720-106">You can control in Azure AD who has access tooZscaler Beta</span></span>
- <span data-ttu-id="e1720-107">Kullanıcıların tooautomatically get açan tooZscaler Beta (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1720-107">You can enable your users tooautomatically get signed-on tooZscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1720-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e1720-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e1720-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1720-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1720-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1720-110">Prerequisites</span></span>

<span data-ttu-id="e1720-111">tooconfigure Zscaler Beta ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1720-111">tooconfigure Azure AD integration with Zscaler Beta, you need hello following items:</span></span>

- <span data-ttu-id="e1720-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1720-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1720-113">Bir Zscaler Beta çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e1720-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1720-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1720-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1720-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1720-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1720-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1720-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1720-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1720-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1720-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1720-118">Scenario description</span></span>
<span data-ttu-id="e1720-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1720-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1720-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1720-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1720-121">Merhaba Galerisi'nden Zscaler Beta ekleme</span><span class="sxs-lookup"><span data-stu-id="e1720-121">Adding Zscaler Beta from hello gallery</span></span>
2. <span data-ttu-id="e1720-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1720-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-hello-gallery"></a><span data-ttu-id="e1720-123">Merhaba Galerisi'nden Zscaler Beta ekleme</span><span class="sxs-lookup"><span data-stu-id="e1720-123">Adding Zscaler Beta from hello gallery</span></span>
<span data-ttu-id="e1720-124">Azure AD'ye tooconfigure hello tümleştirme Zscaler Beta'nin tooadd Zscaler Beta hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1720-124">tooconfigure hello integration of Zscaler Beta into Azure AD, you need tooadd Zscaler Beta from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1720-125">**tooadd Zscaler Beta hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1720-125">**tooadd Zscaler Beta from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1720-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1720-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1720-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1720-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1720-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1720-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e1720-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1720-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e1720-133">Merhaba arama kutusuna yazın **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="e1720-133">In hello search box, type **Zscaler Beta**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. <span data-ttu-id="e1720-135">Merhaba Sonuçlar panelinde seçin **Zscaler Beta**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e1720-135">In hello results panel, select **Zscaler Beta**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1720-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1720-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1720-138">Bu bölümde, yapılandırmanız ve Zscaler Beta ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="e1720-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1720-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler Beta tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1720-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Beta is tooa user in Azure AD.</span></span> <span data-ttu-id="e1720-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Zscaler Beta hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1720-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Beta needs toobe established.</span></span>

<span data-ttu-id="e1720-141">Merhaba hello değeri Zscaler Beta'da atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e1720-141">In Zscaler Beta, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1720-142">tooconfigure ve Zscaler Beta ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1720-142">tooconfigure and test Azure AD single sign-on with Zscaler Beta, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1720-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e1720-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1720-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="e1720-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="e1720-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e1720-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="e1720-146">**[Zscaler Beta test kullanıcısı oluşturma](#creating-a-zscaler-beta-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zscaler Beta, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e1720-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - toohave a counterpart of Britta Simon in Zscaler Beta that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="e1720-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1720-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="e1720-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1720-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1720-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1720-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1720-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler Beta uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1720-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="e1720-151">**tooconfigure Azure AD çoklu oturum açma Zscaler Beta ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1720-151">**tooconfigure Azure AD single sign-on with Zscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1720-152">Hello hello üzerinde Azure portal'ın **Zscaler Beta** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1720-152">In hello Azure portal, on hello **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e1720-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1720-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. <span data-ttu-id="e1720-156">Merhaba üzerinde **Zscaler Beta etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-156">On hello **Zscaler Beta Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="e1720-158">Merhaba oturum açma URL'si metin kutusuna, kullanıcıların toosign üzerinde tooyour tarafından Zscaler Beta uygulama kullanılan hello URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="e1720-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1720-159">Bu değeri hello ile tooupdate sahip gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="e1720-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e1720-160">Kişi [Zscaler Beta istemci destek ekibi](https://www.zscaler.com/company/contact) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="e1720-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="e1720-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1720-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. <span data-ttu-id="e1720-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1720-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1720-165">Merhaba üzerinde **Zscaler Beta yapılandırma** 'yi tıklatın **yapılandırma Zscaler Beta** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e1720-165">On hello **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1720-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e1720-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. <span data-ttu-id="e1720-168">Farklı web tarayıcısı penceresinde tooyour içinde Zscaler Beta şirket site yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="e1720-168">In a different web browser window, log in tooyour Zscaler Beta company site as an administrator.</span></span>

8. <span data-ttu-id="e1720-169">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="e1720-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="e1720-170">![Yönetim](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="e1720-170">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="e1720-171">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="e1720-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="e1720-172">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="e1720-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="e1720-173">Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="e1720-174">![Kimlik doğrulama](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="e1720-174">![Authentication](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="e1720-175">a.</span><span class="sxs-lookup"><span data-stu-id="e1720-175">a.</span></span> <span data-ttu-id="e1720-176">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="e1720-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="e1720-177">b.</span><span class="sxs-lookup"><span data-stu-id="e1720-177">b.</span></span> <span data-ttu-id="e1720-178">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="e1720-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="e1720-179">Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="e1720-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="e1720-180">![Çoklu oturum açma](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="e1720-180">![Single Sign-On](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="e1720-181">a.</span><span class="sxs-lookup"><span data-stu-id="e1720-181">a.</span></span> <span data-ttu-id="e1720-182">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e1720-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="e1720-183">b.</span><span class="sxs-lookup"><span data-stu-id="e1720-183">b.</span></span> <span data-ttu-id="e1720-184">Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="e1720-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="e1720-185">c.</span><span class="sxs-lookup"><span data-stu-id="e1720-185">c.</span></span> <span data-ttu-id="e1720-186">tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="e1720-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="e1720-187">d.</span><span class="sxs-lookup"><span data-stu-id="e1720-187">d.</span></span> <span data-ttu-id="e1720-188">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="e1720-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="e1720-189">Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="e1720-190">![Yönetim](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="e1720-190">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="e1720-191">a.</span><span class="sxs-lookup"><span data-stu-id="e1720-191">a.</span></span> <span data-ttu-id="e1720-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1720-192">Click **Save**.</span></span>

    <span data-ttu-id="e1720-193">b.</span><span class="sxs-lookup"><span data-stu-id="e1720-193">b.</span></span> <span data-ttu-id="e1720-194">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="e1720-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="e1720-195">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1720-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="e1720-196">Internet Explorer'da tooconfigure hello proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="e1720-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="e1720-197">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e1720-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="e1720-198">Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="e1720-199">![Internet Seçenekleri](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="e1720-199">![Internet Options](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="e1720-200">Merhaba tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e1720-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="e1720-201">![Bağlantıları](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="e1720-201">![Connections](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="e1720-202">Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="e1720-203">Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="e1720-204">![Proxy sunucusu](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="e1720-204">![Proxy server](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="e1720-205">a.</span><span class="sxs-lookup"><span data-stu-id="e1720-205">a.</span></span> <span data-ttu-id="e1720-206">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="e1720-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="e1720-207">b.</span><span class="sxs-lookup"><span data-stu-id="e1720-207">b.</span></span> <span data-ttu-id="e1720-208">Başlangıç adresi metin kutusuna yazın **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="e1720-208">In hello Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="e1720-209">c.</span><span class="sxs-lookup"><span data-stu-id="e1720-209">c.</span></span> <span data-ttu-id="e1720-210">Başlangıç bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="e1720-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="e1720-211">d.</span><span class="sxs-lookup"><span data-stu-id="e1720-211">d.</span></span> <span data-ttu-id="e1720-212">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="e1720-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="e1720-213">e.</span><span class="sxs-lookup"><span data-stu-id="e1720-213">e.</span></span> <span data-ttu-id="e1720-214">Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="e1720-215">Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="e1720-216">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1720-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1720-217">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e1720-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1720-218">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1720-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1720-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1720-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1720-220">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1720-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e1720-222">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1720-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1720-223">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1720-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1720-225">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1720-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1720-227">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1720-229">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1720-231">a.</span><span class="sxs-lookup"><span data-stu-id="e1720-231">a.</span></span> <span data-ttu-id="e1720-232">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1720-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1720-233">b.</span><span class="sxs-lookup"><span data-stu-id="e1720-233">b.</span></span> <span data-ttu-id="e1720-234">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e1720-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1720-235">c.</span><span class="sxs-lookup"><span data-stu-id="e1720-235">c.</span></span> <span data-ttu-id="e1720-236">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e1720-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e1720-237">d.</span><span class="sxs-lookup"><span data-stu-id="e1720-237">d.</span></span> <span data-ttu-id="e1720-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1720-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="e1720-239">Zscaler Beta test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1720-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="e1720-240">tooenable Azure AD kullanıcıların toolog tooZscaler Beta'da, sağlanan tooZscaler Beta olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1720-240">tooenable Azure AD users toolog in tooZscaler Beta, they must be provisioned tooZscaler Beta.</span></span> <span data-ttu-id="e1720-241">Zscaler Beta Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e1720-241">In hello case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="e1720-242">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="e1720-243">İçinde tooyour oturum **Zscaler Beta** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="e1720-243">Log in tooyour **Zscaler Beta** tenant.</span></span>

2. <span data-ttu-id="e1720-244">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="e1720-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="e1720-245">![Yönetim](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="e1720-245">![Administration](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="e1720-246">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="e1720-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="e1720-247">![Ekleme](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="e1720-247">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="e1720-248">Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e1720-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="e1720-249">![Ekleme](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="e1720-249">![Add](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="e1720-250">Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1720-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="e1720-251">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="e1720-251">![Add User](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="e1720-252">a.</span><span class="sxs-lookup"><span data-stu-id="e1720-252">a.</span></span> <span data-ttu-id="e1720-253">Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** geçerli bir Azure AD hesabının tooprovision istiyor.</span><span class="sxs-lookup"><span data-stu-id="e1720-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="e1720-254">b.</span><span class="sxs-lookup"><span data-stu-id="e1720-254">b.</span></span> <span data-ttu-id="e1720-255">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1720-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1720-256">API'leri, Azure AD kullanıcı hesapları Zscaler Beta tooprovision tarafından sağlanan veya herhangi diğer Zscaler Beta kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1720-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1720-257">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e1720-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e1720-258">Bu bölümde, erişim tooZscaler Beta vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1720-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Beta.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e1720-260">**tooassign Britta Simon tooZscaler Beta hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1720-260">**tooassign Britta Simon tooZscaler Beta, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1720-261">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1720-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1720-263">Merhaba uygulamalar listesinde **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="e1720-263">In hello applications list, select **Zscaler Beta**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. <span data-ttu-id="e1720-265">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1720-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e1720-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1720-267">Click **Add** button.</span></span> <span data-ttu-id="e1720-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e1720-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1720-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1720-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1720-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1720-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1720-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1720-273">Testing single sign-on</span></span>

<span data-ttu-id="e1720-274">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e1720-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1720-275">Zscaler Beta döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Zscaler Beta uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1720-275">When you click hello Zscaler Beta tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Beta application.</span></span>
<span data-ttu-id="e1720-276">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e1720-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1720-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1720-277">Additional resources</span></span>

* [<span data-ttu-id="e1720-278">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e1720-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1720-279">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1720-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

