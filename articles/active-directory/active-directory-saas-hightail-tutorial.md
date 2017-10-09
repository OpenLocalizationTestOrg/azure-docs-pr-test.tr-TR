---
title: "Öğretici: Azure Active Directory Tümleştirme ile Hightail | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Hightail arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="a797b-103">Öğretici: Azure Active Directory Tümleştirme Hightail ile</span><span class="sxs-lookup"><span data-stu-id="a797b-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="a797b-104">Bu öğreticide, bilgi nasıl toointegrate Hightail Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="a797b-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a797b-105">Hightail Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a797b-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a797b-106">Erişim tooHightail sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a797b-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="a797b-107">Kullanıcıların tooautomatically get açan tooHightail (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a797b-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a797b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a797b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a797b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a797b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a797b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a797b-110">Prerequisites</span></span>

<span data-ttu-id="a797b-111">tooconfigure Hightail ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a797b-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="a797b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a797b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a797b-113">Bir Hightail çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a797b-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a797b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a797b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a797b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a797b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a797b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a797b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a797b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a797b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a797b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a797b-118">Scenario description</span></span>
<span data-ttu-id="a797b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a797b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a797b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a797b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a797b-121">Merhaba Galerisi'nden Hightail ekleme</span><span class="sxs-lookup"><span data-stu-id="a797b-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="a797b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a797b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="a797b-123">Merhaba Galerisi'nden Hightail ekleme</span><span class="sxs-lookup"><span data-stu-id="a797b-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="a797b-124">Azure AD'ye tooconfigure hello tümleştirme Hightail, tooadd Hightail hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a797b-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a797b-125">**tooadd Hightail hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a797b-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a797b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a797b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a797b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a797b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a797b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a797b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a797b-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a797b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a797b-133">Merhaba arama kutusuna yazın **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="a797b-133">In hello search box, type **Hightail**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="a797b-135">Merhaba Sonuçlar panelinde seçin **Hightail**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a797b-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a797b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a797b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a797b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Hightail sınayın.</span><span class="sxs-lookup"><span data-stu-id="a797b-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a797b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Hightail içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a797b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="a797b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Hightail hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a797b-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="a797b-141">Merhaba hello değeri Hightail içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a797b-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a797b-142">tooconfigure ve Hightail ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a797b-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a797b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a797b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a797b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a797b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a797b-145">**[Hightail test kullanıcısı oluşturma](#creating-a-hightail-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Hightail içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a797b-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a797b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a797b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a797b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a797b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a797b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a797b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a797b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Hightail uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a797b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="a797b-150">**tooconfigure Azure AD çoklu oturum açma ile Hightail, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a797b-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="a797b-151">Hello hello üzerinde Azure portal'ın **Hightail** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a797b-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a797b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a797b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="a797b-155">Merhaba üzerinde **Hightail etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a797b-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="a797b-157">Merhaba, **yanıt URL'si** metin kutusuna, türü hello URL'si olarak:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="a797b-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a797b-158">Merhaba önceki değeri gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="a797b-158">hello preceding value is not real value.</span></span> <span data-ttu-id="a797b-159">Merhaba değeri hello öğreticinin ilerleyen bölümlerinde açıklanan hello gerçek yanıt URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a797b-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="a797b-160">Merhaba üzerinde **Hightail etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a797b-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="a797b-162">a.</span><span class="sxs-lookup"><span data-stu-id="a797b-162">a.</span></span> <span data-ttu-id="a797b-163">Merhaba tıklatın **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a797b-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a797b-164">b.</span><span class="sxs-lookup"><span data-stu-id="a797b-164">b.</span></span> <span data-ttu-id="a797b-165">Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü hello URL'si olarak:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="a797b-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="a797b-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a797b-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="a797b-168">Hightail uygulama belirli bir biçimde hello SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="a797b-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a797b-169">Lütfen bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a797b-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="a797b-170">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Atrribute"** hello uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="a797b-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="a797b-171">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="a797b-171">hello following screenshot shows an example for this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="a797b-173">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a797b-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a797b-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="a797b-174">Attribute Name</span></span> | <span data-ttu-id="a797b-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="a797b-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="a797b-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="a797b-176">FirstName</span></span> | <span data-ttu-id="a797b-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="a797b-177">user.givenname</span></span> |
    | <span data-ttu-id="a797b-178">Soyadı</span><span class="sxs-lookup"><span data-stu-id="a797b-178">LastName</span></span> | <span data-ttu-id="a797b-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="a797b-179">user.surname</span></span> |
    | <span data-ttu-id="a797b-180">E-posta</span><span class="sxs-lookup"><span data-stu-id="a797b-180">Email</span></span> | <span data-ttu-id="a797b-181">User.Mail</span><span class="sxs-lookup"><span data-stu-id="a797b-181">user.mail</span></span> |    
    | <span data-ttu-id="a797b-182">Userıdentity</span><span class="sxs-lookup"><span data-stu-id="a797b-182">UserIdentity</span></span> | <span data-ttu-id="a797b-183">User.Mail</span><span class="sxs-lookup"><span data-stu-id="a797b-183">user.mail</span></span> |
    
    <span data-ttu-id="a797b-184">a.</span><span class="sxs-lookup"><span data-stu-id="a797b-184">a.</span></span> <span data-ttu-id="a797b-185">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a797b-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="a797b-188">b.</span><span class="sxs-lookup"><span data-stu-id="a797b-188">b.</span></span> <span data-ttu-id="a797b-189">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="a797b-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="a797b-190">c.</span><span class="sxs-lookup"><span data-stu-id="a797b-190">c.</span></span> <span data-ttu-id="a797b-191">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="a797b-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="a797b-192">d.</span><span class="sxs-lookup"><span data-stu-id="a797b-192">d.</span></span> <span data-ttu-id="a797b-193">Merhaba bırakın **Namespace** boş.</span><span class="sxs-lookup"><span data-stu-id="a797b-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="a797b-194">e.</span><span class="sxs-lookup"><span data-stu-id="a797b-194">e.</span></span> <span data-ttu-id="a797b-195">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a797b-195">Click **Ok**.</span></span>

7. <span data-ttu-id="a797b-196">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a797b-196">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a797b-198">Merhaba üzerinde **Hightail yapılandırma** 'yi tıklatın **yapılandırma Hightail** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a797b-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a797b-199">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="a797b-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="a797b-201">Çoklu oturum açma Hello Hightail uygulamaya yapılandırmadan önce lütfen beyaz liste Hightail ile e-posta etki alanınızın ekip tüm bu etki alanını kullanan kullanıcılar hello çoklu oturum açma işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a797b-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="a797b-202">Uygulamanız için yapılandırılmış SSO tooget, toosign üzerinde tooyour Hightail Kiracı yönetici olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="a797b-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="a797b-203">a.</span><span class="sxs-lookup"><span data-stu-id="a797b-203">a.</span></span> <span data-ttu-id="a797b-204">Hello'nde hello üstte, hello menüsünü **hesap** sekmesinde ve seçin **SAML yapılandırmak**.</span><span class="sxs-lookup"><span data-stu-id="a797b-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="a797b-206">b.</span><span class="sxs-lookup"><span data-stu-id="a797b-206">b.</span></span> <span data-ttu-id="a797b-207">Hello onay kutusunu seçin **SAML kimlik doğrulamasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="a797b-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="a797b-209">c.</span><span class="sxs-lookup"><span data-stu-id="a797b-209">c.</span></span> <span data-ttu-id="a797b-210">Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **SAML belirteç imzalama sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a797b-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="a797b-212">d.</span><span class="sxs-lookup"><span data-stu-id="a797b-212">d.</span></span> <span data-ttu-id="a797b-213">Merhaba, **SAML yetkilisi (Kimlik sağlayıcısı)** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalandığından.</span><span class="sxs-lookup"><span data-stu-id="a797b-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="a797b-215">e.</span><span class="sxs-lookup"><span data-stu-id="a797b-215">e.</span></span> <span data-ttu-id="a797b-216">Tooconfigure hello uygulamada istiyorsanız **IDP başlatılan modu** seçin **"Kimlik sağlayıcıyı (IDP) başlatılan oturum açma"**.</span><span class="sxs-lookup"><span data-stu-id="a797b-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="a797b-217">Varsa **SP tarafından başlatılan modu** seçin **"Hizmet sağlayıcısı (SP) başlatılan oturum açma"**.</span><span class="sxs-lookup"><span data-stu-id="a797b-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="a797b-219">f.</span><span class="sxs-lookup"><span data-stu-id="a797b-219">f.</span></span> <span data-ttu-id="a797b-220">Örneğiniz için Hello SAML tüketici URL'sini kopyalayın ve yapıştırın **yanıt URL'si** metin kutusuna **Hightail etki alanı ve URL'leri** Azure Portal'daki bölümü.</span><span class="sxs-lookup"><span data-stu-id="a797b-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="a797b-221">g.</span><span class="sxs-lookup"><span data-stu-id="a797b-221">g.</span></span> <span data-ttu-id="a797b-222">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a797b-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a797b-223">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a797b-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a797b-224">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a797b-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a797b-225">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a797b-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a797b-226">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a797b-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="a797b-227">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a797b-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a797b-229">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a797b-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a797b-230">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a797b-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a797b-232">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a797b-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a797b-234">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a797b-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a797b-236">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a797b-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a797b-238">a.</span><span class="sxs-lookup"><span data-stu-id="a797b-238">a.</span></span> <span data-ttu-id="a797b-239">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a797b-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a797b-240">b.</span><span class="sxs-lookup"><span data-stu-id="a797b-240">b.</span></span> <span data-ttu-id="a797b-241">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a797b-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a797b-242">c.</span><span class="sxs-lookup"><span data-stu-id="a797b-242">c.</span></span> <span data-ttu-id="a797b-243">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a797b-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a797b-244">d.</span><span class="sxs-lookup"><span data-stu-id="a797b-244">d.</span></span> <span data-ttu-id="a797b-245">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a797b-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="a797b-246">Hightail test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a797b-246">Creating a Hightail test user</span></span>

<span data-ttu-id="a797b-247">Bu bölümde Hello amacı toocreate Britta Simon içinde Hightail adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="a797b-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="a797b-248">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="a797b-248">There is no action item for you in this section.</span></span> <span data-ttu-id="a797b-249">Yalnızca zaman kullanıcı sağlamayı hello özel taleplere dayanarak destekler hightail.</span><span class="sxs-lookup"><span data-stu-id="a797b-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="a797b-250">Merhaba özel talep hello bölümünde gösterildiği gibi yapılandırdıysanız  **[yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on)**  yukarıdaki kullanıcı henüz yok hello uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a797b-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="a797b-251">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [Hightail destek ekibi](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="a797b-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a797b-252">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a797b-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a797b-253">Bu bölümde, erişim tooHightail vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a797b-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a797b-255">**tooassign Britta Simon tooHightail hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a797b-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="a797b-256">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a797b-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a797b-258">Merhaba uygulamalar listesinde **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="a797b-258">In hello applications list, select **Hightail**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="a797b-260">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a797b-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a797b-262">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a797b-262">Click **Add** button.</span></span> <span data-ttu-id="a797b-263">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a797b-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a797b-265">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a797b-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a797b-266">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a797b-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a797b-267">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a797b-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a797b-268">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a797b-268">Testing single sign-on</span></span>

<span data-ttu-id="a797b-269">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a797b-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a797b-270">Merhaba Hightail hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Hightail uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a797b-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a797b-271">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a797b-271">Additional resources</span></span>

* [<span data-ttu-id="a797b-272">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a797b-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a797b-273">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a797b-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

