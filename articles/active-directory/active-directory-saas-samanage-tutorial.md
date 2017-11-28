---
title: "Öğretici: Azure Active Directory Tümleştirme ile Samanage | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Samanage arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="c42be-103">Öğretici: Azure Active Directory Tümleştirme Samanage ile</span><span class="sxs-lookup"><span data-stu-id="c42be-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="c42be-104">Bu öğreticide, bilgi nasıl toointegrate Samanage Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c42be-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c42be-105">Samanage Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c42be-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c42be-106">Erişim tooSamanage sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c42be-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="c42be-107">Kullanıcıların tooautomatically get açan tooSamanage (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c42be-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c42be-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c42be-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c42be-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c42be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c42be-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c42be-110">Prerequisites</span></span>

<span data-ttu-id="c42be-111">tooconfigure Samanage ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c42be-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="c42be-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c42be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c42be-113">Bir Samanage çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c42be-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c42be-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c42be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c42be-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c42be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c42be-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c42be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c42be-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c42be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c42be-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c42be-118">Scenario description</span></span>
<span data-ttu-id="c42be-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c42be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c42be-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c42be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c42be-121">Merhaba Galerisi'nden Samanage ekleme</span><span class="sxs-lookup"><span data-stu-id="c42be-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="c42be-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c42be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="c42be-123">Merhaba Galerisi'nden Samanage ekleme</span><span class="sxs-lookup"><span data-stu-id="c42be-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="c42be-124">Azure AD'ye tooconfigure hello tümleştirme Samanage, tooadd Samanage hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c42be-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c42be-125">**tooadd Samanage hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c42be-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c42be-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c42be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c42be-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c42be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c42be-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c42be-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c42be-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c42be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c42be-133">Merhaba arama kutusuna yazın **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="c42be-133">In hello search box, type **Samanage**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="c42be-135">Merhaba Sonuçlar panelinde seçin **Samanage**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c42be-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c42be-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c42be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c42be-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Samanage sınayın.</span><span class="sxs-lookup"><span data-stu-id="c42be-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c42be-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Samanage içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="c42be-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="c42be-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Samanage hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c42be-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="c42be-141">Merhaba hello değeri Samanage içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="c42be-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c42be-142">tooconfigure ve Samanage ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c42be-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c42be-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="c42be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c42be-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="c42be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c42be-145">**[Samanage test kullanıcısı oluşturma](#creating-a-samanage-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Samanage içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="c42be-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c42be-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c42be-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c42be-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="c42be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c42be-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c42be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c42be-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Samanage uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c42be-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="c42be-150">**tooconfigure Azure AD çoklu oturum açma ile Samanage, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c42be-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="c42be-151">Hello hello üzerinde Azure portal'ın **Samanage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c42be-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c42be-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="c42be-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="c42be-155">Merhaba üzerinde **Samanage etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c42be-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="c42be-157">a.</span><span class="sxs-lookup"><span data-stu-id="c42be-157">a.</span></span> <span data-ttu-id="c42be-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="c42be-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="c42be-159">b.</span><span class="sxs-lookup"><span data-stu-id="c42be-159">b.</span></span> <span data-ttu-id="c42be-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="c42be-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c42be-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c42be-161">These values are not real.</span></span> <span data-ttu-id="c42be-162">Bu değerler, oturum açma hello gerçek URL'si ve hello öğreticinin ilerleyen bölümlerinde açıklanan tanımlayıcısı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c42be-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="c42be-163">Daha fazla ayrıntı başvurun [Samanage istemci destek ekibi](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="c42be-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="c42be-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c42be-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="c42be-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c42be-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c42be-168">Merhaba üzerinde **Samanage yapılandırma** 'yi tıklatın **yapılandırma Samanage** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c42be-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c42be-169">Kopya hello **Sign-Out URL ve SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c42be-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="c42be-171">Farklı web tarayıcısı penceresinde Samanage şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c42be-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="c42be-172">Tıklatın **Pano** seçip **Kurulum** sol gezinti bölmesindeki.</span><span class="sxs-lookup"><span data-stu-id="c42be-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="c42be-173">![Pano](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Panosu")</span><span class="sxs-lookup"><span data-stu-id="c42be-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="c42be-174">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c42be-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="c42be-175">![Çoklu oturum açma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="c42be-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="c42be-176">Çok gidin**SAML kullanarak oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c42be-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c42be-177">![SAML kullanarak oturum açma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "SAML ile oturum açın")</span><span class="sxs-lookup"><span data-stu-id="c42be-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="c42be-178">a.</span><span class="sxs-lookup"><span data-stu-id="c42be-178">a.</span></span> <span data-ttu-id="c42be-179">Tıklatın **çoklu oturum açmayı etkinleştir SAML ile**.</span><span class="sxs-lookup"><span data-stu-id="c42be-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="c42be-180">b.</span><span class="sxs-lookup"><span data-stu-id="c42be-180">b.</span></span> <span data-ttu-id="c42be-181">Merhaba, **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c42be-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="c42be-182">c.</span><span class="sxs-lookup"><span data-stu-id="c42be-182">c.</span></span> <span data-ttu-id="c42be-183">Merhaba onaylayın **oturum açma URL'si** eşleşmeleri hello **oturum üzerinde URL'si** , **Samanage etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="c42be-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="c42be-184">d.</span><span class="sxs-lookup"><span data-stu-id="c42be-184">d.</span></span> <span data-ttu-id="c42be-185">Merhaba, **oturum kapatma URL'si** metin kutusuna, hello değeri girin **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c42be-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="c42be-186">e.</span><span class="sxs-lookup"><span data-stu-id="c42be-186">e.</span></span> <span data-ttu-id="c42be-187">Merhaba, **SAML veren** metin kutusuna, türü hello uygulama kimliği URI kimlik sağlayıcınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c42be-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="c42be-188">f.</span><span class="sxs-lookup"><span data-stu-id="c42be-188">f.</span></span> <span data-ttu-id="c42be-189">Not Defteri'nde, kopyalama hello panonuza bunu içerik Azure portalından indirdiğiniz, base-64 kodlanmış sertifikasını açın ve ardından toohello yapıştırın **, kimlik sağlayıcısı x.509 sertifika aşağıdaki Yapıştır** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c42be-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="c42be-190">g.</span><span class="sxs-lookup"><span data-stu-id="c42be-190">g.</span></span> <span data-ttu-id="c42be-191">Tıklatın **Samanage içinde yoksa, kullanıcılar oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c42be-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="c42be-192">h.</span><span class="sxs-lookup"><span data-stu-id="c42be-192">h.</span></span> <span data-ttu-id="c42be-193">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="c42be-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="c42be-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c42be-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c42be-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="c42be-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c42be-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c42be-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c42be-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c42be-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c42be-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="c42be-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c42be-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c42be-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c42be-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c42be-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c42be-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c42be-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c42be-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c42be-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c42be-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c42be-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c42be-209">a.</span><span class="sxs-lookup"><span data-stu-id="c42be-209">a.</span></span> <span data-ttu-id="c42be-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c42be-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c42be-211">b.</span><span class="sxs-lookup"><span data-stu-id="c42be-211">b.</span></span> <span data-ttu-id="c42be-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c42be-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c42be-213">c.</span><span class="sxs-lookup"><span data-stu-id="c42be-213">c.</span></span> <span data-ttu-id="c42be-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c42be-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c42be-215">d.</span><span class="sxs-lookup"><span data-stu-id="c42be-215">d.</span></span> <span data-ttu-id="c42be-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c42be-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="c42be-217">Samanage test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c42be-217">Creating a Samanage test user</span></span>

<span data-ttu-id="c42be-218">tooenable Azure AD kullanıcıların toolog tooSamanage bunların Samanage sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c42be-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="c42be-219">Samanage Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c42be-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="c42be-220">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c42be-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c42be-221">Samanage şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c42be-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="c42be-222">Tıklatın **Pano** seçip **Kurulum** sol gezinti bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="c42be-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="c42be-223">![Kurulum](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="c42be-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="c42be-224">Merhaba tıklatın **kullanıcılar** sekmesi</span><span class="sxs-lookup"><span data-stu-id="c42be-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="c42be-225">![Kullanıcıların](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="c42be-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="c42be-226">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="c42be-226">Click **New User**.</span></span>
   
    <span data-ttu-id="c42be-227">![Yeni kullanıcı](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="c42be-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="c42be-228">Türü hello **adı** ve hello **e-posta adresi** tooprovision istediğiniz bir Azure Active Directory hesabının **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c42be-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="c42be-229">![Kullanıcı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="c42be-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c42be-230">Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.</span><span class="sxs-lookup"><span data-stu-id="c42be-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="c42be-231">API, kullanıcı hesaplarını Samanage tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer Samanage kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c42be-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c42be-232">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c42be-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c42be-233">Bu bölümde, erişim tooSamanage vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c42be-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c42be-235">**tooassign Britta Simon tooSamanage hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c42be-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="c42be-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c42be-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c42be-238">Merhaba uygulamalar listesinde **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="c42be-238">In hello applications list, select **Samanage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="c42be-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c42be-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c42be-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c42be-242">Click **Add** button.</span></span> <span data-ttu-id="c42be-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c42be-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c42be-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c42be-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c42be-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c42be-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c42be-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c42be-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c42be-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c42be-248">Testing single sign-on</span></span>

<span data-ttu-id="c42be-249">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c42be-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c42be-250">Merhaba Samanage hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Samanage uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c42be-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="c42be-251">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c42be-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c42be-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c42be-252">Additional resources</span></span>

* [<span data-ttu-id="c42be-253">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="c42be-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c42be-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c42be-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

