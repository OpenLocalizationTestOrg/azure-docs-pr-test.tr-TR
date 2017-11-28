---
title: "Öğretici: Azure Active Directory Tümleştirme ile Clever | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Clever arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="a79f4-103">Öğretici: Azure Active Directory Tümleştirme Clever ile</span><span class="sxs-lookup"><span data-stu-id="a79f4-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="a79f4-104">Bu öğreticide, bilgi nasıl toointegrate Clever Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a79f4-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a79f4-105">Clever Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a79f4-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a79f4-106">Erişim tooClever sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a79f4-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="a79f4-107">Kullanıcıların tooautomatically get açan tooClever (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a79f4-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a79f4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a79f4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a79f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a79f4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a79f4-110">Prerequisites</span></span>

<span data-ttu-id="a79f4-111">tooconfigure Clever ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a79f4-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="a79f4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a79f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a79f4-113">Bir akıllı çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a79f4-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a79f4-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a79f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a79f4-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a79f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a79f4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a79f4-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a79f4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a79f4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a79f4-118">Scenario description</span></span>
<span data-ttu-id="a79f4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a79f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a79f4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a79f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a79f4-121">Merhaba Galerisi'nden Clever ekleme</span><span class="sxs-lookup"><span data-stu-id="a79f4-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="a79f4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a79f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="a79f4-123">Merhaba Galerisi'nden Clever ekleme</span><span class="sxs-lookup"><span data-stu-id="a79f4-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="a79f4-124">Azure AD'ye tooconfigure hello tümleştirme Clever, tooadd Clever hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a79f4-125">**tooadd Clever hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a79f4-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79f4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a79f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="a79f4-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a79f4-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="a79f4-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a79f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="a79f4-133">Merhaba arama kutusuna yazın **Clever**seçin **Clever** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a79f4-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Akıllı hello sonuçları listesinde](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a79f4-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a79f4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a79f4-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Clever sınayın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a79f4-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Clever içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="a79f4-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Clever hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="a79f4-139">Merhaba hello değeri Clever içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a79f4-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a79f4-140">tooconfigure ve Clever ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a79f4-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a79f4-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a79f4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a79f4-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a79f4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a79f4-143">**[Akıllı test kullanıcısı oluşturma](#create-a-clever-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Clever içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a79f4-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a79f4-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a79f4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a79f4-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a79f4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a79f4-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a79f4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a79f4-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma akıllı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="a79f4-148">**tooconfigure Azure AD çoklu oturum açma ile Clever, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a79f4-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79f4-149">Hello hello üzerinde Azure portal'ın **Clever** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="a79f4-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a79f4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="a79f4-153">Merhaba üzerinde **akıllı etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a79f4-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Akıllı etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="a79f4-155">a.</span><span class="sxs-lookup"><span data-stu-id="a79f4-155">a.</span></span> <span data-ttu-id="a79f4-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="a79f4-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="a79f4-157">b.</span><span class="sxs-lookup"><span data-stu-id="a79f4-157">b.</span></span> <span data-ttu-id="a79f4-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="a79f4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a79f4-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-159">These values are not real.</span></span> <span data-ttu-id="a79f4-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a79f4-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a79f4-161">Kişi [akıllı istemci destek ekibi](https://clever.com/about/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="a79f4-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="a79f4-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a79f4-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="a79f4-164">Merhaba akıllı uygulama bekliyor hello SAML onaylar tooadd özel öznitelik eşlemelerini tooyour gerektiren belirli bir biçimde, **SAML belirteci öznitelikleri** yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="a79f4-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="a79f4-165">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-165">hello following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="a79f4-167">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a79f4-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a79f4-168">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="a79f4-168">Attribute Name</span></span>  | <span data-ttu-id="a79f4-169">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="a79f4-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="a79f4-170">clever.Student.credentials.District\_kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a79f4-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="a79f4-171">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a79f4-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="a79f4-172">FirstName</span><span class="sxs-lookup"><span data-stu-id="a79f4-172">Firstname</span></span>  | <span data-ttu-id="a79f4-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="a79f4-173">user.givenname</span></span> |
    | <span data-ttu-id="a79f4-174">Soyadı</span><span class="sxs-lookup"><span data-stu-id="a79f4-174">Lastname</span></span>  | <span data-ttu-id="a79f4-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="a79f4-175">user.surname</span></span> |    

    <span data-ttu-id="a79f4-176">a.</span><span class="sxs-lookup"><span data-stu-id="a79f4-176">a.</span></span> <span data-ttu-id="a79f4-177">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a79f4-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a79f4-180">b.</span><span class="sxs-lookup"><span data-stu-id="a79f4-180">b.</span></span> <span data-ttu-id="a79f4-181">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="a79f4-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="a79f4-182">c.</span><span class="sxs-lookup"><span data-stu-id="a79f4-182">c.</span></span> <span data-ttu-id="a79f4-183">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="a79f4-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="a79f4-184">d.</span><span class="sxs-lookup"><span data-stu-id="a79f4-184">d.</span></span> <span data-ttu-id="a79f4-185">Merhaba bırakın **Namespace** metin kutusu boş.</span><span class="sxs-lookup"><span data-stu-id="a79f4-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="a79f4-186">d.</span><span class="sxs-lookup"><span data-stu-id="a79f4-186">d.</span></span> <span data-ttu-id="a79f4-187">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="a79f4-188">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a79f4-188">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a79f4-190">toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a79f4-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="a79f4-191">a.</span><span class="sxs-lookup"><span data-stu-id="a79f4-191">a.</span></span> <span data-ttu-id="a79f4-192">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-192">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="a79f4-194">b.</span><span class="sxs-lookup"><span data-stu-id="a79f4-194">b.</span></span> <span data-ttu-id="a79f4-195">Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a79f4-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="a79f4-197">c.</span><span class="sxs-lookup"><span data-stu-id="a79f4-197">c.</span></span> <span data-ttu-id="a79f4-198">Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="a79f4-200">d.</span><span class="sxs-lookup"><span data-stu-id="a79f4-200">d.</span></span> <span data-ttu-id="a79f4-201">Şimdi toohello özellik sayfasında gidin **Clever** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="a79f4-203">e.</span><span class="sxs-lookup"><span data-stu-id="a79f4-203">e.</span></span> <span data-ttu-id="a79f4-204">Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="a79f4-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="a79f4-205">Farklı web tarayıcısı penceresinde tooyour akıllı şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="a79f4-206">Merhaba araç çubuğunda **anlık oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="a79f4-207">![Hızlı oturum açma](./media/active-directory-saas-clever-tutorial/ic798984.png "anlık oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a79f4-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="a79f4-208">Merhaba üzerinde **anlık oturum açma** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a79f4-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="a79f4-209">![Hızlı oturum açma](./media/active-directory-saas-clever-tutorial/ic798985.png "anlık oturum açma")</span><span class="sxs-lookup"><span data-stu-id="a79f4-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="a79f4-210">a.</span><span class="sxs-lookup"><span data-stu-id="a79f4-210">a.</span></span> <span data-ttu-id="a79f4-211">Türü hello **oturum açma URL'si**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="a79f4-212">Merhaba **oturum açma URL'si** özel bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="a79f4-213">Kişi [akıllı istemci destek ekibi](https://clever.com/about/contact/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="a79f4-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="a79f4-214">b.</span><span class="sxs-lookup"><span data-stu-id="a79f4-214">b.</span></span> <span data-ttu-id="a79f4-215">Olarak **kimlik sistemi**seçin **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="a79f4-216">c.</span><span class="sxs-lookup"><span data-stu-id="a79f4-216">c.</span></span> <span data-ttu-id="a79f4-217">Türü hello **meta veri URL'sini** hello içinde **meta veri URL'sini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a79f4-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="a79f4-218">d.</span><span class="sxs-lookup"><span data-stu-id="a79f4-218">d.</span></span> <span data-ttu-id="a79f4-219">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a79f4-220">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a79f4-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a79f4-221">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a79f4-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a79f4-222">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a79f4-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a79f4-223">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a79f4-223">Create an Azure AD test user</span></span>

<span data-ttu-id="a79f4-224">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a79f4-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="a79f4-226">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a79f4-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79f4-227">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a79f4-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a79f4-229">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a79f4-231">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a79f4-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a79f4-233">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a79f4-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a79f4-235">a.</span><span class="sxs-lookup"><span data-stu-id="a79f4-235">a.</span></span> <span data-ttu-id="a79f4-236">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a79f4-237">b.</span><span class="sxs-lookup"><span data-stu-id="a79f4-237">b.</span></span> <span data-ttu-id="a79f4-238">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a79f4-239">c.</span><span class="sxs-lookup"><span data-stu-id="a79f4-239">c.</span></span> <span data-ttu-id="a79f4-240">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="a79f4-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a79f4-241">d.</span><span class="sxs-lookup"><span data-stu-id="a79f4-241">d.</span></span> <span data-ttu-id="a79f4-242">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a79f4-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="a79f4-243">Akıllı test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a79f4-243">Create a Clever test user</span></span>

<span data-ttu-id="a79f4-244">tooenable Azure AD kullanıcıların toolog tooClever bunların Clever sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="a79f4-245">Clever durumunda çalışmak [akıllı istemci destek ekibi](https://clever.com/about/contact/) hello akıllı platform hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="a79f4-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="a79f4-246">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="a79f4-247">API'leri, Azure AD kullanıcı hesapları akıllı tooprovision tarafından sağlanan veya herhangi diğer akıllı kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a79f4-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a79f4-248">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="a79f4-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a79f4-249">Bu bölümde, erişim tooClever vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a79f4-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="a79f4-251">**tooassign Britta Simon tooClever hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a79f4-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="a79f4-252">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a79f4-254">Merhaba uygulamalar listesinde **Clever**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-254">In hello applications list, select **Clever**.</span></span>

    ![Merhaba Clever hello uygulamalar listesinde bağlantı](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="a79f4-256">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a79f4-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="a79f4-258">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a79f4-258">Click **Add** button.</span></span> <span data-ttu-id="a79f4-259">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a79f4-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="a79f4-261">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a79f4-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a79f4-262">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a79f4-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a79f4-263">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a79f4-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a79f4-264">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="a79f4-264">Test single sign-on</span></span>

<span data-ttu-id="a79f4-265">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a79f4-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a79f4-266">Merhaba akıllı kutucuğa tıkladığınızda de erişim paneli Merhaba, otomatik olarak oturum açma tooyour akıllı uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a79f4-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="a79f4-267">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a79f4-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a79f4-268">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a79f4-268">Additional resources</span></span>

* [<span data-ttu-id="a79f4-269">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a79f4-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a79f4-270">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a79f4-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

