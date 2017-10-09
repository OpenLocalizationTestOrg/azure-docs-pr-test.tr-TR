---
title: "Öğretici: Azure Active Directory Tümleştirme ile CloudPassage | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile CloudPassage arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="30cdd-103">Öğretici: Azure Active Directory Tümleştirme CloudPassage ile</span><span class="sxs-lookup"><span data-stu-id="30cdd-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="30cdd-104">Bu öğreticide, bilgi nasıl toointegrate CloudPassage Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30cdd-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30cdd-105">CloudPassage Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="30cdd-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="30cdd-106">Erişim tooCloudPassage sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="30cdd-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="30cdd-107">Kullanıcıların tooautomatically get açan tooCloudPassage (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="30cdd-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30cdd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="30cdd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="30cdd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30cdd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30cdd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="30cdd-110">Prerequisites</span></span>

<span data-ttu-id="30cdd-111">tooconfigure CloudPassage ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="30cdd-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="30cdd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="30cdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30cdd-113">Bir CloudPassage çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="30cdd-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30cdd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="30cdd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30cdd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="30cdd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30cdd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30cdd-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30cdd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30cdd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="30cdd-118">Scenario description</span></span>
<span data-ttu-id="30cdd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="30cdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30cdd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="30cdd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30cdd-121">Merhaba Galerisi'nden CloudPassage ekleme</span><span class="sxs-lookup"><span data-stu-id="30cdd-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="30cdd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="30cdd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="30cdd-123">Merhaba Galerisi'nden CloudPassage ekleme</span><span class="sxs-lookup"><span data-stu-id="30cdd-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="30cdd-124">Azure AD'ye tooconfigure hello tümleştirme CloudPassage, tooadd CloudPassage hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30cdd-125">**tooadd CloudPassage hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="30cdd-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30cdd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30cdd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="30cdd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="30cdd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="30cdd-133">Merhaba arama kutusuna yazın **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-133">In hello search box, type **CloudPassage**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="30cdd-135">Merhaba Sonuçlar panelinde seçin **CloudPassage**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="30cdd-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30cdd-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="30cdd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30cdd-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı CloudPassage ile test etme</span><span class="sxs-lookup"><span data-stu-id="30cdd-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="30cdd-139">Tek toowork'ın oturum açma hangi hello karşılık gelen CloudPassage içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="30cdd-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı CloudPassage hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="30cdd-141">Merhaba hello değeri CloudPassage içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="30cdd-142">tooconfigure ve CloudPassage ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="30cdd-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30cdd-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="30cdd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30cdd-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="30cdd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30cdd-145">**[CloudPassage test kullanıcısı oluşturma](#creating-a-cloudpassage-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir CloudPassage içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="30cdd-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="30cdd-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="30cdd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30cdd-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="30cdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30cdd-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="30cdd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30cdd-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma CloudPassage uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="30cdd-150">**tooconfigure Azure AD çoklu oturum açma ile CloudPassage, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="30cdd-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="30cdd-151">Hello hello üzerinde Azure portal'ın **CloudPassage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="30cdd-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="30cdd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="30cdd-155">Merhaba üzerinde **CloudPassage etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="30cdd-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="30cdd-157">a.</span><span class="sxs-lookup"><span data-stu-id="30cdd-157">a.</span></span> <span data-ttu-id="30cdd-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="30cdd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="30cdd-159">b.</span><span class="sxs-lookup"><span data-stu-id="30cdd-159">b.</span></span> <span data-ttu-id="30cdd-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="30cdd-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="30cdd-161">Tıklayarak, bu öznitelik için değeriniz alabilirsiniz **SSO Kurulum belgeleri** hello içinde **çoklu oturum açma ayarları** CloudPassage portalınızı bölümü.</span><span class="sxs-lookup"><span data-stu-id="30cdd-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="30cdd-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-163">These values are not real.</span></span> <span data-ttu-id="30cdd-164">Bu değerleri hello gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="30cdd-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="30cdd-165">Kişi [CloudPassage istemci destek ekibi](https://www.cloudpassage.com/company/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="30cdd-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="30cdd-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="30cdd-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="30cdd-168">CloudPassage uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="30cdd-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="30cdd-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-169">hello following screenshot shows an example for this.</span></span>
   
   ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="30cdd-171">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="30cdd-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="30cdd-172">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="30cdd-172">Attribute Name</span></span> | <span data-ttu-id="30cdd-173">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="30cdd-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="30cdd-174">FirstName</span><span class="sxs-lookup"><span data-stu-id="30cdd-174">firstname</span></span> |<span data-ttu-id="30cdd-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="30cdd-175">user.givenname</span></span> |
    | <span data-ttu-id="30cdd-176">Soyadı</span><span class="sxs-lookup"><span data-stu-id="30cdd-176">lastname</span></span> |<span data-ttu-id="30cdd-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="30cdd-177">user.surname</span></span> |
    | <span data-ttu-id="30cdd-178">E-posta</span><span class="sxs-lookup"><span data-stu-id="30cdd-178">email</span></span> |<span data-ttu-id="30cdd-179">User.Mail</span><span class="sxs-lookup"><span data-stu-id="30cdd-179">user.mail</span></span> |
    
    <span data-ttu-id="30cdd-180">a.</span><span class="sxs-lookup"><span data-stu-id="30cdd-180">a.</span></span> <span data-ttu-id="30cdd-181">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="30cdd-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="30cdd-184">b.</span><span class="sxs-lookup"><span data-stu-id="30cdd-184">b.</span></span> <span data-ttu-id="30cdd-185">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="30cdd-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="30cdd-186">c.</span><span class="sxs-lookup"><span data-stu-id="30cdd-186">c.</span></span> <span data-ttu-id="30cdd-187">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="30cdd-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="30cdd-188">d.</span><span class="sxs-lookup"><span data-stu-id="30cdd-188">d.</span></span> <span data-ttu-id="30cdd-189">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-189">Click **Ok**.</span></span>

7. <span data-ttu-id="30cdd-190">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-190">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="30cdd-192">Merhaba üzerinde **CloudPassage yapılandırma** 'yi tıklatın **yapılandırma CloudPassage** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="30cdd-193">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="30cdd-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="30cdd-195">Farklı bir tarayıcı penceresinde yönetici olarak oturum açma tooyour CloudPassage şirket site.</span><span class="sxs-lookup"><span data-stu-id="30cdd-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="30cdd-196">Hello içinde hello üst menüsünde **ayarları**ve ardından **Site Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][12]

11. <span data-ttu-id="30cdd-198">Merhaba tıklatın **kimlik doğrulama ayarlarını** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][13]

12. <span data-ttu-id="30cdd-200">Merhaba, **çoklu oturum açma ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="30cdd-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın][14]

    <span data-ttu-id="30cdd-202">a.</span><span class="sxs-lookup"><span data-stu-id="30cdd-202">a.</span></span> <span data-ttu-id="30cdd-203">Seçin **etkinleştirmek tek sign-on(SSO) (SSO Kurulum belgeleri)** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="30cdd-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="30cdd-204">b.</span><span class="sxs-lookup"><span data-stu-id="30cdd-204">b.</span></span> <span data-ttu-id="30cdd-205">Yapıştır **SAML varlık kimliği** hello içine **SAML veren URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="30cdd-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="30cdd-206">c.</span><span class="sxs-lookup"><span data-stu-id="30cdd-206">c.</span></span> <span data-ttu-id="30cdd-207">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello içine **SAML uç nokta URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="30cdd-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="30cdd-208">d.</span><span class="sxs-lookup"><span data-stu-id="30cdd-208">d.</span></span> <span data-ttu-id="30cdd-209">Yapıştır **Sign-Out URL** hello içine **oturum kapatma giriş sayfası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="30cdd-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="30cdd-210">e.</span><span class="sxs-lookup"><span data-stu-id="30cdd-210">e.</span></span> <span data-ttu-id="30cdd-211">İndirilen sertifikanızı kopyalama hello panonuza, içine indirilen sertifika içeriğini Not Defteri'nde açın ve hello yapıştırma **x 509 Sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="30cdd-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="30cdd-212">f.</span><span class="sxs-lookup"><span data-stu-id="30cdd-212">f.</span></span> <span data-ttu-id="30cdd-213">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="30cdd-214">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="30cdd-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="30cdd-215">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="30cdd-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="30cdd-216">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30cdd-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30cdd-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="30cdd-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="30cdd-218">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="30cdd-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="30cdd-220">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="30cdd-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30cdd-221">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30cdd-223">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30cdd-225">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="30cdd-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30cdd-227">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="30cdd-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30cdd-229">a.</span><span class="sxs-lookup"><span data-stu-id="30cdd-229">a.</span></span> <span data-ttu-id="30cdd-230">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30cdd-231">b.</span><span class="sxs-lookup"><span data-stu-id="30cdd-231">b.</span></span> <span data-ttu-id="30cdd-232">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="30cdd-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30cdd-233">c.</span><span class="sxs-lookup"><span data-stu-id="30cdd-233">c.</span></span> <span data-ttu-id="30cdd-234">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="30cdd-235">d.</span><span class="sxs-lookup"><span data-stu-id="30cdd-235">d.</span></span> <span data-ttu-id="30cdd-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="30cdd-237">CloudPassage test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="30cdd-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="30cdd-238">Bu bölümde Hello amacı toocreate Britta Simon içinde CloudPassage adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="30cdd-239">**toocreate CloudPassage içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="30cdd-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="30cdd-240">Oturum açma tooyour **CloudPassage** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="30cdd-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="30cdd-241">Merhaba üstte Hello araç çubuğunda **ayarları**ve ardından **Site Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![CloudPassage test kullanıcısı oluşturma][22] 

3. <span data-ttu-id="30cdd-243">Merhaba tıklatın **kullanıcılar** sekmesini ve ardından **yeni kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![CloudPassage test kullanıcısı oluşturma][23]

4. <span data-ttu-id="30cdd-245">Merhaba, **yeni kullanıcı Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="30cdd-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![CloudPassage test kullanıcısı oluşturma][24]
    
    <span data-ttu-id="30cdd-247">a.</span><span class="sxs-lookup"><span data-stu-id="30cdd-247">a.</span></span> <span data-ttu-id="30cdd-248">Merhaba, **ad** metin kutusuna, Britta yazın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="30cdd-249">b.</span><span class="sxs-lookup"><span data-stu-id="30cdd-249">b.</span></span> <span data-ttu-id="30cdd-250">Merhaba, **Soyadı** metin kutusuna, Simon yazın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="30cdd-251">c.</span><span class="sxs-lookup"><span data-stu-id="30cdd-251">c.</span></span> <span data-ttu-id="30cdd-252">Merhaba, **kullanıcıadı** metin kutusuna, hello **e-posta** textbox ve hello **yeniden e-posta** metin kutusuna, Azure AD'de Britta'nin kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="30cdd-253">d.</span><span class="sxs-lookup"><span data-stu-id="30cdd-253">d.</span></span> <span data-ttu-id="30cdd-254">Olarak **erişim türü**seçin **hale Portal erişimi etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="30cdd-255">e.</span><span class="sxs-lookup"><span data-stu-id="30cdd-255">e.</span></span> <span data-ttu-id="30cdd-256">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="30cdd-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="30cdd-257">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="30cdd-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="30cdd-258">Bu bölümde, erişim tooCloudPassage vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="30cdd-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="30cdd-260">**tooassign Britta Simon tooCloudPassage hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="30cdd-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="30cdd-261">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="30cdd-263">Merhaba uygulamalar listesinde **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="30cdd-265">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="30cdd-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="30cdd-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="30cdd-267">Click **Add** button.</span></span> <span data-ttu-id="30cdd-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="30cdd-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="30cdd-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="30cdd-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="30cdd-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="30cdd-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30cdd-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="30cdd-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30cdd-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="30cdd-273">Testing single sign-on</span></span>

<span data-ttu-id="30cdd-274">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="30cdd-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="30cdd-275">Merhaba CloudPassage hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour CloudPassage uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="30cdd-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30cdd-276">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="30cdd-276">Additional resources</span></span>

* [<span data-ttu-id="30cdd-277">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="30cdd-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30cdd-278">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="30cdd-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

