---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2894534f5d6711fd6af618cd699fa5837b5bf26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="38aef-103">Öğretici: Azure Active Directory Tümleştirme Zscaler ile</span><span class="sxs-lookup"><span data-stu-id="38aef-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="38aef-104">Bu öğreticide, bilgi nasıl toointegrate Zscaler Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38aef-104">In this tutorial, you learn how toointegrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38aef-105">Zscaler Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="38aef-105">Integrating Zscaler with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="38aef-106">Erişim tooZscaler sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="38aef-106">You can control in Azure AD who has access tooZscaler</span></span>
- <span data-ttu-id="38aef-107">Kullanıcıların tooautomatically get açan tooZscaler (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="38aef-107">You can enable your users tooautomatically get signed-on tooZscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38aef-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="38aef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="38aef-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38aef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38aef-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="38aef-110">Prerequisites</span></span>

<span data-ttu-id="38aef-111">tooconfigure Zscaler ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="38aef-111">tooconfigure Azure AD integration with Zscaler, you need hello following items:</span></span>

- <span data-ttu-id="38aef-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="38aef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38aef-113">Bir Zscaler çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="38aef-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38aef-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="38aef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38aef-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="38aef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38aef-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="38aef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38aef-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38aef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38aef-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="38aef-118">Scenario description</span></span>
<span data-ttu-id="38aef-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="38aef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38aef-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="38aef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38aef-121">Merhaba Galerisi'nden Zscaler ekleme</span><span class="sxs-lookup"><span data-stu-id="38aef-121">Adding Zscaler from hello gallery</span></span>
2. <span data-ttu-id="38aef-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="38aef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-hello-gallery"></a><span data-ttu-id="38aef-123">Merhaba Galerisi'nden Zscaler ekleme</span><span class="sxs-lookup"><span data-stu-id="38aef-123">Adding Zscaler from hello gallery</span></span>
<span data-ttu-id="38aef-124">Azure AD'ye tooconfigure hello tümleştirme Zscaler, tooadd Zscaler hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="38aef-124">tooconfigure hello integration of Zscaler into Azure AD, you need tooadd Zscaler from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="38aef-125">**tooadd Zscaler hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="38aef-125">**tooadd Zscaler from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38aef-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="38aef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38aef-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="38aef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="38aef-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="38aef-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="38aef-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38aef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="38aef-133">Merhaba arama kutusuna yazın **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="38aef-133">In hello search box, type **Zscaler**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="38aef-135">Merhaba Sonuçlar panelinde seçin **Zscaler**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="38aef-135">In hello results panel, select **Zscaler**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38aef-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="38aef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38aef-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zscaler sınayın.</span><span class="sxs-lookup"><span data-stu-id="38aef-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38aef-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="38aef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler is tooa user in Azure AD.</span></span> <span data-ttu-id="38aef-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zscaler hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="38aef-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler needs toobe established.</span></span>

<span data-ttu-id="38aef-141">Merhaba hello değeri Zscaler içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="38aef-141">In Zscaler, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="38aef-142">tooconfigure ve Zscaler ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="38aef-142">tooconfigure and test Azure AD single sign-on with Zscaler, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38aef-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="38aef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38aef-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="38aef-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="38aef-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="38aef-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="38aef-146">**[Zscaler test kullanıcısı oluşturma](#creating-a-zscaler-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zscaler içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="38aef-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - toohave a counterpart of Britta Simon in Zscaler that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="38aef-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="38aef-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="38aef-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="38aef-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38aef-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="38aef-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38aef-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="38aef-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="38aef-151">**tooconfigure Azure AD çoklu oturum açma ile Zscaler, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="38aef-151">**tooconfigure Azure AD single sign-on with Zscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="38aef-152">Hello hello üzerinde Azure portal'ın **Zscaler** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="38aef-152">In hello Azure portal, on hello **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="38aef-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="38aef-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="38aef-156">Merhaba üzerinde **Zscaler etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-156">On hello **Zscaler Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="38aef-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="38aef-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38aef-159">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="38aef-159">This value is not real.</span></span> <span data-ttu-id="38aef-160">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="38aef-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="38aef-161">Kişi [Zscaler istemci destek ekibi](https://www.zscaler.com/company/contact) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="38aef-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="38aef-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="38aef-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="38aef-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38aef-164">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38aef-166">Merhaba üzerinde **Zscaler yapılandırma** 'yi tıklatın **yapılandırma Zscaler** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="38aef-166">On hello **Zscaler Configuration** section, click **Configure Zscaler** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="38aef-167">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="38aef-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="38aef-169">Farklı web tarayıcısı penceresinde tooyour ZScaler şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="38aef-169">In a different web browser window, log in tooyour ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="38aef-170">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="38aef-170">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="38aef-171">![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="38aef-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="38aef-172">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="38aef-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="38aef-173">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="38aef-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="38aef-174">Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-174">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="38aef-175">![Kimlik doğrulama](./media/active-directory-saas-zscaler-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="38aef-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="38aef-176">a.</span><span class="sxs-lookup"><span data-stu-id="38aef-176">a.</span></span> <span data-ttu-id="38aef-177">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="38aef-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="38aef-178">b.</span><span class="sxs-lookup"><span data-stu-id="38aef-178">b.</span></span> <span data-ttu-id="38aef-179">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="38aef-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="38aef-180">Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="38aef-180">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="38aef-181">![Çoklu oturum açma](./media/active-directory-saas-zscaler-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="38aef-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="38aef-182">a.</span><span class="sxs-lookup"><span data-stu-id="38aef-182">a.</span></span> <span data-ttu-id="38aef-183">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="38aef-183">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="38aef-184">b.</span><span class="sxs-lookup"><span data-stu-id="38aef-184">b.</span></span> <span data-ttu-id="38aef-185">Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="38aef-185">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="38aef-186">c.</span><span class="sxs-lookup"><span data-stu-id="38aef-186">c.</span></span> <span data-ttu-id="38aef-187">tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="38aef-187">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="38aef-188">d.</span><span class="sxs-lookup"><span data-stu-id="38aef-188">d.</span></span> <span data-ttu-id="38aef-189">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="38aef-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="38aef-190">Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-190">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="38aef-191">![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="38aef-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="38aef-192">a.</span><span class="sxs-lookup"><span data-stu-id="38aef-192">a.</span></span> <span data-ttu-id="38aef-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38aef-193">Click **Save**.</span></span>

    <span data-ttu-id="38aef-194">b.</span><span class="sxs-lookup"><span data-stu-id="38aef-194">b.</span></span> <span data-ttu-id="38aef-195">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="38aef-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="38aef-196">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="38aef-196">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="38aef-197">Internet Explorer'da tooconfigure hello proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="38aef-197">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="38aef-198">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="38aef-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="38aef-199">Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-199">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="38aef-200">![Internet Seçenekleri](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="38aef-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="38aef-201">Merhaba tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="38aef-201">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="38aef-202">![Bağlantıları](./media/active-directory-saas-zscaler-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="38aef-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="38aef-203">Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-203">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="38aef-204">Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-204">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="38aef-205">![Proxy sunucusu](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="38aef-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="38aef-206">a.</span><span class="sxs-lookup"><span data-stu-id="38aef-206">a.</span></span> <span data-ttu-id="38aef-207">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="38aef-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="38aef-208">b.</span><span class="sxs-lookup"><span data-stu-id="38aef-208">b.</span></span> <span data-ttu-id="38aef-209">Başlangıç adresi metin kutusuna yazın **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="38aef-209">In hello Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="38aef-210">c.</span><span class="sxs-lookup"><span data-stu-id="38aef-210">c.</span></span> <span data-ttu-id="38aef-211">Başlangıç bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="38aef-211">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="38aef-212">d.</span><span class="sxs-lookup"><span data-stu-id="38aef-212">d.</span></span> <span data-ttu-id="38aef-213">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="38aef-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="38aef-214">e.</span><span class="sxs-lookup"><span data-stu-id="38aef-214">e.</span></span> <span data-ttu-id="38aef-215">Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-215">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="38aef-216">Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-216">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="38aef-217">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="38aef-217">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="38aef-218">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="38aef-218">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="38aef-219">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38aef-219">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38aef-220">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="38aef-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="38aef-221">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="38aef-221">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="38aef-223">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="38aef-223">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38aef-224">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="38aef-224">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38aef-226">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="38aef-226">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38aef-228">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-228">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38aef-230">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-230">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38aef-232">a.</span><span class="sxs-lookup"><span data-stu-id="38aef-232">a.</span></span> <span data-ttu-id="38aef-233">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38aef-233">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38aef-234">b.</span><span class="sxs-lookup"><span data-stu-id="38aef-234">b.</span></span> <span data-ttu-id="38aef-235">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="38aef-235">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38aef-236">c.</span><span class="sxs-lookup"><span data-stu-id="38aef-236">c.</span></span> <span data-ttu-id="38aef-237">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="38aef-237">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="38aef-238">d.</span><span class="sxs-lookup"><span data-stu-id="38aef-238">d.</span></span> <span data-ttu-id="38aef-239">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38aef-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="38aef-240">Zscaler test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="38aef-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="38aef-241">tooenable Azure AD kullanıcıların toolog tooZScaler içinde sağlanan tooZScaler olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="38aef-241">tooenable Azure AD users toolog in tooZScaler, they must be provisioned tooZScaler.</span></span>  
<span data-ttu-id="38aef-242">ZScaler Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="38aef-242">In hello case of ZScaler, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="38aef-243">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-243">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="38aef-244">İçinde tooyour oturum **Zscaler** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="38aef-244">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="38aef-245">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="38aef-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="38aef-246">![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="38aef-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="38aef-247">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="38aef-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="38aef-248">![Ekleme](./media/active-directory-saas-zscaler-tutorial/ic781036.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="38aef-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="38aef-249">Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="38aef-249">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="38aef-250">![Ekleme](./media/active-directory-saas-zscaler-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="38aef-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="38aef-251">Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38aef-251">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="38aef-252">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="38aef-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="38aef-253">a.</span><span class="sxs-lookup"><span data-stu-id="38aef-253">a.</span></span> <span data-ttu-id="38aef-254">Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** tooprovision istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="38aef-254">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="38aef-255">b.</span><span class="sxs-lookup"><span data-stu-id="38aef-255">b.</span></span> <span data-ttu-id="38aef-256">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38aef-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="38aef-257">API AAD kullanıcı hesaplarının ZScaler tooprovision tarafından sağlanan veya herhangi diğer ZScaler kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38aef-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38aef-258">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="38aef-258">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="38aef-259">Bu bölümde, erişim tooZscaler vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="38aef-259">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="38aef-261">**tooassign Britta Simon tooZscaler hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="38aef-261">**tooassign Britta Simon tooZscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="38aef-262">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="38aef-262">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="38aef-264">Merhaba uygulamalar listesinde **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="38aef-264">In hello applications list, select **Zscaler**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="38aef-266">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="38aef-266">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="38aef-268">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38aef-268">Click **Add** button.</span></span> <span data-ttu-id="38aef-269">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="38aef-271">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="38aef-271">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="38aef-272">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38aef-273">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="38aef-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38aef-274">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="38aef-274">Testing single sign-on</span></span>

<span data-ttu-id="38aef-275">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="38aef-275">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="38aef-276">Merhaba Zscaler hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Zscaler uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="38aef-276">When you click hello Zscaler tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler application.</span></span>
<span data-ttu-id="38aef-277">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38aef-277">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38aef-278">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="38aef-278">Additional resources</span></span>

* [<span data-ttu-id="38aef-279">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="38aef-279">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38aef-280">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="38aef-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

