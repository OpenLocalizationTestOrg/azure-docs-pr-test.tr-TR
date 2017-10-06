---
title: "Öğretici: Azure Active Directory Tümleştirme ile LinkedIn öğrenme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve LinkedIn öğrenme arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="0bab4-103">Öğretici: Azure Active Directory Tümleştirme ile LinkedIn öğrenme</span><span class="sxs-lookup"><span data-stu-id="0bab4-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="0bab4-104">Bu öğreticide, bilgi nasıl toointegrate LinkedIn öğrenme Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0bab4-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0bab4-105">LinkedIn öğrenme Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="0bab4-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0bab4-106">Erişim tooLinkedIn sahip Azure AD'de denetleyebilirsiniz öğrenme</span><span class="sxs-lookup"><span data-stu-id="0bab4-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="0bab4-107">Oturum açma, kullanıcıların tooautomatically get tooLinkedIn etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip öğrenme</span><span class="sxs-lookup"><span data-stu-id="0bab4-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0bab4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="0bab4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0bab4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0bab4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bab4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0bab4-110">Prerequisites</span></span>

<span data-ttu-id="0bab4-111">tooconfigure LinkedIn öğrenme ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0bab4-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="0bab4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="0bab4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0bab4-113">Bir LinkedIn öğrenme çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="0bab4-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0bab4-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0bab4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0bab4-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="0bab4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0bab4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="0bab4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0bab4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bab4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0bab4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="0bab4-118">Scenario description</span></span>
<span data-ttu-id="0bab4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="0bab4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0bab4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="0bab4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0bab4-121">LinkedIn öğrenme hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0bab4-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="0bab4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0bab4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="0bab4-123">LinkedIn öğrenme hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="0bab4-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="0bab4-124">Azure AD'ye tooconfigure hello tümleştirme LinkedIn öğrenme tooadd LinkedIn öğrenme hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0bab4-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0bab4-125">**tooadd LinkedIn öğrenme hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0bab4-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bab4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0bab4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0bab4-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0bab4-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="0bab4-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0bab4-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="0bab4-133">Merhaba arama kutusuna yazın **LinkedIn öğrenme**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="0bab4-134">Sonuçları panelinden tıklatın **LinkedIn öğrenme** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0bab4-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0bab4-136">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="0bab4-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0bab4-137">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma LinkedIn "Britta Simon" adlı bir test kullanıcı tabanlı Learning ile test etme.</span><span class="sxs-lookup"><span data-stu-id="0bab4-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0bab4-138">Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn learning'de tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="0bab4-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="0bab4-139">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LinkedIn öğrenme hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0bab4-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="0bab4-140">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** LinkedIn learning'de.</span><span class="sxs-lookup"><span data-stu-id="0bab4-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="0bab4-141">tooconfigure ve LinkedIn Learning ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0bab4-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0bab4-142">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="0bab4-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0bab4-143">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0bab4-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0bab4-144">**[Bir LinkedIn öğrenme test kullanıcısı oluşturma](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="0bab4-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="0bab4-145">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0bab4-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0bab4-146">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="0bab4-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0bab4-147">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0bab4-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0bab4-148">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LinkedIn öğrenme uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0bab4-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="0bab4-149">**tooconfigure Azure AD çoklu oturum açma LinkedIn Learning ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0bab4-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bab4-150">Merhaba hello üzerinde Azure portal'ın **LinkedIn öğrenme** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="0bab4-152">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="0bab4-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="0bab4-154">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour LinkedIn öğrenme Kiracı.</span><span class="sxs-lookup"><span data-stu-id="0bab4-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="0bab4-155">İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="0bab4-156">Ayrıca, seçin **öğrenme - varsayılan** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="0bab4-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="0bab4-158">Tıklatın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) URL'si**</span><span class="sxs-lookup"><span data-stu-id="0bab4-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="0bab4-160">Azure Portal'da altında **LinkedIn öğrenme etki alanı ve URL'leri**, hello tooconfigure SSO istiyorsanız aşağıdaki adımları gerçekleştirin içinde **IDP başlatılan** modu</span><span class="sxs-lookup"><span data-stu-id="0bab4-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="0bab4-162">a.</span><span class="sxs-lookup"><span data-stu-id="0bab4-162">a.</span></span> <span data-ttu-id="0bab4-163">Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="0bab4-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="0bab4-164">b.</span><span class="sxs-lookup"><span data-stu-id="0bab4-164">b.</span></span> <span data-ttu-id="0bab4-165">Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="0bab4-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="0bab4-166">Tooconfigure SSO istiyorsanız içinde **SP tarafından başlatılan**, ardından hello yapılandırma bölümündeki Gelişmiş URL Göster ayarı seçeneğini tıklatın ve desen aşağıdaki hello ile hello oturum açma URL'si yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0bab4-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="0bab4-168">LinkedIn öğrenme uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0bab4-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="0bab4-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0bab4-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="0bab4-170">Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn öğrenme hello kullanıcının e-posta adresiyle eşleşen bu toobe bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0bab4-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="0bab4-171">Bunun için kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="0bab4-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="0bab4-173">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0bab4-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="0bab4-174">Merhaba kullanıcının ihtiyacı tooadd dört talep adlı **e-posta**, **departmanı**, **firstname**, ve **lastname** ve hello değeri ile eşleşen toobe **user.mail**, **user.department**, **user.givenname**, ve **user.surname** sırasıyla</span><span class="sxs-lookup"><span data-stu-id="0bab4-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="0bab4-175">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="0bab4-175">Attribute Name</span></span> | <span data-ttu-id="0bab4-176">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="0bab4-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0bab4-177">E-posta</span><span class="sxs-lookup"><span data-stu-id="0bab4-177">email</span></span>| <span data-ttu-id="0bab4-178">User.Mail</span><span class="sxs-lookup"><span data-stu-id="0bab4-178">user.mail</span></span> |    
    | <span data-ttu-id="0bab4-179">Bölüm</span><span class="sxs-lookup"><span data-stu-id="0bab4-179">department</span></span>| <span data-ttu-id="0bab4-180">User.Department</span><span class="sxs-lookup"><span data-stu-id="0bab4-180">user.department</span></span> |
    | <span data-ttu-id="0bab4-181">FirstName</span><span class="sxs-lookup"><span data-stu-id="0bab4-181">firstname</span></span>| <span data-ttu-id="0bab4-182">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0bab4-182">user.givenname</span></span> |
    | <span data-ttu-id="0bab4-183">Soyadı</span><span class="sxs-lookup"><span data-stu-id="0bab4-183">lastname</span></span>| <span data-ttu-id="0bab4-184">User.surname</span><span class="sxs-lookup"><span data-stu-id="0bab4-184">user.surname</span></span> |
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="0bab4-186">a.</span><span class="sxs-lookup"><span data-stu-id="0bab4-186">a.</span></span> <span data-ttu-id="0bab4-187">Tıklatın **özniteliği eklemek** tooopen hello özniteliği iletişim.</span><span class="sxs-lookup"><span data-stu-id="0bab4-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="0bab4-190">b.</span><span class="sxs-lookup"><span data-stu-id="0bab4-190">b.</span></span> <span data-ttu-id="0bab4-191">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="0bab4-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0bab4-192">c.</span><span class="sxs-lookup"><span data-stu-id="0bab4-192">c.</span></span> <span data-ttu-id="0bab4-193">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="0bab4-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0bab4-194">d.</span><span class="sxs-lookup"><span data-stu-id="0bab4-194">d.</span></span> <span data-ttu-id="0bab4-195">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="0bab4-195">Click **Ok**</span></span>

10. <span data-ttu-id="0bab4-196">Merhaba hello üzerinde aşağıdaki adımları gerçekleştirin **adı** öznitelik -</span><span class="sxs-lookup"><span data-stu-id="0bab4-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="0bab4-197">a.</span><span class="sxs-lookup"><span data-stu-id="0bab4-197">a.</span></span> <span data-ttu-id="0bab4-198">Tıklatın hello özniteliği tooopen hello üzerinde **öznitelik Düzenle** penceresi.</span><span class="sxs-lookup"><span data-stu-id="0bab4-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="0bab4-200">b.</span><span class="sxs-lookup"><span data-stu-id="0bab4-200">b.</span></span> <span data-ttu-id="0bab4-201">Hello Hello URL değeri Sil **ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="0bab4-202">c.</span><span class="sxs-lookup"><span data-stu-id="0bab4-202">c.</span></span> <span data-ttu-id="0bab4-203">Tıklatın **Tamam** toosave hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="0bab4-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="0bab4-204">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0bab4-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="0bab4-206">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0bab4-206">Click **Save**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="0bab4-208">Çok Git**LinkedIn yönetici ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="0bab4-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="0bab4-209">Merhaba karşıya yükleme XML dosyası seçeneğini tıklatarak hello Azure portal ' yüklenen hello XML dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0bab4-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="0bab4-211">Tıklatın **üzerinde** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="0bab4-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="0bab4-212">SSO durumu değişir **bağlı** çok**bağlandı**</span><span class="sxs-lookup"><span data-stu-id="0bab4-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0bab4-214">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0bab4-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="0bab4-215">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="0bab4-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="0bab4-217">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0bab4-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bab4-218">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="0bab4-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0bab4-220">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0bab4-222">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="0bab4-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0bab4-224">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="0bab4-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0bab4-226">a.</span><span class="sxs-lookup"><span data-stu-id="0bab4-226">a.</span></span> <span data-ttu-id="0bab4-227">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0bab4-228">b.</span><span class="sxs-lookup"><span data-stu-id="0bab4-228">b.</span></span> <span data-ttu-id="0bab4-229">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="0bab4-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0bab4-230">c.</span><span class="sxs-lookup"><span data-stu-id="0bab4-230">c.</span></span> <span data-ttu-id="0bab4-231">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0bab4-232">d.</span><span class="sxs-lookup"><span data-stu-id="0bab4-232">d.</span></span> <span data-ttu-id="0bab4-233">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0bab4-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="0bab4-234">Bir LinkedIn öğrenme test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0bab4-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="0bab4-235">Bağlantılı öğrenme uygulama destekler.</span><span class="sxs-lookup"><span data-stu-id="0bab4-235">Linked Learning Application supports.</span></span> <span data-ttu-id="0bab4-236">Yalnızca zaman kullanıcı sağlama ve kimlik doğrulamasından sonra kullanıcılar hello uygulamada otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0bab4-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="0bab4-237">Merhaba yönetici ayarları sayfasında hello LinkedIn öğrenme portal Çevir hello anahtar **otomatik olarak ata lisansları** zaman sağlama sadece tooactive tooenable ve bu ayrıca atamak lisans toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0bab4-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0bab4-239">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="0bab4-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0bab4-240">Bu bölümde, Azure çoklu oturum açma Britta Simon toouse erişim tooLinkedIn vererek etkinleştirmeniz öğrenme.</span><span class="sxs-lookup"><span data-stu-id="0bab4-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="0bab4-242">**tooassign Britta Simon tooLinkedIn öğrenme, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="0bab4-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bab4-243">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="0bab4-245">Merhaba uygulamalar listesinde **LinkedIn öğrenme**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="0bab4-247">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="0bab4-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="0bab4-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0bab4-249">Click **Add** button.</span></span> <span data-ttu-id="0bab4-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0bab4-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="0bab4-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="0bab4-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0bab4-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0bab4-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0bab4-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="0bab4-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0bab4-255">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="0bab4-255">Testing single sign-on</span></span>

<span data-ttu-id="0bab4-256">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="0bab4-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0bab4-257">Merhaba LinkedIn öğrenme hello erişim paneli parçasında tıklattığınızda hello Azure oturum açma sayfasına almanız gerekir ve üzerinde başarılı oturum açma sonra bunu LinkedIn öğrenme uygulamanıza almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0bab4-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0bab4-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="0bab4-258">Additional resources</span></span>

* [<span data-ttu-id="0bab4-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="0bab4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0bab4-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="0bab4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png