---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler bir | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler bir arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 5179cb2cc54482334d574951a1ac64e722e5f578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="03adf-103">Öğretici: Azure Active Directory Tümleştirme ile Zscaler bir</span><span class="sxs-lookup"><span data-stu-id="03adf-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="03adf-104">Bu öğreticide, bilgi nasıl toointegrate Zscaler bir Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03adf-104">In this tutorial, you learn how toointegrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03adf-105">Zscaler bir Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="03adf-105">Integrating Zscaler One with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="03adf-106">Erişim tooZscaler biri olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="03adf-106">You can control in Azure AD who has access tooZscaler One</span></span>
- <span data-ttu-id="03adf-107">Kullanıcıların tooautomatically get açan tooZscaler biri (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="03adf-107">You can enable your users tooautomatically get signed-on tooZscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03adf-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="03adf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="03adf-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03adf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03adf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="03adf-110">Prerequisites</span></span>

<span data-ttu-id="03adf-111">tooconfigure Zscaler bir ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="03adf-111">tooconfigure Azure AD integration with Zscaler One, you need hello following items:</span></span>

- <span data-ttu-id="03adf-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="03adf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03adf-113">Bir Zscaler bir çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="03adf-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03adf-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="03adf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03adf-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="03adf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03adf-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="03adf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03adf-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03adf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03adf-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="03adf-118">Scenario description</span></span>
<span data-ttu-id="03adf-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="03adf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03adf-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="03adf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03adf-121">Zscaler bir hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="03adf-121">Adding Zscaler One from hello gallery</span></span>
2. <span data-ttu-id="03adf-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="03adf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-hello-gallery"></a><span data-ttu-id="03adf-123">Zscaler bir hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="03adf-123">Adding Zscaler One from hello gallery</span></span>
<span data-ttu-id="03adf-124">Azure AD'ye tooconfigure hello tümleştirme, Zscaler bir hello galeri tooyour yönetilen SaaS uygulamaları listesinden Zscaler bir tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="03adf-124">tooconfigure hello integration of Zscaler One into Azure AD, you need tooadd Zscaler One from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="03adf-125">**tooadd Zscaler bir hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="03adf-125">**tooadd Zscaler One from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="03adf-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="03adf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="03adf-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="03adf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03adf-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="03adf-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="03adf-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="03adf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="03adf-133">Merhaba arama kutusuna yazın **Zscaler bir**.</span><span class="sxs-lookup"><span data-stu-id="03adf-133">In hello search box, type **Zscaler One**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="03adf-135">Merhaba Sonuçlar panelinde seçin **Zscaler bir**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="03adf-135">In hello results panel, select **Zscaler One**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03adf-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="03adf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03adf-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Zscaler "Britta Simon" adlı bir test kullanıcı tabanlı bir test.</span><span class="sxs-lookup"><span data-stu-id="03adf-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="03adf-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler bir içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="03adf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler One is tooa user in Azure AD.</span></span> <span data-ttu-id="03adf-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Zscaler bir arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="03adf-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler One needs toobe established.</span></span>

<span data-ttu-id="03adf-141">Bir Zscaler içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="03adf-141">In Zscaler One, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="03adf-142">tooconfigure ve Zscaler bir ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="03adf-142">tooconfigure and test Azure AD single sign-on with Zscaler One, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="03adf-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="03adf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="03adf-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="03adf-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="03adf-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="03adf-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="03adf-146">**[Zscaler bir test kullanıcısı oluşturma](#creating-a-zscaler-one-test-user)**  -toohave Britta Simon Zscaler bağlantılı toohello Azure AD kullanıcı gösterimi olan bir içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="03adf-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - toohave a counterpart of Britta Simon in Zscaler One that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="03adf-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="03adf-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="03adf-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="03adf-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03adf-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="03adf-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03adf-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler bir uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="03adf-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="03adf-151">**tooconfigure Azure AD çoklu oturum açma ile Zscaler bir hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="03adf-151">**tooconfigure Azure AD single sign-on with Zscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="03adf-152">Hello hello üzerinde Azure portal'ın **Zscaler bir** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="03adf-152">In hello Azure portal, on hello **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="03adf-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="03adf-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="03adf-156">Merhaba üzerinde **Zscaler bir etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-156">On hello **Zscaler One Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="03adf-158">Merhaba oturum açma URL'si metin kutusuna, kullanıcıların toosign üzerinde tooyour tarafından Zscaler bir uygulama kullanılan hello URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="03adf-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="03adf-159">Bu değeri hello ile tooupdate sahip gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="03adf-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="03adf-160">Kişi [Zscaler bir istemci destek ekibi](https://www.zscaler.com/company/contact) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="03adf-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="03adf-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="03adf-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="03adf-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="03adf-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03adf-165">Merhaba üzerinde **Zscaler bir yapılandırma** 'yi tıklatın **Zscaler bir yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="03adf-165">On hello **Zscaler One Configuration** section, click **Configure Zscaler One** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="03adf-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="03adf-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="03adf-168">Farklı web tarayıcısı penceresinde tooyour Zscaler bir şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="03adf-168">In a different web browser window, log in tooyour Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="03adf-169">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="03adf-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="03adf-170">![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="03adf-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="03adf-171">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="03adf-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="03adf-172">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="03adf-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="03adf-173">Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="03adf-174">![Kimlik doğrulama](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="03adf-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="03adf-175">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-175">a.</span></span> <span data-ttu-id="03adf-176">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="03adf-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="03adf-177">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-177">b.</span></span> <span data-ttu-id="03adf-178">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="03adf-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="03adf-179">Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="03adf-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="03adf-180">![Çoklu oturum açma](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="03adf-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="03adf-181">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-181">a.</span></span> <span data-ttu-id="03adf-182">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="03adf-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="03adf-183">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-183">b.</span></span> <span data-ttu-id="03adf-184">Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="03adf-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="03adf-185">c.</span><span class="sxs-lookup"><span data-stu-id="03adf-185">c.</span></span> <span data-ttu-id="03adf-186">tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="03adf-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="03adf-187">d.</span><span class="sxs-lookup"><span data-stu-id="03adf-187">d.</span></span> <span data-ttu-id="03adf-188">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="03adf-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="03adf-189">Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="03adf-190">![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="03adf-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="03adf-191">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-191">a.</span></span> <span data-ttu-id="03adf-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="03adf-192">Click **Save**.</span></span>

    <span data-ttu-id="03adf-193">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-193">b.</span></span> <span data-ttu-id="03adf-194">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="03adf-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="03adf-195">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="03adf-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="03adf-196">Internet Explorer'da tooconfigure hello proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="03adf-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="03adf-197">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="03adf-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="03adf-198">Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="03adf-199">![Internet Seçenekleri](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="03adf-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="03adf-200">Merhaba tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="03adf-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="03adf-201">![Bağlantıları](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="03adf-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="03adf-202">Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="03adf-203">Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="03adf-204">![Proxy sunucusu](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="03adf-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="03adf-205">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-205">a.</span></span> <span data-ttu-id="03adf-206">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="03adf-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="03adf-207">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-207">b.</span></span> <span data-ttu-id="03adf-208">Başlangıç adresi metin kutusuna yazın **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="03adf-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="03adf-209">c.</span><span class="sxs-lookup"><span data-stu-id="03adf-209">c.</span></span> <span data-ttu-id="03adf-210">Başlangıç bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="03adf-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="03adf-211">d.</span><span class="sxs-lookup"><span data-stu-id="03adf-211">d.</span></span> <span data-ttu-id="03adf-212">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="03adf-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="03adf-213">e.</span><span class="sxs-lookup"><span data-stu-id="03adf-213">e.</span></span> <span data-ttu-id="03adf-214">Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="03adf-215">Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="03adf-216">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="03adf-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="03adf-217">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="03adf-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="03adf-218">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03adf-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03adf-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="03adf-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="03adf-220">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="03adf-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="03adf-222">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="03adf-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="03adf-223">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="03adf-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03adf-225">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="03adf-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03adf-227">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03adf-229">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03adf-231">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-231">a.</span></span> <span data-ttu-id="03adf-232">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03adf-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03adf-233">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-233">b.</span></span> <span data-ttu-id="03adf-234">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="03adf-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03adf-235">c.</span><span class="sxs-lookup"><span data-stu-id="03adf-235">c.</span></span> <span data-ttu-id="03adf-236">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="03adf-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="03adf-237">d.</span><span class="sxs-lookup"><span data-stu-id="03adf-237">d.</span></span> <span data-ttu-id="03adf-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="03adf-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="03adf-239">Zscaler bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="03adf-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="03adf-240">tooenable Azure AD kullanıcıların toolog tooZscaler biri, sağlanan tooZscaler biri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03adf-240">tooenable Azure AD users toolog in tooZscaler One, they must be provisioned tooZscaler One.</span></span> <span data-ttu-id="03adf-241">Merhaba Zscaler bir içinde sağlama el ile bir görev durumudur.</span><span class="sxs-lookup"><span data-stu-id="03adf-241">In hello case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="03adf-242">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="03adf-243">İçinde tooyour oturum **Zscaler bir** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="03adf-243">Log in tooyour **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="03adf-244">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="03adf-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="03adf-245">![Yönetim](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="03adf-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="03adf-246">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="03adf-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="03adf-247">![Ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="03adf-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="03adf-248">Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="03adf-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="03adf-249">![Ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="03adf-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="03adf-250">Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="03adf-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="03adf-251">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="03adf-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="03adf-252">a.</span><span class="sxs-lookup"><span data-stu-id="03adf-252">a.</span></span> <span data-ttu-id="03adf-253">Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** geçerli bir Azure AD hesabının tooprovision istiyor.</span><span class="sxs-lookup"><span data-stu-id="03adf-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="03adf-254">b.</span><span class="sxs-lookup"><span data-stu-id="03adf-254">b.</span></span> <span data-ttu-id="03adf-255">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="03adf-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="03adf-256">API'leri, Azure AD kullanıcı hesapları Zscaler bir tooprovision tarafından sağlanan veya herhangi diğer Zscaler bir kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03adf-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="03adf-257">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="03adf-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="03adf-258">Bu bölümde, erişim tooZscaler biri vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="03adf-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler One.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="03adf-260">**tooassign Britta Simon tooZscaler bir hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="03adf-260">**tooassign Britta Simon tooZscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="03adf-261">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="03adf-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="03adf-263">Merhaba uygulamalar listesinde **Zscaler bir**.</span><span class="sxs-lookup"><span data-stu-id="03adf-263">In hello applications list, select **Zscaler One**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="03adf-265">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="03adf-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="03adf-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="03adf-267">Click **Add** button.</span></span> <span data-ttu-id="03adf-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="03adf-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="03adf-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="03adf-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03adf-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="03adf-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03adf-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="03adf-273">Testing single sign-on</span></span>

<span data-ttu-id="03adf-274">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="03adf-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="03adf-275">Merhaba Zscaler bir hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zscaler bir uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03adf-275">When you click hello Zscaler One tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler One application.</span></span>
<span data-ttu-id="03adf-276">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03adf-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03adf-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="03adf-277">Additional resources</span></span>

* [<span data-ttu-id="03adf-278">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="03adf-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03adf-279">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="03adf-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

