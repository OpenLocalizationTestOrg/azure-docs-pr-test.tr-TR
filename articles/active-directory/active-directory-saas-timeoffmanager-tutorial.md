---
title: "Öğretici: Azure Active Directory Tümleştirme ile TimeOffManager | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TimeOffManager arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="d7b59-103">Öğretici: Azure Active Directory Tümleştirme TimeOffManager ile</span><span class="sxs-lookup"><span data-stu-id="d7b59-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="d7b59-104">Bu öğreticide, bilgi nasıl toointegrate TimeOffManager Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7b59-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7b59-105">TimeOffManager Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d7b59-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7b59-106">Erişim tooTimeOffManager sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7b59-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="d7b59-107">Kullanıcıların tooautomatically get açan tooTimeOffManager (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7b59-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7b59-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d7b59-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d7b59-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7b59-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7b59-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7b59-110">Prerequisites</span></span>

<span data-ttu-id="d7b59-111">tooconfigure TimeOffManager ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7b59-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="d7b59-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d7b59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7b59-113">Bir TimeOffManager çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d7b59-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7b59-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d7b59-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7b59-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7b59-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7b59-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d7b59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7b59-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7b59-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7b59-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d7b59-118">Scenario description</span></span>
<span data-ttu-id="d7b59-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d7b59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7b59-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d7b59-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7b59-121">Merhaba Galerisi'nden TimeOffManager ekleme</span><span class="sxs-lookup"><span data-stu-id="d7b59-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="d7b59-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d7b59-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="d7b59-123">Merhaba Galerisi'nden TimeOffManager ekleme</span><span class="sxs-lookup"><span data-stu-id="d7b59-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="d7b59-124">Azure AD'ye tooconfigure hello tümleştirme TimeOffManager, tooadd TimeOffManager hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7b59-125">**tooadd TimeOffManager hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7b59-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7b59-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7b59-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d7b59-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d7b59-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d7b59-133">Merhaba arama kutusuna yazın **TimeOffManager**seçin **TimeOffManager** sonuç paneli ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d7b59-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Galerisi'nden ekleme](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d7b59-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d7b59-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d7b59-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı TimeOffManager sınayın.</span><span class="sxs-lookup"><span data-stu-id="d7b59-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7b59-137">Tek toowork'ın oturum açma hangi hello karşılık gelen TimeOffManager içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="d7b59-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı TimeOffManager hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="d7b59-139">Merhaba hello değeri TimeOffManager içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d7b59-140">tooconfigure ve TimeOffManager ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7b59-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7b59-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d7b59-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7b59-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d7b59-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7b59-143">**[TimeOffManager test kullanıcısı oluşturma](#create-a-timeoffmanager-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir TimeOffManager içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d7b59-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7b59-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d7b59-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7b59-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d7b59-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d7b59-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d7b59-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d7b59-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma TimeOffManager uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d7b59-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="d7b59-148">**tooconfigure Azure AD çoklu oturum açma ile TimeOffManager, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7b59-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7b59-149">Hello hello üzerinde Azure portal'ın **TimeOffManager** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d7b59-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d7b59-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML oturum açma tabanlı](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="d7b59-153">Merhaba üzerinde **TimeOffManager etki alanı ve URL'leri** bölümünde, hello aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="d7b59-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![TimeOffManager etki alanı ve URL'ler bölümü](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="d7b59-155">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="d7b59-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7b59-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="d7b59-156">This value is not real.</span></span> <span data-ttu-id="d7b59-157">Bu değer hello gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7b59-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="d7b59-158">Bu değerden alabilirsiniz **çoklu oturum açma ayarları sayfasında** daha sonra hello öğretici veya kişi içinde açıklanan [TimeOffManager destek ekibi](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7b59-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="d7b59-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7b59-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="d7b59-161">Bu bölümde Hello amacı nasıl tooenable kullanıcılar tooauthenticate tooTimeOffManger Federasyon kullanarak Azure AD'de hesabıyla hello SAML protokolünü temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="d7b59-162">TimeOffManger uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="d7b59-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="d7b59-163">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="d7b59-164">![SAML belirteci öznitelikleri](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml belirteci öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="d7b59-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="d7b59-165">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="d7b59-165">Attribute Name</span></span> | <span data-ttu-id="d7b59-166">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="d7b59-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d7b59-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="d7b59-167">Firstname</span></span> |<span data-ttu-id="d7b59-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="d7b59-168">User.givenname</span></span> |
    | <span data-ttu-id="d7b59-169">Soyadı</span><span class="sxs-lookup"><span data-stu-id="d7b59-169">Lastname</span></span> |<span data-ttu-id="d7b59-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="d7b59-170">User.surname</span></span> |
    | <span data-ttu-id="d7b59-171">E-posta</span><span class="sxs-lookup"><span data-stu-id="d7b59-171">Email</span></span> |<span data-ttu-id="d7b59-172">User.Mail</span><span class="sxs-lookup"><span data-stu-id="d7b59-172">User.mail</span></span> |
    
    <span data-ttu-id="d7b59-173">a.</span><span class="sxs-lookup"><span data-stu-id="d7b59-173">a.</span></span>  <span data-ttu-id="d7b59-174">Yukarıdaki hello tablosundaki her veri satırı için tıklatın **kullanıcı özniteliği eklemek**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="d7b59-175">![SAML belirteci öznitelikleri](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml belirteci öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="d7b59-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="d7b59-176">![SAML belirteci öznitelikleri](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml belirteci öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="d7b59-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="d7b59-177">b.</span><span class="sxs-lookup"><span data-stu-id="d7b59-177">b.</span></span>  <span data-ttu-id="d7b59-178">Merhaba, **öznitelik adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="d7b59-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d7b59-179">c.</span><span class="sxs-lookup"><span data-stu-id="d7b59-179">c.</span></span>  <span data-ttu-id="d7b59-180">Merhaba, **öznitelik değeri** metin kutusuna, ilgili satır için gösterilen select hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="d7b59-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="d7b59-181">d.</span><span class="sxs-lookup"><span data-stu-id="d7b59-181">d.</span></span>  <span data-ttu-id="d7b59-182">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7b59-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="d7b59-183">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-183">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d7b59-185">Merhaba üzerinde **TimeOffManager yapılandırma** 'yi tıklatın **yapılandırma TimeOffManager** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d7b59-186">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d7b59-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TimeOffManager yapılandırma bölümü](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="d7b59-188">Farklı web tarayıcısı penceresinde TimeOffManager şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d7b59-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="d7b59-189">Çok Git**hesap \> Hesap seçenekleri \> çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="d7b59-190">![Çoklu oturum açma ayarları](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="d7b59-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="d7b59-191">Merhaba, **çoklu oturum açma ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7b59-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d7b59-192">![Çoklu oturum açma ayarları](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="d7b59-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="d7b59-193">a.</span><span class="sxs-lookup"><span data-stu-id="d7b59-193">a.</span></span> <span data-ttu-id="d7b59-194">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve ardından yapıştırın içine tüm sertifika hello **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d7b59-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="d7b59-195">b.</span><span class="sxs-lookup"><span data-stu-id="d7b59-195">b.</span></span> <span data-ttu-id="d7b59-196">İçinde **IDP veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d7b59-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="d7b59-197">c.</span><span class="sxs-lookup"><span data-stu-id="d7b59-197">c.</span></span> <span data-ttu-id="d7b59-198">İçinde **IDP uç nokta URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d7b59-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="d7b59-199">d.</span><span class="sxs-lookup"><span data-stu-id="d7b59-199">d.</span></span> <span data-ttu-id="d7b59-200">Olarak **zorunlu SAML**seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="d7b59-201">e.</span><span class="sxs-lookup"><span data-stu-id="d7b59-201">e.</span></span> <span data-ttu-id="d7b59-202">Olarak **otomatik olarak oluşturma kullanıcıların**seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="d7b59-203">f.</span><span class="sxs-lookup"><span data-stu-id="d7b59-203">f.</span></span> <span data-ttu-id="d7b59-204">İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d7b59-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="d7b59-205">g.</span><span class="sxs-lookup"><span data-stu-id="d7b59-205">g.</span></span> <span data-ttu-id="d7b59-206">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="d7b59-207">İçinde **çoklu oturum açma ayarları** sayfası, kopyalama hello değerini **onaylama tüketici hizmeti URL'si** hello yapıştırın **yanıt URL'si** metin kutusu altında **TimeOffManager Etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="d7b59-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="d7b59-208">![Çoklu oturum açma ayarları](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="d7b59-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="d7b59-209">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d7b59-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d7b59-210">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d7b59-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d7b59-211">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7b59-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d7b59-212">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7b59-212">Create an Azure AD test user</span></span>
<span data-ttu-id="d7b59-213">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d7b59-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d7b59-215">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7b59-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7b59-216">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7b59-218">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların ve grupların tüm kullanıcılar-->](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7b59-220">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7b59-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7b59-222">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7b59-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7b59-224">a.</span><span class="sxs-lookup"><span data-stu-id="d7b59-224">a.</span></span> <span data-ttu-id="d7b59-225">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7b59-226">b.</span><span class="sxs-lookup"><span data-stu-id="d7b59-226">b.</span></span> <span data-ttu-id="d7b59-227">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d7b59-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7b59-228">c.</span><span class="sxs-lookup"><span data-stu-id="d7b59-228">c.</span></span> <span data-ttu-id="d7b59-229">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d7b59-230">d.</span><span class="sxs-lookup"><span data-stu-id="d7b59-230">d.</span></span> <span data-ttu-id="d7b59-231">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7b59-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="d7b59-232">TimeOffManager test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7b59-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="d7b59-233">Sağlanan tooTimeOffManager TimeOffManager içine sipariş tooenable Azure AD kullanıcıların toolog içinde olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="d7b59-234">Yalnızca zaman sağlama kullanıcı TimeOffManager destekler.</span><span class="sxs-lookup"><span data-stu-id="d7b59-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="d7b59-235">Sizin için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="d7b59-235">There is no action item for you.</span></span>  

<span data-ttu-id="d7b59-236">Merhaba kullanıcılar, çoklu oturum açma kullanarak hello ilk oturum açma sırasında otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="d7b59-237">API'leri, Azure AD kullanıcı hesapları TimeOffManager tooprovision tarafından sağlanan veya herhangi diğer TimeOffManager kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7b59-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d7b59-238">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="d7b59-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d7b59-239">Bu bölümde, erişim tooTimeOffManager vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7b59-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d7b59-241">**tooassign Britta Simon tooTimeOffManager hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7b59-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7b59-242">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d7b59-244">Merhaba uygulamalar listesinde **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![Uygulama listesinde TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="d7b59-246">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d7b59-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d7b59-248">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7b59-248">Click **Add** button.</span></span> <span data-ttu-id="d7b59-249">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7b59-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d7b59-251">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d7b59-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d7b59-252">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7b59-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7b59-253">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7b59-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d7b59-254">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="d7b59-254">Test single sign-on</span></span>

<span data-ttu-id="d7b59-255">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d7b59-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7b59-256">Merhaba TimeOffManager hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour TimeOffManager uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7b59-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="d7b59-257">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7b59-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7b59-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d7b59-258">Additional resources</span></span>

* [<span data-ttu-id="d7b59-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d7b59-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7b59-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d7b59-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

