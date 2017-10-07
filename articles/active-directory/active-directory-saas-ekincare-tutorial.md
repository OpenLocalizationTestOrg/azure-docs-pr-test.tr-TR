---
title: "Öğretici: Azure Active Directory Tümleştirme ile eKincare | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile eKincare arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="261af-103">Öğretici: Azure Active Directory Tümleştirme eKincare ile</span><span class="sxs-lookup"><span data-stu-id="261af-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="261af-104">Bu öğreticide, bilgi nasıl toointegrate eKincare Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="261af-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="261af-105">EKincare Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="261af-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="261af-106">Erişim tooeKincare sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="261af-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="261af-107">Kullanıcıların tooautomatically get açan tooeKincare (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="261af-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="261af-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="261af-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="261af-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="261af-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="261af-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="261af-110">Prerequisites</span></span>

<span data-ttu-id="261af-111">tooconfigure eKincare ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="261af-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="261af-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="261af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="261af-113">Bir eKincare çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="261af-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="261af-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="261af-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="261af-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="261af-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="261af-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="261af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="261af-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="261af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="261af-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="261af-118">Scenario description</span></span>
<span data-ttu-id="261af-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="261af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="261af-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="261af-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="261af-121">Merhaba Galerisi'nden eKincare ekleme</span><span class="sxs-lookup"><span data-stu-id="261af-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="261af-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="261af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="261af-123">Merhaba Galerisi'nden eKincare ekleme</span><span class="sxs-lookup"><span data-stu-id="261af-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="261af-124">Azure AD'ye tooconfigure hello tümleştirme eKincare, tooadd eKincare hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="261af-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="261af-125">**Merhaba galerisinden tooadd eKincare hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="261af-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="261af-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="261af-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="261af-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="261af-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="261af-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="261af-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="261af-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="261af-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="261af-133">Merhaba arama kutusuna yazın **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="261af-133">In hello search box, type **eKincare**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="261af-135">Merhaba Sonuçlar panelinde seçin **eKincare**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="261af-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="261af-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="261af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="261af-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı eKincare ile test etme</span><span class="sxs-lookup"><span data-stu-id="261af-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="261af-139">Tek toowork'ın oturum açma hangi hello karşılık gelen eKincare içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="261af-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="261af-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı eKincare hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="261af-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="261af-141">Merhaba hello değeri eKincare içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="261af-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="261af-142">tooconfigure ve eKincare ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="261af-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="261af-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="261af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="261af-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="261af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="261af-145">**[EKincare test kullanıcısı oluşturma](#creating-a-ekincare-test-user)**  -toohave bir Britta Simon karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir eKincare içinde.</span><span class="sxs-lookup"><span data-stu-id="261af-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="261af-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="261af-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="261af-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="261af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="261af-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="261af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="261af-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma eKincare uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="261af-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="261af-150">**tooconfigure Azure AD çoklu oturum açma ile eKincare, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="261af-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="261af-151">Hello hello üzerinde Azure portal'ın **eKincare** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="261af-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="261af-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="261af-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="261af-155">Merhaba üzerinde **eKincare etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="261af-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="261af-157">a.</span><span class="sxs-lookup"><span data-stu-id="261af-157">a.</span></span> <span data-ttu-id="261af-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="261af-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="261af-159">b.</span><span class="sxs-lookup"><span data-stu-id="261af-159">b.</span></span> <span data-ttu-id="261af-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="261af-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="261af-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="261af-161">These values are not real.</span></span> <span data-ttu-id="261af-162">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="261af-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="261af-163">Kişi [eKincare destek ekibi](mailto:tech@ekincare.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="261af-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="261af-164">eKincare uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="261af-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="261af-165">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="261af-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="261af-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="261af-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="261af-167">Ekran aşağıdaki hello Bu yapılandırmanın bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="261af-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="261af-168">Merhaba talep adı her zaman olacaktır **"EmployeeID"** ve hangisinin biz eşlenen hello kullanıcının hello EmployeeID içeren toouser.extensionattribute1 hello değeri.</span><span class="sxs-lookup"><span data-stu-id="261af-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="261af-169">diğer iki talep adı yani hello</span><span class="sxs-lookup"><span data-stu-id="261af-169">hello other two claims' name i.e</span></span> <span data-ttu-id="261af-170">**"organizationid"** ve **"Kuruluş adı"** her zaman aynı olacaktır ve bunların değerleri sırasıyla hello kullanıcı hello organizasyonu hello ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="261af-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="261af-172">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="261af-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="261af-173">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="261af-173">Attribute Name</span></span> | <span data-ttu-id="261af-174">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="261af-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="261af-175">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="261af-175">employeeid</span></span> | <span data-ttu-id="261af-176">*User.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="261af-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="261af-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="261af-177">organizationid</span></span> | <span data-ttu-id="261af-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="261af-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="261af-179">Kuruluş adı</span><span class="sxs-lookup"><span data-stu-id="261af-179">organizationname</span></span> | <span data-ttu-id="261af-180">*User.CompanyName*</span><span class="sxs-lookup"><span data-stu-id="261af-180">*user.companyname*</span></span> |

    <span data-ttu-id="261af-181">a.</span><span class="sxs-lookup"><span data-stu-id="261af-181">a.</span></span> <span data-ttu-id="261af-182">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="261af-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="261af-185">b.</span><span class="sxs-lookup"><span data-stu-id="261af-185">b.</span></span> <span data-ttu-id="261af-186">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="261af-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="261af-187">c.</span><span class="sxs-lookup"><span data-stu-id="261af-187">c.</span></span> <span data-ttu-id="261af-188">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="261af-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="261af-189">d.</span><span class="sxs-lookup"><span data-stu-id="261af-189">d.</span></span> <span data-ttu-id="261af-190">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="261af-190">Click **Ok**</span></span>

6. <span data-ttu-id="261af-191">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="261af-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="261af-193">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="261af-193">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="261af-195">tooconfigure çoklu oturum açma üzerinde **eKincare** yan, indirilen toosend hello ihtiyacınız **meta veri XML** çok[eKincare destek ekibi](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="261af-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="261af-196">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="261af-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="261af-197">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="261af-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="261af-198">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="261af-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="261af-199">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="261af-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="261af-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="261af-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="261af-201">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="261af-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="261af-203">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="261af-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="261af-204">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="261af-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="261af-206">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="261af-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="261af-208">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="261af-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="261af-210">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="261af-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="261af-212">a.</span><span class="sxs-lookup"><span data-stu-id="261af-212">a.</span></span> <span data-ttu-id="261af-213">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="261af-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="261af-214">b.</span><span class="sxs-lookup"><span data-stu-id="261af-214">b.</span></span> <span data-ttu-id="261af-215">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="261af-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="261af-216">c.</span><span class="sxs-lookup"><span data-stu-id="261af-216">c.</span></span> <span data-ttu-id="261af-217">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="261af-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="261af-218">d.</span><span class="sxs-lookup"><span data-stu-id="261af-218">d.</span></span> <span data-ttu-id="261af-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="261af-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="261af-220">EKincare test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="261af-220">Creating a eKincare test user</span></span>

<span data-ttu-id="261af-221">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="261af-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="261af-222">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="261af-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="261af-223">Bu bölümde, erişim tooeKincare vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="261af-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="261af-225">**tooassign Britta Simon tooeKincare hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="261af-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="261af-226">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="261af-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="261af-228">Merhaba uygulamalar listesinde **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="261af-228">In hello applications list, select **eKincare**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="261af-230">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="261af-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="261af-232">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="261af-232">Click **Add** button.</span></span> <span data-ttu-id="261af-233">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="261af-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="261af-235">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="261af-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="261af-236">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="261af-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="261af-237">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="261af-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="261af-238">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="261af-238">Testing single sign-on</span></span>

<span data-ttu-id="261af-239">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="261af-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="261af-240">Merhaba eKincare hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour eKincare uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="261af-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="261af-241">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="261af-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="261af-242">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="261af-242">Additional resources</span></span>

* [<span data-ttu-id="261af-243">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="261af-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="261af-244">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="261af-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

