---
title: "Öğretici: Azure Active Directory Tümleştirme LinkedIn arama ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve LinkedIn arama arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="bdc93-103">Öğretici: Azure Active Directory Tümleştirme ile LinkedIn arama</span><span class="sxs-lookup"><span data-stu-id="bdc93-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="bdc93-104">Bu öğreticide, bilgi nasıl toointegrate LinkedIn arama Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdc93-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdc93-105">LinkedIn arama Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bdc93-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bdc93-106">Erişim tooLinkedIn arama sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bdc93-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="bdc93-107">Kullanıcıların tooautomatically get açan tooLinkedIn arama (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bdc93-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdc93-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bdc93-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bdc93-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdc93-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc93-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bdc93-110">Prerequisites</span></span>

<span data-ttu-id="bdc93-111">tooconfigure LinkedIn arama ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdc93-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="bdc93-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bdc93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdc93-113">Bir LinkedIn arama çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="bdc93-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdc93-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bdc93-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdc93-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdc93-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdc93-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bdc93-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdc93-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdc93-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdc93-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bdc93-118">Scenario description</span></span>
<span data-ttu-id="bdc93-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bdc93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdc93-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bdc93-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdc93-121">LinkedIn arama hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="bdc93-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="bdc93-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdc93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="bdc93-123">LinkedIn arama hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="bdc93-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="bdc93-124">Azure AD'ye tooconfigure hello tümleştirme LinkedIn arama tooadd LinkedIn arama hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc93-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdc93-125">**tooadd LinkedIn arama hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc93-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc93-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdc93-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bdc93-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bdc93-131">Tıklatın **yeni uygulama** hello iletişim tooadd yeni uygulamanın hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bdc93-133">Merhaba arama kutusuna yazın **LinkedIn arama**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="bdc93-135">Merhaba Sonuçlar panelinde seçin **LinkedIn arama**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bdc93-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdc93-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bdc93-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdc93-138">Bu bölümde, yapılandırmanız ve LinkedIn arama ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="bdc93-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdc93-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn aramada tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc93-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="bdc93-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve LinkedIn aramada hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdc93-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="bdc93-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LinkedIn aramada.</span><span class="sxs-lookup"><span data-stu-id="bdc93-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="bdc93-142">tooconfigure ve LinkedIn arama ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdc93-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdc93-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="bdc93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdc93-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="bdc93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdc93-145">**[Bir LinkedIn arama test kullanıcısı oluşturma](#creating-an-linkedin-lookup-test-user)**  -toohave karşılık gelen, Britta Simon LinkedIn aramada bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="bdc93-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="bdc93-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bdc93-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdc93-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="bdc93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdc93-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bdc93-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdc93-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LinkedIn arama uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bdc93-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="bdc93-150">**tooconfigure Azure AD çoklu oturum açma LinkedIn arama ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc93-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc93-151">Hello hello üzerinde Azure portal'ın **LinkedIn arama** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bdc93-153">Merhaba üzerinde **çoklu oturum açma** iletişim, **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="bdc93-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="bdc93-155">Farklı bir web tarayıcısı penceresinde, oturum açma tooyour **LinkedIn arama** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="bdc93-156">İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="bdc93-157">Ayrıca, seçin **arama** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="bdc93-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="bdc93-159">Tıklatın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) URL'si**</span><span class="sxs-lookup"><span data-stu-id="bdc93-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="bdc93-161">Azure Portal'da altında **LinkedIn arama etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="bdc93-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="bdc93-163">a.</span><span class="sxs-lookup"><span data-stu-id="bdc93-163">a.</span></span> <span data-ttu-id="bdc93-164">Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="bdc93-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="bdc93-165">b.</span><span class="sxs-lookup"><span data-stu-id="bdc93-165">b.</span></span> <span data-ttu-id="bdc93-166">Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="bdc93-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="bdc93-167">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="bdc93-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="bdc93-169">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="bdc93-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bdc93-170">Bu, gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="bdc93-170">This is not real value.</span></span> <span data-ttu-id="bdc93-171">Merhaba kullanıcının sahip tooupdate hello bu değerlerle gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="bdc93-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="bdc93-172">Kişi [LinkedIn arama istemci destek ekibi](https://business.LinkedIn.com/lookup) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="bdc93-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="bdc93-173">**LinkedIn arama** uygulama belirli bir biçimde hello SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="bdc93-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bdc93-174">Hello kullanıcı tooadd özel öznitelik eşlemelerini toohello SAML belirteci öznitelikleri yapılandırmasına sahip.</span><span class="sxs-lookup"><span data-stu-id="bdc93-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="bdc93-175">Aşağıdaki ekran görüntüsü hello bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="bdc93-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="bdc93-176">Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn arama hello kullanıcının e-posta adresiyle eşleşen bu toobe bekliyor.</span><span class="sxs-lookup"><span data-stu-id="bdc93-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="bdc93-177">Kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bdc93-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="bdc93-179">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bdc93-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="bdc93-180">Merhaba kullanıcının ihtiyacı tooadd dört talep adlı **e-posta**, **departmanı**, **firstname**, ve **lastname** ve hello değeri ile eşleşen toobe **user.mail**, **user.department**, **user.givenname**, ve **user.surname** sırasıyla</span><span class="sxs-lookup"><span data-stu-id="bdc93-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="bdc93-181">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="bdc93-181">Attribute Name</span></span> | <span data-ttu-id="bdc93-182">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="bdc93-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bdc93-183">E-posta</span><span class="sxs-lookup"><span data-stu-id="bdc93-183">email</span></span>| <span data-ttu-id="bdc93-184">User.Mail</span><span class="sxs-lookup"><span data-stu-id="bdc93-184">user.mail</span></span> |    
    | <span data-ttu-id="bdc93-185">Bölüm</span><span class="sxs-lookup"><span data-stu-id="bdc93-185">department</span></span>| <span data-ttu-id="bdc93-186">User.Department</span><span class="sxs-lookup"><span data-stu-id="bdc93-186">user.department</span></span> |
    | <span data-ttu-id="bdc93-187">FirstName</span><span class="sxs-lookup"><span data-stu-id="bdc93-187">firstname</span></span>| <span data-ttu-id="bdc93-188">User.givenName</span><span class="sxs-lookup"><span data-stu-id="bdc93-188">user.givenname</span></span> |
    | <span data-ttu-id="bdc93-189">Soyadı</span><span class="sxs-lookup"><span data-stu-id="bdc93-189">lastname</span></span>| <span data-ttu-id="bdc93-190">User.surname</span><span class="sxs-lookup"><span data-stu-id="bdc93-190">user.surname</span></span> |

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="bdc93-192">a.</span><span class="sxs-lookup"><span data-stu-id="bdc93-192">a.</span></span> <span data-ttu-id="bdc93-193">Tıklatın **özniteliği eklemek** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc93-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="bdc93-196">b.</span><span class="sxs-lookup"><span data-stu-id="bdc93-196">b.</span></span> <span data-ttu-id="bdc93-197">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="bdc93-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bdc93-198">c.</span><span class="sxs-lookup"><span data-stu-id="bdc93-198">c.</span></span> <span data-ttu-id="bdc93-199">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="bdc93-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bdc93-200">d.</span><span class="sxs-lookup"><span data-stu-id="bdc93-200">d.</span></span> <span data-ttu-id="bdc93-201">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="bdc93-201">Click **Ok**</span></span>

10. <span data-ttu-id="bdc93-202">Merhaba hello üzerinde aşağıdaki adımları gerçekleştirin **adı** öznitelik -</span><span class="sxs-lookup"><span data-stu-id="bdc93-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="bdc93-203">a.</span><span class="sxs-lookup"><span data-stu-id="bdc93-203">a.</span></span> <span data-ttu-id="bdc93-204">Tıklatın hello özniteliği tooopen hello üzerinde **öznitelik Düzenle** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="bdc93-206">b.</span><span class="sxs-lookup"><span data-stu-id="bdc93-206">b.</span></span> <span data-ttu-id="bdc93-207">Hello Hello URL değeri Sil **ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="bdc93-208">c.</span><span class="sxs-lookup"><span data-stu-id="bdc93-208">c.</span></span> <span data-ttu-id="bdc93-209">Tıklatın **Tamam** toosave hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="bdc93-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="bdc93-210">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bdc93-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="bdc93-212">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-212">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="bdc93-214">Çok Git**LinkedIn yönetici ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="bdc93-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="bdc93-215">Karşıya yükleme hello XML dosyasını hello Azure portal'ı karşıdan hello tıklayarak **karşıya yükleme XML dosyası** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bdc93-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="bdc93-217">Tıklatın **üzerinde** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="bdc93-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="bdc93-218">SSO durumu değişir **bağlı** çok**bağlandı**</span><span class="sxs-lookup"><span data-stu-id="bdc93-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="bdc93-220">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bdc93-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bdc93-221">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="bdc93-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bdc93-222">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdc93-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdc93-223">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdc93-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdc93-224">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="bdc93-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bdc93-226">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc93-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc93-227">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdc93-229">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdc93-231">Tıklatın **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc93-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdc93-233">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bdc93-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdc93-235">a.</span><span class="sxs-lookup"><span data-stu-id="bdc93-235">a.</span></span> <span data-ttu-id="bdc93-236">Merhaba, **adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="bdc93-237">b.</span><span class="sxs-lookup"><span data-stu-id="bdc93-237">b.</span></span> <span data-ttu-id="bdc93-238">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="bdc93-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bdc93-239">c.</span><span class="sxs-lookup"><span data-stu-id="bdc93-239">c.</span></span> <span data-ttu-id="bdc93-240">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bdc93-241">d.</span><span class="sxs-lookup"><span data-stu-id="bdc93-241">d.</span></span> <span data-ttu-id="bdc93-242">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bdc93-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="bdc93-243">Bir LinkedIn arama test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdc93-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="bdc93-244">Bağlantılı arama uygulama sadece kullanıcı zamanı (JIT) sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra destekler.</span><span class="sxs-lookup"><span data-stu-id="bdc93-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="bdc93-245">Etkinleştirme **otomatik olarak lisansları atama** tooassign lisans toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="bdc93-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bdc93-247">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bdc93-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bdc93-248">Bu bölümde, erişim tooLinkedIn arama vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bdc93-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bdc93-250">**tooassign Britta Simon tooLinkedIn arama hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bdc93-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc93-251">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bdc93-253">Merhaba uygulamalar listesinde **LinkedIn arama**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="bdc93-255">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bdc93-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bdc93-257">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc93-257">Click **Add** button.</span></span> <span data-ttu-id="bdc93-258">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc93-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bdc93-260">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bdc93-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bdc93-261">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc93-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdc93-262">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bdc93-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdc93-263">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bdc93-263">Testing single sign-on</span></span>

<span data-ttu-id="bdc93-264">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="bdc93-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdc93-265">LinkedIn arama döşeme hello erişim paneli hello tıklattığınızda yeniden yönlendirilen tooOrganizational sayfa tooprovide sahip olduğu kişisel LinkedIn hesap bilgilerinizi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bdc93-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="bdc93-266">Kişisel hesabınızı LinkedIn iş hesabınızla bağlar.</span><span class="sxs-lookup"><span data-stu-id="bdc93-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="bdc93-267">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdc93-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bdc93-268">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bdc93-268">Additional resources</span></span>

* [<span data-ttu-id="bdc93-269">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bdc93-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdc93-270">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bdc93-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

