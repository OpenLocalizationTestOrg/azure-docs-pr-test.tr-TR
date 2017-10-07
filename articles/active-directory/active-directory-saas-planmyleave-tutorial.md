---
title: "Öğretici: Azure Active Directory Tümleştirme ile PlanMyLeave | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile PlanMyLeave arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="ddd05-103">Öğretici: Azure Active Directory Tümleştirme PlanMyLeave ile</span><span class="sxs-lookup"><span data-stu-id="ddd05-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="ddd05-104">Bu öğreticide, bilgi nasıl toointegrate PlanMyLeave Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddd05-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddd05-105">PlanMyLeave Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ddd05-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ddd05-106">Erişim tooPlanMyLeave sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ddd05-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="ddd05-107">Kullanıcıların tooautomatically get açan tooPlanMyLeave (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ddd05-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddd05-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="ddd05-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ddd05-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddd05-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddd05-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ddd05-110">Prerequisites</span></span>

<span data-ttu-id="ddd05-111">tooconfigure PlanMyLeave ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ddd05-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="ddd05-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ddd05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddd05-113">Bir PlanMyLeave çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="ddd05-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ddd05-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ddd05-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ddd05-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ddd05-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddd05-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ddd05-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddd05-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ddd05-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ddd05-118">Scenario description</span></span>
<span data-ttu-id="ddd05-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ddd05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddd05-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ddd05-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddd05-121">Merhaba Galerisi'nden PlanMyLeave ekleme</span><span class="sxs-lookup"><span data-stu-id="ddd05-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="ddd05-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ddd05-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="ddd05-123">Merhaba Galerisi'nden PlanMyLeave ekleme</span><span class="sxs-lookup"><span data-stu-id="ddd05-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="ddd05-124">Azure AD'ye tooconfigure hello tümleştirme PlanMyLeave, tooadd PlanMyLeave hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ddd05-125">**tooadd PlanMyLeave hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ddd05-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddd05-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ddd05-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ddd05-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="ddd05-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="ddd05-133">Merhaba arama kutusuna yazın **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="ddd05-135">Merhaba Sonuçlar panelinde seçin **PlanMyLeave**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ddd05-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddd05-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ddd05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddd05-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PlanMyLeave sınayın.</span><span class="sxs-lookup"><span data-stu-id="ddd05-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ddd05-139">Tek toowork'ın oturum açma hangi hello karşılık gelen PlanMyLeave içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="ddd05-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı PlanMyLeave hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="ddd05-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** PlanMyLeave içinde.</span><span class="sxs-lookup"><span data-stu-id="ddd05-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="ddd05-142">tooconfigure ve PlanMyLeave ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ddd05-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ddd05-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="ddd05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ddd05-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="ddd05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddd05-145">**[PlanMyLeave test kullanıcısı oluşturma](#creating-a-planmyleave-test-user)**  -toohave karşılık gelen her bağlantılı toohello Azure AD gösterimidir PlanMyLeave içinde Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="ddd05-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ddd05-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ddd05-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddd05-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="ddd05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddd05-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ddd05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddd05-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma PlanMyLeave uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ddd05-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="ddd05-150">**tooconfigure Azure AD çoklu oturum açma ile PlanMyLeave, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ddd05-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddd05-151">Merhaba üzerinde hello Azure Yönetim Portalı'nda **PlanMyLeave** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="ddd05-153">Merhaba üzerinde **çoklu oturum açma** iletişim sayfası olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ddd05-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="ddd05-155">Merhaba üzerinde **PlanMyLeave etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ddd05-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="ddd05-157">a.</span><span class="sxs-lookup"><span data-stu-id="ddd05-157">a.</span></span> <span data-ttu-id="ddd05-158">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="ddd05-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="ddd05-159">b.</span><span class="sxs-lookup"><span data-stu-id="ddd05-159">b.</span></span> <span data-ttu-id="ddd05-160">Merhaba, **tanımlayıcı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="ddd05-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ddd05-161">Lütfen bu hello gerçek değerler olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ddd05-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="ddd05-162">Bu değerlerle hello gerçek oturum açma URL'si ve tanımlayıcı tooupdate sahip.</span><span class="sxs-lookup"><span data-stu-id="ddd05-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="ddd05-163">Kişi [PlanMyLeave destek ekibi](mailto:support@planmyleave.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="ddd05-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="ddd05-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="ddd05-166">Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ddd05-167">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-167">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="ddd05-169">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="ddd05-171">Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ddd05-173">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ddd05-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="ddd05-175">Merhaba üzerinde **PlanMyLeave yapılandırma** 'yi tıklatın **yapılandırma PlanMyLeave** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="ddd05-178">Farklı web tarayıcısı penceresinde PlanMyLeave Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ddd05-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="ddd05-179">Çok Git**sistem kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-179">Go too**System Setup**.</span></span> <span data-ttu-id="ddd05-180">Sonra da hello **güvenlik yönetimi** bölümünde **şirket SAML ayarları** .</span><span class="sxs-lookup"><span data-stu-id="ddd05-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="ddd05-182">Merhaba üzerinde **SAML ayarları** bölümünde, düzenleyici simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddd05-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="ddd05-184">Merhaba üzerinde **güncelleştirme SAML ayarlarını** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ddd05-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="ddd05-186">a.</span><span class="sxs-lookup"><span data-stu-id="ddd05-186">a.</span></span>  <span data-ttu-id="ddd05-187">Merhaba, **oturum açma URL'si** hello değerini put textbox **SAML çoklu oturum açma hizmet URL'si** Azure AD uygulama yapılandırma penceresinden.</span><span class="sxs-lookup"><span data-stu-id="ddd05-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="ddd05-188">b.</span><span class="sxs-lookup"><span data-stu-id="ddd05-188">b.</span></span>  <span data-ttu-id="ddd05-189">İndirilen sertifika dosyasını Not Defteri'nde açın, yalnızca hello---başlamak sertifika---ve---son sertifika---bunu panonuza, içine arasında hello içerik kopyalayıp toohello yapıştırın **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ddd05-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="ddd05-190">c.</span><span class="sxs-lookup"><span data-stu-id="ddd05-190">c.</span></span> <span data-ttu-id="ddd05-191">Ayarlama"**etkin**"çok"**Evet**".</span><span class="sxs-lookup"><span data-stu-id="ddd05-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="ddd05-192">d.</span><span class="sxs-lookup"><span data-stu-id="ddd05-192">d.</span></span> <span data-ttu-id="ddd05-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddd05-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddd05-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddd05-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddd05-195">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="ddd05-197">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ddd05-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddd05-198">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddd05-200">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddd05-202">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ddd05-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddd05-204">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ddd05-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddd05-206">a.</span><span class="sxs-lookup"><span data-stu-id="ddd05-206">a.</span></span> <span data-ttu-id="ddd05-207">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddd05-208">b.</span><span class="sxs-lookup"><span data-stu-id="ddd05-208">b.</span></span> <span data-ttu-id="ddd05-209">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="ddd05-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddd05-210">c.</span><span class="sxs-lookup"><span data-stu-id="ddd05-210">c.</span></span> <span data-ttu-id="ddd05-211">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ddd05-212">d.</span><span class="sxs-lookup"><span data-stu-id="ddd05-212">d.</span></span> <span data-ttu-id="ddd05-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ddd05-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="ddd05-214">PlanMyLeave test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddd05-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="ddd05-215">Bu bölümde Hello amacı toocreate Britta Simon içinde PlanMyLeave adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="ddd05-216">PlanMyLeave yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="ddd05-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ddd05-217">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="ddd05-217">There is no action item for you in this section.</span></span> <span data-ttu-id="ddd05-218">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess PlanMyLeave sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ddd05-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ddd05-219">Bir kullanıcı toocreate el ile gerekiyorsa, toocontact gerek [PlanMyLeave destek ekibi](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="ddd05-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ddd05-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="ddd05-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ddd05-221">Bu bölümde, kendi erişim tooPlanMyLeave vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ddd05-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="ddd05-223">**tooassign Britta Simon tooPlanMyLeave hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ddd05-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddd05-224">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ddd05-226">Merhaba uygulamalar listesinde **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="ddd05-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ddd05-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="ddd05-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ddd05-230">Click **Add** button.</span></span> <span data-ttu-id="ddd05-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ddd05-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="ddd05-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ddd05-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ddd05-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ddd05-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddd05-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ddd05-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ddd05-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ddd05-236">Testing single sign-on</span></span>

<span data-ttu-id="ddd05-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ddd05-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ddd05-238">Merhaba PlanMyLeave hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour PlanMyLeave uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddd05-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ddd05-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ddd05-239">Additional resources</span></span>

* [<span data-ttu-id="ddd05-240">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ddd05-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddd05-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ddd05-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png