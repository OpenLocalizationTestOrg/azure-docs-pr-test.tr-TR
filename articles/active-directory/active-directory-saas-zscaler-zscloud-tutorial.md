---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler ZSCloud | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Zscaler ZSCloud arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="48dc1-103">Öğretici: Azure Active Directory Tümleştirme Zscaler ZSCloud ile</span><span class="sxs-lookup"><span data-stu-id="48dc1-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="48dc1-104">Bu öğreticide, bilgi nasıl toointegrate Zscaler ZSCloud Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48dc1-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48dc1-105">Zscaler ZSCloud Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="48dc1-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="48dc1-106">Erişim tooZscaler ZSCloud sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="48dc1-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="48dc1-107">Kullanıcıların tooautomatically get açan tooZscaler ZSCloud (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="48dc1-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48dc1-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="48dc1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="48dc1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48dc1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48dc1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="48dc1-110">Prerequisites</span></span>

<span data-ttu-id="48dc1-111">tooconfigure Zscaler ZSCloud ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="48dc1-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="48dc1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="48dc1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48dc1-113">Bir Zscaler ZSCloud çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="48dc1-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48dc1-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="48dc1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48dc1-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="48dc1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48dc1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="48dc1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48dc1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48dc1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48dc1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="48dc1-118">Scenario description</span></span>
<span data-ttu-id="48dc1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="48dc1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48dc1-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="48dc1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48dc1-121">Merhaba Galerisi'nden Zscaler ZSCloud ekleme</span><span class="sxs-lookup"><span data-stu-id="48dc1-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="48dc1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="48dc1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="48dc1-123">Merhaba Galerisi'nden Zscaler ZSCloud ekleme</span><span class="sxs-lookup"><span data-stu-id="48dc1-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="48dc1-124">Azure AD'ye tooconfigure hello tümleştirme Zscaler ZSCloud, tooadd Zscaler ZSCloud hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dc1-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="48dc1-125">**tooadd Zscaler ZSCloud hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48dc1-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="48dc1-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48dc1-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="48dc1-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="48dc1-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="48dc1-133">Merhaba arama kutusuna yazın **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="48dc1-135">Merhaba Sonuçlar panelinde seçin **Zscaler ZSCloud**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="48dc1-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48dc1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="48dc1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48dc1-138">Bu bölümde, yapılandırmanız ve Zscaler ZSCloud ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="48dc1-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="48dc1-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Zscaler ZSCloud içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dc1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="48dc1-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Zscaler ZSCloud hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dc1-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="48dc1-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Zscaler ZSCloud içinde.</span><span class="sxs-lookup"><span data-stu-id="48dc1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="48dc1-142">tooconfigure ve Zscaler ZSCloud ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="48dc1-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="48dc1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="48dc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="48dc1-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  -tooconfigure hello Internet Explorer proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="48dc1-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="48dc1-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="48dc1-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48dc1-146">**[Zscaler ZSCloud test kullanıcısı oluşturma](#creating-a-zscaler-zscloud-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Zscaler ZSCloud içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="48dc1-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="48dc1-147">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="48dc1-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48dc1-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="48dc1-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48dc1-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48dc1-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48dc1-150">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Zscaler ZSCloud uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="48dc1-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="48dc1-151">**tooconfigure Azure AD çoklu oturum açma Zscaler ZSCloud ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48dc1-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="48dc1-152">Hello hello üzerinde Azure portal'ın **Zscaler ZSCloud** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="48dc1-154">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="48dc1-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="48dc1-156">Merhaba üzerinde **Zscaler ZSCloud etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="48dc1-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello URL, kullanıcıların toosign üzerinde tooyour tarafından ZScaler ZSCloud uygulama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48dc1-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="48dc1-159">Bu değeri hello ile tooupdate sahip gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="48dc1-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="48dc1-160">Kişi [Zscaler ZSCloud istemci destek ekibi](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="48dc1-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="48dc1-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="48dc1-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="48dc1-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48dc1-165">Merhaba üzerinde **Zscaler ZSCloud yapılandırma** 'yi tıklatın **yapılandırma Zscaler ZSCloud** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="48dc1-166">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="48dc1-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="48dc1-168">Farklı web tarayıcısı penceresinde içinde tooyour ZScaler ZSCloud şirket site yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="48dc1-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="48dc1-169">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="48dc1-170">![Yönetim](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="48dc1-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="48dc1-171">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="48dc1-172">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="48dc1-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="48dc1-173">Merhaba, **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="48dc1-174">![Kimlik doğrulama](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="48dc1-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="48dc1-175">a.</span><span class="sxs-lookup"><span data-stu-id="48dc1-175">a.</span></span> <span data-ttu-id="48dc1-176">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="48dc1-177">b.</span><span class="sxs-lookup"><span data-stu-id="48dc1-177">b.</span></span> <span data-ttu-id="48dc1-178">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="48dc1-179">Merhaba üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfa hello aşağıdaki adımları gerçekleştirin ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="48dc1-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="48dc1-180">![Çoklu oturum açma](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="48dc1-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="48dc1-181">a.</span><span class="sxs-lookup"><span data-stu-id="48dc1-181">a.</span></span> <span data-ttu-id="48dc1-182">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello değerine **URL hello SAML Portal toowhich kullanıcıların kimlik doğrulaması için gönderilen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="48dc1-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="48dc1-183">b.</span><span class="sxs-lookup"><span data-stu-id="48dc1-183">b.</span></span> <span data-ttu-id="48dc1-184">Merhaba, **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="48dc1-185">c.</span><span class="sxs-lookup"><span data-stu-id="48dc1-185">c.</span></span> <span data-ttu-id="48dc1-186">tooupload indirilen sertifikanızı tıklatın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="48dc1-187">d.</span><span class="sxs-lookup"><span data-stu-id="48dc1-187">d.</span></span> <span data-ttu-id="48dc1-188">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="48dc1-189">Merhaba üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="48dc1-190">![Yönetim](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="48dc1-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="48dc1-191">a.</span><span class="sxs-lookup"><span data-stu-id="48dc1-191">a.</span></span> <span data-ttu-id="48dc1-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48dc1-192">Click **Save**.</span></span>

    <span data-ttu-id="48dc1-193">b.</span><span class="sxs-lookup"><span data-stu-id="48dc1-193">b.</span></span> <span data-ttu-id="48dc1-194">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="48dc1-195">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48dc1-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="48dc1-196">Internet Explorer'da tooconfigure hello proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="48dc1-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="48dc1-197">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="48dc1-198">Seçin **Internet Seçenekleri** hello gelen **Araçları** açık hello menüsüne **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="48dc1-199">![Internet Seçenekleri](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="48dc1-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="48dc1-200">Merhaba tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="48dc1-201">![Bağlantıları](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="48dc1-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="48dc1-202">Tıklatın **LAN Ayarları** tooopen hello **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="48dc1-203">Hello Proxy sunucu bölümüne, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="48dc1-204">![Proxy sunucusu](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="48dc1-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="48dc1-205">a.</span><span class="sxs-lookup"><span data-stu-id="48dc1-205">a.</span></span> <span data-ttu-id="48dc1-206">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="48dc1-207">b.</span><span class="sxs-lookup"><span data-stu-id="48dc1-207">b.</span></span> <span data-ttu-id="48dc1-208">Başlangıç adresi metin kutusuna yazın **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="48dc1-209">c.</span><span class="sxs-lookup"><span data-stu-id="48dc1-209">c.</span></span> <span data-ttu-id="48dc1-210">Başlangıç bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="48dc1-211">d.</span><span class="sxs-lookup"><span data-stu-id="48dc1-211">d.</span></span> <span data-ttu-id="48dc1-212">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="48dc1-213">e.</span><span class="sxs-lookup"><span data-stu-id="48dc1-213">e.</span></span> <span data-ttu-id="48dc1-214">Tıklatın **Tamam** tooclose hello **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="48dc1-215">Tıklatın **Tamam** tooclose hello **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48dc1-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48dc1-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="48dc1-217">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="48dc1-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="48dc1-219">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48dc1-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="48dc1-220">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48dc1-222">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48dc1-224">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48dc1-226">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48dc1-228">a.</span><span class="sxs-lookup"><span data-stu-id="48dc1-228">a.</span></span> <span data-ttu-id="48dc1-229">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48dc1-230">b.</span><span class="sxs-lookup"><span data-stu-id="48dc1-230">b.</span></span> <span data-ttu-id="48dc1-231">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="48dc1-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48dc1-232">c.</span><span class="sxs-lookup"><span data-stu-id="48dc1-232">c.</span></span> <span data-ttu-id="48dc1-233">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="48dc1-234">d.</span><span class="sxs-lookup"><span data-stu-id="48dc1-234">d.</span></span> <span data-ttu-id="48dc1-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48dc1-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="48dc1-236">Zscaler ZSCloud test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="48dc1-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="48dc1-237">tooenable Azure AD kullanıcıların toolog tooZScaler ZSCloud, sağlanan tooZScaler ZSCloud olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dc1-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="48dc1-238">ZScaler ZSCloud Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="48dc1-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="48dc1-239">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="48dc1-240">İçinde tooyour oturum **Zscaler** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="48dc1-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="48dc1-241">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="48dc1-242">![Yönetim](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="48dc1-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="48dc1-243">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="48dc1-244">![Ekleme](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="48dc1-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="48dc1-245">Merhaba, **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="48dc1-246">![Ekleme](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="48dc1-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="48dc1-247">Hello kullanıcı ekle bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="48dc1-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="48dc1-248">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="48dc1-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="48dc1-249">a.</span><span class="sxs-lookup"><span data-stu-id="48dc1-249">a.</span></span> <span data-ttu-id="48dc1-250">Türü hello **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları**ve hello **departmanı** tooprovision istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="48dc1-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="48dc1-251">b.</span><span class="sxs-lookup"><span data-stu-id="48dc1-251">b.</span></span> <span data-ttu-id="48dc1-252">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48dc1-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="48dc1-253">API AAD kullanıcı hesaplarının ZScaler ZSCloud tooprovision tarafından sağlanan veya herhangi diğer ZScaler ZSCloud kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48dc1-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="48dc1-254">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="48dc1-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="48dc1-255">Bu bölümde, erişim tooZscaler ZSCloud vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="48dc1-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="48dc1-257">**tooassign Britta Simon tooZscaler ZSCloud, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="48dc1-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="48dc1-258">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="48dc1-260">Merhaba uygulamalar listesinde **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="48dc1-262">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="48dc1-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="48dc1-264">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="48dc1-264">Click **Add** button.</span></span> <span data-ttu-id="48dc1-265">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="48dc1-267">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="48dc1-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="48dc1-268">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48dc1-269">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="48dc1-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48dc1-270">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="48dc1-270">Testing single sign-on</span></span>

<span data-ttu-id="48dc1-271">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="48dc1-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="48dc1-272">Zscaler ZSCloud döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Zscaler ZSCloud uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48dc1-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="48dc1-273">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48dc1-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="48dc1-274">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="48dc1-274">Additional resources</span></span>

* [<span data-ttu-id="48dc1-275">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="48dc1-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48dc1-276">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="48dc1-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

