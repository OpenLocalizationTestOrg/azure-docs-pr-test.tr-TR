---
title: "Öğretici: Azure Active Directory Tümleştirme ile Humanity | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Humanity arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="7b043-103">Öğretici: Azure Active Directory Tümleştirme Humanity ile</span><span class="sxs-lookup"><span data-stu-id="7b043-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="7b043-104">Bu öğreticide, bilgi nasıl toointegrate Humanity Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b043-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b043-105">Humanity Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7b043-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b043-106">Erişim tooHumanity sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7b043-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="7b043-107">Kullanıcıların tooautomatically get açan tooHumanity (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7b043-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b043-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7b043-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b043-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b043-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b043-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7b043-110">Prerequisites</span></span>

<span data-ttu-id="7b043-111">tooconfigure Humanity ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b043-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="7b043-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7b043-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b043-113">Bir Humanity çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7b043-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b043-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7b043-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b043-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b043-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b043-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7b043-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b043-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b043-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b043-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7b043-118">Scenario description</span></span>
<span data-ttu-id="7b043-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7b043-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b043-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7b043-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b043-121">Merhaba Galerisi'nden Humanity ekleme</span><span class="sxs-lookup"><span data-stu-id="7b043-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="7b043-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7b043-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="7b043-123">Merhaba Galerisi'nden Humanity ekleme</span><span class="sxs-lookup"><span data-stu-id="7b043-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="7b043-124">Azure AD'ye Humanity tooconfigure hello tümleştirilmesi, tooadd Humanity hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b043-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b043-125">**tooadd Humanity hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b043-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b043-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7b043-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b043-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7b043-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b043-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7b043-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7b043-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b043-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7b043-133">Merhaba arama kutusuna yazın **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="7b043-133">In hello search box, type **Humanity**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="7b043-135">Merhaba Sonuçlar panelinde seçin **Humanity**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7b043-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b043-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7b043-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b043-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Humanity ile test etme</span><span class="sxs-lookup"><span data-stu-id="7b043-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b043-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Humanity içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b043-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="7b043-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Humanity hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b043-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="7b043-141">Merhaba hello değeri Humanity içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7b043-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b043-142">tooconfigure ve Humanity ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b043-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b043-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7b043-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b043-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7b043-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b043-145">**[Humanity test kullanıcısı oluşturma](#creating-a-humanity-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Humanity içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7b043-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b043-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7b043-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b043-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7b043-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b043-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b043-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b043-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Humanity uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b043-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="7b043-150">**tooconfigure Azure AD çoklu oturum açma ile Humanity, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b043-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b043-151">Hello hello üzerinde Azure portal'ın **Humanity** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7b043-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7b043-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7b043-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="7b043-155">Merhaba üzerinde **Humanity etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b043-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="7b043-157">a.</span><span class="sxs-lookup"><span data-stu-id="7b043-157">a.</span></span> <span data-ttu-id="7b043-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="7b043-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="7b043-159">b.</span><span class="sxs-lookup"><span data-stu-id="7b043-159">b.</span></span> <span data-ttu-id="7b043-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="7b043-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b043-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7b043-161">These values are not real.</span></span> <span data-ttu-id="7b043-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b043-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7b043-163">Kişi [Humanity istemci destek ekibi](https://www.humanity.com/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7b043-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="7b043-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7b043-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="7b043-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b043-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b043-168">Merhaba üzerinde **Humanity yapılandırma** 'yi tıklatın **yapılandırma Humanity** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7b043-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b043-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si ve Sign-Out URL** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="7b043-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="7b043-171">Farklı web tarayıcısı penceresinde tooyour içinde oturum **Humanity** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="7b043-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="7b043-172">Hello içinde hello üst menüsünde **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="7b043-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="7b043-173">![Yönetici](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="7b043-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="7b043-174">Altında **tümleştirme**, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7b043-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="7b043-175">![Çoklu oturum açma](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="7b043-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="7b043-176">Merhaba, **çoklu oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b043-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7b043-177">![Çoklu oturum açma](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="7b043-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="7b043-178">a.</span><span class="sxs-lookup"><span data-stu-id="7b043-178">a.</span></span> <span data-ttu-id="7b043-179">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="7b043-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="7b043-180">b.</span><span class="sxs-lookup"><span data-stu-id="7b043-180">b.</span></span> <span data-ttu-id="7b043-181">Seçin **parola oturum açma izin**.</span><span class="sxs-lookup"><span data-stu-id="7b043-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="7b043-182">c.</span><span class="sxs-lookup"><span data-stu-id="7b043-182">c.</span></span> <span data-ttu-id="7b043-183">Yapıştır hello **SAML çoklu oturum açma hizmet URL'si** hello değerine **SAML veren URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7b043-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="7b043-184">d.</span><span class="sxs-lookup"><span data-stu-id="7b043-184">d.</span></span> <span data-ttu-id="7b043-185">Yapıştır hello **Sign-Out URL** hello değerine **uzak oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7b043-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="7b043-186">e.</span><span class="sxs-lookup"><span data-stu-id="7b043-186">e.</span></span> <span data-ttu-id="7b043-187">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7b043-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="7b043-188">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7b043-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="7b043-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7b043-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b043-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7b043-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b043-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b043-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b043-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b043-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b043-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b043-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7b043-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b043-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b043-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7b043-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b043-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7b043-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b043-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b043-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b043-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b043-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b043-204">a.</span><span class="sxs-lookup"><span data-stu-id="7b043-204">a.</span></span> <span data-ttu-id="7b043-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b043-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b043-206">b.</span><span class="sxs-lookup"><span data-stu-id="7b043-206">b.</span></span> <span data-ttu-id="7b043-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7b043-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b043-208">c.</span><span class="sxs-lookup"><span data-stu-id="7b043-208">c.</span></span> <span data-ttu-id="7b043-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7b043-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b043-210">d.</span><span class="sxs-lookup"><span data-stu-id="7b043-210">d.</span></span> <span data-ttu-id="7b043-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b043-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="7b043-212">Humanity test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b043-212">Creating a Humanity test user</span></span>

<span data-ttu-id="7b043-213">TooHumanity içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Humanity sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b043-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="7b043-214">Humanity Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="7b043-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="7b043-215">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b043-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b043-216">İçinde tooyour oturum **Humanity** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="7b043-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="7b043-217">Tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="7b043-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="7b043-218">![Yönetici](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="7b043-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="7b043-219">Tıklatın **personel**.</span><span class="sxs-lookup"><span data-stu-id="7b043-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="7b043-220">![Personel](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "personel")</span><span class="sxs-lookup"><span data-stu-id="7b043-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="7b043-221">Altında **Eylemler**, tıklatın **eklemek çalışanlar**.</span><span class="sxs-lookup"><span data-stu-id="7b043-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="7b043-222">![Çalışanlar eklemek](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "çalışanları ekleme")</span><span class="sxs-lookup"><span data-stu-id="7b043-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="7b043-223">Merhaba, **eklemek çalışanlar** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b043-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7b043-224">![Çalışanlar Kaydet](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "çalışanlar Kaydet")</span><span class="sxs-lookup"><span data-stu-id="7b043-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="7b043-225">a.</span><span class="sxs-lookup"><span data-stu-id="7b043-225">a.</span></span> <span data-ttu-id="7b043-226">Türü hello **ad**, **Soyadı**, ve **e-posta** , metin kutuları hello tooprovision istediğiniz geçerli bir AAD hesabıyla ilgili.</span><span class="sxs-lookup"><span data-stu-id="7b043-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="7b043-227">b.</span><span class="sxs-lookup"><span data-stu-id="7b043-227">b.</span></span> <span data-ttu-id="7b043-228">Tıklatın **çalışanlar kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7b043-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="7b043-229">API AAD kullanıcı hesaplarının Humanity tooprovision tarafından sağlanan veya herhangi diğer Humanity kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b043-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7b043-230">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7b043-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7b043-231">Bu bölümde, erişim tooHumanity vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b043-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7b043-233">**tooassign Britta Simon tooHumanity hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b043-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b043-234">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7b043-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7b043-236">Merhaba uygulamalar listesinde **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="7b043-236">In hello applications list, select **Humanity**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="7b043-238">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7b043-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7b043-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b043-240">Click **Add** button.</span></span> <span data-ttu-id="7b043-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b043-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7b043-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7b043-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b043-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b043-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b043-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b043-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b043-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7b043-246">Testing single sign-on</span></span>

<span data-ttu-id="7b043-247">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7b043-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b043-248">Merhaba Humanity hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Humanity uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b043-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="7b043-249">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b043-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b043-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7b043-250">Additional resources</span></span>

* [<span data-ttu-id="7b043-251">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7b043-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b043-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7b043-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

