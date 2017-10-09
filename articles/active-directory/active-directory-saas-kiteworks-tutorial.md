---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kiteworks | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Kiteworks arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="90423-103">Öğretici: Azure Active Directory Tümleştirme Kiteworks ile</span><span class="sxs-lookup"><span data-stu-id="90423-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="90423-104">Bu öğreticide, bilgi nasıl toointegrate Kiteworks Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90423-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90423-105">Kiteworks Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="90423-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90423-106">Erişim tooKiteworks sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="90423-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="90423-107">Kullanıcıların tooautomatically get açan tooKiteworks (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="90423-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90423-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="90423-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="90423-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90423-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90423-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="90423-110">Prerequisites</span></span>

<span data-ttu-id="90423-111">tooconfigure Kiteworks ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="90423-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="90423-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="90423-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90423-113">Bir Kiteworks çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="90423-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90423-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="90423-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90423-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="90423-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90423-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="90423-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90423-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90423-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90423-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="90423-118">Scenario description</span></span>
<span data-ttu-id="90423-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="90423-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90423-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="90423-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90423-121">Merhaba Galerisi'nden Kiteworks ekleme</span><span class="sxs-lookup"><span data-stu-id="90423-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="90423-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="90423-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="90423-123">Merhaba Galerisi'nden Kiteworks ekleme</span><span class="sxs-lookup"><span data-stu-id="90423-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="90423-124">Azure AD'ye tooconfigure hello tümleştirme Kiteworks, tooadd Kiteworks hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="90423-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90423-125">**tooadd Kiteworks hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90423-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90423-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="90423-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90423-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="90423-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90423-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="90423-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="90423-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90423-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="90423-133">Merhaba arama kutusuna yazın **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="90423-133">In hello search box, type **Kiteworks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="90423-135">Merhaba Sonuçlar panelinde seçin **Kiteworks**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="90423-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90423-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="90423-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90423-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kiteworks sınayın.</span><span class="sxs-lookup"><span data-stu-id="90423-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="90423-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Kiteworks içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="90423-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="90423-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Kiteworks hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="90423-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="90423-141">Merhaba hello değeri Kiteworks içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="90423-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="90423-142">tooconfigure ve Kiteworks ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="90423-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90423-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="90423-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90423-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="90423-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90423-145">**[Kiteworks test kullanıcısı oluşturma](#creating-a-kiteworks-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Kiteworks içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="90423-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="90423-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="90423-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90423-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="90423-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90423-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90423-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90423-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Kiteworks uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="90423-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="90423-150">**tooconfigure Azure AD çoklu oturum açma ile Kiteworks, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90423-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="90423-151">Hello hello üzerinde Azure portal'ın **Kiteworks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="90423-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="90423-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="90423-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="90423-155">Merhaba üzerinde **Kiteworks etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90423-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="90423-157">a.</span><span class="sxs-lookup"><span data-stu-id="90423-157">a.</span></span> <span data-ttu-id="90423-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="90423-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="90423-159">b.</span><span class="sxs-lookup"><span data-stu-id="90423-159">b.</span></span> <span data-ttu-id="90423-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="90423-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90423-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="90423-161">These values are not real.</span></span> <span data-ttu-id="90423-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="90423-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="90423-163">Kişi [Kiteworks istemci destek ekibi](http://accellion.com/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="90423-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="90423-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90423-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="90423-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90423-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90423-168">Merhaba üzerinde **Kiteworks yapılandırma** 'yi tıklatın **yapılandırma Kiteworks** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="90423-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="90423-169">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="90423-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="90423-171">Üzerinde tooyour Kiteworks şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="90423-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="90423-172">Merhaba üstte Hello araç çubuğunda **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="90423-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="90423-174">Merhaba, **kimlik doğrulama ve yetkilendirme** 'yi tıklatın **SSO Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="90423-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="90423-176">Merhaba SSO Kurulum sayfasında hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90423-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="90423-178">a.</span><span class="sxs-lookup"><span data-stu-id="90423-178">a.</span></span> <span data-ttu-id="90423-179">Seçin **SSO kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="90423-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="90423-180">b.</span><span class="sxs-lookup"><span data-stu-id="90423-180">b.</span></span> <span data-ttu-id="90423-181">Seçin **başlatmak AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="90423-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="90423-182">c.</span><span class="sxs-lookup"><span data-stu-id="90423-182">c.</span></span> <span data-ttu-id="90423-183">Merhaba, **IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="90423-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="90423-184">d.</span><span class="sxs-lookup"><span data-stu-id="90423-184">d.</span></span> <span data-ttu-id="90423-185">Merhaba, **çoklu oturum açma hizmet URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="90423-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="90423-186">e.</span><span class="sxs-lookup"><span data-stu-id="90423-186">e.</span></span> <span data-ttu-id="90423-187">Merhaba, **tek oturum kapatma hizmeti URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="90423-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="90423-188">f.</span><span class="sxs-lookup"><span data-stu-id="90423-188">f.</span></span> <span data-ttu-id="90423-189">İndirilen sertifikanızı kopyalama Merhaba içeriğine Not Defteri'nde açın ve hello yapıştırma **RSA ortak anahtar sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="90423-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="90423-190">g.</span><span class="sxs-lookup"><span data-stu-id="90423-190">g.</span></span> <span data-ttu-id="90423-191">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90423-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="90423-192">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="90423-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="90423-193">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="90423-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="90423-194">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="90423-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90423-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90423-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="90423-196">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="90423-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="90423-198">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90423-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90423-199">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="90423-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90423-201">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="90423-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90423-203">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="90423-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90423-205">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="90423-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90423-207">a.</span><span class="sxs-lookup"><span data-stu-id="90423-207">a.</span></span> <span data-ttu-id="90423-208">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90423-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90423-209">b.</span><span class="sxs-lookup"><span data-stu-id="90423-209">b.</span></span> <span data-ttu-id="90423-210">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="90423-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90423-211">c.</span><span class="sxs-lookup"><span data-stu-id="90423-211">c.</span></span> <span data-ttu-id="90423-212">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="90423-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90423-213">d.</span><span class="sxs-lookup"><span data-stu-id="90423-213">d.</span></span> <span data-ttu-id="90423-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90423-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="90423-215">Kiteworks test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90423-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="90423-216">Bu bölümde Hello amacı toocreate Britta Simon içinde Kiteworks adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="90423-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="90423-217">Kiteworks yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="90423-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="90423-218">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="90423-218">There is no action item for you in this section.</span></span> <span data-ttu-id="90423-219">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Kitewors sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="90423-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="90423-220">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [Kiteworks destek ekibi](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="90423-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90423-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="90423-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90423-222">Bu bölümde, erişim tooKiteworks vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="90423-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="90423-224">**tooassign Britta Simon tooKiteworks hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="90423-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="90423-225">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="90423-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="90423-227">Merhaba uygulamalar listesinde **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="90423-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="90423-229">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="90423-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="90423-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90423-231">Click **Add** button.</span></span> <span data-ttu-id="90423-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="90423-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="90423-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="90423-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90423-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="90423-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90423-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="90423-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90423-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="90423-237">Testing single sign-on</span></span>

<span data-ttu-id="90423-238">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="90423-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="90423-239">Hello erişim paneli Kiteworks döşeme hello tıkladığınızda, otomatik olarak oturum açma Kiteworks uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="90423-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90423-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="90423-240">Additional resources</span></span>

* [<span data-ttu-id="90423-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="90423-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90423-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="90423-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

