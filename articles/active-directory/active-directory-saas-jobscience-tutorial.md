---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jobscience | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jobscience arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="4d5bf-103">Öğretici: Azure Active Directory Tümleştirme Jobscience ile</span><span class="sxs-lookup"><span data-stu-id="4d5bf-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="4d5bf-104">Bu öğreticide, bilgi nasıl toointegrate Jobscience Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d5bf-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d5bf-105">Jobscience Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d5bf-106">Erişim tooJobscience sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4d5bf-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="4d5bf-107">Kullanıcıların tooautomatically get açan tooJobscience (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4d5bf-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d5bf-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4d5bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d5bf-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d5bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d5bf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4d5bf-110">Prerequisites</span></span>

<span data-ttu-id="4d5bf-111">tooconfigure Jobscience ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="4d5bf-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4d5bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d5bf-113">Bir Jobscience çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4d5bf-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d5bf-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d5bf-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d5bf-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d5bf-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d5bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d5bf-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4d5bf-118">Scenario description</span></span>
<span data-ttu-id="4d5bf-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d5bf-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d5bf-121">Merhaba Galerisi'nden Jobscience ekleme</span><span class="sxs-lookup"><span data-stu-id="4d5bf-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="4d5bf-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4d5bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="4d5bf-123">Merhaba Galerisi'nden Jobscience ekleme</span><span class="sxs-lookup"><span data-stu-id="4d5bf-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="4d5bf-124">Azure AD'ye tooconfigure hello tümleştirme Jobscience, tooadd Jobscience hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d5bf-125">**tooadd Jobscience hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d5bf-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d5bf-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d5bf-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d5bf-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4d5bf-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4d5bf-133">Merhaba arama kutusuna yazın **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-133">In hello search box, type **Jobscience**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="4d5bf-135">Merhaba Sonuçlar panelinde seçin **Jobscience**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d5bf-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4d5bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d5bf-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Jobscience ile test etme</span><span class="sxs-lookup"><span data-stu-id="4d5bf-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d5bf-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Jobscience içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="4d5bf-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Jobscience hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="4d5bf-141">Merhaba hello değeri Jobscience içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d5bf-142">tooconfigure ve Jobscience ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d5bf-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d5bf-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d5bf-145">**[Jobscience test kullanıcısı oluşturma](#creating-a-jobscience-test-user) ** -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Jobscience içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d5bf-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d5bf-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d5bf-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d5bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d5bf-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Jobscience uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="4d5bf-150">**tooconfigure Azure AD çoklu oturum açma ile Jobscience, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d5bf-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d5bf-151">Hello hello üzerinde Azure portal'ın **Jobscience** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4d5bf-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="4d5bf-155">Merhaba üzerinde **Jobscience etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="4d5bf-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4d5bf-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4d5bf-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-158">This value is not real.</span></span> <span data-ttu-id="4d5bf-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4d5bf-160">Bu değer alma [Jobscience istemci destek ekibi](https://www.jobscience.com/support) veya hello SSO profilinden hello öğreticinin ilerleyen bölümlerinde açıklanan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="4d5bf-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="4d5bf-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4d5bf-165">Merhaba üzerinde **Jobscience yapılandırma** 'yi tıklatın **yapılandırma Jobscience** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4d5bf-166">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4d5bf-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="4d5bf-168">İçinde tooyour Jobscience şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="4d5bf-169">Çok Git**Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="4d5bf-170">![Kurulum](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="4d5bf-171">Merhaba de hello sol gezinti bölmesindeki **Yönet** 'yi tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello ** Etki alanım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="4d5bf-172">![Etki alanım](./media/active-directory-saas-jobscience-tutorial/ic767825.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="4d5bf-173">etki alanınızın doğru olarak ayarlanmış tooverify alanında olduğundan emin olun "**4 adım dağıtılan tooUsers**" ve gözden geçirin, "**My etki alanı ayarları**".</span><span class="sxs-lookup"><span data-stu-id="4d5bf-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="4d5bf-174">![Etki alanı dağıtıldı tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "etki alanı dağıtılan tooUser")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="4d5bf-175">Merhaba Jobscience şirket sitesinde tıklatın **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="4d5bf-176">![Güvenlik denetimleri](./media/active-directory-saas-jobscience-tutorial/ic784364.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="4d5bf-177">Merhaba, **çoklu oturum açma ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="4d5bf-178">![Çoklu oturum açma ayarları](./media/active-directory-saas-jobscience-tutorial/ic781026.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="4d5bf-179">a.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-179">a.</span></span> <span data-ttu-id="4d5bf-180">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="4d5bf-181">b.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-181">b.</span></span> <span data-ttu-id="4d5bf-182">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-182">Click **New**.</span></span>

13. <span data-ttu-id="4d5bf-183">Merhaba üzerinde **SAML çoklu oturum açma ayarını Düzenle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="4d5bf-184">![Oturum açma SAML tek ayar](./media/active-directory-saas-jobscience-tutorial/ic784365.png "oturum açma SAML tek ayar")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="4d5bf-185">a.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-185">a.</span></span> <span data-ttu-id="4d5bf-186">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="4d5bf-187">b.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-187">b.</span></span> <span data-ttu-id="4d5bf-188">İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4d5bf-189">c.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-189">c.</span></span> <span data-ttu-id="4d5bf-190">Merhaba, **varlık kimliği** metin kutusuna, türü`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="4d5bf-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="4d5bf-191">d.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-191">d.</span></span> <span data-ttu-id="4d5bf-192">Tıklatın **Gözat** tooupload Azure AD sertifikanızı.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="4d5bf-193">e.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-193">e.</span></span> <span data-ttu-id="4d5bf-194">Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="4d5bf-195">f.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-195">f.</span></span> <span data-ttu-id="4d5bf-196">Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentfier öğesinde hello konu deyimi**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="4d5bf-197">g.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-197">g.</span></span> <span data-ttu-id="4d5bf-198">İçinde **kimlik sağlayıcısı oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4d5bf-199">h.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-199">h.</span></span> <span data-ttu-id="4d5bf-200">İçinde **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4d5bf-201">ı.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-201">i.</span></span> <span data-ttu-id="4d5bf-202">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-202">Click **Save**.</span></span>

14. <span data-ttu-id="4d5bf-203">Merhaba de hello sol gezinti bölmesindeki **Yönet** 'yi tıklatın **etki alanı yönetimi** tooexpand hello ilgili bölümü ve ardından **My etki alanı** tooopen hello ** Etki alanım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="4d5bf-204">![Etki alanım](./media/active-directory-saas-jobscience-tutorial/ic767825.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="4d5bf-205">Merhaba üzerinde **My etki alanı** sayfasında hello **oturum açma sayfası markalama** 'yi tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="4d5bf-206">![Oturum açma sayfası markalama](./media/active-directory-saas-jobscience-tutorial/ic767826.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="4d5bf-207">Merhaba üzerinde **oturum açma sayfası markalama** sayfasında hello **kimlik doğrulama hizmeti** bölümü, hello adını, **SAML SSO ayarları** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="4d5bf-208">Seçin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="4d5bf-209">![Oturum açma sayfası markalama](./media/active-directory-saas-jobscience-tutorial/ic784366.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="4d5bf-210">tooget hello SP tarafından başlatılan çoklu oturum açma hello üzerinde oturum açma URL'si tıklatıldığında **çoklu oturum açma ayarları** hello içinde **güvenlik denetimleri** menü bölümü.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="4d5bf-211">![Güvenlik denetimleri](./media/active-directory-saas-jobscience-tutorial/ic784368.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="4d5bf-212">Merhaba Yukarıdaki adımda oluşturduğunuz hello SSO profiline tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="4d5bf-213">Bu sayfa hello çoklu oturum açma URL'SİNDE şirketiniz için gösterir (örneğin, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="4d5bf-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="4d5bf-214">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4d5bf-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d5bf-215">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d5bf-216">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d5bf-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d5bf-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d5bf-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d5bf-218">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4d5bf-220">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d5bf-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d5bf-221">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d5bf-223">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d5bf-225">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d5bf-227">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d5bf-229">a.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-229">a.</span></span> <span data-ttu-id="4d5bf-230">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d5bf-231">b.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-231">b.</span></span> <span data-ttu-id="4d5bf-232">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d5bf-233">c.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-233">c.</span></span> <span data-ttu-id="4d5bf-234">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d5bf-235">d.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-235">d.</span></span> <span data-ttu-id="4d5bf-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="4d5bf-237">Jobscience test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d5bf-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="4d5bf-238">TooJobscience içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Jobscience sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="4d5bf-239">Jobscience Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="4d5bf-240">API, kullanıcı hesaplarını Jobscience tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer Jobscience kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="4d5bf-241">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d5bf-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d5bf-242">İçinde tooyour oturum **Jobscience** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="4d5bf-243">TooSetup gidin.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="4d5bf-244">![Kurulum](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="4d5bf-245">Çok Git**kullanıcıları yönetme \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="4d5bf-246">![Kullanıcıların](./media/active-directory-saas-jobscience-tutorial/ic784369.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="4d5bf-247">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-247">Click **New User**.</span></span>
   
   <span data-ttu-id="4d5bf-248">![Tüm kullanıcılar](./media/active-directory-saas-jobscience-tutorial/ic784370.png "tüm kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="4d5bf-249">Merhaba üzerinde **kullanıcı düzenleme** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d5bf-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="4d5bf-250">![Kullanıcı düzenleme](./media/active-directory-saas-jobscience-tutorial/ic784371.png "kullanıcı düzenleme")</span><span class="sxs-lookup"><span data-stu-id="4d5bf-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="4d5bf-251">a.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-251">a.</span></span> <span data-ttu-id="4d5bf-252">Merhaba, **ad** metin kutusuna, Britta gibi hello kullanıcının ilk adını yazın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="4d5bf-253">b.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-253">b.</span></span> <span data-ttu-id="4d5bf-254">Merhaba, **Soyadı** metin kutusuna, Simon gibi hello kullanıcının soyadını yazın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="4d5bf-255">c.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-255">c.</span></span> <span data-ttu-id="4d5bf-256">Merhaba, **diğer** metin kutusuna, hello kullanıcı brittas gibi diğer adını yazın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="4d5bf-257">d.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-257">d.</span></span> <span data-ttu-id="4d5bf-258">Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="4d5bf-259">e.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-259">e.</span></span> <span data-ttu-id="4d5bf-260">Merhaba, **kullanıcı adı** metin kutusuna, türü kullanıcının kullanıcı adını ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="4d5bf-261">f.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-261">f.</span></span> <span data-ttu-id="4d5bf-262">Merhaba, **takma ad** metin kutusu, kullanıcı Simon gibi takma adını yazın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="4d5bf-263">g.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-263">g.</span></span> <span data-ttu-id="4d5bf-264">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="4d5bf-265">Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4d5bf-266">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4d5bf-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4d5bf-267">Bu bölümde, erişim tooJobscience vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4d5bf-269">**tooassign Britta Simon tooJobscience hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d5bf-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d5bf-270">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4d5bf-272">Merhaba uygulamalar listesinde **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-272">In hello applications list, select **Jobscience**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="4d5bf-274">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4d5bf-276">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-276">Click **Add** button.</span></span> <span data-ttu-id="4d5bf-277">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4d5bf-279">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d5bf-280">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d5bf-281">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d5bf-282">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4d5bf-282">Testing single sign-on</span></span>

<span data-ttu-id="4d5bf-283">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4d5bf-284">Merhaba Jobscience hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Jobscience uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d5bf-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="4d5bf-285">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d5bf-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d5bf-286">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4d5bf-286">Additional resources</span></span>

* [<span data-ttu-id="4d5bf-287">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4d5bf-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d5bf-288">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4d5bf-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

