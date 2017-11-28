---
title: "Öğretici: Azure Active Directory Tümleştirme ile myPolicies | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile myPolicies arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="138c3-103">Öğretici: Azure Active Directory Tümleştirme myPolicies ile</span><span class="sxs-lookup"><span data-stu-id="138c3-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="138c3-104">Bu öğreticide, bilgi nasıl toointegrate myPolicies Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="138c3-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="138c3-105">MyPolicies Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="138c3-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="138c3-106">Erişim toomyPolicies sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="138c3-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="138c3-107">Kullanıcıların tooautomatically get açan toomyPolicies (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="138c3-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="138c3-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="138c3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="138c3-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="138c3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="138c3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="138c3-110">Prerequisites</span></span>

<span data-ttu-id="138c3-111">tooconfigure myPolicies ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="138c3-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="138c3-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="138c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="138c3-113">Bir myPolicies çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="138c3-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="138c3-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="138c3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="138c3-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="138c3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="138c3-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="138c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="138c3-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="138c3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="138c3-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="138c3-118">Scenario description</span></span>
<span data-ttu-id="138c3-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="138c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="138c3-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="138c3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="138c3-121">Merhaba Galerisi'nden myPolicies ekleme</span><span class="sxs-lookup"><span data-stu-id="138c3-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="138c3-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="138c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="138c3-123">Merhaba Galerisi'nden myPolicies ekleme</span><span class="sxs-lookup"><span data-stu-id="138c3-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="138c3-124">Azure AD'ye tooconfigure hello tümleştirme myPolicies, tooadd myPolicies hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="138c3-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="138c3-125">**Merhaba galerisinden tooadd myPolicies hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="138c3-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="138c3-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="138c3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="138c3-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="138c3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="138c3-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="138c3-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="138c3-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="138c3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="138c3-133">Merhaba arama kutusuna yazın **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="138c3-133">In hello search box, type **myPolicies**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="138c3-135">Merhaba Sonuçlar panelinde seçin **myPolicies**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="138c3-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="138c3-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="138c3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="138c3-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı myPolicies sınayın.</span><span class="sxs-lookup"><span data-stu-id="138c3-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="138c3-139">Tek toowork'ın oturum açma hangi hello karşılık gelen myPolicies içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="138c3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="138c3-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı myPolicies hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="138c3-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="138c3-141">Merhaba hello değeri myPolicies içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="138c3-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="138c3-142">tooconfigure ve myPolicies ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="138c3-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="138c3-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="138c3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="138c3-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="138c3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="138c3-145">**[MyPolicies test kullanıcısı oluşturma](#creating-a-mypolicies-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir myPolicies içinde.</span><span class="sxs-lookup"><span data-stu-id="138c3-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="138c3-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="138c3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="138c3-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="138c3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="138c3-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="138c3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="138c3-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma myPolicies uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="138c3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="138c3-150">**tooconfigure Azure AD çoklu oturum açma ile myPolicies, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="138c3-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="138c3-151">Hello hello üzerinde Azure portal'ın **myPolicies** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="138c3-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="138c3-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="138c3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="138c3-155">Merhaba üzerinde **myPolicies etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="138c3-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="138c3-157">a.</span><span class="sxs-lookup"><span data-stu-id="138c3-157">a.</span></span> <span data-ttu-id="138c3-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="138c3-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="138c3-159">b.</span><span class="sxs-lookup"><span data-stu-id="138c3-159">b.</span></span> <span data-ttu-id="138c3-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="138c3-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="138c3-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="138c3-161">These values are not real.</span></span> <span data-ttu-id="138c3-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="138c3-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="138c3-163">Kişi [myPolicies destek ekibi](mailto:support@mypolicies.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="138c3-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="138c3-164">Merhaba myPolicies uygulaması hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="138c3-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="138c3-165">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="138c3-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="138c3-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="138c3-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="138c3-167">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="138c3-167">hello following screenshot shows an example for this.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="138c3-169">Tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** hello onay kutusu **kullanıcı öznitelikleri** bölümünde tooexpand hello öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="138c3-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="138c3-170">Merhaba her biri görüntülenen hello öznitelikleri - aşağıdaki adımları gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="138c3-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="138c3-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="138c3-171">Attribute Name</span></span> | <span data-ttu-id="138c3-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="138c3-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="138c3-173">givenName</span><span class="sxs-lookup"><span data-stu-id="138c3-173">givenname</span></span> | <span data-ttu-id="138c3-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="138c3-174">user.givenname</span></span> |
    | <span data-ttu-id="138c3-175">Soyadı</span><span class="sxs-lookup"><span data-stu-id="138c3-175">surname</span></span> | <span data-ttu-id="138c3-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="138c3-176">user.surname</span></span> |
    | <span data-ttu-id="138c3-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="138c3-177">emailaddress</span></span> | <span data-ttu-id="138c3-178">User.Mail</span><span class="sxs-lookup"><span data-stu-id="138c3-178">user.mail</span></span> |
    | <span data-ttu-id="138c3-179">ad</span><span class="sxs-lookup"><span data-stu-id="138c3-179">name</span></span> | <span data-ttu-id="138c3-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="138c3-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="138c3-181">a.</span><span class="sxs-lookup"><span data-stu-id="138c3-181">a.</span></span> <span data-ttu-id="138c3-182">Tıklatın hello özniteliği tooopen hello üzerinde **öznitelik Düzenle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="138c3-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="138c3-184">b.</span><span class="sxs-lookup"><span data-stu-id="138c3-184">b.</span></span> <span data-ttu-id="138c3-185">Hello Hello URL değeri Sil **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="138c3-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="138c3-186">c.</span><span class="sxs-lookup"><span data-stu-id="138c3-186">c.</span></span> <span data-ttu-id="138c3-187">Tıklatın **Tamam** toosave hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="138c3-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="138c3-188">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="138c3-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="138c3-190">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="138c3-190">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="138c3-192">Merhaba üzerinde **myPolicies yapılandırma** 'yi tıklatın **myPolicies yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="138c3-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="138c3-193">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="138c3-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="138c3-195">tooconfigure çoklu oturum açma üzerinde **myPolicies** yan, indirilen toosend hello ihtiyacınız **Certificate(Base64)** ve **SAML çoklu oturum açma hizmet URL'si** çok[myPolicies destek ekibi](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="138c3-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="138c3-196">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="138c3-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="138c3-197">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="138c3-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="138c3-198">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="138c3-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="138c3-199">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="138c3-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="138c3-200">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="138c3-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="138c3-202">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="138c3-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="138c3-203">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="138c3-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="138c3-205">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="138c3-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="138c3-207">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="138c3-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="138c3-209">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="138c3-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="138c3-211">a.</span><span class="sxs-lookup"><span data-stu-id="138c3-211">a.</span></span> <span data-ttu-id="138c3-212">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="138c3-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="138c3-213">b.</span><span class="sxs-lookup"><span data-stu-id="138c3-213">b.</span></span> <span data-ttu-id="138c3-214">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="138c3-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="138c3-215">c.</span><span class="sxs-lookup"><span data-stu-id="138c3-215">c.</span></span> <span data-ttu-id="138c3-216">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="138c3-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="138c3-217">d.</span><span class="sxs-lookup"><span data-stu-id="138c3-217">d.</span></span> <span data-ttu-id="138c3-218">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="138c3-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="138c3-219">MyPolicies test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="138c3-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="138c3-220">Bu bölümde, myPolicies içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="138c3-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="138c3-221">Çalışmak [myPolicies destek ekibi](mailto:support@mypolicies.com) hello myPolicies platform hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="138c3-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="138c3-222">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="138c3-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="138c3-223">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="138c3-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="138c3-224">Bu bölümde, erişim toomyPolicies vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="138c3-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="138c3-226">**tooassign Britta Simon toomyPolicies hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="138c3-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="138c3-227">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="138c3-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="138c3-229">Merhaba uygulamalar listesinde **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="138c3-229">In hello applications list, select **myPolicies**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="138c3-231">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="138c3-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="138c3-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="138c3-233">Click **Add** button.</span></span> <span data-ttu-id="138c3-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="138c3-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="138c3-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="138c3-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="138c3-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="138c3-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="138c3-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="138c3-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="138c3-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="138c3-239">Testing single sign-on</span></span>

<span data-ttu-id="138c3-240">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="138c3-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="138c3-241">Merhaba erişim paneli myPolicies döşeme hello tıkladığınızda, otomatik olarak oturum açma tooyour myPolicies uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="138c3-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="138c3-242">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="138c3-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="138c3-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="138c3-243">Additional resources</span></span>

* [<span data-ttu-id="138c3-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="138c3-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="138c3-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="138c3-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

