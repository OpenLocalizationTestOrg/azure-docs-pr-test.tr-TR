---
title: "Öğretici: Azure Active Directory Tümleştirme ile Freshservice | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Freshservice arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="0fffb-103">Öğretici: Azure Active Directory Tümleştirme Freshservice ile</span><span class="sxs-lookup"><span data-stu-id="0fffb-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="0fffb-104">Bu öğreticide, bilgi nasıl toointegrate Freshservice Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fffb-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fffb-105">Freshservice Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0fffb-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0fffb-106">Erişim tooFreshservice sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0fffb-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="0fffb-107">Kullanıcıların tooautomatically get açan tooFreshservice (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0fffb-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fffb-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0fffb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0fffb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fffb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fffb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0fffb-110">Prerequisites</span></span>

<span data-ttu-id="0fffb-111">tooconfigure Freshservice ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0fffb-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="0fffb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0fffb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fffb-113">Bir Freshservice çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0fffb-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fffb-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0fffb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fffb-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0fffb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fffb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0fffb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fffb-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fffb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fffb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0fffb-118">Scenario description</span></span>
<span data-ttu-id="0fffb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0fffb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fffb-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0fffb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fffb-121">Merhaba Galerisi'nden Freshservice ekleme</span><span class="sxs-lookup"><span data-stu-id="0fffb-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="0fffb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0fffb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="0fffb-123">Merhaba Galerisi'nden Freshservice ekleme</span><span class="sxs-lookup"><span data-stu-id="0fffb-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="0fffb-124">Azure AD'ye tooconfigure hello tümleştirme Freshservice, tooadd Freshservice hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0fffb-125">**tooadd Freshservice hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fffb-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fffb-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fffb-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0fffb-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0fffb-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0fffb-133">Merhaba arama kutusuna yazın **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-133">In hello search box, type **Freshservice**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="0fffb-135">Merhaba Sonuçlar panelinde seçin **Freshservice**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0fffb-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fffb-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0fffb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fffb-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Freshservice sınayın.</span><span class="sxs-lookup"><span data-stu-id="0fffb-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0fffb-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Freshservice içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="0fffb-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Freshservice hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="0fffb-141">Merhaba hello değeri Freshservice içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0fffb-142">tooconfigure ve Freshservice ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0fffb-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0fffb-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0fffb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0fffb-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0fffb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fffb-145">**[Freshservice test kullanıcısı oluşturma](#creating-a-freshservice-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Freshservice içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0fffb-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fffb-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0fffb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fffb-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0fffb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fffb-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0fffb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fffb-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Freshservice uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0fffb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="0fffb-150">**tooconfigure Azure AD çoklu oturum açma ile Freshservice, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fffb-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fffb-151">Hello hello üzerinde Azure portal'ın **Freshservice** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0fffb-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0fffb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="0fffb-155">Merhaba üzerinde **Freshservice etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fffb-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="0fffb-157">a.</span><span class="sxs-lookup"><span data-stu-id="0fffb-157">a.</span></span> <span data-ttu-id="0fffb-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="0fffb-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="0fffb-159">b.</span><span class="sxs-lookup"><span data-stu-id="0fffb-159">b.</span></span> <span data-ttu-id="0fffb-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="0fffb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0fffb-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-161">These values are not real.</span></span> <span data-ttu-id="0fffb-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="0fffb-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0fffb-163">Kişi [Freshservice istemci destek ekibi](https://support.freshservice.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="0fffb-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="0fffb-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="0fffb-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="0fffb-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0fffb-168">Merhaba üzerinde **Freshservice yapılandırma** 'yi tıklatın **yapılandırma Freshservice** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0fffb-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0fffb-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="0fffb-171">Farklı web tarayıcısı penceresinde tooyour Freshservice şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0fffb-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="0fffb-172">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="0fffb-173">![Yönetici](./media/active-directory-saas-freshservice-tutorial/ic790814.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="0fffb-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="0fffb-174">Merhaba, **müşteri portalı**, tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="0fffb-175">![Güvenlik](./media/active-directory-saas-freshservice-tutorial/ic790815.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="0fffb-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="0fffb-176">Merhaba, **güvenlik** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fffb-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0fffb-177">![Çoklu oturum açmayı](./media/active-directory-saas-freshservice-tutorial/ic790816.png "çoklu oturum açmayı")</span><span class="sxs-lookup"><span data-stu-id="0fffb-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="0fffb-178">a.</span><span class="sxs-lookup"><span data-stu-id="0fffb-178">a.</span></span> <span data-ttu-id="0fffb-179">Anahtar **çoklu oturum açmayı**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="0fffb-180">b.</span><span class="sxs-lookup"><span data-stu-id="0fffb-180">b.</span></span> <span data-ttu-id="0fffb-181">Seçin **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="0fffb-182">c.</span><span class="sxs-lookup"><span data-stu-id="0fffb-182">c.</span></span> <span data-ttu-id="0fffb-183">Merhaba, **SAML oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0fffb-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0fffb-184">d.</span><span class="sxs-lookup"><span data-stu-id="0fffb-184">d.</span></span> <span data-ttu-id="0fffb-185">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0fffb-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0fffb-186">e.</span><span class="sxs-lookup"><span data-stu-id="0fffb-186">e.</span></span> <span data-ttu-id="0fffb-187">İçinde **güvenlik sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak İZİ** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="0fffb-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0fffb-188">f.</span><span class="sxs-lookup"><span data-stu-id="0fffb-188">f.</span></span> <span data-ttu-id="0fffb-189">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="0fffb-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="0fffb-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0fffb-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0fffb-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0fffb-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0fffb-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0fffb-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fffb-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fffb-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fffb-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0fffb-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0fffb-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fffb-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fffb-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fffb-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fffb-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fffb-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fffb-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fffb-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fffb-205">a.</span><span class="sxs-lookup"><span data-stu-id="0fffb-205">a.</span></span> <span data-ttu-id="0fffb-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fffb-207">b.</span><span class="sxs-lookup"><span data-stu-id="0fffb-207">b.</span></span> <span data-ttu-id="0fffb-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0fffb-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fffb-209">c.</span><span class="sxs-lookup"><span data-stu-id="0fffb-209">c.</span></span> <span data-ttu-id="0fffb-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0fffb-211">d.</span><span class="sxs-lookup"><span data-stu-id="0fffb-211">d.</span></span> <span data-ttu-id="0fffb-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0fffb-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="0fffb-213">Freshservice test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fffb-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="0fffb-214">tooenable Azure AD kullanıcıların toolog tooFreshService bunların FreshService sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="0fffb-215">FreshService Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="0fffb-216">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fffb-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fffb-217">İçinde tooyour oturum **FreshService** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="0fffb-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="0fffb-218">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="0fffb-219">![Yönetici](./media/active-directory-saas-freshservice-tutorial/ic790814.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="0fffb-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="0fffb-220">Merhaba, **kullanıcı yönetimi** 'yi tıklatın **sahiplerini**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="0fffb-221">![Sahiplerini](./media/active-directory-saas-freshservice-tutorial/ic790818.png "sahiplerini")</span><span class="sxs-lookup"><span data-stu-id="0fffb-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="0fffb-222">Tıklatın **yeni istek**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="0fffb-223">![Yeni sahiplerini](./media/active-directory-saas-freshservice-tutorial/ic790819.png "yeni sahiplerini")</span><span class="sxs-lookup"><span data-stu-id="0fffb-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="0fffb-224">Merhaba, **yeni istek** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fffb-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0fffb-225">![Yeni İstek](./media/active-directory-saas-freshservice-tutorial/ic790820.png "yeni istek")</span><span class="sxs-lookup"><span data-stu-id="0fffb-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="0fffb-226">a.</span><span class="sxs-lookup"><span data-stu-id="0fffb-226">a.</span></span> <span data-ttu-id="0fffb-227">Merhaba girin **ad** ve **e-posta** hello tooprovision istediğiniz geçerli bir Azure Active Directory hesabı özniteliklerini ilgili metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="0fffb-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="0fffb-228">b.</span><span class="sxs-lookup"><span data-stu-id="0fffb-228">b.</span></span> <span data-ttu-id="0fffb-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0fffb-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="0fffb-230">Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabı da dahil olmak üzere bir e-posta alır</span><span class="sxs-lookup"><span data-stu-id="0fffb-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="0fffb-231">API AAD kullanıcı hesaplarının FreshService tooprovision tarafından sağlanan veya herhangi diğer FreshService kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fffb-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Kullanıcı atama][200] 

<span data-ttu-id="0fffb-233">**tooassign Britta Simon tooFreshservice hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fffb-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fffb-234">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0fffb-236">Merhaba uygulamalar listesinde **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-236">In hello applications list, select **Freshservice**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="0fffb-238">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0fffb-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0fffb-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0fffb-240">Click **Add** button.</span></span> <span data-ttu-id="0fffb-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fffb-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0fffb-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0fffb-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0fffb-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fffb-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fffb-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fffb-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fffb-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0fffb-246">Testing single sign-on</span></span>

<span data-ttu-id="0fffb-247">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0fffb-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0fffb-248">Merhaba Freshservice hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Freshservice uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fffb-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fffb-249">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0fffb-249">Additional resources</span></span>

* [<span data-ttu-id="0fffb-250">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0fffb-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fffb-251">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0fffb-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

