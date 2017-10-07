---
title: "Öğretici: Azure Active Directory Tümleştirme ile ITRP | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ITRP arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="317f3-103">Öğretici: Azure Active Directory Tümleştirme ITRP ile</span><span class="sxs-lookup"><span data-stu-id="317f3-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="317f3-104">Bu öğreticide, bilgi nasıl toointegrate ITRP Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="317f3-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="317f3-105">ITRP Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="317f3-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="317f3-106">Erişim tooITRP sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="317f3-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="317f3-107">Kullanıcıların tooautomatically get açan tooITRP (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="317f3-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="317f3-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="317f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="317f3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="317f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="317f3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="317f3-110">Prerequisites</span></span>

<span data-ttu-id="317f3-111">tooconfigure ITRP ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="317f3-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="317f3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="317f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="317f3-113">Bir ITRP çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="317f3-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="317f3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="317f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="317f3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="317f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="317f3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="317f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="317f3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="317f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="317f3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="317f3-118">Scenario description</span></span>
<span data-ttu-id="317f3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="317f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="317f3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="317f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="317f3-121">Merhaba Galerisi'nden ITRP ekleme</span><span class="sxs-lookup"><span data-stu-id="317f3-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="317f3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="317f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="317f3-123">Merhaba Galerisi'nden ITRP ekleme</span><span class="sxs-lookup"><span data-stu-id="317f3-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="317f3-124">Merhaba tümleştirilmesi tooconfigure ITRP tooAzure AD içinde tooadd ITRP hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="317f3-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="317f3-125">**tooadd ITRP hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="317f3-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="317f3-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="317f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="317f3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="317f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="317f3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="317f3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="317f3-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="317f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="317f3-133">Merhaba arama kutusuna yazın **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="317f3-133">In hello search box, type **ITRP**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="317f3-135">Merhaba Sonuçlar panelinde seçin **ITRP**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="317f3-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="317f3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="317f3-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="317f3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ITRP ile test etme</span><span class="sxs-lookup"><span data-stu-id="317f3-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="317f3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ITRP içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="317f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="317f3-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ITRP hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="317f3-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="317f3-141">Merhaba hello değeri ITRP içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="317f3-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="317f3-142">tooconfigure ve ITRP ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="317f3-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="317f3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="317f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="317f3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="317f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="317f3-145">**[Test kullanıcı bir ITRP oluşturma](#creating-an-itrp-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ITRP içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="317f3-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="317f3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="317f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="317f3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="317f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="317f3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="317f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="317f3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ITRP uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="317f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="317f3-150">**tooconfigure Azure AD çoklu oturum açma ile ITRP, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="317f3-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="317f3-151">Hello hello üzerinde Azure portal'ın **ITRP** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="317f3-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="317f3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="317f3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="317f3-155">Merhaba üzerinde **ITRP etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="317f3-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="317f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="317f3-157">a.</span></span> <span data-ttu-id="317f3-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="317f3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="317f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="317f3-159">b.</span></span> <span data-ttu-id="317f3-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="317f3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="317f3-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="317f3-161">These values are not real.</span></span> <span data-ttu-id="317f3-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="317f3-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="317f3-163">Kişi [ITRP istemci destek ekibi](https://www.itrp.com/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="317f3-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="317f3-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="317f3-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="317f3-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="317f3-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="317f3-168">Merhaba üzerinde **ITRP yapılandırma** 'yi tıklatın **yapılandırma ITRP** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="317f3-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="317f3-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="317f3-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="317f3-171">Farklı web tarayıcısı penceresinde tooyour ITRP şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="317f3-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="317f3-172">Merhaba üstte Hello araç çubuğunda **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="317f3-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="317f3-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="317f3-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="317f3-174">Merhaba sol gezinti bölmesinde seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="317f3-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="317f3-175">![Çoklu oturum açma](./media/active-directory-saas-itrp-tutorial/ic775571.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="317f3-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="317f3-176">Hello çoklu oturum açma yapılandırma bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="317f3-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="317f3-177">![Çoklu oturum açma](./media/active-directory-saas-itrp-tutorial/ic775572.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="317f3-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="317f3-178">![Çoklu oturum açma](./media/active-directory-saas-itrp-tutorial/ic775573.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="317f3-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="317f3-179">a.</span><span class="sxs-lookup"><span data-stu-id="317f3-179">a.</span></span> <span data-ttu-id="317f3-180">**Etkinleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="317f3-180">Click **Enable**.</span></span>

    <span data-ttu-id="317f3-181">b.</span><span class="sxs-lookup"><span data-stu-id="317f3-181">b.</span></span> <span data-ttu-id="317f3-182">İçinde **uzak oturum kapatma URL'sini** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="317f3-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="317f3-183">c.</span><span class="sxs-lookup"><span data-stu-id="317f3-183">c.</span></span> <span data-ttu-id="317f3-184">İçinde **SAML SSO URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="317f3-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="317f3-185">d.In **sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="317f3-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="317f3-186">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="317f3-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="317f3-187">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="317f3-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="317f3-188">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="317f3-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="317f3-189">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="317f3-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="317f3-190">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="317f3-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="317f3-191">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="317f3-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="317f3-193">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="317f3-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="317f3-194">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="317f3-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="317f3-196">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="317f3-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="317f3-198">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="317f3-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="317f3-200">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="317f3-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="317f3-202">a.</span><span class="sxs-lookup"><span data-stu-id="317f3-202">a.</span></span> <span data-ttu-id="317f3-203">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="317f3-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="317f3-204">b.</span><span class="sxs-lookup"><span data-stu-id="317f3-204">b.</span></span> <span data-ttu-id="317f3-205">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="317f3-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="317f3-206">c.</span><span class="sxs-lookup"><span data-stu-id="317f3-206">c.</span></span> <span data-ttu-id="317f3-207">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="317f3-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="317f3-208">d.</span><span class="sxs-lookup"><span data-stu-id="317f3-208">d.</span></span> <span data-ttu-id="317f3-209">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="317f3-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="317f3-210">Bir ITRP test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="317f3-210">Creating an ITRP test user</span></span>

<span data-ttu-id="317f3-211">tooenable Azure AD kullanıcıların toolog tooITRP bunlar içinde tooITRP sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="317f3-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="317f3-212">ITRP Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="317f3-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="317f3-213">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="317f3-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="317f3-214">İçinde tooyour oturum **ITRP** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="317f3-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="317f3-215">Merhaba üstte Hello araç çubuğunda **kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="317f3-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="317f3-216">![Yönetici](./media/active-directory-saas-itrp-tutorial/ic775575.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="317f3-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="317f3-217">Merhaba açılır menüden seçin **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="317f3-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="317f3-218">![Kişiler](./media/active-directory-saas-itrp-tutorial/ic775587.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="317f3-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="317f3-219">Tıklatın **yeni bir kişiye eklemek** ("+").</span><span class="sxs-lookup"><span data-stu-id="317f3-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="317f3-220">![Yönetici](./media/active-directory-saas-itrp-tutorial/ic775576.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="317f3-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="317f3-221">Merhaba Yeni Kişi Ekle iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="317f3-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="317f3-222">![Kullanıcı](./media/active-directory-saas-itrp-tutorial/ic775577.png "kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="317f3-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="317f3-223">a.</span><span class="sxs-lookup"><span data-stu-id="317f3-223">a.</span></span> <span data-ttu-id="317f3-224">Türü hello **adı**, **e-posta** tooprovision istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="317f3-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="317f3-225">b.</span><span class="sxs-lookup"><span data-stu-id="317f3-225">b.</span></span> <span data-ttu-id="317f3-226">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="317f3-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="317f3-227">API AAD kullanıcı hesaplarının ITRP tooprovision tarafından sağlanan veya herhangi diğer ITRP kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="317f3-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="317f3-228">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="317f3-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="317f3-229">Bu bölümde, erişim tooITRP vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="317f3-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="317f3-231">**tooassign Britta Simon tooITRP hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="317f3-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="317f3-232">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="317f3-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="317f3-234">Merhaba uygulamalar listesinde **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="317f3-234">In hello applications list, select **ITRP**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="317f3-236">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="317f3-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="317f3-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="317f3-238">Click **Add** button.</span></span> <span data-ttu-id="317f3-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="317f3-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="317f3-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="317f3-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="317f3-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="317f3-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="317f3-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="317f3-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="317f3-244">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="317f3-244">Testing single sign-on</span></span>

<span data-ttu-id="317f3-245">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="317f3-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="317f3-246">ITRP döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma tooyour ITRP uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="317f3-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="317f3-247">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="317f3-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="317f3-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="317f3-248">Additional resources</span></span>

* [<span data-ttu-id="317f3-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="317f3-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="317f3-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="317f3-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

