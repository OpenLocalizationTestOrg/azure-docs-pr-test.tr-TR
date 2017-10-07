---
title: "Öğretici: Azure Active Directory Tümleştirme ile görüntü geçiş | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve görüntü geçiş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="2a6b5-103">Öğretici: Azure Active Directory Tümleştirme ile görüntü geçişi</span><span class="sxs-lookup"><span data-stu-id="2a6b5-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="2a6b5-104">Bu öğreticide, bilgi nasıl toointegrate görüntü geçiş Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a6b5-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a6b5-105">Görüntü geçiş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2a6b5-106">Erişim tooImage geçiş sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2a6b5-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="2a6b5-107">Kullanıcıların tooautomatically get açan tooImage geçişi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2a6b5-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a6b5-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2a6b5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2a6b5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a6b5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a6b5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2a6b5-110">Prerequisites</span></span>

<span data-ttu-id="2a6b5-111">tooconfigure görüntü geçiş ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="2a6b5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2a6b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a6b5-113">Bir görüntü geçiş çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2a6b5-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a6b5-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a6b5-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a6b5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a6b5-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a6b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a6b5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2a6b5-118">Scenario description</span></span>
<span data-ttu-id="2a6b5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a6b5-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a6b5-121">Görüntü geçiş hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="2a6b5-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="2a6b5-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2a6b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="2a6b5-123">Görüntü geçiş hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="2a6b5-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="2a6b5-124">Azure AD'ye tooconfigure hello tümleştirme görüntü geçişinin hello galeri tooyour yönetilen SaaS uygulamaları listesinden görüntü geçiş tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2a6b5-125">**tooadd görüntü geçiş hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a6b5-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a6b5-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a6b5-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2a6b5-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2a6b5-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2a6b5-133">Merhaba arama kutusuna yazın **görüntü geçiş**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-133">In hello search box, type **Image Relay**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="2a6b5-135">Merhaba Sonuçlar panelinde seçin **görüntü geçiş**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a6b5-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2a6b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a6b5-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma görüntü "Britta Simon" adlı bir test kullanıcı tabanlı geçiş ile test etme.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a6b5-139">Tek toowork'ın oturum açma hangi hello karşılık gelen görüntü geçiş içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="2a6b5-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve görüntü geçiş hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="2a6b5-141">Görüntü geçiş hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2a6b5-142">tooconfigure ve görüntü geçiş ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2a6b5-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2a6b5-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a6b5-145">**[Bir görüntü geçiş test kullanıcısı oluşturma](#creating-an-image-relay-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir görüntü geçiş içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a6b5-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a6b5-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a6b5-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2a6b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a6b5-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma görüntü geçiş uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="2a6b5-150">**tooconfigure Azure AD çoklu oturum açma görüntü geçiş ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a6b5-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a6b5-151">Merhaba hello üzerinde Azure portal'ın **görüntü geçiş** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2a6b5-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="2a6b5-155">Merhaba üzerinde **görüntü geçiş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="2a6b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-157">a.</span></span> <span data-ttu-id="2a6b5-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="2a6b5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="2a6b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-159">b.</span></span> <span data-ttu-id="2a6b5-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="2a6b5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a6b5-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-161">These values are not real.</span></span> <span data-ttu-id="2a6b5-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2a6b5-163">Kişi [görüntü geçiş istemci destek ekibi](http://support.imagerelay.com/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="2a6b5-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="2a6b5-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2a6b5-168">Merhaba üzerinde **görüntü geçiş yapılandırma** 'yi tıklatın **yapılandırma görüntü geçiş** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2a6b5-169">Kopya hello **Sign-Out hizmet URL'sini ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2a6b5-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="2a6b5-171">Başka bir tarayıcı penceresinde tooyour görüntü geçiş şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="2a6b5-172">Merhaba hello üstte Hello araç çubuğunda tıklatın **kullanıcılar ve izinler** iş yükü.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="2a6b5-174">Tıklatın **oluşturma yeni izni**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-174">Click **Create New Permission**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="2a6b5-176">Merhaba, **tek oturum açma ayarları** iş yükü, select hello **bu grup için yalnızca oturum açma aracılığıyla çoklu oturum açma** onay kutusunu işaretleyin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="2a6b5-178">Çok Git**hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-178">Go too**Account Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="2a6b5-180">Toohello Git **tek oturum açma ayarları** iş yükü.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="2a6b5-182">Merhaba üzerinde **SAML ayarları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="2a6b5-184">a.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-184">a.</span></span> <span data-ttu-id="2a6b5-185">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2a6b5-186">b.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-186">b.</span></span> <span data-ttu-id="2a6b5-187">İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **tek Sign-Out hizmeti URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2a6b5-188">c.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-188">c.</span></span> <span data-ttu-id="2a6b5-189">Olarak **ad kimliği biçimi**seçin **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="2a6b5-190">d.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-190">d.</span></span> <span data-ttu-id="2a6b5-191">Olarak **bağlama seçenekleri hello hizmet sağlayıcısı (görüntü geçiş) gelen istekleri için**seçin **POST bağlama**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="2a6b5-192">e.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-192">e.</span></span> <span data-ttu-id="2a6b5-193">Altında **x.509 sertifikası**, tıklatın **güncelleştirme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="2a6b5-195">f.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-195">f.</span></span> <span data-ttu-id="2a6b5-196">İndirilen hello sertifika Not Defteri'nde açın, hello içeriği Kopyala ve hello x.509 sertifikası metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="2a6b5-198">g.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-198">g.</span></span> <span data-ttu-id="2a6b5-199">İçinde **Just-In-Time kullanıcı sağlamayı** bölümü, select hello **Just-In-Time kullanıcı sağlamayı etkinleştirin**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="2a6b5-201">h.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-201">h.</span></span> <span data-ttu-id="2a6b5-202">Select hello izin grubu (örneğin, **SSO temel**) içinde toosign çoklu oturum açma yalnızca aracılığıyla izin.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="2a6b5-204">ı.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-204">i.</span></span> <span data-ttu-id="2a6b5-205">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2a6b5-206">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2a6b5-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2a6b5-207">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2a6b5-208">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2a6b5-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a6b5-209">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a6b5-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a6b5-210">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2a6b5-212">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a6b5-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a6b5-213">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a6b5-215">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a6b5-217">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a6b5-219">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a6b5-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a6b5-221">a.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-221">a.</span></span> <span data-ttu-id="2a6b5-222">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a6b5-223">b.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-223">b.</span></span> <span data-ttu-id="2a6b5-224">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a6b5-225">c.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-225">c.</span></span> <span data-ttu-id="2a6b5-226">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2a6b5-227">d.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-227">d.</span></span> <span data-ttu-id="2a6b5-228">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="2a6b5-229">Bir görüntü geçiş test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a6b5-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="2a6b5-230">Bu bölümde Hello amacı toocreate de görüntü geçişi Britta Simon adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="2a6b5-231">**toocreate Britta Simon görüntü geçiş adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a6b5-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a6b5-232">Yönetici olarak oturum açma tooyour görüntü geçiş şirket sitesi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="2a6b5-233">Çok Git**kullanıcılar ve izinler** seçip **SSO kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="2a6b5-235">Merhaba girin **e-posta**, **ad**, **Soyadı**, ve **şirket** hello kullanıcısı tooprovision ve select hello izin grubu istediğiniz (örneğin, SSO temel) yalnızca çoklu oturum açma oturum açarak hello grup olduğu.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="2a6b5-237">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2a6b5-238">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2a6b5-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2a6b5-239">Bu bölümde, erişim tooImage geçiş vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2a6b5-241">**tooassign Britta Simon tooImage geçiş hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a6b5-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a6b5-242">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2a6b5-244">Merhaba uygulamalar listesinde **görüntü geçiş**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-244">In hello applications list, select **Image Relay**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="2a6b5-246">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2a6b5-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-248">Click **Add** button.</span></span> <span data-ttu-id="2a6b5-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2a6b5-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2a6b5-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a6b5-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2a6b5-254">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2a6b5-254">Testing single sign-on</span></span>

<span data-ttu-id="2a6b5-255">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="2a6b5-256">Merhaba görüntü geçiş hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour görüntü geçiş uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a6b5-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2a6b5-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2a6b5-257">Additional resources</span></span>

* [<span data-ttu-id="2a6b5-258">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2a6b5-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a6b5-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2a6b5-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

