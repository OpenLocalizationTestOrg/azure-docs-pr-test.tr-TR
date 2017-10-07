---
title: "Öğretici: Azure Active Directory Tümleştirme ile LinkedInSalesNavigator | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LinkedInSalesNavigator arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="89c98-103">Öğretici: Azure Active Directory Tümleştirme ile LinkedIn satış Gezgini</span><span class="sxs-lookup"><span data-stu-id="89c98-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="89c98-104">Bu öğreticide, bilgi nasıl toointegrate LinkedIn satış Gezgini Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89c98-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89c98-105">LinkedIn satış Gezgini Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="89c98-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89c98-106">Erişim tooLinkedIn satış Gezgini sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="89c98-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="89c98-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooLinkedIn satış Gezgini (çoklu oturum açma) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="89c98-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89c98-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="89c98-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="89c98-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow isterseniz, Gözat [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89c98-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89c98-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89c98-110">Prerequisites</span></span>

<span data-ttu-id="89c98-111">tooconfigure LinkedIn satış Gezgini ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="89c98-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="89c98-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="89c98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89c98-113">Bir LinkedIn satış Gezgini çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="89c98-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89c98-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="89c98-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89c98-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="89c98-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89c98-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="89c98-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89c98-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89c98-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89c98-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="89c98-118">Scenario description</span></span>
<span data-ttu-id="89c98-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="89c98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89c98-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="89c98-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89c98-121">LinkedIn satış Gezgini hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="89c98-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="89c98-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="89c98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="89c98-123">LinkedIn satış Gezgini hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="89c98-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="89c98-124">Azure AD'ye tooconfigure hello tümleştirme LinkedIn satış Gezgini, tooadd LinkedIn satış Gezgini hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="89c98-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89c98-125">**tooadd LinkedIn satış Gezgini hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89c98-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89c98-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="89c98-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89c98-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="89c98-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89c98-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="89c98-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="89c98-131">Tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89c98-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="89c98-133">Merhaba arama kutusuna yazın **LinkedIn satış Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="89c98-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="89c98-135">Merhaba Sonuçlar panelinde seçin **LinkedIn satış Gezgini**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="89c98-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89c98-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="89c98-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89c98-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma LinkedIn satış "Britta Simon" adlı bir test kullanıcı tabanlı Gezgini ile test etme.</span><span class="sxs-lookup"><span data-stu-id="89c98-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89c98-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn satış Gezgininde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="89c98-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="89c98-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve LinkedIn satış Gezgininde hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="89c98-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="89c98-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LinkedIn satış Gezgininde.</span><span class="sxs-lookup"><span data-stu-id="89c98-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="89c98-142">tooconfigure ve Azure AD çoklu oturum açma LinkedIn satış Gezgini ile test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="89c98-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89c98-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="89c98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89c98-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="89c98-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89c98-145">**[Bir LinkedIn satış Gezgini test kullanıcısı oluşturma](#creating-a-linkedin-sales-navigator-test-user) ** -toohave karşılık gelen, Britta Simon LinkedIn satış Gezgininde, hello kullanıcı bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="89c98-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="89c98-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="89c98-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89c98-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="89c98-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89c98-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89c98-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89c98-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LinkedIn satış Gezgini uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89c98-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="89c98-150">**Azure AD çoklu oturum açma tooconfigure LinkedIn satış Gezgini ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89c98-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="89c98-151">Merhaba hello üzerinde Azure portal'ın **LinkedIn satış Gezgini** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="89c98-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="89c98-153">Merhaba üzerinde **çoklu oturum açma** iletişim, **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="89c98-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="89c98-155">Farklı bir web tarayıcısı penceresinde, oturum açma tooyour **LinkedIn satış Gezgini** yönetici olarak Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="89c98-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="89c98-156">İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="89c98-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="89c98-157">Ayrıca, seçin **satış Gezgini** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="89c98-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="89c98-159">Tıklatın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) Url**.</span><span class="sxs-lookup"><span data-stu-id="89c98-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="89c98-161">Azure Portal'da altında **LinkedIn satış Gezgini etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modunda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="89c98-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="89c98-163">a.</span><span class="sxs-lookup"><span data-stu-id="89c98-163">a.</span></span> <span data-ttu-id="89c98-164">Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="89c98-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="89c98-165">b.</span><span class="sxs-lookup"><span data-stu-id="89c98-165">b.</span></span> <span data-ttu-id="89c98-166">Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="89c98-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="89c98-167">Denetleyin **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="89c98-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="89c98-169">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="89c98-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="89c98-170">**LinkedIn satış Gezgini** uygulama tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, hello SAML onaylar bekler.</span><span class="sxs-lookup"><span data-stu-id="89c98-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="89c98-171">Aşağıdaki ekran görüntüsü hello bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="89c98-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="89c98-172">Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn satış Gezgini, hello kullanıcının e-posta adresiyle eşleşen toobe bekliyor.</span><span class="sxs-lookup"><span data-stu-id="89c98-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="89c98-173">Kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="89c98-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="89c98-175">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="89c98-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="89c98-176">Merhaba kullanıcının ihtiyacı tooadd dört talep adlı **e-posta**, **departmanı**, **firstname**, ve **lastname** ve hello değeri ile eşleşen toobe **user.mail**, **user.department**, **user.givenname**, ve **user.surname** sırasıyla</span><span class="sxs-lookup"><span data-stu-id="89c98-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="89c98-177">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="89c98-177">Attribute Name</span></span> | <span data-ttu-id="89c98-178">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="89c98-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="89c98-179">E-posta</span><span class="sxs-lookup"><span data-stu-id="89c98-179">email</span></span>| <span data-ttu-id="89c98-180">User.Mail</span><span class="sxs-lookup"><span data-stu-id="89c98-180">user.mail</span></span> |
    | <span data-ttu-id="89c98-181">Bölüm</span><span class="sxs-lookup"><span data-stu-id="89c98-181">department</span></span>| <span data-ttu-id="89c98-182">User.Department</span><span class="sxs-lookup"><span data-stu-id="89c98-182">user.department</span></span> |
    | <span data-ttu-id="89c98-183">FirstName</span><span class="sxs-lookup"><span data-stu-id="89c98-183">firstname</span></span>| <span data-ttu-id="89c98-184">User.givenName</span><span class="sxs-lookup"><span data-stu-id="89c98-184">user.givenname</span></span> |
    | <span data-ttu-id="89c98-185">Soyadı</span><span class="sxs-lookup"><span data-stu-id="89c98-185">lastname</span></span>| <span data-ttu-id="89c98-186">User.surname</span><span class="sxs-lookup"><span data-stu-id="89c98-186">user.surname</span></span> |
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="89c98-188">a.</span><span class="sxs-lookup"><span data-stu-id="89c98-188">a.</span></span> <span data-ttu-id="89c98-189">Tıklayın **özniteliği eklemek** tooopen hello özniteliği iletişim.</span><span class="sxs-lookup"><span data-stu-id="89c98-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="89c98-192">b.</span><span class="sxs-lookup"><span data-stu-id="89c98-192">b.</span></span> <span data-ttu-id="89c98-193">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="89c98-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="89c98-194">c.</span><span class="sxs-lookup"><span data-stu-id="89c98-194">c.</span></span> <span data-ttu-id="89c98-195">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="89c98-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="89c98-196">d.</span><span class="sxs-lookup"><span data-stu-id="89c98-196">d.</span></span> <span data-ttu-id="89c98-197">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="89c98-197">Click **Ok**</span></span>

10. <span data-ttu-id="89c98-198">Merhaba hello üzerinde aşağıdaki adımları gerçekleştirin **adı** öznitelik -</span><span class="sxs-lookup"><span data-stu-id="89c98-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="89c98-199">a.</span><span class="sxs-lookup"><span data-stu-id="89c98-199">a.</span></span> <span data-ttu-id="89c98-200">Tıklatın hello özniteliği tooopen hello üzerinde **öznitelik Düzenle** penceresi.</span><span class="sxs-lookup"><span data-stu-id="89c98-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="89c98-202">b.</span><span class="sxs-lookup"><span data-stu-id="89c98-202">b.</span></span> <span data-ttu-id="89c98-203">Hello Hello URL değeri Sil **ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="89c98-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="89c98-204">c.</span><span class="sxs-lookup"><span data-stu-id="89c98-204">c.</span></span> <span data-ttu-id="89c98-205">Tıklatın **Tamam** toosave hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="89c98-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="89c98-206">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89c98-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="89c98-208">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89c98-208">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="89c98-210">Çok Git**LinkedIn yönetici ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="89c98-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="89c98-211">Tıklatın **karşıya yükleme XML dosyası** tooupload hello hello Azure portal ' indirmiş meta veri XML dosyası.</span><span class="sxs-lookup"><span data-stu-id="89c98-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="89c98-213">Tıklatın **üzerinde** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="89c98-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="89c98-214">SSO durumu değişir **bağlı** çok**bağlandı**</span><span class="sxs-lookup"><span data-stu-id="89c98-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="89c98-216">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="89c98-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89c98-217">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="89c98-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89c98-218">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89c98-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89c98-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89c98-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="89c98-220">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="89c98-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="89c98-222">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89c98-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89c98-223">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="89c98-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89c98-225">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="89c98-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89c98-227">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89c98-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89c98-229">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="89c98-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89c98-231">a.</span><span class="sxs-lookup"><span data-stu-id="89c98-231">a.</span></span> <span data-ttu-id="89c98-232">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89c98-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89c98-233">b.</span><span class="sxs-lookup"><span data-stu-id="89c98-233">b.</span></span> <span data-ttu-id="89c98-234">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="89c98-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89c98-235">c.</span><span class="sxs-lookup"><span data-stu-id="89c98-235">c.</span></span> <span data-ttu-id="89c98-236">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="89c98-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="89c98-237">d.</span><span class="sxs-lookup"><span data-stu-id="89c98-237">d.</span></span> <span data-ttu-id="89c98-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89c98-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="89c98-239">Bir LinkedIn satış Gezgini test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89c98-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="89c98-240">Bağlantılı satış Gezgin uygulaması sadece kullanıcı zamanı (JIT) sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra destekler.</span><span class="sxs-lookup"><span data-stu-id="89c98-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="89c98-241">Etkinleştirme **otomatik olarak lisansları atama** tooassign lisans toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="89c98-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="89c98-243">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="89c98-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="89c98-244">Bu bölümde, erişim tooLinkedIn satış Gezgini vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="89c98-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="89c98-246">**tooassign Britta Simon tooLinkedIn satış Gezgini hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89c98-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="89c98-247">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="89c98-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="89c98-249">Merhaba uygulamalar listesinde **LinkedIn satış Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="89c98-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="89c98-251">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="89c98-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="89c98-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89c98-253">Click **Add** button.</span></span> <span data-ttu-id="89c98-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89c98-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="89c98-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="89c98-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89c98-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89c98-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89c98-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89c98-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89c98-259">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="89c98-259">Testing single sign-on</span></span>

<span data-ttu-id="89c98-260">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="89c98-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89c98-261">Merhaba LinkedIn satış Gezgini hello erişim paneli parçasında tıklattığınızda yeniden yönlendirilen tooOrganizational sayfa tooprovide sahip olduğu kişisel LinkedIn hesap bilgilerinizi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89c98-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="89c98-262">Kişisel hesabınızı LinkedIn iş hesabınızla bağlar.</span><span class="sxs-lookup"><span data-stu-id="89c98-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="89c98-263">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="89c98-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89c98-264">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="89c98-264">Additional resources</span></span>

* [<span data-ttu-id="89c98-265">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="89c98-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89c98-266">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="89c98-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

