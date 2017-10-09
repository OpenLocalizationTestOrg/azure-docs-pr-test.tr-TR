---
title: "Öğretici: Salesforce korumalı alan Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Salesforce korumalı alan arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="0a95b-103">Öğretici: Azure Active Directory Tümleştirme ile Salesforce korumalı alan</span><span class="sxs-lookup"><span data-stu-id="0a95b-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="0a95b-104">Bu öğreticide, bilgi nasıl toointegrate Salesforce korumalı alan Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a95b-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a95b-105">Salesforce korumalı alan Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0a95b-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a95b-106">Korumalı alan erişimi tooSalesforce sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0a95b-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="0a95b-107">Kullanıcıların tooautomatically get açan tooSalesforce Sandbox (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0a95b-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a95b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0a95b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0a95b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a95b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a95b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0a95b-110">Prerequisites</span></span>

<span data-ttu-id="0a95b-111">Salesforce korumalı alan ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0a95b-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="0a95b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0a95b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a95b-113">Bir Salesforce korumalı alan çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0a95b-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a95b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0a95b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a95b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0a95b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a95b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a95b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a95b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a95b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0a95b-118">Scenario description</span></span>
<span data-ttu-id="0a95b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0a95b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a95b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0a95b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a95b-121">Salesforce korumalı alan hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0a95b-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="0a95b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0a95b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="0a95b-123">Salesforce korumalı alan hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0a95b-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="0a95b-124">Azure AD'ye tooconfigure hello tümleştirme Salesforce korumalı alan, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd Salesforce korumalı alan gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a95b-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a95b-125">**Salesforce korumalı alan hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0a95b-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a95b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0a95b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a95b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a95b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0a95b-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0a95b-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0a95b-133">Merhaba arama kutusuna yazın **Salesforce korumalı alan**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="0a95b-135">Merhaba Sonuçlar panelinde seçin **Salesforce korumalı alan**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0a95b-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a95b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0a95b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a95b-138">Bu bölümde, yapılandırmanız ve Salesforce korumalı alan Azure AD çoklu oturum açma testiyle "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="0a95b-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a95b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Salesforce korumalı alanı içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a95b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="0a95b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Salesforce korumalı alan hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a95b-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="0a95b-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** Salesforce korumalı alanı içinde.</span><span class="sxs-lookup"><span data-stu-id="0a95b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="0a95b-142">tooconfigure ve Salesforce korumalı alan ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0a95b-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a95b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0a95b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a95b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0a95b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a95b-145">**[Salesforce korumalı alan test kullanıcısı oluşturma](#creating-a-salesforce-sandbox-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini Salesforce korumalı alanı içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0a95b-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a95b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0a95b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a95b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0a95b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a95b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0a95b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a95b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Salesforce korumalı alan uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="0a95b-150">**tooconfigure Azure AD çoklu oturum açma Salesforce korumalı alan ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0a95b-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a95b-151">Hello hello üzerinde Azure portal'ın **Salesforce korumalı alan** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0a95b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0a95b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="0a95b-155">Merhaba üzerinde **Salesforce korumalı alan etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0a95b-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="0a95b-157">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a95b-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a95b-158">Bu değer hello gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="0a95b-158">This value is not hello real.</span></span> <span data-ttu-id="0a95b-159">Bu değer hello gerçek oturum açma URL'si ile güncelleştirin. Kişi [Salesforce korumalı alan istemci destek ekibi](https://help.salesforce.com/support) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="0a95b-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="0a95b-160">Zaten başka bir Salesforce korumalı alan örneği için çoklu oturum açmayı dizininizde yapılandırdıktan sonra hello yapılandırmanız da gerekir **tanımlayıcısı** toohave hello hello aynı değere **URL üzerinde oturum**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="0a95b-161">Merhaba **tanımlayıcısı** alan hello denetleyerek bulunabilir **Göster Gelişmiş ayarları** hello onay kutusuna **uygulama URL'sini yapılandırın** hello iletişim sayfası</span><span class="sxs-lookup"><span data-stu-id="0a95b-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="0a95b-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0a95b-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="0a95b-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0a95b-164">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0a95b-166">Merhaba üzerinde **Salesforce korumalı alan yapılandırma** 'yi tıklatın **yapılandırma Salesforce korumalı alan** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0a95b-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a95b-167">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0a95b-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="0a95b-168">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="0a95b-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="0a95b-169">Tarayıcınızda yeni bir sekme açın ve oturum tooyour Salesforce korumalı alan yönetici hesabı.</span><span class="sxs-lookup"><span data-stu-id="0a95b-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="0a95b-170">Hello içinde hello üst menüsünde **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="0a95b-172">Merhaba Gezinti hello sol taraftaki bölmede **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="0a95b-174">Hello çoklu oturum açma ayarları bölümü, hello aşağıdaki adımları gerçekleştirin: ![yapılandırma çoklu oturum açma](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="0a95b-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="0a95b-175">a.</span><span class="sxs-lookup"><span data-stu-id="0a95b-175">a.</span></span>  <span data-ttu-id="0a95b-176">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="0a95b-177">b.</span><span class="sxs-lookup"><span data-stu-id="0a95b-177">b.</span></span>  <span data-ttu-id="0a95b-178">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-178">Click **New**.</span></span>

12. <span data-ttu-id="0a95b-179">SAML çoklu oturum açma ayarları bölümü Hello üzerinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0a95b-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="0a95b-181">a.In hello adı metin kutusuna, tür hello hello yapılandırma adını (örneğin: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="0a95b-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="0a95b-182">b.</span><span class="sxs-lookup"><span data-stu-id="0a95b-182">b.</span></span> <span data-ttu-id="0a95b-183">Yapıştır **SMAL varlık kimliği** hello değerine **veren** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0a95b-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="0a95b-184">c.</span><span class="sxs-lookup"><span data-stu-id="0a95b-184">c.</span></span> <span data-ttu-id="0a95b-185">Merhaba, **varlık kimliği** metin kutusuna, türü **https://test.salesforce.com** tooyour directory eklediğiniz ilk Salesforce korumalı alan örneği hello ise.</span><span class="sxs-lookup"><span data-stu-id="0a95b-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="0a95b-186">Salesforce korumalı alan, sonra da hello için bir örneği zaten eklediyseniz **varlık kimliği** hello türü **oturum üzerinde URL'si**, şu biçimde olmalıdır:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a95b-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="0a95b-187">d.</span><span class="sxs-lookup"><span data-stu-id="0a95b-187">d.</span></span> <span data-ttu-id="0a95b-188">Tıklatın **Gözat** tooupload hello sertifika indirilir.</span><span class="sxs-lookup"><span data-stu-id="0a95b-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="0a95b-189">e.</span><span class="sxs-lookup"><span data-stu-id="0a95b-189">e.</span></span> <span data-ttu-id="0a95b-190">Olarak **SAML kimlik türü**seçin **onaylamayı içeren hello Federasyon kimliği hello kullanıcı nesnesinden**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="0a95b-191">f.</span><span class="sxs-lookup"><span data-stu-id="0a95b-191">f.</span></span> <span data-ttu-id="0a95b-192">Olarak **SAML kimlik konumu**seçin **kimliktir hello NameIdentifier öğesinde hello konu deyimi**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="0a95b-193">g.</span><span class="sxs-lookup"><span data-stu-id="0a95b-193">g.</span></span> <span data-ttu-id="0a95b-194">Yapıştır **çoklu oturum açma hizmet URL'si** hello içine **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0a95b-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="0a95b-195">h.</span><span class="sxs-lookup"><span data-stu-id="0a95b-195">h.</span></span> <span data-ttu-id="0a95b-196">SAML oturum kapatma SFDC desteklemez.</span><span class="sxs-lookup"><span data-stu-id="0a95b-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="0a95b-197">Geçici bir çözüm olarak Yapıştır 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello içine **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="0a95b-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="0a95b-198">ı.</span><span class="sxs-lookup"><span data-stu-id="0a95b-198">i.</span></span> <span data-ttu-id="0a95b-199">Olarak **hizmet sağlayıcısı tarafından başlatılan bağlama isteği**seçin **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="0a95b-200">j.</span><span class="sxs-lookup"><span data-stu-id="0a95b-200">j.</span></span> <span data-ttu-id="0a95b-201">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="0a95b-202">Etki alanınızı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0a95b-202">Enable your domain</span></span>
<span data-ttu-id="0a95b-203">Bu bölümde, bir etki alanı zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0a95b-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="0a95b-204">Daha fazla bilgi için bkz: [etki alanı adınız tanımlama](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="0a95b-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="0a95b-205">**tooenable etki alanınızı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0a95b-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a95b-206">Merhaba sol gezinti bölmesinde **etki alanı yönetimi**ve ardından **My etki alanı.**</span><span class="sxs-lookup"><span data-stu-id="0a95b-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="0a95b-208">Lütfen etki alanınızı doğru yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0a95b-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="0a95b-209">Merhaba, **oturum açma sayfası ayarları** 'yi tıklatın **Düzenle**, sonra **kimlik doğrulama hizmeti**seçin hello önceki gelen oturum açma SAML tek ayar hello hello adı bölümünde ve son olarak tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="0a95b-211">Yapılandırılmış bir etki alanınız hemen kullanıcılarınızın hello etki alanı URL'si toologin toohello Salesforce korumalı alan kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a95b-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="0a95b-212">Merhaba URL tooget hello değeri hello önceki bölümde oluşturduğunuz hello SSO profil'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="0a95b-213">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0a95b-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a95b-214">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0a95b-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a95b-215">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a95b-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a95b-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a95b-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a95b-217">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0a95b-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0a95b-219">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0a95b-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a95b-220">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0a95b-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a95b-222">Kullanıcıların toodisplay hello listesini Git çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a95b-224">Merhaba iletişim Hello üstünde tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0a95b-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a95b-226">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0a95b-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a95b-228">a.</span><span class="sxs-lookup"><span data-stu-id="0a95b-228">a.</span></span> <span data-ttu-id="0a95b-229">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a95b-230">b.</span><span class="sxs-lookup"><span data-stu-id="0a95b-230">b.</span></span> <span data-ttu-id="0a95b-231">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0a95b-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a95b-232">c.</span><span class="sxs-lookup"><span data-stu-id="0a95b-232">c.</span></span> <span data-ttu-id="0a95b-233">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a95b-234">d.</span><span class="sxs-lookup"><span data-stu-id="0a95b-234">d.</span></span> <span data-ttu-id="0a95b-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="0a95b-236">Salesforce korumalı alan test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a95b-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="0a95b-237">Bu bölümde, Britta Simon adlı bir kullanıcı Salesforce korumalı alanda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0a95b-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="0a95b-238">Salesforce korumalı alan yeni saat sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="0a95b-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="0a95b-239">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="0a95b-239">There is no action item for you in this section.</span></span> <span data-ttu-id="0a95b-240">Salesforce korumalı alanda bir kullanıcı zaten mevcut değilse tooaccess Salesforce korumalı alan çalıştığında yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0a95b-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a95b-241">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0a95b-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a95b-242">Bu bölümde, erişim tooSalesforce Sandbox vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0a95b-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0a95b-244">**tooassign Britta Simon tooSalesforce korumalı alan, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0a95b-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a95b-245">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0a95b-247">Merhaba uygulamalar listesinde **Salesforce korumalı alan**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="0a95b-249">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0a95b-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0a95b-251">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0a95b-251">Click **Add** button.</span></span> <span data-ttu-id="0a95b-252">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0a95b-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0a95b-254">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0a95b-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a95b-255">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0a95b-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a95b-256">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0a95b-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a95b-257">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0a95b-257">Testing single sign-on</span></span>

<span data-ttu-id="0a95b-258">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="0a95b-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="0a95b-259">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a95b-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a95b-260">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0a95b-260">Additional resources</span></span>

* [<span data-ttu-id="0a95b-261">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0a95b-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a95b-262">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0a95b-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0a95b-263">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="0a95b-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

