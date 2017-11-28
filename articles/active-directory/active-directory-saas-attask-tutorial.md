---
title: "Öğretici: Azure Active Directory Tümleştirme ile @Task| Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasında ve @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="91496-103">Öğretici: Azure Active Directory ile tümleştirme@Task</span><span class="sxs-lookup"><span data-stu-id="91496-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="91496-104">Bu öğreticinin Hello hedefi olan tooshow, nasıl toointegrate @Task Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91496-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="91496-105">Tümleştirme @Task ile Azure AD ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="91496-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="91496-106">Erişimi olan Azure AD'de kontrol edebilirsiniztoo@Task</span><span class="sxs-lookup"><span data-stu-id="91496-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="91496-107">Tooautomatically alma oturum açma, kullanıcılarınızın etkinleştirebilirsiniz too@Task (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="91496-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="91496-108">Hesaplarınızı bir merkezi konumda - hello Klasik Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="91496-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="91496-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91496-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91496-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="91496-110">Prerequisites</span></span>
<span data-ttu-id="91496-111">tooconfigure Azure AD ile tümleştirme @Task, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="91496-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="91496-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="91496-112">An Azure AD subscription</span></span>
* <span data-ttu-id="91496-113">Bir @Task çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="91496-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91496-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="91496-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="91496-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="91496-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="91496-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91496-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="91496-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91496-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="91496-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="91496-118">Scenario Description</span></span>
<span data-ttu-id="91496-119">Bu öğreticinin Hello hedefi olan tooenable, tootest Azure AD çoklu oturum açma bir sınama ortamında.</span><span class="sxs-lookup"><span data-stu-id="91496-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="91496-120">Bu öğreticide gösterilen hello senaryo üç ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="91496-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="91496-121">Ekleme @Task hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="91496-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="91496-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="91496-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="91496-123">Ekleme @Task hello Galeriden</span><span class="sxs-lookup"><span data-stu-id="91496-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="91496-124">tooconfigure hello tümleştirilmesi @Task tooadd gereken Azure AD ile @Task hello galeri tooyour listesinden yönetilen SaaS uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="91496-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91496-125">**tooadd @Task hello Galerisi'nden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="91496-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91496-126">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91496-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="91496-128">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="91496-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="91496-129">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="91496-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Uygulamalar][2] 
4. <span data-ttu-id="91496-131">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="91496-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Uygulamalar][3] 
5. <span data-ttu-id="91496-133">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="91496-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Uygulamalar][4] 
6. <span data-ttu-id="91496-135">Merhaba arama kutusuna yazın  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="91496-135">In hello search box, type **@Task**.</span></span>
   
    ![Uygulamalar][5] 
7. <span data-ttu-id="91496-137">Merhaba sonuçlar bölmesinde seçin  **@Task** ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="91496-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Uygulamalar][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91496-139">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="91496-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91496-140">Merhaba, bu bölümün amacı olan, nasıl tooconfigure ve test Azure AD çoklu oturum açma ile tooshow @Task "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="91496-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91496-141">Tek toowork'ın oturum açma Azure AD tooknow hangi hello karşılık gelen kullanıcı gereken @Task Azure AD'de tooan kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="91496-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="91496-142">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı arasında bir bağlantı ilişki @Task kurulan toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="91496-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="91496-143">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** içinde @Task.</span><span class="sxs-lookup"><span data-stu-id="91496-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="91496-144">tooconfigure ve test Azure AD çoklu oturum açma ile @Task, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="91496-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91496-145">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="91496-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91496-146">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="91496-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91496-147">**[Oluşturma bir @Tasktest kullanıcı](#creating-a-halogen-software-test-user)**  -toohave Britta Simon, karşılık gelen bir @Taskthat her bağlantılı toohello Azure AD gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="91496-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="91496-148">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="91496-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91496-149">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="91496-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91496-150">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91496-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="91496-151">Bu bölümde Hello amacı olduğundan tooenable Azure AD çoklu oturum açma hello Klasik Azure Portalı'nda ve tooconfigure çoklu oturum açma içinde @Task uygulama.</span><span class="sxs-lookup"><span data-stu-id="91496-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="91496-152">**Azure AD çoklu oturum açma tooconfigure ile @Task, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="91496-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="91496-153">Merhaba hello üzerinde Klasik Azure Portalı'nda  **@Task**  uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**  iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="91496-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][6] 
2. <span data-ttu-id="91496-155">Merhaba üzerinde **nasıl gibi kullanıcıların toosign üzerinde yaptığınız too@Task**  sayfasında, **Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="91496-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD çoklu oturum açma][7] 
3. <span data-ttu-id="91496-157">Merhaba üzerinde **uygulama ayarlarını yapılandır** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="91496-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Uygulama ayarlarını yapılandırın][8] 
   
     <span data-ttu-id="91496-159">a.</span><span class="sxs-lookup"><span data-stu-id="91496-159">a.</span></span> <span data-ttu-id="91496-160">Merhaba, **oturum üzerinde URL'si** metin kutusuna, toosign üzerinde kullanıcıların tooyour tarafından kullanılan türü hello URL @Task uygulama (örn:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="91496-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="91496-161">b.</span><span class="sxs-lookup"><span data-stu-id="91496-161">b.</span></span> <span data-ttu-id="91496-162">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91496-162">Click **Next**.</span></span>
4. <span data-ttu-id="91496-163">Merhaba üzerinde **çoklu oturum açma sırasında yapılandırma @Task**  sayfasında, **karşıdan meta veri**hello meta veri dosyası, bilgisayarınıza yerel olarak kaydedin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="91496-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Azure AD Connect nedir?][9] 
5. <span data-ttu-id="91496-165">Oturum açma tooyour @Task yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="91496-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="91496-166">Çok Git**tek oturum açma yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="91496-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="91496-167">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, aşağıdaki adımları hello gerçekleştirmek</span><span class="sxs-lookup"><span data-stu-id="91496-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Çoklu oturum açmayı yapılandırın][23]
   
    <span data-ttu-id="91496-169">a.</span><span class="sxs-lookup"><span data-stu-id="91496-169">a.</span></span> <span data-ttu-id="91496-170">Olarak **türü**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="91496-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="91496-171">b.</span><span class="sxs-lookup"><span data-stu-id="91496-171">b.</span></span> <span data-ttu-id="91496-172">Seçin **hizmet sağlayıcı kimliği**.</span><span class="sxs-lookup"><span data-stu-id="91496-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="91496-173">c.</span><span class="sxs-lookup"><span data-stu-id="91496-173">c.</span></span> <span data-ttu-id="91496-174">Merhaba Hello Klasik Azure portalı, kopyalama **uzaktan oturum açma URL'si**ve hello yapıştırma **oturum açma portalı URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="91496-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="91496-175">d.</span><span class="sxs-lookup"><span data-stu-id="91496-175">d.</span></span> <span data-ttu-id="91496-176">Merhaba Hello Klasik Azure portalı, kopyalama **tek Sign-Out hizmeti URL'si**ve hello yapıştırma **Sign-Out URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="91496-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="91496-177">e.</span><span class="sxs-lookup"><span data-stu-id="91496-177">e.</span></span> <span data-ttu-id="91496-178">Merhaba Hello Klasik Azure portalı, kopyalama **değişiklik parola URL'si**ve hello yapıştırma **değişiklik parola URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="91496-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="91496-179">f.</span><span class="sxs-lookup"><span data-stu-id="91496-179">f.</span></span> <span data-ttu-id="91496-180">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91496-180">Click **Save**.</span></span>
8. <span data-ttu-id="91496-181">Hello Klasik Azure portalı, hello tek oturum açma yapılandırması onay seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="91496-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect nedir?][10]
9. <span data-ttu-id="91496-183">Merhaba üzerinde **tek oturum açma onay** sayfasında, **tam**.</span><span class="sxs-lookup"><span data-stu-id="91496-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect nedir?][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91496-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91496-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="91496-186">Bu bölümde Hello amacı toocreate hello Britta Simon adlı Klasik Azure portalında bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="91496-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Azure AD Kullanıcı oluşturma][20]

<span data-ttu-id="91496-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="91496-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91496-189">Merhaba, **Klasik Azure portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91496-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="91496-191">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="91496-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="91496-192">toodisplay hello hello üstte hello menüde kullanıcıların listesini tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="91496-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="91496-194">tooopen hello **Kullanıcı Ekle** hello araç çubuğunda hello altta iletişim tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="91496-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="91496-196">Merhaba üzerinde **bu kullanıcı hakkında bize** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="91496-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="91496-198">a.</span><span class="sxs-lookup"><span data-stu-id="91496-198">a.</span></span> <span data-ttu-id="91496-199">Kullanıcı türü olarak, kuruluşunuzdaki yeni kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="91496-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="91496-200">b.</span><span class="sxs-lookup"><span data-stu-id="91496-200">b.</span></span> <span data-ttu-id="91496-201">Merhaba kullanıcı adı olarak **textbox**, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91496-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="91496-202">c.</span><span class="sxs-lookup"><span data-stu-id="91496-202">c.</span></span> <span data-ttu-id="91496-203">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91496-203">Click **Next**.</span></span>
6. <span data-ttu-id="91496-204">Merhaba üzerinde **kullanıcı profili** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="91496-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="91496-206">a.</span><span class="sxs-lookup"><span data-stu-id="91496-206">a.</span></span> <span data-ttu-id="91496-207">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="91496-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="91496-208">b.</span><span class="sxs-lookup"><span data-stu-id="91496-208">b.</span></span> <span data-ttu-id="91496-209">Merhaba, **Soyadı** metin kutusuna, türü, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="91496-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="91496-210">c.</span><span class="sxs-lookup"><span data-stu-id="91496-210">c.</span></span> <span data-ttu-id="91496-211">Merhaba, **görünen adı** metin kutusuna, türü **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="91496-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="91496-212">d.</span><span class="sxs-lookup"><span data-stu-id="91496-212">d.</span></span> <span data-ttu-id="91496-213">Merhaba, **rol** listesinde **kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="91496-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="91496-214">e.</span><span class="sxs-lookup"><span data-stu-id="91496-214">e.</span></span> <span data-ttu-id="91496-215">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91496-215">Click **Next**.</span></span>

7. <span data-ttu-id="91496-216">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="91496-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="91496-218">Merhaba üzerinde **Get geçici parola** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="91496-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="91496-220">a.</span><span class="sxs-lookup"><span data-stu-id="91496-220">a.</span></span> <span data-ttu-id="91496-221">Merhaba Hello değerini yazmak **yeni parola**.</span><span class="sxs-lookup"><span data-stu-id="91496-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="91496-222">b.</span><span class="sxs-lookup"><span data-stu-id="91496-222">b.</span></span> <span data-ttu-id="91496-223">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91496-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="91496-224">Oluşturma bir @Task test kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="91496-224">Creating an @Task test user</span></span>
<span data-ttu-id="91496-225">Bu bölümde Hello amacı olan toocreate Britta Simon adlı bir kullanıcı @Task.</span><span class="sxs-lookup"><span data-stu-id="91496-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="91496-226">**toocreate Britta Simon adlı bir kullanıcı @Task, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="91496-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="91496-227">Tooyour üzerinde oturum @Task yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="91496-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="91496-228">Hello içinde hello üst menüsünde **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="91496-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="91496-229">Tıklatın **yeni bir kişiye**.</span><span class="sxs-lookup"><span data-stu-id="91496-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="91496-230">Merhaba yeni bir kişiye iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="91496-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Oluşturma bir @Task test kullanıcısı][21] 
   
    <span data-ttu-id="91496-232">a.</span><span class="sxs-lookup"><span data-stu-id="91496-232">a.</span></span> <span data-ttu-id="91496-233">Merhaba, **ad** metin kutusuna, "Britta" yazın.</span><span class="sxs-lookup"><span data-stu-id="91496-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="91496-234">b.</span><span class="sxs-lookup"><span data-stu-id="91496-234">b.</span></span> <span data-ttu-id="91496-235">Merhaba, **Soyadı** metin kutusuna, "Simon" yazın.</span><span class="sxs-lookup"><span data-stu-id="91496-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="91496-236">c.</span><span class="sxs-lookup"><span data-stu-id="91496-236">c.</span></span> <span data-ttu-id="91496-237">Merhaba, **e-posta adresi** metin kutusuna, Azure Active Directory'de Britta Simon'ın e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="91496-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="91496-238">d.</span><span class="sxs-lookup"><span data-stu-id="91496-238">d.</span></span> <span data-ttu-id="91496-239">Tıklatın **kişiyi ekler**.</span><span class="sxs-lookup"><span data-stu-id="91496-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91496-240">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="91496-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="91496-241">Merhaba amacı, bu bölümde her erişim vererek tooenabling Azure çoklu oturum açma Britta Simon toouse olan too@Task.</span><span class="sxs-lookup"><span data-stu-id="91496-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="91496-243">**tooassign Britta Simon too@Task, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="91496-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="91496-244">Hello üzerinde Azure Klasik portalı, hello dizin görünümünde tooopen hello uygulamaları Görünüm'e tıklayın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="91496-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Kullanıcı atama][201] 
2. <span data-ttu-id="91496-246">Merhaba uygulamalar listesinde  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="91496-246">In hello applications list, select **@Task**.</span></span>
   
    ![Kullanıcı atama][202] 
3. <span data-ttu-id="91496-248">Hello içinde hello üst menüsünde **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="91496-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Kullanıcı atama][203] 
4. <span data-ttu-id="91496-250">Merhaba kullanıcılar listesinden seçin **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="91496-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="91496-251">Merhaba altta Hello araç çubuğunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="91496-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Kullanıcı atama][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="91496-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="91496-253">Testing Single Sign-On</span></span>
<span data-ttu-id="91496-254">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="91496-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="91496-255">Merhaba tıkladığınızda @Task parçasında Merhaba erişim paneli, otomatik olarak oturum açma tooyour alması gereken @Task uygulama.</span><span class="sxs-lookup"><span data-stu-id="91496-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91496-256">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="91496-256">Additional Resources</span></span>
* [<span data-ttu-id="91496-257">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="91496-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91496-258">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="91496-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






