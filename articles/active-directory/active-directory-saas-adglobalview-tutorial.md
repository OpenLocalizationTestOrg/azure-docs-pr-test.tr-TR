---
title: "Öğretici: Azure Active Directory Tümleştirme ile ADP Globalview | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ADP Globalview arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="4e476-103">Öğretici: Azure Active Directory Tümleştirme ADP Globalview ile</span><span class="sxs-lookup"><span data-stu-id="4e476-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="4e476-104">Bu öğreticide, bilgi nasıl toointegrate ADP Globalview Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e476-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e476-105">ADP Globalview Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4e476-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e476-106">Erişim tooADP Globalview sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4e476-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="4e476-107">Kullanıcıların tooautomatically get açan tooADP Globalview (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4e476-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e476-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4e476-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4e476-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e476-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e476-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e476-110">Prerequisites</span></span>

<span data-ttu-id="4e476-111">tooconfigure ADP Globalview ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e476-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="4e476-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4e476-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e476-113">Bir ADP Globalview çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4e476-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e476-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4e476-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e476-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e476-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e476-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4e476-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e476-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e476-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e476-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4e476-118">Scenario description</span></span>
<span data-ttu-id="4e476-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4e476-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e476-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4e476-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e476-121">Merhaba Galerisi'nden ADP Globalview ekleme</span><span class="sxs-lookup"><span data-stu-id="4e476-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="4e476-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4e476-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="4e476-123">Merhaba Galerisi'nden ADP Globalview ekleme</span><span class="sxs-lookup"><span data-stu-id="4e476-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="4e476-124">Azure AD'ye tooconfigure hello tümleştirme ADP Globalview, tooadd ADP Globalview hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e476-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e476-125">**tooadd ADP Globalview hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e476-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e476-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4e476-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e476-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4e476-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e476-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4e476-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4e476-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e476-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4e476-133">Merhaba arama kutusuna yazın **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="4e476-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="4e476-135">Merhaba Sonuçlar panelinde seçin **ADP Globalview**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4e476-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e476-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4e476-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e476-138">Bu bölümde, yapılandırmanız ve ADP Globalview ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="4e476-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e476-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ADP Globalview içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e476-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="4e476-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ADP Globalview hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e476-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="4e476-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ADP Globalview içinde.</span><span class="sxs-lookup"><span data-stu-id="4e476-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="4e476-142">tooconfigure ve ADP Globalview ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4e476-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e476-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4e476-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e476-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4e476-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e476-145">**[ADP Globalview test kullanıcısı oluşturma](#creating-an-adp-globalview-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ADP Globalview içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="4e476-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e476-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4e476-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e476-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4e476-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e476-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e476-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e476-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ADP Globalview uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4e476-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="4e476-150">**tooconfigure Azure AD çoklu oturum açma ADP Globalview ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e476-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e476-151">Hello hello üzerinde Azure portal'ın **ADP Globalview** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4e476-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4e476-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4e476-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="4e476-155">Merhaba üzerinde **ADP Globalview etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e476-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="4e476-157">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın: `https://<subdomain>.globalview.adp.com/federate` veya`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="4e476-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e476-158">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="4e476-158">hello value is not real.</span></span> <span data-ttu-id="4e476-159">Merhaba değeri ile Merhaba güncelleştirin gerçek tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e476-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="4e476-160">Kişi [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="4e476-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="4e476-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4e476-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="4e476-163">Merhaba ADP GlobalView uygulama hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="4e476-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="4e476-164">Aşağıdaki ekran görüntüsü hello için bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e476-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="4e476-165">Merhaba talep adlarının her zaman olması **"PersonImmutableID"** ve hangisinin biz eşlenen içeren tooExtensionAttribute2 hello değeri hello hello kullanıcının EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="4e476-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="4e476-166">Burada Azure AD tooADP GlobalView hello kullanıcı eşlemeyi EmployeeID hello üzerinde gerçekleştirilir ancak tooa farklı değer de uygulama ayarlarınızı temel alan eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e476-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="4e476-167">İş hello ADP GlobalView takım ilk toouse hello doğru tanıtıcısı bir kullanıcı ile ve bu değerle hello eşleyin **"PersonImmutableID"** talep.</span><span class="sxs-lookup"><span data-stu-id="4e476-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="4e476-168">Ayrıca hello resimde görüldüğü gibi hello e-posta ve UserID talep eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e476-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="4e476-170">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e476-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4e476-171">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="4e476-171">Attribute Name</span></span> | <span data-ttu-id="4e476-172">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="4e476-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="4e476-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="4e476-173">personalimmutableid</span></span> | <span data-ttu-id="4e476-174">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="4e476-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="4e476-175">E-posta</span><span class="sxs-lookup"><span data-stu-id="4e476-175">email</span></span>               | <span data-ttu-id="4e476-176">User.Mail</span><span class="sxs-lookup"><span data-stu-id="4e476-176">user.mail</span></span> |
    | <span data-ttu-id="4e476-177">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="4e476-177">userid</span></span>              | <span data-ttu-id="4e476-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="4e476-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="4e476-179">a.</span><span class="sxs-lookup"><span data-stu-id="4e476-179">a.</span></span> <span data-ttu-id="4e476-180">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e476-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4e476-183">b.</span><span class="sxs-lookup"><span data-stu-id="4e476-183">b.</span></span> <span data-ttu-id="4e476-184">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="4e476-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4e476-185">c.</span><span class="sxs-lookup"><span data-stu-id="4e476-185">c.</span></span> <span data-ttu-id="4e476-186">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="4e476-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4e476-187">d.</span><span class="sxs-lookup"><span data-stu-id="4e476-187">d.</span></span> <span data-ttu-id="4e476-188">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e476-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e476-189">Merhaba SAML onayı yapılandırmadan önce toocontact gerekir, [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) ve kiracınız için hello benzersiz tanımlayıcı özniteliği hello değerini isteyin.</span><span class="sxs-lookup"><span data-stu-id="4e476-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="4e476-190">Değer bu tooconfigure hello özel talep uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e476-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="4e476-191">Merhaba üzerinde **ADP Globalview yapılandırma** 'yi tıklatın **yapılandırma ADP Globalview** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4e476-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4e476-192">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4e476-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="4e476-194">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e476-194">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="4e476-196">tooconfigure çoklu oturum açma üzerinde **ADP Globalview** yan, indirilen toosend hello ihtiyacınız **sertifika (Base64)**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e476-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="4e476-197">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4e476-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4e476-198">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4e476-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4e476-199">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e476-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e476-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e476-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e476-201">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4e476-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4e476-203">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e476-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e476-204">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4e476-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="4e476-206">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4e476-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e476-208">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e476-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e476-210">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4e476-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e476-212">a.</span><span class="sxs-lookup"><span data-stu-id="4e476-212">a.</span></span> <span data-ttu-id="4e476-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e476-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e476-214">b.</span><span class="sxs-lookup"><span data-stu-id="4e476-214">b.</span></span> <span data-ttu-id="4e476-215">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4e476-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e476-216">c.</span><span class="sxs-lookup"><span data-stu-id="4e476-216">c.</span></span> <span data-ttu-id="4e476-217">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4e476-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4e476-218">d.</span><span class="sxs-lookup"><span data-stu-id="4e476-218">d.</span></span> <span data-ttu-id="4e476-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e476-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="4e476-220">ADP Globalview test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e476-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="4e476-221">Bu bölümde Hello amacı toocreate Britta Simon ADP GlobalView adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="4e476-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="4e476-222">Çalışmak [ADP Globalview Destek](https://www.adp.com/contact-us/overview.aspx) tooadd hello hello ADP GlobalView hesap kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="4e476-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4e476-223">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4e476-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4e476-224">Bu bölümde, erişim tooADP Globalview vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4e476-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4e476-226">**tooassign Britta Simon tooADP Globalview, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4e476-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e476-227">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4e476-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4e476-229">Merhaba uygulamalar listesinde **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="4e476-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="4e476-231">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4e476-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4e476-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e476-233">Click **Add** button.</span></span> <span data-ttu-id="4e476-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e476-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4e476-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4e476-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e476-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e476-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e476-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4e476-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e476-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4e476-239">Testing single sign-on</span></span>

<span data-ttu-id="4e476-240">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4e476-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="4e476-241">ADP GlobalView döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma ADP GlobalView uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e476-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e476-242">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4e476-242">Additional resources</span></span>

* [<span data-ttu-id="4e476-243">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4e476-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e476-244">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4e476-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

