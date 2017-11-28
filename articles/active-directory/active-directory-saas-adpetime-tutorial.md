---
title: "Öğretici: Azure Active Directory Tümleştirme ile ADP eTime | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ADP eTime arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="05cc9-103">Öğretici: Azure Active Directory Tümleştirme ADP eTime ile</span><span class="sxs-lookup"><span data-stu-id="05cc9-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="05cc9-104">Bu öğreticide, bilgi nasıl toointegrate ADP eTime Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05cc9-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05cc9-105">ADP eTime Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="05cc9-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05cc9-106">Erişim tooADP eTime sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="05cc9-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="05cc9-107">Kullanıcıların tooautomatically get açan tooADP eTime (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="05cc9-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05cc9-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="05cc9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="05cc9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05cc9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05cc9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="05cc9-110">Prerequisites</span></span>

<span data-ttu-id="05cc9-111">tooconfigure ADP eTime ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="05cc9-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="05cc9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="05cc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05cc9-113">Bir ADP eTime çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="05cc9-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05cc9-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="05cc9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05cc9-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="05cc9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05cc9-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="05cc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05cc9-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05cc9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05cc9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="05cc9-118">Scenario description</span></span>
<span data-ttu-id="05cc9-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="05cc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05cc9-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="05cc9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05cc9-121">Merhaba Galerisi'nden ADP eTime ekleme</span><span class="sxs-lookup"><span data-stu-id="05cc9-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="05cc9-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="05cc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="05cc9-123">Merhaba Galerisi'nden ADP eTime ekleme</span><span class="sxs-lookup"><span data-stu-id="05cc9-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="05cc9-124">Azure AD'ye tooconfigure hello tümleştirme ADP eTime, tooadd ADP eTime hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05cc9-125">**Merhaba galerisinden tooadd ADP eTime hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="05cc9-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05cc9-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="05cc9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05cc9-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05cc9-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="05cc9-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="05cc9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="05cc9-133">Merhaba arama kutusuna yazın **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-133">In hello search box, type **ADP eTime**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="05cc9-135">Merhaba Sonuçlar panelinde seçin **ADP eTime**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="05cc9-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05cc9-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="05cc9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05cc9-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı ADP eTime ile test etme</span><span class="sxs-lookup"><span data-stu-id="05cc9-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05cc9-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ADP eTime içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="05cc9-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ADP eTime hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="05cc9-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ADP eTime içinde.</span><span class="sxs-lookup"><span data-stu-id="05cc9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="05cc9-142">tooconfigure ve ADP eTime ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="05cc9-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05cc9-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="05cc9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05cc9-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="05cc9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05cc9-145">**[Bir ADP eTime test kullanıcısı oluşturma](#creating-an-adp-etime-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir ADP eTime içinde.</span><span class="sxs-lookup"><span data-stu-id="05cc9-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05cc9-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="05cc9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05cc9-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="05cc9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05cc9-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="05cc9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05cc9-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ADP eTime uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="05cc9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="05cc9-150">**tooconfigure Azure AD çoklu oturum açma ADP eTime ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="05cc9-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="05cc9-151">Hello hello üzerinde Azure portal'ın **ADP eTime** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="05cc9-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="05cc9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="05cc9-155">Merhaba üzerinde **ADP eTime etki alanı ve URL'leri** bölümünde, adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="05cc9-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="05cc9-157">a.</span><span class="sxs-lookup"><span data-stu-id="05cc9-157">a.</span></span> <span data-ttu-id="05cc9-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="05cc9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="05cc9-159">b.</span><span class="sxs-lookup"><span data-stu-id="05cc9-159">b.</span></span> <span data-ttu-id="05cc9-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="05cc9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="05cc9-161">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-161">These values are not hello real.</span></span> <span data-ttu-id="05cc9-162">Bu değerleri hello gerçek yanıt URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="05cc9-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="05cc9-163">Kişi [ADP eTime destek ekibi](https://www.adp.com/contact-us/overview.aspx) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="05cc9-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="05cc9-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="05cc9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="05cc9-166">Merhaba ADP eTime uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="05cc9-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="05cc9-167">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="05cc9-168">Merhaba talep adı her zaman olacaktır **"PersonImmutableID"** ve hangisinin biz eşlenen içeren tooExtensionAttribute2 hello değeri hello hello kullanıcının EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="05cc9-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="05cc9-169">Burada Azure AD tooADP eTime hello kullanıcı eşlemeyi EmployeeID hello üzerinde gerçekleştirilir ancak aynı zamanda uygulama ayarlarınızı temel alan bu tooa farklı bir değer eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05cc9-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="05cc9-170">İş, bu nedenle Lütfen ile [ADP eTime destek ekibi](https://www.adp.com/contact-us/overview.aspx) ilk toouse bir kullanıcının doğru tanıtıcısı hello ve söz konusu hello değerle eşleyin **"PersonImmutableID"** talep.</span><span class="sxs-lookup"><span data-stu-id="05cc9-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="05cc9-172">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="05cc9-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="05cc9-173">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="05cc9-173">Attribute Name</span></span> | <span data-ttu-id="05cc9-174">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="05cc9-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="05cc9-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="05cc9-175">PersonImmutableID</span></span> | <span data-ttu-id="05cc9-176">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="05cc9-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="05cc9-177">a.</span><span class="sxs-lookup"><span data-stu-id="05cc9-177">a.</span></span> <span data-ttu-id="05cc9-178">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="05cc9-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="05cc9-181">b.</span><span class="sxs-lookup"><span data-stu-id="05cc9-181">b.</span></span> <span data-ttu-id="05cc9-182">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="05cc9-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="05cc9-183">c.</span><span class="sxs-lookup"><span data-stu-id="05cc9-183">c.</span></span> <span data-ttu-id="05cc9-184">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="05cc9-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="05cc9-185">d.</span><span class="sxs-lookup"><span data-stu-id="05cc9-185">d.</span></span> <span data-ttu-id="05cc9-186">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="05cc9-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05cc9-187">Merhaba SAML onayı yapılandırmadan önce toocontact gerekir, [ADP eTime destek ekibi](https://www.adp.com/contact-us/overview.aspx) ve kiracınız için hello benzersiz tanımlayıcı özniteliği hello değerini isteyin.</span><span class="sxs-lookup"><span data-stu-id="05cc9-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="05cc9-188">Değer bu tooconfigure hello özel talep uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="05cc9-189">Merhaba üzerinde **ADP eTime yapılandırma** 'yi tıklatın **yapılandırma ADP eTime** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="05cc9-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="05cc9-191">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="05cc9-191">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="05cc9-193">tooconfigure çoklu oturum açma üzerinde **ADP eTime** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[ADP eTime destek ekibi](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="05cc9-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="05cc9-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="05cc9-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05cc9-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="05cc9-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05cc9-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05cc9-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05cc9-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="05cc9-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="05cc9-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="05cc9-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="05cc9-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="05cc9-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05cc9-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="05cc9-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05cc9-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05cc9-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="05cc9-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05cc9-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="05cc9-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05cc9-209">a.</span><span class="sxs-lookup"><span data-stu-id="05cc9-209">a.</span></span> <span data-ttu-id="05cc9-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05cc9-211">b.</span><span class="sxs-lookup"><span data-stu-id="05cc9-211">b.</span></span> <span data-ttu-id="05cc9-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="05cc9-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05cc9-213">c.</span><span class="sxs-lookup"><span data-stu-id="05cc9-213">c.</span></span> <span data-ttu-id="05cc9-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="05cc9-215">d.</span><span class="sxs-lookup"><span data-stu-id="05cc9-215">d.</span></span> <span data-ttu-id="05cc9-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="05cc9-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="05cc9-217">Bir ADP eTime test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="05cc9-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="05cc9-218">Bu bölümde Hello amacı toocreate Britta Simon ADP eTime adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="05cc9-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="05cc9-219">Çalışmak [ADP eTime destek ekibi](https://www.adp.com/contact-us/overview.aspx) hello ADP eTime hesap tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="05cc9-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="05cc9-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="05cc9-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="05cc9-221">Bu bölümde, erişim tooADP eTime vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="05cc9-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="05cc9-223">**tooassign Britta Simon tooADP eTime hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="05cc9-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="05cc9-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="05cc9-226">Merhaba uygulamalar listesinde **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="05cc9-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="05cc9-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="05cc9-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="05cc9-230">Click **Add** button.</span></span> <span data-ttu-id="05cc9-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="05cc9-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="05cc9-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="05cc9-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05cc9-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="05cc9-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05cc9-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="05cc9-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05cc9-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="05cc9-236">Testing single sign-on</span></span>

<span data-ttu-id="05cc9-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="05cc9-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="05cc9-238">Merhaba ADP eTime hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma ADP tooyour eTime uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05cc9-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="05cc9-239">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05cc9-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05cc9-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="05cc9-240">Additional resources</span></span>

* [<span data-ttu-id="05cc9-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="05cc9-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05cc9-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="05cc9-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

