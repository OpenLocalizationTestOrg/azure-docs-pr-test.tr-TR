---
title: "Öğretici: Azure Active Directory Tümleştirme ile Domo | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Domo arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: cc70f8e5013f864d275762bbc1f84bd9677e8c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="0fe5a-103">Öğretici: Azure Active Directory Tümleştirme Domo ile</span><span class="sxs-lookup"><span data-stu-id="0fe5a-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="0fe5a-104">Bu öğreticide, bilgi nasıl toointegrate Domo Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fe5a-104">In this tutorial, you learn how toointegrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fe5a-105">Domo Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-105">Integrating Domo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0fe5a-106">Erişim tooDomo sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0fe5a-106">You can control in Azure AD who has access tooDomo</span></span>
- <span data-ttu-id="0fe5a-107">Kullanıcıların tooautomatically get açan tooDomo (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0fe5a-107">You can enable your users tooautomatically get signed-on tooDomo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fe5a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0fe5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0fe5a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fe5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fe5a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0fe5a-110">Prerequisites</span></span>

<span data-ttu-id="0fe5a-111">tooconfigure Domo ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-111">tooconfigure Azure AD integration with Domo, you need hello following items:</span></span>

- <span data-ttu-id="0fe5a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0fe5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fe5a-113">Bir Domo çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0fe5a-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fe5a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fe5a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fe5a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fe5a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fe5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fe5a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0fe5a-118">Scenario description</span></span>
<span data-ttu-id="0fe5a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fe5a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fe5a-121">Merhaba Galerisi'nden Domo ekleme</span><span class="sxs-lookup"><span data-stu-id="0fe5a-121">Adding Domo from hello gallery</span></span>
2. <span data-ttu-id="0fe5a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0fe5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-hello-gallery"></a><span data-ttu-id="0fe5a-123">Merhaba Galerisi'nden Domo ekleme</span><span class="sxs-lookup"><span data-stu-id="0fe5a-123">Adding Domo from hello gallery</span></span>
<span data-ttu-id="0fe5a-124">Azure AD'ye tooconfigure hello tümleştirme Domo, tooadd Domo hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-124">tooconfigure hello integration of Domo into Azure AD, you need tooadd Domo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0fe5a-125">**tooadd Domo hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fe5a-125">**tooadd Domo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe5a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fe5a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0fe5a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0fe5a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0fe5a-133">Merhaba arama kutusuna yazın **Domo**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-133">In hello search box, type **Domo**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="0fe5a-135">Merhaba Sonuçlar panelinde seçin **Domo**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-135">In hello results panel, select **Domo**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fe5a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0fe5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fe5a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Domo ile test etme</span><span class="sxs-lookup"><span data-stu-id="0fe5a-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0fe5a-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Domo içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Domo is tooa user in Azure AD.</span></span> <span data-ttu-id="0fe5a-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Domo hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-140">In other words, a link relationship between an Azure AD user and hello related user in Domo needs toobe established.</span></span>

<span data-ttu-id="0fe5a-141">Merhaba hello değeri Domo içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-141">In Domo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0fe5a-142">tooconfigure ve Domo ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-142">tooconfigure and test Azure AD single sign-on with Domo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0fe5a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0fe5a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fe5a-145">**[Domo test kullanıcısı oluşturma](#creating-a-domo-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Domo içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - toohave a counterpart of Britta Simon in Domo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fe5a-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fe5a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fe5a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0fe5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fe5a-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Domo uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="0fe5a-150">**tooconfigure Azure AD çoklu oturum açma ile Domo, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fe5a-150">**tooconfigure Azure AD single sign-on with Domo, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe5a-151">Hello hello üzerinde Azure portal'ın **Domo** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-151">In hello Azure portal, on hello **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0fe5a-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="0fe5a-155">Merhaba üzerinde **Domo etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-155">On hello **Domo Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="0fe5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-157">a.</span></span> <span data-ttu-id="0fe5a-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="0fe5a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="0fe5a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-159">b.</span></span> <span data-ttu-id="0fe5a-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="0fe5a-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-161">These values are not real.</span></span> <span data-ttu-id="0fe5a-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0fe5a-163">Kişi [Domo istemci destek ekibi](mailto:support@domo.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-163">Contact [Domo Client support team](mailto:support@domo.com) tooget these values.</span></span>

4. <span data-ttu-id="0fe5a-164">Domo uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-164">Domo application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0fe5a-165">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="0fe5a-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0fe5a-167">Ekran aşağıdaki hello Bu yapılandırmanın bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-167">hello following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="0fe5a-169">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="0fe5a-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="0fe5a-170">Attribute Name</span></span> | <span data-ttu-id="0fe5a-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="0fe5a-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="0fe5a-172">ad</span><span class="sxs-lookup"><span data-stu-id="0fe5a-172">name</span></span> | <span data-ttu-id="0fe5a-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="0fe5a-173">user.displayname</span></span> |
    | <span data-ttu-id="0fe5a-174">E-posta</span><span class="sxs-lookup"><span data-stu-id="0fe5a-174">email</span></span> | <span data-ttu-id="0fe5a-175">User.Mail</span><span class="sxs-lookup"><span data-stu-id="0fe5a-175">user.mail</span></span> |
    
    <span data-ttu-id="0fe5a-176">a.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-176">a.</span></span> <span data-ttu-id="0fe5a-177">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0fe5a-180">b.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-180">b.</span></span> <span data-ttu-id="0fe5a-181">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0fe5a-182">c.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-182">c.</span></span> <span data-ttu-id="0fe5a-183">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0fe5a-184">d.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-184">d.</span></span> <span data-ttu-id="0fe5a-185">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="0fe5a-186">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-186">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="0fe5a-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-188">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="0fe5a-190">Merhaba üzerinde **Domo yapılandırma** 'yi tıklatın **yapılandırma Domo** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-190">On hello **Domo Configuration** section, click **Configure Domo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0fe5a-191">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="0fe5a-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="0fe5a-193">tooconfigure çoklu oturum açma üzerinde **Domo** yan, indirilen toosend hello ihtiyacınız **sertifika**, **SAML varlık kimliği**, hello **SAML çoklu oturum açma hizmeti URL** ve hello **Sign-Out URL** çok[Domo destek ekibi](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="0fe5a-193">tooconfigure single sign-on on **Domo** side, you need toosend hello downloaded **Certificate**, **SAML Entity ID**, hello **SAML Single Sign-On Service URL** and hello **Sign-Out URL** too[Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="0fe5a-194">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-194">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0fe5a-195">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="0fe5a-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0fe5a-196">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0fe5a-197">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0fe5a-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fe5a-198">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fe5a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fe5a-199">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0fe5a-201">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fe5a-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe5a-202">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fe5a-204">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fe5a-206">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fe5a-208">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0fe5a-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fe5a-210">a.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-210">a.</span></span> <span data-ttu-id="0fe5a-211">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fe5a-212">b.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-212">b.</span></span> <span data-ttu-id="0fe5a-213">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fe5a-214">c.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-214">c.</span></span> <span data-ttu-id="0fe5a-215">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0fe5a-216">d.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-216">d.</span></span> <span data-ttu-id="0fe5a-217">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="0fe5a-218">Domo test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fe5a-218">Creating a Domo test user</span></span>

<span data-ttu-id="0fe5a-219">Bu bölümde Hello amacı toocreate Britta Simon içinde Domo adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-219">hello objective of this section is toocreate a user called Britta Simon in Domo.</span></span> <span data-ttu-id="0fe5a-220">Domo yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0fe5a-221">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-221">There is no action item for you in this section.</span></span> <span data-ttu-id="0fe5a-222">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Domo sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-222">A new user is created during an attempt tooaccess Domo if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0fe5a-223">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0fe5a-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0fe5a-224">Bu bölümde, erişim tooDomo vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDomo.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0fe5a-226">**tooassign Britta Simon tooDomo hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0fe5a-226">**tooassign Britta Simon tooDomo, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe5a-227">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0fe5a-229">Merhaba uygulamalar listesinde **Domo**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-229">In hello applications list, select **Domo**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="0fe5a-231">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0fe5a-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-233">Click **Add** button.</span></span> <span data-ttu-id="0fe5a-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0fe5a-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0fe5a-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fe5a-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fe5a-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0fe5a-239">Testing single sign-on</span></span>

<span data-ttu-id="0fe5a-240">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="0fe5a-241">Merhaba Domo hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Domo uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0fe5a-241">When you click hello Domo tile in hello Access Panel, you should get automatically signed-on tooyour Domo application.</span></span>

<span data-ttu-id="0fe5a-242">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0fe5a-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0fe5a-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0fe5a-243">Additional resources</span></span>

* [<span data-ttu-id="0fe5a-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0fe5a-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fe5a-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0fe5a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

