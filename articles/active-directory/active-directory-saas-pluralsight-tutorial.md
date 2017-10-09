---
title: "Öğretici: Azure Active Directory Tümleştirme ile Pluralsight | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Pluralsight arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="66eef-103">Öğretici: Azure Active Directory Tümleştirme Pluralsight ile</span><span class="sxs-lookup"><span data-stu-id="66eef-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="66eef-104">Bu öğreticide, bilgi nasıl toointegrate Pluralsight Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66eef-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66eef-105">Pluralsight Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="66eef-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66eef-106">Erişim tooPluralsight sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="66eef-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="66eef-107">Kullanıcıların tooautomatically get açan tooPluralsight (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="66eef-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66eef-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="66eef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66eef-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66eef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66eef-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66eef-110">Prerequisites</span></span>

<span data-ttu-id="66eef-111">tooconfigure Pluralsight ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="66eef-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="66eef-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="66eef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66eef-113">Bir Pluralsight çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="66eef-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66eef-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="66eef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66eef-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="66eef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66eef-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="66eef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66eef-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66eef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66eef-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="66eef-118">Scenario description</span></span>
<span data-ttu-id="66eef-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="66eef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66eef-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="66eef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66eef-121">Merhaba Galerisi'nden Pluralsight ekleme</span><span class="sxs-lookup"><span data-stu-id="66eef-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="66eef-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="66eef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="66eef-123">Merhaba Galerisi'nden Pluralsight ekleme</span><span class="sxs-lookup"><span data-stu-id="66eef-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="66eef-124">Azure AD'ye tooconfigure hello tümleştirme Pluralsight, tooadd Pluralsight hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eef-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66eef-125">**tooadd Pluralsight hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eef-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eef-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="66eef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66eef-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="66eef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66eef-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="66eef-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="66eef-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66eef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="66eef-133">Merhaba arama kutusuna yazın **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="66eef-133">In hello search box, type **Pluralsight**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="66eef-135">Merhaba Sonuçlar panelinde seçin **Pluralsight**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="66eef-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66eef-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="66eef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66eef-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Pluralsight sınayın.</span><span class="sxs-lookup"><span data-stu-id="66eef-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66eef-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Pluralsight içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="66eef-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Pluralsight hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eef-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="66eef-141">Merhaba hello değeri Pluralsight içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="66eef-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66eef-142">tooconfigure ve Pluralsight ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="66eef-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66eef-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="66eef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66eef-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="66eef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66eef-145">**[Pluralsight test kullanıcısı oluşturma](#creating-a-pluralsight-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Pluralsight içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="66eef-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66eef-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="66eef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66eef-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="66eef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66eef-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="66eef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66eef-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Pluralsight uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="66eef-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="66eef-150">**tooconfigure Azure AD çoklu oturum açma ile Pluralsight, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eef-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eef-151">Hello hello üzerinde Azure portal'ın **Pluralsight** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="66eef-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="66eef-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="66eef-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="66eef-155">Merhaba üzerinde **Pluralsight etki alanı ve URL'leri** bölümünde, hello aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="66eef-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="66eef-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="66eef-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66eef-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="66eef-158">This value is not real.</span></span> <span data-ttu-id="66eef-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="66eef-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="66eef-160">Kişi [Pluralsight istemci destek ekibi](mailto:support@pluralsight.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="66eef-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="66eef-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="66eef-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="66eef-163">Bu bölümde Hello amacı tooenable Azure AD çoklu oturum açma hello Azure portal ve hello Pluralsight uygulamada SSO tooconfigure ' dir.</span><span class="sxs-lookup"><span data-stu-id="66eef-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="66eef-164">Merhaba Pluralsight uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="66eef-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="66eef-165">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="66eef-165">hello following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="66eef-167">Merhaba de ekleyebilirsiniz **"Benzersiz kimliği"** , kuruluşunuz için uygun hello uygun değerli özniteliği EmployeeID veya başka bir şey gibi.</span><span class="sxs-lookup"><span data-stu-id="66eef-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="66eef-168">Ayrıca bu hello gerekli öznitelik olmadığını unutmayın; Ancak, ekleyebilirsiniz çok hello benzersiz kullanıcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="66eef-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="66eef-169">gerekli tooadd hello **SAML belirteci öznitelikleri**, hello aşağıdaki tabloda gösterilen her satır için hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66eef-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="66eef-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="66eef-170">Attribute Name</span></span> | <span data-ttu-id="66eef-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="66eef-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="66eef-172">Ad</span><span class="sxs-lookup"><span data-stu-id="66eef-172">First Name</span></span> |<span data-ttu-id="66eef-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="66eef-173">user.givenname</span></span> |
   | <span data-ttu-id="66eef-174">Soyadı</span><span class="sxs-lookup"><span data-stu-id="66eef-174">Last Name</span></span> |<span data-ttu-id="66eef-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="66eef-175">user.surname</span></span> |
   | <span data-ttu-id="66eef-176">E-posta</span><span class="sxs-lookup"><span data-stu-id="66eef-176">Email</span></span> |<span data-ttu-id="66eef-177">User.Mail</span><span class="sxs-lookup"><span data-stu-id="66eef-177">user.mail</span></span> |
   
   <span data-ttu-id="66eef-178">a.</span><span class="sxs-lookup"><span data-stu-id="66eef-178">a.</span></span> <span data-ttu-id="66eef-179">Tıklatın **kullanıcı özniteliği eklemek** tooopen hello **ekleme kullanıcı Attribure** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eef-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="66eef-181">b.</span><span class="sxs-lookup"><span data-stu-id="66eef-181">b.</span></span> <span data-ttu-id="66eef-182">Merhaba, **öznitelik adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="66eef-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="66eef-183">c.</span><span class="sxs-lookup"><span data-stu-id="66eef-183">c.</span></span> <span data-ttu-id="66eef-184">Merhaba gelen **öznitelik değeri** listesinde, ilgili satır için gösterilen select hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="66eef-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="66eef-185">d.</span><span class="sxs-lookup"><span data-stu-id="66eef-185">d.</span></span> <span data-ttu-id="66eef-186">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66eef-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="66eef-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66eef-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="66eef-189">tooget SSO yapılandırılmış uygulamanızın, kişi [Pluralsight Profesyonel Hizmetler](mailTo:professionalservices@pluralsight.com) ekip ve hello indirilen meta veri dosyası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="66eef-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="66eef-190">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="66eef-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66eef-191">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="66eef-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66eef-192">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66eef-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66eef-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="66eef-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="66eef-194">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="66eef-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="66eef-196">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eef-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eef-197">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="66eef-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66eef-199">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="66eef-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66eef-201">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eef-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66eef-203">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="66eef-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66eef-205">a.</span><span class="sxs-lookup"><span data-stu-id="66eef-205">a.</span></span> <span data-ttu-id="66eef-206">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66eef-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66eef-207">b.</span><span class="sxs-lookup"><span data-stu-id="66eef-207">b.</span></span> <span data-ttu-id="66eef-208">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="66eef-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66eef-209">c.</span><span class="sxs-lookup"><span data-stu-id="66eef-209">c.</span></span> <span data-ttu-id="66eef-210">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="66eef-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66eef-211">d.</span><span class="sxs-lookup"><span data-stu-id="66eef-211">d.</span></span> <span data-ttu-id="66eef-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66eef-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="66eef-213">Pluralsight test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="66eef-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="66eef-214">Bu bölümde Hello amacı toocreate Britta Simon içinde Pluralsight adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="66eef-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="66eef-215">Lütfen çalışmak [Pluralsight istemci destek ekibi](mailto:support@pluralsight.com) hello Pluralsight hesap tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="66eef-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66eef-216">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="66eef-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66eef-217">Bu bölümde, erişim tooPluralsight vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="66eef-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="66eef-219">**tooassign Britta Simon tooPluralsight hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="66eef-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="66eef-220">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="66eef-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="66eef-222">Merhaba uygulamalar listesinde **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="66eef-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="66eef-224">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="66eef-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="66eef-226">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66eef-226">Click **Add** button.</span></span> <span data-ttu-id="66eef-227">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eef-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="66eef-229">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="66eef-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66eef-230">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eef-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66eef-231">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="66eef-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66eef-232">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="66eef-232">Testing single sign-on</span></span>

<span data-ttu-id="66eef-233">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="66eef-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66eef-234">Merhaba Pluralsight hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Pluralsight uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66eef-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="66eef-235">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66eef-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66eef-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="66eef-236">Additional resources</span></span>

* [<span data-ttu-id="66eef-237">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="66eef-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66eef-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="66eef-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

