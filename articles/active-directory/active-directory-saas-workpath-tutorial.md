---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workpath | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Workpath arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 69f443f314edb7c8c489a6c193e09b6f8fe6795a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="174da-103">Öğretici: Azure Active Directory Tümleştirme Workpath ile</span><span class="sxs-lookup"><span data-stu-id="174da-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="174da-104">Bu öğreticide, bilgi nasıl toointegrate Workpath Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="174da-104">In this tutorial, you learn how toointegrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="174da-105">Workpath Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="174da-105">Integrating Workpath with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="174da-106">Erişim tooWorkpath sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="174da-106">You can control in Azure AD who has access tooWorkpath</span></span>
- <span data-ttu-id="174da-107">Kullanıcıların tooautomatically get açan tooWorkpath (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="174da-107">You can enable your users tooautomatically get signed-on tooWorkpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="174da-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="174da-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="174da-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="174da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="174da-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="174da-110">Prerequisites</span></span>

<span data-ttu-id="174da-111">tooconfigure Workpath ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="174da-111">tooconfigure Azure AD integration with Workpath, you need hello following items:</span></span>

- <span data-ttu-id="174da-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="174da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="174da-113">Bir Workpath çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="174da-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="174da-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="174da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="174da-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="174da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="174da-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="174da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="174da-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="174da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="174da-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="174da-118">Scenario description</span></span>
<span data-ttu-id="174da-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="174da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="174da-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="174da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="174da-121">Merhaba Galerisi'nden Workpath ekleme</span><span class="sxs-lookup"><span data-stu-id="174da-121">Adding Workpath from hello gallery</span></span>
2. <span data-ttu-id="174da-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="174da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-hello-gallery"></a><span data-ttu-id="174da-123">Merhaba Galerisi'nden Workpath ekleme</span><span class="sxs-lookup"><span data-stu-id="174da-123">Adding Workpath from hello gallery</span></span>
<span data-ttu-id="174da-124">Azure AD'ye tooconfigure hello tümleştirme Workpath, tooadd Workpath hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="174da-124">tooconfigure hello integration of Workpath into Azure AD, you need tooadd Workpath from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="174da-125">**tooadd Workpath hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="174da-125">**tooadd Workpath from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="174da-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="174da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="174da-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="174da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="174da-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="174da-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="174da-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="174da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="174da-133">Merhaba arama kutusuna yazın **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="174da-133">In hello search box, type **Workpath**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="174da-135">Merhaba Sonuçlar panelinde seçin **Workpath**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="174da-135">In hello results panel, select **Workpath**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="174da-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="174da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="174da-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Workpath ile test etme</span><span class="sxs-lookup"><span data-stu-id="174da-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="174da-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Workpath içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="174da-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workpath is tooa user in Azure AD.</span></span> <span data-ttu-id="174da-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Workpath hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="174da-140">In other words, a link relationship between an Azure AD user and hello related user in Workpath needs toobe established.</span></span>

<span data-ttu-id="174da-141">Merhaba hello değeri Workpath içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="174da-141">In Workpath, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="174da-142">tooconfigure ve Workpath ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="174da-142">tooconfigure and test Azure AD single sign-on with Workpath, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="174da-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="174da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="174da-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="174da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="174da-145">**[Workpath test kullanıcısı oluşturma](#creating-a-workpath-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Workpath içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="174da-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - toohave a counterpart of Britta Simon in Workpath that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="174da-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="174da-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="174da-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="174da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="174da-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="174da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="174da-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Workpath uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="174da-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="174da-150">**tooconfigure Azure AD çoklu oturum açma ile Workpath, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="174da-150">**tooconfigure Azure AD single sign-on with Workpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="174da-151">Hello hello üzerinde Azure portal'ın **Workpath** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="174da-151">In hello Azure portal, on hello **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="174da-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="174da-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="174da-155">Merhaba üzerinde **Workpath etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP** başlatılan modu hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="174da-155">On hello **Workpath Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="174da-157">a.</span><span class="sxs-lookup"><span data-stu-id="174da-157">a.</span></span> <span data-ttu-id="174da-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="174da-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="174da-159">b.</span><span class="sxs-lookup"><span data-stu-id="174da-159">b.</span></span> <span data-ttu-id="174da-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="174da-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="174da-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="174da-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="174da-162">Tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="174da-162">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="174da-164">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="174da-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="174da-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="174da-165">These values are not real.</span></span> <span data-ttu-id="174da-166">Bu değerleri, oturum açma hello gerçek URL'si, tanımlayıcı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="174da-166">Update these values with hello actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="174da-167">Kişi [Workpath destek ekibi](https://help.workpath.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="174da-167">Contact [Workpath support team](https://help.workpath.com) tooget these values.</span></span>

5. <span data-ttu-id="174da-168">Workpath uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="174da-168">Workpath application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="174da-169">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="174da-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="174da-170">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="174da-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="174da-171">Ekran aşağıdaki hello Bu yapılandırmanın bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="174da-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="174da-173">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="174da-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="174da-174">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="174da-174">Attribute Name</span></span> | <span data-ttu-id="174da-175">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="174da-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="174da-176">ilk_ad</span><span class="sxs-lookup"><span data-stu-id="174da-176">first_name</span></span> | <span data-ttu-id="174da-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="174da-177">user.givenname</span></span> |
    | <span data-ttu-id="174da-178">Soyadı</span><span class="sxs-lookup"><span data-stu-id="174da-178">last_name</span></span> | <span data-ttu-id="174da-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="174da-179">user.surname</span></span> |
    
    <span data-ttu-id="174da-180">a.</span><span class="sxs-lookup"><span data-stu-id="174da-180">a.</span></span> <span data-ttu-id="174da-181">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="174da-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="174da-183">b.</span><span class="sxs-lookup"><span data-stu-id="174da-183">b.</span></span> <span data-ttu-id="174da-184">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="174da-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="174da-186">c.</span><span class="sxs-lookup"><span data-stu-id="174da-186">c.</span></span> <span data-ttu-id="174da-187">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="174da-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="174da-188">d.</span><span class="sxs-lookup"><span data-stu-id="174da-188">d.</span></span> <span data-ttu-id="174da-189">Merhaba bırakın **Namespace** metin kutusu boş.</span><span class="sxs-lookup"><span data-stu-id="174da-189">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="174da-190">e.</span><span class="sxs-lookup"><span data-stu-id="174da-190">e.</span></span> <span data-ttu-id="174da-191">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="174da-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="174da-192">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="174da-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="174da-194">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="174da-194">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="174da-196">Merhaba üzerinde **Workpath yapılandırma** 'yi tıklatın **yapılandırma Workpath** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="174da-196">On hello **Workpath Configuration** section, click **Configure Workpath** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="174da-197">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="174da-197">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="174da-199">tooconfigure çoklu oturum açma üzerinde **Workpath** yan, indirilen toosend hello ihtiyacınız **meta veri XML**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Workpath destek ekibi](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="174da-199">tooconfigure single sign-on on **Workpath** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="174da-200">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="174da-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="174da-201">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="174da-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="174da-202">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="174da-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="174da-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="174da-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="174da-204">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="174da-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="174da-206">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="174da-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="174da-207">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="174da-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="174da-209">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="174da-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="174da-211">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="174da-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="174da-213">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="174da-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="174da-215">a.</span><span class="sxs-lookup"><span data-stu-id="174da-215">a.</span></span> <span data-ttu-id="174da-216">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="174da-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="174da-217">b.</span><span class="sxs-lookup"><span data-stu-id="174da-217">b.</span></span> <span data-ttu-id="174da-218">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="174da-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="174da-219">c.</span><span class="sxs-lookup"><span data-stu-id="174da-219">c.</span></span> <span data-ttu-id="174da-220">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="174da-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="174da-221">d.</span><span class="sxs-lookup"><span data-stu-id="174da-221">d.</span></span> <span data-ttu-id="174da-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="174da-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="174da-223">Workpath test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="174da-223">Creating a Workpath test user</span></span>

<span data-ttu-id="174da-224">Workpath sadece kullanıcı zaman sağlama destekler.</span><span class="sxs-lookup"><span data-stu-id="174da-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="174da-225">Kimlik doğrulamasından sonra kullanıcılar hello uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="174da-225">After authentication users are created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="174da-226">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="174da-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="174da-227">Bu bölümde, erişim tooWorkpath vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="174da-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkpath.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="174da-229">**tooassign Britta Simon tooWorkpath hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="174da-229">**tooassign Britta Simon tooWorkpath, perform hello following steps:**</span></span>

1. <span data-ttu-id="174da-230">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="174da-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="174da-232">Merhaba uygulamalar listesinde **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="174da-232">In hello applications list, select **Workpath**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="174da-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="174da-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="174da-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="174da-236">Click **Add** button.</span></span> <span data-ttu-id="174da-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="174da-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="174da-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="174da-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="174da-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="174da-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="174da-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="174da-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="174da-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="174da-242">Testing single sign-on</span></span>

<span data-ttu-id="174da-243">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="174da-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="174da-244">Merhaba Workpath hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Workpath uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="174da-244">When you click hello Workpath tile in hello Access Panel, you should get automatically signed-on tooyour Workpath application.</span></span>
<span data-ttu-id="174da-245">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="174da-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="174da-246">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="174da-246">Additional resources</span></span>

* [<span data-ttu-id="174da-247">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="174da-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="174da-248">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="174da-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

