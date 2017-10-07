---
title: "Öğretici: Azure Active Directory Tümleştirme ile Allocadia | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Allocadia arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="9765d-103">Öğretici: Azure Active Directory Tümleştirme Allocadia ile</span><span class="sxs-lookup"><span data-stu-id="9765d-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="9765d-104">Bu öğreticide, bilgi nasıl toointegrate Allocadia Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9765d-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9765d-105">Allocadia Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9765d-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9765d-106">Erişim tooAllocadia sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9765d-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="9765d-107">Kullanıcıların tooautomatically get açan tooAllocadia (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9765d-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9765d-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9765d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9765d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9765d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9765d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9765d-110">Prerequisites</span></span>

<span data-ttu-id="9765d-111">tooconfigure Allocadia ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9765d-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="9765d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9765d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9765d-113">Bir Allocadia çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="9765d-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9765d-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9765d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9765d-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9765d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9765d-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9765d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9765d-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9765d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9765d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9765d-118">Scenario description</span></span>
<span data-ttu-id="9765d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9765d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9765d-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9765d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9765d-121">Merhaba Galerisi'nden Allocadia ekleme</span><span class="sxs-lookup"><span data-stu-id="9765d-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="9765d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9765d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="9765d-123">Merhaba Galerisi'nden Allocadia ekleme</span><span class="sxs-lookup"><span data-stu-id="9765d-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="9765d-124">Azure AD'ye tooconfigure hello tümleştirme Allocadia, tooadd Allocadia hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9765d-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9765d-125">**tooadd Allocadia hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9765d-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9765d-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9765d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9765d-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9765d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9765d-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9765d-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9765d-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9765d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9765d-133">Merhaba arama kutusuna yazın **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="9765d-133">In hello search box, type **Allocadia**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="9765d-135">Merhaba Sonuçlar panelinde seçin **Allocadia**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9765d-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9765d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9765d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9765d-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Allocadia ile test etme</span><span class="sxs-lookup"><span data-stu-id="9765d-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9765d-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Allocadia içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="9765d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="9765d-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Allocadia hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9765d-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="9765d-141">Merhaba hello değeri Allocadia içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="9765d-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9765d-142">tooconfigure ve Allocadia ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9765d-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9765d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="9765d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9765d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="9765d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9765d-145">**[Bir Allocadia test kullanıcısı oluşturma](#creating-an-allocadia-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Allocadia içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="9765d-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9765d-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9765d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9765d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="9765d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9765d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9765d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9765d-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Allocadia uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9765d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="9765d-150">**tooconfigure Azure AD çoklu oturum açma ile Allocadia, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9765d-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="9765d-151">Hello hello üzerinde Azure portal'ın **Allocadia** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9765d-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9765d-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9765d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="9765d-155">Merhaba üzerinde **Allocadia etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9765d-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="9765d-157">a.</span><span class="sxs-lookup"><span data-stu-id="9765d-157">a.</span></span> <span data-ttu-id="9765d-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="9765d-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="9765d-159">Test ortamı için-`https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="9765d-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="9765d-160">Üretim ortamı için-`https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="9765d-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="9765d-161">b.</span><span class="sxs-lookup"><span data-stu-id="9765d-161">b.</span></span> <span data-ttu-id="9765d-162">Merhaba, **yanıt URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="9765d-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="9765d-163">Test ortamı için-`https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="9765d-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="9765d-164">Üretim ortamı için-`https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="9765d-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9765d-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="9765d-165">These values are not real.</span></span> <span data-ttu-id="9765d-166">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9765d-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9765d-167">Kişi [Allocadia destek ekibi](mailTo:support@allocadia.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="9765d-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="9765d-168">Allocadia uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="9765d-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9765d-169">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9765d-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="9765d-170">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="9765d-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9765d-171">Ekran aşağıdaki hello Bu yapılandırmanın bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="9765d-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="9765d-173">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9765d-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="9765d-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="9765d-174">Attribute Name</span></span> | <span data-ttu-id="9765d-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="9765d-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="9765d-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="9765d-176">firstname</span></span> | <span data-ttu-id="9765d-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="9765d-177">user.givenname</span></span> |
    | <span data-ttu-id="9765d-178">Soyadı</span><span class="sxs-lookup"><span data-stu-id="9765d-178">lastname</span></span> | <span data-ttu-id="9765d-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="9765d-179">user.surname</span></span> |
    | <span data-ttu-id="9765d-180">E-posta</span><span class="sxs-lookup"><span data-stu-id="9765d-180">email</span></span> | <span data-ttu-id="9765d-181">User.Mail</span><span class="sxs-lookup"><span data-stu-id="9765d-181">user.mail</span></span> |
    
    <span data-ttu-id="9765d-182">a.</span><span class="sxs-lookup"><span data-stu-id="9765d-182">a.</span></span> <span data-ttu-id="9765d-183">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9765d-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="9765d-185">b.</span><span class="sxs-lookup"><span data-stu-id="9765d-185">b.</span></span> <span data-ttu-id="9765d-186">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="9765d-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9765d-188">c.</span><span class="sxs-lookup"><span data-stu-id="9765d-188">c.</span></span> <span data-ttu-id="9765d-189">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="9765d-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="9765d-190">d.</span><span class="sxs-lookup"><span data-stu-id="9765d-190">d.</span></span> <span data-ttu-id="9765d-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9765d-191">Click **Ok**.</span></span>



6. <span data-ttu-id="9765d-192">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9765d-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="9765d-194">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9765d-194">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9765d-196">tooconfigure çoklu oturum açma üzerinde **Allocadia** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[Allocadia destek ekibi](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="9765d-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="9765d-197">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9765d-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9765d-198">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9765d-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9765d-199">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="9765d-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9765d-200">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9765d-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9765d-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9765d-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="9765d-202">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9765d-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9765d-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9765d-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9765d-205">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9765d-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9765d-207">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9765d-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9765d-209">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="9765d-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9765d-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9765d-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9765d-213">a.</span><span class="sxs-lookup"><span data-stu-id="9765d-213">a.</span></span> <span data-ttu-id="9765d-214">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9765d-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9765d-215">b.</span><span class="sxs-lookup"><span data-stu-id="9765d-215">b.</span></span> <span data-ttu-id="9765d-216">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9765d-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9765d-217">c.</span><span class="sxs-lookup"><span data-stu-id="9765d-217">c.</span></span> <span data-ttu-id="9765d-218">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9765d-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9765d-219">d.</span><span class="sxs-lookup"><span data-stu-id="9765d-219">d.</span></span> <span data-ttu-id="9765d-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9765d-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="9765d-221">Bir Allocadia test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9765d-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="9765d-222">Uygulama, sadece kullanıcı zaman sağlama destekler.</span><span class="sxs-lookup"><span data-stu-id="9765d-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="9765d-223">Kimlik doğrulamasından sonra kullanıcılar hello uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9765d-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9765d-224">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9765d-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9765d-225">Bu bölümde, erişim tooAllocadia vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9765d-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9765d-227">**tooassign Britta Simon tooAllocadia hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9765d-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="9765d-228">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9765d-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9765d-230">Merhaba uygulamalar listesinde **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="9765d-230">In hello applications list, select **Allocadia**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="9765d-232">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9765d-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9765d-234">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9765d-234">Click **Add** button.</span></span> <span data-ttu-id="9765d-235">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9765d-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9765d-237">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9765d-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9765d-238">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9765d-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9765d-239">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9765d-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9765d-240">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9765d-240">Testing single sign-on</span></span>

<span data-ttu-id="9765d-241">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9765d-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9765d-242">Merhaba Allocadia hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Allocadia uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9765d-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="9765d-243">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="9765d-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9765d-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9765d-244">Additional resources</span></span>

* [<span data-ttu-id="9765d-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9765d-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9765d-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9765d-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

