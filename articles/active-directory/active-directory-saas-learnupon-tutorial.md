---
title: "Öğretici: Azure Active Directory Tümleştirme ile LearnUpon | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LearnUpon arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="0e214-103">Öğretici: Azure Active Directory Tümleştirme LearnUpon ile</span><span class="sxs-lookup"><span data-stu-id="0e214-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="0e214-104">Bu öğreticide, bilgi nasıl toointegrate LearnUpon Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e214-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e214-105">LearnUpon Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0e214-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e214-106">Erişim tooLearnUpon sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0e214-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="0e214-107">Kullanıcıların tooautomatically get açan tooLearnUpon (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0e214-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e214-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0e214-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e214-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e214-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e214-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0e214-110">Prerequisites</span></span>

<span data-ttu-id="0e214-111">tooconfigure LearnUpon ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e214-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="0e214-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0e214-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e214-113">Bir LearnUpon çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="0e214-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e214-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0e214-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e214-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e214-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e214-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0e214-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e214-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e214-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e214-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0e214-118">Scenario description</span></span>
<span data-ttu-id="0e214-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0e214-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e214-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0e214-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e214-121">Merhaba Galerisi'nden LearnUpon ekleme</span><span class="sxs-lookup"><span data-stu-id="0e214-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="0e214-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0e214-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="0e214-123">Merhaba Galerisi'nden LearnUpon ekleme</span><span class="sxs-lookup"><span data-stu-id="0e214-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="0e214-124">Azure AD'ye tooconfigure hello tümleştirme LearnUpon, tooadd LearnUpon hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e214-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e214-125">**tooadd LearnUpon hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e214-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e214-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0e214-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e214-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0e214-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e214-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0e214-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0e214-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e214-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0e214-133">Merhaba arama kutusuna yazın **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="0e214-133">In hello search box, type **LearnUpon**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="0e214-135">Merhaba Sonuçlar panelinde seçin **LearnUpon**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0e214-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e214-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0e214-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e214-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LearnUpon sınayın.</span><span class="sxs-lookup"><span data-stu-id="0e214-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e214-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LearnUpon içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e214-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="0e214-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LearnUpon hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e214-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="0e214-141">Merhaba hello değeri LearnUpon içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="0e214-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e214-142">tooconfigure ve LearnUpon ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e214-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e214-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0e214-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e214-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0e214-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e214-145">**[LearnUpon test kullanıcısı oluşturma](#creating-a-learnupon-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LearnUpon içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0e214-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e214-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0e214-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e214-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0e214-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e214-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0e214-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e214-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LearnUpon uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0e214-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="0e214-150">**tooconfigure Azure AD çoklu oturum açma ile LearnUpon, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e214-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e214-151">Hello hello üzerinde Azure portal'ın **LearnUpon** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0e214-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0e214-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0e214-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="0e214-155">Merhaba üzerinde **LearnUpon etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e214-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="0e214-157">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="0e214-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e214-158">Lütfen bu hello gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e214-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="0e214-159">tooupdate hello gerçek yanıt URL'si ile bu değere sahip.</span><span class="sxs-lookup"><span data-stu-id="0e214-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="0e214-160">Bu değer tooget başvurun [LearnUpon destek ekibi](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="0e214-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="0e214-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e214-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="0e214-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e214-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e214-165">Merhaba üzerinde **LearnUpon yapılandırma** 'yi tıklatın **yapılandırma LearnUpon** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0e214-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e214-166">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0e214-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="0e214-168">Başka bir tarayıcı örneği ve oturum açma LearnUpon bir yönetici hesabıyla açın.</span><span class="sxs-lookup"><span data-stu-id="0e214-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="0e214-169">Merhaba tıklatın **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0e214-169">Click hello **settings** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="0e214-171">Tıklatın **çoklu oturum açma - SAML**ve ardından **genel ayarları** tooconfigure SAML ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0e214-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="0e214-173">Merhaba, **genel ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e214-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="0e214-175">a.</span><span class="sxs-lookup"><span data-stu-id="0e214-175">a.</span></span> <span data-ttu-id="0e214-176">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="0e214-176">Select **Enabled**.</span></span>

    <span data-ttu-id="0e214-177">b.</span><span class="sxs-lookup"><span data-stu-id="0e214-177">b.</span></span> <span data-ttu-id="0e214-178">Seçin **sürüm** olarak **2.0**.</span><span class="sxs-lookup"><span data-stu-id="0e214-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="0e214-179">c.</span><span class="sxs-lookup"><span data-stu-id="0e214-179">c.</span></span> <span data-ttu-id="0e214-180">Seçin **Skip koşullar** olarak **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="0e214-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="0e214-181">d.</span><span class="sxs-lookup"><span data-stu-id="0e214-181">d.</span></span> <span data-ttu-id="0e214-182">Merhaba, **SAML belirteci sonrası parametre adı** metin kutusuna, tür hello adı doğrulandı ve kimlik doğrulaması - örneğin hello SAML onayı toobe içeren SAML tüketici URL belirtilen yukarıda isteği post parametresi toohello  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="0e214-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="0e214-183">e.</span><span class="sxs-lookup"><span data-stu-id="0e214-183">e.</span></span> <span data-ttu-id="0e214-184">Merhaba, **ad tanımlayıcısı biçimi** metin kutusuna, türü hello SAML onayı hello kullanıcılarınızın tanımlayıcısı (e-posta adresi) - örneğin bulunduğu gösteren bir değer **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="0e214-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="0e214-185">f.</span><span class="sxs-lookup"><span data-stu-id="0e214-185">f.</span></span> <span data-ttu-id="0e214-186">Merhaba, **tanımlamak sağlayıcı konumu** metin kutusuna, türü hello kullanıcılar tooif gönderilen hello burada gösteren bir değer bunlar tıklayın, Azure portalı oturum açma ekranından karşıya yüklenen simge.</span><span class="sxs-lookup"><span data-stu-id="0e214-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="0e214-187">g.</span><span class="sxs-lookup"><span data-stu-id="0e214-187">g.</span></span> <span data-ttu-id="0e214-188">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello **Sign-Out URL** hello Azure portal ' Kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="0e214-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="0e214-189">h.</span><span class="sxs-lookup"><span data-stu-id="0e214-189">h.</span></span> <span data-ttu-id="0e214-190">Tıklatın **parmak baskı siparişi yönetmek**ve indirilen sertifikanızın hello parmak izi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e214-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="0e214-191">Tıklatın **kullanıcı ayarlarını**ve ardından hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e214-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="0e214-193">a.</span><span class="sxs-lookup"><span data-stu-id="0e214-193">a.</span></span> <span data-ttu-id="0e214-194">Merhaba, **ilk ad tanımlayıcısı biçimi** metin kutusuna, bize, SAML onayı hello kullanıcılar firstname burada içinde söyler türü hello değeri bulunduğu - örneğin: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="0e214-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="0e214-195">b.</span><span class="sxs-lookup"><span data-stu-id="0e214-195">b.</span></span> <span data-ttu-id="0e214-196">Merhaba, **son ad tanımlayıcısı biçimi** metin kutusuna, bize, SAML onayı hello kullanıcılar lastname burada içinde söyler türü hello değeri bulunduğu - örneğin: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="0e214-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="0e214-197">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0e214-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e214-198">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0e214-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e214-199">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e214-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e214-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e214-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e214-201">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0e214-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0e214-203">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e214-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e214-204">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0e214-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e214-206">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0e214-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e214-208">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e214-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e214-210">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0e214-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e214-212">a.</span><span class="sxs-lookup"><span data-stu-id="0e214-212">a.</span></span> <span data-ttu-id="0e214-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e214-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e214-214">b.</span><span class="sxs-lookup"><span data-stu-id="0e214-214">b.</span></span> <span data-ttu-id="0e214-215">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0e214-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e214-216">c.</span><span class="sxs-lookup"><span data-stu-id="0e214-216">c.</span></span> <span data-ttu-id="0e214-217">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0e214-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e214-218">d.</span><span class="sxs-lookup"><span data-stu-id="0e214-218">d.</span></span> <span data-ttu-id="0e214-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e214-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="0e214-220">LearnUpon test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e214-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="0e214-221">Bu bölümde Hello amacı toocreate Britta Simon içinde LearnUpon adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="0e214-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="0e214-222">LearnUpon yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="0e214-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0e214-223">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="0e214-223">There is no action item for you in this section.</span></span> <span data-ttu-id="0e214-224">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess LearnUpon sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0e214-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="0e214-225">[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0e214-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="0e214-226">Bir kullanıcı toocreate el ile gerekiyorsa, toocontact gerek [LearnUpon destek ekibi](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="0e214-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e214-227">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0e214-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e214-228">Bu bölümde, erişim tooLearnUpon vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e214-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0e214-230">**tooassign Britta Simon tooLearnUpon hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0e214-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e214-231">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0e214-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0e214-233">Merhaba uygulamalar listesinde **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="0e214-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="0e214-235">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0e214-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0e214-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0e214-237">Click **Add** button.</span></span> <span data-ttu-id="0e214-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e214-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0e214-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0e214-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e214-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e214-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e214-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0e214-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e214-243">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0e214-243">Testing single sign-on</span></span>

<span data-ttu-id="0e214-244">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0e214-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e214-245">Merhaba LearnUpon hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour LearnUpon uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e214-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="0e214-246">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e214-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e214-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0e214-247">Additional resources</span></span>

* [<span data-ttu-id="0e214-248">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0e214-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e214-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0e214-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

