---
title: "Öğretici: Azure Active Directory Tümleştirme ile Syncplicity | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Syncplicity arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="4baa4-103">Öğretici: Syncplicity Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="4baa4-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="4baa4-104">Bu öğreticide, bilgi nasıl toointegrate Syncplicity Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4baa4-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4baa4-105">Syncplicity Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4baa4-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4baa4-106">Erişim tooSyncplicity sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4baa4-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="4baa4-107">Kullanıcıların tooautomatically get açan tooSyncplicity (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4baa4-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4baa4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4baa4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4baa4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4baa4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4baa4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4baa4-110">Prerequisites</span></span>

<span data-ttu-id="4baa4-111">tooconfigure Syncplicity ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4baa4-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="4baa4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4baa4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4baa4-113">Bir Syncplicity çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4baa4-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4baa4-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4baa4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4baa4-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4baa4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4baa4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4baa4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4baa4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4baa4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4baa4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4baa4-118">Scenario description</span></span>
<span data-ttu-id="4baa4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4baa4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4baa4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4baa4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4baa4-121">Syncplicity hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="4baa4-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="4baa4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4baa4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="4baa4-123">Syncplicity hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="4baa4-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="4baa4-124">Azure AD'ye tooconfigure hello tümleştirme Syncplicity, tooadd Syncplicity hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4baa4-125">**tooadd Syncplicity hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4baa4-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4baa4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4baa4-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4baa4-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4baa4-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4baa4-133">Merhaba arama kutusuna yazın **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-133">In hello search box, type **Syncplicity**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="4baa4-135">Merhaba Sonuçlar panelinde seçin **Syncplicity**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4baa4-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4baa4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4baa4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4baa4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Syncplicity ile test etme</span><span class="sxs-lookup"><span data-stu-id="4baa4-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4baa4-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Syncplicity içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="4baa4-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Syncplicity hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="4baa4-141">Syncplicity içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4baa4-142">tooconfigure ve Syncplicity ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4baa4-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4baa4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4baa4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4baa4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4baa4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4baa4-145">**[Syncplicity test kullanıcısı oluşturma](#creating-a-syncplicity-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Syncplicity içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="4baa4-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4baa4-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4baa4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4baa4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4baa4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4baa4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4baa4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4baa4-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Syncplicity uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4baa4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="4baa4-150">**tooconfigure Azure AD çoklu oturum açma ile Syncplicity, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4baa4-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="4baa4-151">Hello hello üzerinde Azure portal'ın **Syncplicity** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4baa4-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4baa4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="4baa4-155">Merhaba üzerinde **Syncplicity etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4baa4-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="4baa4-157">a.</span><span class="sxs-lookup"><span data-stu-id="4baa4-157">a.</span></span> <span data-ttu-id="4baa4-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="4baa4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="4baa4-159">b.</span><span class="sxs-lookup"><span data-stu-id="4baa4-159">b.</span></span> <span data-ttu-id="4baa4-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4baa4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4baa4-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-161">These values are not real.</span></span> <span data-ttu-id="4baa4-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4baa4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4baa4-163">Kişi [Syncplicity istemci destek ekibi](https://www.syncplicity.com/contact-us) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="4baa4-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="4baa4-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4baa4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="4baa4-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4baa4-168">Merhaba üzerinde **Syncplicity yapılandırma** 'yi tıklatın **yapılandırma Syncplicity** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4baa4-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4baa4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="4baa4-171">İçinde tooyour oturum **Syncplicity** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="4baa4-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="4baa4-172">Hello içinde hello üst menüsünde **yönetici**seçin **ayarları**ve ardından **özel etki alanı ve çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="4baa4-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="4baa4-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="4baa4-174">Merhaba üzerinde **çoklu oturum açma (SSO)** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4baa4-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="4baa4-175">![Çoklu oturum açma \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="4baa4-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="4baa4-176">a.</span><span class="sxs-lookup"><span data-stu-id="4baa4-176">a.</span></span> <span data-ttu-id="4baa4-177">Merhaba, **özel etki alanı** metin kutusuna, etki alanınızın türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="4baa4-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="4baa4-178">b.</span><span class="sxs-lookup"><span data-stu-id="4baa4-178">b.</span></span> <span data-ttu-id="4baa4-179">Seçin **etkin** olarak **tek oturum açma durumu**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="4baa4-180">c.</span><span class="sxs-lookup"><span data-stu-id="4baa4-180">c.</span></span> <span data-ttu-id="4baa4-181">Merhaba, **varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4baa4-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4baa4-182">d.</span><span class="sxs-lookup"><span data-stu-id="4baa4-182">d.</span></span> <span data-ttu-id="4baa4-183">Merhaba, **oturum açma sayfası URL'si** metin kutusuna, Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4baa4-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4baa4-184">e.</span><span class="sxs-lookup"><span data-stu-id="4baa4-184">e.</span></span> <span data-ttu-id="4baa4-185">Merhaba, **oturum kapatma sayfası URL'si** metin kutusuna, Yapıştır hello **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4baa4-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4baa4-186">f.</span><span class="sxs-lookup"><span data-stu-id="4baa4-186">f.</span></span> <span data-ttu-id="4baa4-187">İçinde **kimlik sağlayıcısı sertifikası**, tıklatın **dosya**ve hello Azure portal ' indirilen hello sertifikasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4baa4-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="4baa4-188">g.</span><span class="sxs-lookup"><span data-stu-id="4baa4-188">g.</span></span> <span data-ttu-id="4baa4-189">Tıklatın **değişiklikleri kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="4baa4-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4baa4-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4baa4-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4baa4-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4baa4-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4baa4-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4baa4-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4baa4-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="4baa4-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4baa4-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4baa4-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4baa4-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4baa4-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4baa4-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4baa4-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4baa4-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4baa4-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4baa4-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4baa4-205">a.</span><span class="sxs-lookup"><span data-stu-id="4baa4-205">a.</span></span> <span data-ttu-id="4baa4-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4baa4-207">b.</span><span class="sxs-lookup"><span data-stu-id="4baa4-207">b.</span></span> <span data-ttu-id="4baa4-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4baa4-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4baa4-209">c.</span><span class="sxs-lookup"><span data-stu-id="4baa4-209">c.</span></span> <span data-ttu-id="4baa4-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4baa4-211">d.</span><span class="sxs-lookup"><span data-stu-id="4baa4-211">d.</span></span> <span data-ttu-id="4baa4-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4baa4-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="4baa4-213">Syncplicity test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4baa4-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="4baa4-214">AAD kullanıcılar toobe mümkün toosign için bunların sağlanan tooSyncplicity uygulama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="4baa4-215">Bu bölümde, nasıl Syncplicity içinde toocreate AAD kullanıcı hesapları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4baa4-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="4baa4-216">**bir kullanıcı hesabı tooSyncplicity tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4baa4-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="4baa4-217">İçinde tooyour oturum **Syncplicity** Kiracı (örneğin: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="4baa4-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="4baa4-218">Tıklatın **yönetici** seçip **kullanıcı hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="4baa4-219">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="4baa4-220">![Kullanıcıları yönetme](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="4baa4-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="4baa4-221">Türü hello **e-posta addressess** tooprovision, select istediğiniz bir AAD hesabın **kullanıcı** olarak **rol**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4baa4-222">![Hesap bilgileri](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "hesap bilgileri")</span><span class="sxs-lookup"><span data-stu-id="4baa4-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4baa4-223">Merhaba AAD hesap sahibi bağlantı tooconfirm dahil olmak üzere bir e-posta alır ve hello hesabını etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="4baa4-224">Yeni kullanıcı bir üyesi haline gelir ve ardından, şirketinizde bir grup seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4baa4-225">![Grup üyelikleri](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "grup üyelikleri")</span><span class="sxs-lookup"><span data-stu-id="4baa4-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4baa4-226">Listelenen hiçbir grup varsa tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="4baa4-227">Merhaba kullanıcının bilgisayarındaki Syncplicity'nın denetimindeki tooplace ister ve ardından hello klasörleri seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4baa4-228">![Syncplicity klasörleri](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity klasörleri")</span><span class="sxs-lookup"><span data-stu-id="4baa4-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="4baa4-229">API AAD kullanıcı hesaplarının Syncplicity tooprovision tarafından sağlanan veya herhangi diğer Syncplicity kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4baa4-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4baa4-230">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4baa4-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4baa4-231">Bu bölümde, erişim tooSyncplicity vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4baa4-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4baa4-233">**tooassign Britta Simon tooSyncplicity hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4baa4-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="4baa4-234">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4baa4-236">Merhaba uygulamalar listesinde **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="4baa4-238">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4baa4-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4baa4-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4baa4-240">Click **Add** button.</span></span> <span data-ttu-id="4baa4-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4baa4-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4baa4-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4baa4-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4baa4-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4baa4-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4baa4-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4baa4-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4baa4-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4baa4-246">Testing single sign-on</span></span>

<span data-ttu-id="4baa4-247">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4baa4-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4baa4-248">Merhaba Syncplicity hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Syncplicity uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baa4-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="4baa4-249">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4baa4-249">Additional resources</span></span>

* [<span data-ttu-id="4baa4-250">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4baa4-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4baa4-251">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4baa4-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

