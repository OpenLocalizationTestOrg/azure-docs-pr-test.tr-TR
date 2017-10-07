---
title: "Öğretici: Azure Active Directory Tümleştirme ile Yazı tahtası öğrenin | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki Yazı tahtası öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="cab29-103">Öğretici: Azure Active Directory Tümleştirme ile Yazı tahtası öğrenin</span><span class="sxs-lookup"><span data-stu-id="cab29-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="cab29-104">Bu öğreticide, bilgi toointegrate Yazı tahtası öğrenin nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="cab29-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cab29-105">Azure AD ile tümleştirme Yazı tahtası öğrenin ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cab29-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cab29-106">Erişim tooBlackboard öğrenin sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cab29-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="cab29-107">Kullanıcıların tooautomatically get açan tooBlackboard öğrenin (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cab29-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cab29-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cab29-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cab29-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cab29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cab29-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cab29-110">Prerequisites</span></span>

<span data-ttu-id="cab29-111">tooconfigure Yazı tahtası öğrenin ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cab29-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="cab29-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cab29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cab29-113">Bir Yazı tahtası öğrenin çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cab29-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cab29-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cab29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cab29-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cab29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cab29-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cab29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cab29-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cab29-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cab29-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cab29-118">Scenario description</span></span>
<span data-ttu-id="cab29-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cab29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cab29-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cab29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cab29-121">Yazı tahtası öğrenin hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cab29-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="cab29-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cab29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="cab29-123">Yazı tahtası öğrenin hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="cab29-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="cab29-124">Azure AD'ye tooconfigure hello tümleştirme Yazı tahtası öğrenin, tooadd Yazı tahtası öğrenin hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="cab29-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cab29-125">**tooadd Yazı tahtası öğrenin hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cab29-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cab29-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cab29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cab29-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cab29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cab29-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cab29-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cab29-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cab29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cab29-133">Merhaba arama kutusuna yazın **Yazı tahtası öğrenin**.</span><span class="sxs-lookup"><span data-stu-id="cab29-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="cab29-135">Merhaba Sonuçlar panelinde seçin **Yazı tahtası öğrenin**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="cab29-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cab29-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cab29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cab29-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Yazı tahtası öğrenin ile test etme</span><span class="sxs-lookup"><span data-stu-id="cab29-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cab29-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Yazı tahtası öğrenin içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="cab29-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="cab29-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı Yazı tahtası öğrenin arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cab29-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="cab29-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** Yazı tahtası öğrenin içinde.</span><span class="sxs-lookup"><span data-stu-id="cab29-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="cab29-142">tooconfigure ve Yazı tahtası öğrenin ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cab29-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cab29-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="cab29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cab29-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="cab29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cab29-145">**[Yazı tahtası öğrenin test kullanıcısı oluşturma](#creating-a-blackboard-learn-test-user)**  -toohave Britta Simon Yazı tahtası bağlantılı toohello Azure AD kullanıcı gösterimi olan bilgi olarak, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="cab29-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cab29-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cab29-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cab29-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="cab29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cab29-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cab29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cab29-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Yazı tahtası öğrenin uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cab29-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="cab29-150">**tooconfigure Azure AD çoklu oturum açma ile Yazı tahtası öğrenme, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cab29-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="cab29-151">Merhaba hello üzerinde Azure portal'ın **Yazı tahtası öğrenin** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cab29-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cab29-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cab29-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="cab29-155">Merhaba üzerinde **Yazı tahtası öğrenin etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cab29-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="cab29-157">a.</span><span class="sxs-lookup"><span data-stu-id="cab29-157">a.</span></span> <span data-ttu-id="cab29-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="cab29-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="cab29-159">b.</span><span class="sxs-lookup"><span data-stu-id="cab29-159">b.</span></span> <span data-ttu-id="cab29-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="cab29-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="cab29-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cab29-161">These values are not real.</span></span> <span data-ttu-id="cab29-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cab29-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cab29-163">Kişi [Yazı tahtası öğrenin istemci destek ekibi](https://www.blackboard.com/support/index.aspx) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="cab29-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="cab29-164">Yazı tahtası öğrenin uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="cab29-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="cab29-165">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cab29-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="cab29-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="cab29-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="cab29-167">Aşağıdaki ekran görüntüsü hello ilgili bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="cab29-167">hello following screenshot shows an example about it.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="cab29-169">Merhaba, **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliklerini hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cab29-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="cab29-170">Merhaba Userprincipalname burada hello benzersiz kullanıcı özniteliği eşledikten ancak hangi benzersiz şekilde hello kullanıcı hello Kuruluşunuzdaki ayırır ve tooBlackboard öğrenin username alan eşlemelerini toohello uygun değere eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab29-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="cab29-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="cab29-171">Attribute Name</span></span> | <span data-ttu-id="cab29-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="cab29-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="cab29-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="cab29-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="cab29-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="cab29-174">user.userprincipalname</span></span> |

    <span data-ttu-id="cab29-175">a.</span><span class="sxs-lookup"><span data-stu-id="cab29-175">a.</span></span> <span data-ttu-id="cab29-176">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cab29-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="cab29-179">b.</span><span class="sxs-lookup"><span data-stu-id="cab29-179">b.</span></span> <span data-ttu-id="cab29-180">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="cab29-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="cab29-181">c.</span><span class="sxs-lookup"><span data-stu-id="cab29-181">c.</span></span> <span data-ttu-id="cab29-182">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="cab29-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cab29-183">d.</span><span class="sxs-lookup"><span data-stu-id="cab29-183">d.</span></span> <span data-ttu-id="cab29-184">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cab29-184">Click **Ok**.</span></span>

4. <span data-ttu-id="cab29-185">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cab29-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="cab29-187">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cab29-187">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cab29-189">Merhaba üzerinde **Yazı tahtası öğrenin yapılandırma** 'yi tıklatın **yapılandırma Yazı tahtası öğrenin** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cab29-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cab29-190">Kopya hello **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cab29-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="cab29-192">tooconfigure çoklu oturum açma üzerinde **Yazı tahtası öğrenin** yan, indirilen toosend hello ihtiyacınız **meta veri XML** ve **SAML varlık kimliği** çok[Yazı tahtası öğrenin Destek](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="cab29-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="cab29-193">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cab29-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cab29-194">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="cab29-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cab29-195">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cab29-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cab29-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cab29-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="cab29-197">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="cab29-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cab29-199">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cab29-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cab29-200">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cab29-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cab29-202">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cab29-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cab29-204">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="cab29-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cab29-206">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cab29-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cab29-208">a.</span><span class="sxs-lookup"><span data-stu-id="cab29-208">a.</span></span> <span data-ttu-id="cab29-209">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cab29-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cab29-210">b.</span><span class="sxs-lookup"><span data-stu-id="cab29-210">b.</span></span> <span data-ttu-id="cab29-211">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="cab29-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="cab29-212">c.</span><span class="sxs-lookup"><span data-stu-id="cab29-212">c.</span></span> <span data-ttu-id="cab29-213">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cab29-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cab29-214">d.</span><span class="sxs-lookup"><span data-stu-id="cab29-214">d.</span></span> <span data-ttu-id="cab29-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cab29-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="cab29-216">Yazı tahtası öğrenin test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cab29-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="cab29-217">Bu bölümde, Yazı tahtası öğrenin Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cab29-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="cab29-218">Yazı tahtası öğrenin uygulama desteği yalnızca zaman sağlama kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="cab29-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="cab29-219">Merhaba bölümde açıklandığı gibi hello talep yapılandırdığınızdan emin olun  **[yapılandırma Azure AD çoklu oturum açma](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="cab29-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cab29-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cab29-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cab29-221">Bu bölümde, erişim tooBlackboard öğrenin vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cab29-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cab29-223">**tooassign Britta Simon tooBlackboard öğrenin, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cab29-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="cab29-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cab29-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cab29-226">Merhaba uygulamalar listesinde **Yazı tahtası öğrenin**.</span><span class="sxs-lookup"><span data-stu-id="cab29-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="cab29-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cab29-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cab29-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cab29-230">Click **Add** button.</span></span> <span data-ttu-id="cab29-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cab29-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cab29-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cab29-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cab29-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cab29-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cab29-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cab29-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cab29-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cab29-236">Testing single sign-on</span></span>

<span data-ttu-id="cab29-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="cab29-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cab29-238">Merhaba Yazı tahtası öğrenin parçasında hello erişim paneli tıkladığınızda, otomatik olarak oturum açma tooyour Yazı tahtası öğrenin uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cab29-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="cab29-239">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cab29-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cab29-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cab29-240">Additional resources</span></span>

* [<span data-ttu-id="cab29-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="cab29-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cab29-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cab29-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

