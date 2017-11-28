---
title: "Öğretici: Azure Active Directory Tümleştirme ile Picturepark | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Picturepark arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="6b21b-103">Öğretici: Azure Active Directory Tümleştirme Picturepark ile</span><span class="sxs-lookup"><span data-stu-id="6b21b-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="6b21b-104">Bu öğreticide, bilgi nasıl toointegrate Picturepark Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b21b-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b21b-105">Picturepark Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6b21b-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6b21b-106">Erişim tooPicturepark sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6b21b-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="6b21b-107">Kullanıcıların tooautomatically get açan tooPicturepark (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6b21b-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b21b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6b21b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6b21b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b21b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b21b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6b21b-110">Prerequisites</span></span>

<span data-ttu-id="6b21b-111">tooconfigure Picturepark ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b21b-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="6b21b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6b21b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b21b-113">Bir Picturepark çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6b21b-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b21b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6b21b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b21b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b21b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b21b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b21b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b21b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b21b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6b21b-118">Scenario description</span></span>
<span data-ttu-id="6b21b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6b21b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b21b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6b21b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b21b-121">Merhaba Galerisi'nden Picturepark ekleme</span><span class="sxs-lookup"><span data-stu-id="6b21b-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="6b21b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6b21b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="6b21b-123">Merhaba Galerisi'nden Picturepark ekleme</span><span class="sxs-lookup"><span data-stu-id="6b21b-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="6b21b-124">Azure AD'ye tooconfigure hello tümleştirme Picturepark, tooadd Picturepark hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b21b-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6b21b-125">**tooadd Picturepark hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6b21b-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b21b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b21b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6b21b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6b21b-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6b21b-133">Merhaba arama kutusuna yazın **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-133">In hello search box, type **Picturepark**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="6b21b-135">Merhaba Sonuçlar panelinde seçin **Picturepark**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6b21b-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b21b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6b21b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b21b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Picturepark sınayın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b21b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Picturepark içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b21b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="6b21b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Picturepark hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b21b-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="6b21b-141">Merhaba hello değeri Picturepark içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6b21b-142">tooconfigure ve Picturepark ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b21b-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6b21b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6b21b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6b21b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6b21b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b21b-145">**[Picturepark test kullanıcısı oluşturma](#creating-a-picturepark-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Picturepark içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6b21b-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b21b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6b21b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b21b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6b21b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b21b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6b21b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b21b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Picturepark uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="6b21b-150">**tooconfigure Azure AD çoklu oturum açma ile Picturepark, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6b21b-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b21b-151">Hello hello üzerinde Azure portal'ın **Picturepark** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6b21b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6b21b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="6b21b-155">Merhaba üzerinde **Picturepark etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6b21b-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="6b21b-157">a.</span><span class="sxs-lookup"><span data-stu-id="6b21b-157">a.</span></span> <span data-ttu-id="6b21b-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="6b21b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="6b21b-159">b.</span><span class="sxs-lookup"><span data-stu-id="6b21b-159">b.</span></span> <span data-ttu-id="6b21b-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="6b21b-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="6b21b-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6b21b-161">These values are not real.</span></span> <span data-ttu-id="6b21b-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="6b21b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6b21b-163">Kişi [Picturepark istemci destek ekibi](https://picturepark.com/about/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="6b21b-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="6b21b-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="6b21b-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="6b21b-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b21b-168">Merhaba üzerinde **Picturepark yapılandırma** 'yi tıklatın **yapılandırma Picturepark** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6b21b-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6b21b-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="6b21b-171">Farklı web tarayıcısı penceresinde Picturepark şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="6b21b-172">Merhaba üstte Hello araç çubuğunda **Yönetimsel Araçlar**ve ardından **Yönetim Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="6b21b-173">![Yönetim Konsolu](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Yönetim Konsolu")</span><span class="sxs-lookup"><span data-stu-id="6b21b-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="6b21b-174">Tıklatın **kimlik doğrulaması**ve ardından **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="6b21b-175">![Kimlik doğrulama](./media/active-directory-saas-picturepark-tutorial/ic795063.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="6b21b-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="6b21b-176">Merhaba, **kimlik sağlayıcı Yapılandırması** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6b21b-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6b21b-177">![Kimlik sağlayıcısı Yapılandırması](./media/active-directory-saas-picturepark-tutorial/ic795064.png "kimlik sağlayıcı yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="6b21b-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="6b21b-178">a.</span><span class="sxs-lookup"><span data-stu-id="6b21b-178">a.</span></span> <span data-ttu-id="6b21b-179">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-179">Click **Add**.</span></span>
  
    <span data-ttu-id="6b21b-180">b.</span><span class="sxs-lookup"><span data-stu-id="6b21b-180">b.</span></span> <span data-ttu-id="6b21b-181">Yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="6b21b-182">c.</span><span class="sxs-lookup"><span data-stu-id="6b21b-182">c.</span></span> <span data-ttu-id="6b21b-183">Seçin **varsayılan olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="6b21b-184">d.</span><span class="sxs-lookup"><span data-stu-id="6b21b-184">d.</span></span> <span data-ttu-id="6b21b-185">İçinde **veren URI** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6b21b-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6b21b-186">e.</span><span class="sxs-lookup"><span data-stu-id="6b21b-186">e.</span></span> <span data-ttu-id="6b21b-187">İçinde **güvenilir verenin parmak iziyle** metin kutusuna, Yapıştır hello değerini **parmak izi** kopyalanan **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="6b21b-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="6b21b-188">Tıklatın **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="6b21b-189">tooset hello **Emailaddress** hello özniteliğinde **talep** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="6b21b-190">![Yapılandırma](./media/active-directory-saas-picturepark-tutorial/ic795065.png "yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="6b21b-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="6b21b-191">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6b21b-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6b21b-192">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6b21b-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6b21b-193">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b21b-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b21b-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b21b-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b21b-195">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6b21b-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6b21b-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6b21b-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b21b-198">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b21b-200">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b21b-202">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b21b-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b21b-204">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6b21b-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b21b-206">a.</span><span class="sxs-lookup"><span data-stu-id="6b21b-206">a.</span></span> <span data-ttu-id="6b21b-207">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b21b-208">b.</span><span class="sxs-lookup"><span data-stu-id="6b21b-208">b.</span></span> <span data-ttu-id="6b21b-209">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6b21b-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b21b-210">c.</span><span class="sxs-lookup"><span data-stu-id="6b21b-210">c.</span></span> <span data-ttu-id="6b21b-211">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6b21b-212">d.</span><span class="sxs-lookup"><span data-stu-id="6b21b-212">d.</span></span> <span data-ttu-id="6b21b-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="6b21b-214">Picturepark test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b21b-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="6b21b-215">Picturepark içine sipariş tooenable Azure AD kullanıcıların toolog bunların Picturepark sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b21b-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="6b21b-216">Picturepark Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6b21b-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="6b21b-217">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6b21b-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b21b-218">İçinde tooyour oturum **Picturepark** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="6b21b-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="6b21b-219">Merhaba üstte Hello araç çubuğunda **Yönetimsel Araçlar**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="6b21b-220">![Kullanıcıların](./media/active-directory-saas-picturepark-tutorial/ic795067.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="6b21b-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="6b21b-221">Merhaba, **kullanıcılara genel bakış** sekmesini tıklatın, **yeni**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="6b21b-222">![Kullanıcı Yönetimi](./media/active-directory-saas-picturepark-tutorial/ic795068.png "kullanıcı yönetimi")</span><span class="sxs-lookup"><span data-stu-id="6b21b-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="6b21b-223">Merhaba üzerinde **kullanıcı oluştur** iletişim kutusunda, hello gerçekleştirmek geçerli bir Azure Active Directory kullanıcı adımları izleyerek tooprovision istiyor:</span><span class="sxs-lookup"><span data-stu-id="6b21b-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="6b21b-224">![Kullanıcı oluşturma](./media/active-directory-saas-picturepark-tutorial/ic795069.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="6b21b-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="6b21b-225">a.</span><span class="sxs-lookup"><span data-stu-id="6b21b-225">a.</span></span> <span data-ttu-id="6b21b-226">Merhaba, **e-posta adresi** metin kutusuna, türü hello **e-posta adresi** hello kullanıcının  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6b21b-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="6b21b-227">b.</span><span class="sxs-lookup"><span data-stu-id="6b21b-227">b.</span></span> <span data-ttu-id="6b21b-228">Merhaba, **parola** ve **parolayı onayla** metin kutuları, türü hello **parola** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6b21b-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="6b21b-229">c.</span><span class="sxs-lookup"><span data-stu-id="6b21b-229">c.</span></span> <span data-ttu-id="6b21b-230">Merhaba, **ad** metin kutusuna, türü hello **ad** hello kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="6b21b-231">d.</span><span class="sxs-lookup"><span data-stu-id="6b21b-231">d.</span></span> <span data-ttu-id="6b21b-232">Merhaba, **Soyadı** metin kutusuna, türü hello **Soyadı** hello kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="6b21b-233">e.</span><span class="sxs-lookup"><span data-stu-id="6b21b-233">e.</span></span> <span data-ttu-id="6b21b-234">Merhaba, **şirket** metin kutusuna, türü hello **şirket adı** hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="6b21b-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="6b21b-235">f.</span><span class="sxs-lookup"><span data-stu-id="6b21b-235">f.</span></span> <span data-ttu-id="6b21b-236">Merhaba, **Ülke** metin kutusuna, select hello **Ülke** hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="6b21b-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="6b21b-237">g.</span><span class="sxs-lookup"><span data-stu-id="6b21b-237">g.</span></span> <span data-ttu-id="6b21b-238">Merhaba, **ZIP** metin kutusuna, türü hello **posta kodu** hello şehrin.</span><span class="sxs-lookup"><span data-stu-id="6b21b-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="6b21b-239">h.</span><span class="sxs-lookup"><span data-stu-id="6b21b-239">h.</span></span> <span data-ttu-id="6b21b-240">Merhaba, **Şehir** metin kutusuna, türü hello **şehir adı** hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="6b21b-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="6b21b-241">ı.</span><span class="sxs-lookup"><span data-stu-id="6b21b-241">i.</span></span> <span data-ttu-id="6b21b-242">Seçin bir **dil**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="6b21b-243">j.</span><span class="sxs-lookup"><span data-stu-id="6b21b-243">j.</span></span> <span data-ttu-id="6b21b-244">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b21b-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="6b21b-245">API'leri, Azure AD kullanıcı hesapları Picturepark tooprovision tarafından sağlanan veya herhangi diğer Picturepark kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b21b-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6b21b-246">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6b21b-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6b21b-247">Bu bölümde, erişim tooPicturepark vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b21b-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6b21b-249">**tooassign Britta Simon tooPicturepark hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6b21b-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b21b-250">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6b21b-252">Merhaba uygulamalar listesinde **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-252">In hello applications list, select **Picturepark**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="6b21b-254">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6b21b-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6b21b-256">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6b21b-256">Click **Add** button.</span></span> <span data-ttu-id="6b21b-257">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b21b-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6b21b-259">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6b21b-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6b21b-260">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b21b-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b21b-261">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b21b-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b21b-262">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6b21b-262">Testing single sign-on</span></span>

<span data-ttu-id="6b21b-263">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6b21b-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6b21b-264">Merhaba Picturepark hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Picturepark uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b21b-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="6b21b-265">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6b21b-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b21b-266">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6b21b-266">Additional resources</span></span>

* [<span data-ttu-id="6b21b-267">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6b21b-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b21b-268">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6b21b-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

