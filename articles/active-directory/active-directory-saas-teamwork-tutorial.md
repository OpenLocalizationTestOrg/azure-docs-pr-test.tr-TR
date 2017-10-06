---
title: "Öğretici: Azure Active Directory Tümleştirme ekip çalışması ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve ekip çalışması arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="58298-103">Öğretici: Azure Active Directory Tümleştirme ile ekip çalışması</span><span class="sxs-lookup"><span data-stu-id="58298-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="58298-104">Bu öğreticide, bilgi nasıl toointegrate ekip çalışması Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58298-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58298-105">Ekip çalışması Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="58298-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="58298-106">Erişim tooTeamwork sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58298-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="58298-107">Kullanıcıların tooautomatically get açan tooTeamwork (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58298-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58298-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="58298-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="58298-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58298-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58298-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58298-110">Prerequisites</span></span>

<span data-ttu-id="58298-111">tooconfigure ekip çalışması ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="58298-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="58298-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="58298-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58298-113">Bir ekip çalışması çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="58298-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="58298-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="58298-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="58298-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="58298-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58298-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58298-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="58298-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58298-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="58298-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="58298-118">Scenario description</span></span>
<span data-ttu-id="58298-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="58298-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58298-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="58298-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58298-121">Ekip çalışması hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="58298-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="58298-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="58298-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="58298-123">Ekip çalışması hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="58298-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="58298-124">Azure AD'ye tooconfigure hello tümleştirme ekip çalışması, hello galeri tooyour yönetilen SaaS uygulamaları listesinden tooadd ekip çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58298-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="58298-125">**tooadd ekip çalışması hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58298-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="58298-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="58298-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="58298-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="58298-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="58298-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="58298-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="58298-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58298-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="58298-133">Merhaba arama kutusuna yazın **ekip çalışması**.</span><span class="sxs-lookup"><span data-stu-id="58298-133">In hello search box, type **Teamwork**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="58298-135">Merhaba Sonuçlar panelinde seçin **ekip çalışması**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="58298-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="58298-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="58298-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="58298-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ekip çalışması ile test etme.</span><span class="sxs-lookup"><span data-stu-id="58298-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58298-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ekip çalışması içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="58298-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="58298-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ekip çalışması hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="58298-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="58298-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** ekip çalışması içinde.</span><span class="sxs-lookup"><span data-stu-id="58298-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="58298-142">tooconfigure ve ekip çalışması ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="58298-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="58298-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="58298-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="58298-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="58298-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58298-145">**[Bir ekip çalışması test kullanıcısı oluşturma](#creating-a-teamwork-test-user)**  -toohave Britta Simon her bağlantılı toohello Azure AD gösterimidir ekip çalışması içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="58298-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="58298-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="58298-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58298-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="58298-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="58298-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58298-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="58298-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma ekip çalışması uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58298-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="58298-150">**tooconfigure Azure AD çoklu oturum açma ile ekip çalışması, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58298-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="58298-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **ekip çalışması** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="58298-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="58298-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="58298-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="58298-155">Merhaba üzerinde **ekip çalışması etki alanı ve URL'leri** bölümünde hello **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="58298-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="58298-157">Lütfen bu hello gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="58298-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="58298-158">Bu değeri hello gerçek ile oturum URL'yi tooupdate sahip.</span><span class="sxs-lookup"><span data-stu-id="58298-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="58298-159">Kişi [ekip çalışması destek ekibi](mailto:support@teamwork.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="58298-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="58298-160">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="58298-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="58298-162">Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="58298-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="58298-163">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58298-163">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="58298-165">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58298-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="58298-167">Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="58298-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="58298-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58298-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="58298-171">tooget SSO yapılandırılmış uygulamanızın, kişi [ekip çalışması destek ekibi](mailto:support@teamwork.com) ve indirilen hello ile verin **meta verileri**.</span><span class="sxs-lookup"><span data-stu-id="58298-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="58298-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58298-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="58298-173">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="58298-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="58298-175">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58298-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="58298-176">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="58298-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58298-178">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="58298-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58298-180">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58298-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58298-182">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="58298-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58298-184">a.</span><span class="sxs-lookup"><span data-stu-id="58298-184">a.</span></span> <span data-ttu-id="58298-185">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58298-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58298-186">b.</span><span class="sxs-lookup"><span data-stu-id="58298-186">b.</span></span> <span data-ttu-id="58298-187">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="58298-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58298-188">c.</span><span class="sxs-lookup"><span data-stu-id="58298-188">c.</span></span> <span data-ttu-id="58298-189">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="58298-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="58298-190">d.</span><span class="sxs-lookup"><span data-stu-id="58298-190">d.</span></span> <span data-ttu-id="58298-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58298-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="58298-192">Bir ekip çalışması test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58298-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="58298-193">Bu bölümde, ekip çalışması içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58298-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="58298-194">Lütfen çalışmak [ekip çalışması destek ekibi](mailto:support@teamwork.com) tooadd hello kullanıcılar hello ekip çalışması Platform.</span><span class="sxs-lookup"><span data-stu-id="58298-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="58298-195">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="58298-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="58298-196">Bu bölümde, kendi erişim tooTeamwork vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="58298-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="58298-198">**tooassign Britta Simon tooTeamwork hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="58298-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="58298-199">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="58298-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="58298-201">Merhaba uygulamalar listesinde **ekip çalışması**.</span><span class="sxs-lookup"><span data-stu-id="58298-201">In hello applications list, select **Teamwork**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="58298-203">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="58298-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="58298-205">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58298-205">Click **Add** button.</span></span> <span data-ttu-id="58298-206">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58298-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="58298-208">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="58298-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="58298-209">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58298-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58298-210">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="58298-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="58298-211">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="58298-211">Testing single sign-on</span></span>

<span data-ttu-id="58298-212">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="58298-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="58298-213">Merhaba ekip çalışması hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ekip çalışması uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58298-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="58298-214">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="58298-214">Additional resources</span></span>

* [<span data-ttu-id="58298-215">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="58298-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58298-216">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="58298-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png