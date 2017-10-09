---
title: "Öğretici: Azure Active Directory Tümleştirme ile Klue | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Klue arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="bddfe-103">Öğretici: Azure Active Directory Tümleştirme Klue ile</span><span class="sxs-lookup"><span data-stu-id="bddfe-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="bddfe-104">Bu öğreticide, bilgi nasıl toointegrate Klue Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bddfe-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bddfe-105">Klue Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bddfe-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bddfe-106">Erişim tooKlue sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bddfe-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="bddfe-107">Kullanıcıların tooautomatically get açan tooKlue (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bddfe-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bddfe-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bddfe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bddfe-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bddfe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bddfe-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bddfe-110">Prerequisites</span></span>

<span data-ttu-id="bddfe-111">tooconfigure Klue ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bddfe-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="bddfe-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bddfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bddfe-113">Bir Klue çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="bddfe-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bddfe-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bddfe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bddfe-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bddfe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bddfe-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bddfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bddfe-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bddfe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bddfe-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bddfe-118">Scenario description</span></span>
<span data-ttu-id="bddfe-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bddfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bddfe-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bddfe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bddfe-121">Merhaba Galerisi'nden Klue ekleme</span><span class="sxs-lookup"><span data-stu-id="bddfe-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="bddfe-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bddfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="bddfe-123">Merhaba Galerisi'nden Klue ekleme</span><span class="sxs-lookup"><span data-stu-id="bddfe-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="bddfe-124">Azure AD'ye tooconfigure hello tümleştirme Klue, tooadd Klue hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bddfe-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bddfe-125">**tooadd Klue hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bddfe-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bddfe-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bddfe-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bddfe-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bddfe-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bddfe-133">Merhaba arama kutusuna yazın **Klue**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-133">In hello search box, type **Klue**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="bddfe-135">Merhaba Sonuçlar panelinde seçin **Klue**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bddfe-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bddfe-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bddfe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bddfe-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Klue sınayın.</span><span class="sxs-lookup"><span data-stu-id="bddfe-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bddfe-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Klue içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="bddfe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="bddfe-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Klue hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bddfe-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="bddfe-141">Merhaba hello değeri Klue içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bddfe-142">tooconfigure ve Klue ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bddfe-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bddfe-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="bddfe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bddfe-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="bddfe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bddfe-145">**[Klue test kullanıcısı oluşturma](#creating-a-klue-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Klue içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="bddfe-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bddfe-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bddfe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bddfe-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="bddfe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bddfe-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bddfe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bddfe-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Klue uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bddfe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="bddfe-150">**tooconfigure Azure AD çoklu oturum açma ile Klue, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bddfe-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="bddfe-151">Hello hello üzerinde Azure portal'ın **Klue** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bddfe-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bddfe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="bddfe-155">Merhaba üzerinde **Klue etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="bddfe-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="bddfe-157">a.</span><span class="sxs-lookup"><span data-stu-id="bddfe-157">a.</span></span> <span data-ttu-id="bddfe-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="bddfe-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="bddfe-159">b.</span><span class="sxs-lookup"><span data-stu-id="bddfe-159">b.</span></span> <span data-ttu-id="bddfe-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="bddfe-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="bddfe-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="bddfe-162">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="bddfe-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="bddfe-164">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="bddfe-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bddfe-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="bddfe-165">These values are not real.</span></span> <span data-ttu-id="bddfe-166">Bu değerleri hello gerçek yanıt URL'si, tanımlayıcı ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bddfe-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="bddfe-167">Kişi [Klue istemci destek ekibi](mailto:support@klue.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="bddfe-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="bddfe-168">Merhaba Klue uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="bddfe-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="bddfe-169">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="bddfe-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="bddfe-171">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği görüntü önceki hello gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bddfe-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="bddfe-172">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="bddfe-172">Attribute Name</span></span>      | <span data-ttu-id="bddfe-173">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="bddfe-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="bddfe-174">ilk_ad</span><span class="sxs-lookup"><span data-stu-id="bddfe-174">first_name</span></span>          | <span data-ttu-id="bddfe-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="bddfe-175">user.givenname</span></span> |
    | <span data-ttu-id="bddfe-176">Soyadı</span><span class="sxs-lookup"><span data-stu-id="bddfe-176">last_name</span></span>           | <span data-ttu-id="bddfe-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="bddfe-177">user.surname</span></span> |
    | <span data-ttu-id="bddfe-178">E-posta</span><span class="sxs-lookup"><span data-stu-id="bddfe-178">email</span></span>               | <span data-ttu-id="bddfe-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="bddfe-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="bddfe-180">a.</span><span class="sxs-lookup"><span data-stu-id="bddfe-180">a.</span></span> <span data-ttu-id="bddfe-181">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bddfe-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bddfe-184">b.</span><span class="sxs-lookup"><span data-stu-id="bddfe-184">b.</span></span> <span data-ttu-id="bddfe-185">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="bddfe-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="bddfe-186">c.</span><span class="sxs-lookup"><span data-stu-id="bddfe-186">c.</span></span> <span data-ttu-id="bddfe-187">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="bddfe-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bddfe-188">d.</span><span class="sxs-lookup"><span data-stu-id="bddfe-188">d.</span></span> <span data-ttu-id="bddfe-189">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bddfe-189">Click **Ok**.</span></span>

7. <span data-ttu-id="bddfe-190">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bddfe-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="bddfe-192">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-192">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="bddfe-194">Merhaba üzerinde **Klue yapılandırma** 'yi tıklatın **yapılandırma Klue** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bddfe-195">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="bddfe-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="bddfe-197">tooconfigure çoklu oturum açma üzerinde **Klue** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64), SAML çoklu oturum açma hizmet URL'si ve SAML varlık kimliği** çok[Klue destek ekibi](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="bddfe-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="bddfe-198">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bddfe-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bddfe-199">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="bddfe-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bddfe-200">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bddfe-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bddfe-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bddfe-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="bddfe-202">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="bddfe-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bddfe-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bddfe-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bddfe-205">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bddfe-207">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bddfe-209">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="bddfe-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bddfe-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bddfe-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bddfe-213">a.</span><span class="sxs-lookup"><span data-stu-id="bddfe-213">a.</span></span> <span data-ttu-id="bddfe-214">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bddfe-215">b.</span><span class="sxs-lookup"><span data-stu-id="bddfe-215">b.</span></span> <span data-ttu-id="bddfe-216">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="bddfe-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bddfe-217">c.</span><span class="sxs-lookup"><span data-stu-id="bddfe-217">c.</span></span> <span data-ttu-id="bddfe-218">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bddfe-219">d.</span><span class="sxs-lookup"><span data-stu-id="bddfe-219">d.</span></span> <span data-ttu-id="bddfe-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bddfe-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="bddfe-221">Klue test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bddfe-221">Creating a Klue test user</span></span>

<span data-ttu-id="bddfe-222">Bu bölümde Hello amacı toocreate Britta Simon içinde Klue adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="bddfe-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="bddfe-223">Klue yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="bddfe-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="bddfe-224">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="bddfe-224">There is no action item for you in this section.</span></span> <span data-ttu-id="bddfe-225">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess Klue sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bddfe-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="bddfe-226">El ile bir kullanıcıyla iletişim toocreate gerekiyorsa [Klue destek ekibi](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="bddfe-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bddfe-227">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bddfe-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bddfe-228">Bu bölümde, erişim tooKlue vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bddfe-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bddfe-230">**tooassign Britta Simon tooKlue hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bddfe-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="bddfe-231">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bddfe-233">Merhaba uygulamalar listesinde **Klue**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-233">In hello applications list, select **Klue**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="bddfe-235">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bddfe-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bddfe-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bddfe-237">Click **Add** button.</span></span> <span data-ttu-id="bddfe-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bddfe-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bddfe-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bddfe-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bddfe-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bddfe-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bddfe-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bddfe-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bddfe-243">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bddfe-243">Testing single sign-on</span></span>

<span data-ttu-id="bddfe-244">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="bddfe-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bddfe-245">Merhaba Klue hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Klue uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bddfe-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="bddfe-246">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bddfe-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bddfe-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bddfe-247">Additional resources</span></span>

* [<span data-ttu-id="bddfe-248">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bddfe-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bddfe-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bddfe-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

