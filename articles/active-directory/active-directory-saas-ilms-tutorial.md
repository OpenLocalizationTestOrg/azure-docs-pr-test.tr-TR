---
title: "Öğretici: Azure Active Directory Tümleştirme ile iLMS | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile iLMS arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="7a668-103">Öğretici: Azure Active Directory Tümleştirme iLMS ile</span><span class="sxs-lookup"><span data-stu-id="7a668-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="7a668-104">Bu öğreticide, bilgi nasıl toointegrate iLMS Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a668-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a668-105">İLMS Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7a668-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7a668-106">Erişim tooiLMS sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7a668-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="7a668-107">Kullanıcıların tooautomatically get açan tooiLMS (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7a668-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a668-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="7a668-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7a668-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a668-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a668-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7a668-110">Prerequisites</span></span>

<span data-ttu-id="7a668-111">tooconfigure iLMS ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a668-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="7a668-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7a668-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a668-113">Bir iLMS çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="7a668-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a668-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7a668-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a668-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a668-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a668-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a668-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7a668-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a668-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a668-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7a668-118">Scenario description</span></span>
<span data-ttu-id="7a668-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7a668-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a668-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7a668-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a668-121">Merhaba Galerisi'nden iLMS ekleme</span><span class="sxs-lookup"><span data-stu-id="7a668-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="7a668-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7a668-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="7a668-123">Merhaba Galerisi'nden iLMS ekleme</span><span class="sxs-lookup"><span data-stu-id="7a668-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="7a668-124">Azure AD'ye tooconfigure hello tümleştirme iLMS, tooadd iLMS hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a668-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a668-125">**Merhaba galerisinden tooadd iLMS hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a668-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a668-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7a668-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a668-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7a668-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7a668-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7a668-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="7a668-131">tooadd yeni uygulama tıklatın **yeni uygulama** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a668-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="7a668-133">Merhaba arama kutusuna yazın **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="7a668-133">In hello search box, type **iLMS**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="7a668-135">Merhaba Sonuçlar panelinde seçin **iLMS**, ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7a668-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a668-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7a668-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a668-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı iLMS sınayın.</span><span class="sxs-lookup"><span data-stu-id="7a668-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7a668-139">Tek toowork'ın oturum açma hangi hello karşılık gelen iLMS içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a668-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="7a668-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı iLMS hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a668-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="7a668-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** iLMS içinde.</span><span class="sxs-lookup"><span data-stu-id="7a668-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="7a668-142">tooconfigure ve iLMS ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a668-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a668-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7a668-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a668-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7a668-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a668-145">**[Bir iLMS test kullanıcısı oluşturma](#creating-an-ilms-test-user)**  -toohave bir Britta Simon karşılık gelen her bağlantılı toohello Azure AD gösterimidir iLMS içinde.</span><span class="sxs-lookup"><span data-stu-id="7a668-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7a668-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7a668-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a668-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7a668-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a668-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7a668-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a668-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma iLMS uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7a668-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="7a668-150">**tooconfigure Azure AD çoklu oturum açma ile iLMS, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a668-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a668-151">Hello hello üzerinde Azure portal'ın **iLMS** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7a668-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="7a668-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7a668-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="7a668-155">Merhaba üzerinde **iLMS etki alanı ve URL'leri** bölümünde, hello tooconfigure hello uygulamada istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="7a668-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="7a668-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a668-157">a.</span></span> <span data-ttu-id="7a668-158">Merhaba, **tanımlayıcısı** metin kutusuna, Yapıştır hello **tanımlayıcısı** değer, kopyalama **hizmet sağlayıcısı** iLMS Yönetim Portalı'nda SAML ayarları bölümü.</span><span class="sxs-lookup"><span data-stu-id="7a668-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="7a668-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a668-159">b.</span></span> <span data-ttu-id="7a668-160">Merhaba, **yanıt URL'si** metin kutusuna, Yapıştır hello **uç noktası (URL)** değer, kopyalama **hizmet sağlayıcısı** hello aşağıdaki sahip iLMS Yönetim Portalı'nda SAML ayarları bölümü düzeni`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="7a668-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="7a668-161">Bu '123456' tanımlayıcısının bir örnek değeridir.</span><span class="sxs-lookup"><span data-stu-id="7a668-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="7a668-162">Denetleme **Göster Gelişmiş URL ayarları**, tooconfigure hello uygulamada istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="7a668-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="7a668-164">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello **uç noktası (URL)** değer, kopyalama **hizmet sağlayıcısı** olarak iLMS Yönetim Portalı'nda SAML ayarları bölümü`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="7a668-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="7a668-165">tooenable sağlama JIT iLMS uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="7a668-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7a668-166">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7a668-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="7a668-167">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="7a668-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="7a668-168">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="7a668-168">hello following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="7a668-170">Oluşturma **departman, bölge** ve **bölme** öznitelikleri ve iLMS içinde bu özniteliklerin hello ad ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7a668-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="7a668-171">Yukarıda gösterilen bu öznitelikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7a668-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="7a668-172">Tooenable sahip **Un-recognized kullanıcı hesabı oluşturma** iLMS toomap olarak bu öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="7a668-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="7a668-173">Merhaba yönergeleri izleyerek [burada](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget hello öznitelikleri yapılandırması hakkında bir fikir.</span><span class="sxs-lookup"><span data-stu-id="7a668-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="7a668-174">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a668-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7a668-175">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="7a668-175">Attribute Name</span></span> | <span data-ttu-id="7a668-176">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="7a668-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="7a668-177">bölme</span><span class="sxs-lookup"><span data-stu-id="7a668-177">division</span></span> | <span data-ttu-id="7a668-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="7a668-178">user.department</span></span> |
    | <span data-ttu-id="7a668-179">Bölge</span><span class="sxs-lookup"><span data-stu-id="7a668-179">region</span></span> | <span data-ttu-id="7a668-180">User.State</span><span class="sxs-lookup"><span data-stu-id="7a668-180">user.state</span></span> |
    | <span data-ttu-id="7a668-181">Bölüm</span><span class="sxs-lookup"><span data-stu-id="7a668-181">department</span></span> | <span data-ttu-id="7a668-182">User.jobtitle</span><span class="sxs-lookup"><span data-stu-id="7a668-182">user.jobtitle</span></span> |

    <span data-ttu-id="7a668-183">a.</span><span class="sxs-lookup"><span data-stu-id="7a668-183">a.</span></span> <span data-ttu-id="7a668-184">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a668-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="7a668-187">b.</span><span class="sxs-lookup"><span data-stu-id="7a668-187">b.</span></span> <span data-ttu-id="7a668-188">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="7a668-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7a668-189">c.</span><span class="sxs-lookup"><span data-stu-id="7a668-189">c.</span></span> <span data-ttu-id="7a668-190">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="7a668-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7a668-191">d.</span><span class="sxs-lookup"><span data-stu-id="7a668-191">d.</span></span> <span data-ttu-id="7a668-192">Tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="7a668-192">Click **Ok**</span></span>

7. <span data-ttu-id="7a668-193">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7a668-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="7a668-195">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a668-195">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="7a668-197">Farklı web tarayıcısı penceresinde tooyour içinde oturum **iLMS Yönetici portalı** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="7a668-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="7a668-198">Tıklatın **SSO:SAML** altında **ayarları** sekmesinde tooopen SAML ayarları ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a668-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="7a668-200">a.</span><span class="sxs-lookup"><span data-stu-id="7a668-200">a.</span></span> <span data-ttu-id="7a668-201">Merhaba genişletin **hizmet sağlayıcısı** bölümü ve kopyalama hello **tanımlayıcısı** ve **uç noktası (URL)** değeri.</span><span class="sxs-lookup"><span data-stu-id="7a668-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="7a668-203">b.</span><span class="sxs-lookup"><span data-stu-id="7a668-203">b.</span></span> <span data-ttu-id="7a668-204">Altında **kimlik sağlayıcısı** 'yi tıklatın **meta verileri içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="7a668-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="7a668-205">c.</span><span class="sxs-lookup"><span data-stu-id="7a668-205">c.</span></span> <span data-ttu-id="7a668-206">Select hello **meta veri** Azure Portalı'ndan ' ndan indirilen dosya **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7a668-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="7a668-208">d.</span><span class="sxs-lookup"><span data-stu-id="7a668-208">d.</span></span> <span data-ttu-id="7a668-209">Tooenable JIT istiyorsanız toocreate sağlama iLMS kaldırmak için hesapları-kullanıcıların tanıyacağı, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7a668-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="7a668-210">Denetleme **beklemediğiniz tanınan bir kullanıcı hesabı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="7a668-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="7a668-212">İLMS hello özniteliklerle Azure ad'deki harita Hello öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="7a668-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="7a668-213">Merhaba özniteliği sütununda hello öznitelikleri adı veya hello varsayılan değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a668-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="7a668-214">e.</span><span class="sxs-lookup"><span data-stu-id="7a668-214">e.</span></span> <span data-ttu-id="7a668-215">Çok Git**iş kuralları** sekmesinde ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a668-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="7a668-217">Denetleme **Un-recognized bölgeler oluşturmak, bölümler ve Departmanlar** toocreate bölgeler, bölümler ve çoklu oturum açma, hello zaman zaten var olmadığından Departmanlar.</span><span class="sxs-lookup"><span data-stu-id="7a668-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="7a668-218">Denetleme **güncelleştirme kullanıcı profili sırasında oturum açma** toospecify hello kullanıcının profilini her çoklu oturum açma ile olup güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7a668-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="7a668-219">Merhaba, **"Güncelleştirme boş değerler için olmayan zorunlu alanlar, kullanıcı profili"** seçeneği seçiliyse, oturum açma üzerine boş isteğe bağlı profili alanları toocontain boş değerler hesaplanan alanlar hello kullanıcının iLMS profili de neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a668-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="7a668-220">Denetleme **hata bildirim e-posta Gönder** ve tooreceive hello hata bildirim e-posta istediğiniz hello kullanıcının hello e-posta girin.</span><span class="sxs-lookup"><span data-stu-id="7a668-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="7a668-221">Tıklatın **kaydetmek** düğmesini toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="7a668-221">Click **Save** button toosave hello settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="7a668-223">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7a668-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7a668-224">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7a668-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7a668-225">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a668-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a668-226">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a668-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a668-227">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7a668-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="7a668-229">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a668-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a668-230">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7a668-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a668-232">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="7a668-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a668-234">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a668-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a668-236">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a668-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a668-238">a.</span><span class="sxs-lookup"><span data-stu-id="7a668-238">a.</span></span> <span data-ttu-id="7a668-239">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a668-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a668-240">b.</span><span class="sxs-lookup"><span data-stu-id="7a668-240">b.</span></span> <span data-ttu-id="7a668-241">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="7a668-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a668-242">c.</span><span class="sxs-lookup"><span data-stu-id="7a668-242">c.</span></span> <span data-ttu-id="7a668-243">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="7a668-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7a668-244">d.</span><span class="sxs-lookup"><span data-stu-id="7a668-244">d.</span></span> <span data-ttu-id="7a668-245">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7a668-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="7a668-246">Bir iLMS test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a668-246">Creating an iLMS test user</span></span>

<span data-ttu-id="7a668-247">Uygulama, süresi kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulduktan sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="7a668-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="7a668-248">JIT çalışır, hello tıkladıysanız **Un-recognized kullanıcı hesabı oluşturma** iLMS Yönetici portalı SAML yapılandırma ayarı sırasında onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a668-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="7a668-249">Bir kullanıcı toocreate el ile gerekiyorsa, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7a668-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="7a668-250">Tooyour iLMS şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7a668-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="7a668-251">Tıklatın **"Kullanıcı kaydetme"** altında **kullanıcılar** tooopen sekmesinde **kullanıcı Kaydet** sayfası.</span><span class="sxs-lookup"><span data-stu-id="7a668-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Çalışanı ekleyin](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="7a668-253">Merhaba üzerinde **"Kullanıcı kaydetme"** sayfasında, hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7a668-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="7a668-255">a.</span><span class="sxs-lookup"><span data-stu-id="7a668-255">a.</span></span> <span data-ttu-id="7a668-256">Merhaba, **ad** metin kutusuna, tür hello ilk adı Britta.</span><span class="sxs-lookup"><span data-stu-id="7a668-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="7a668-257">b.</span><span class="sxs-lookup"><span data-stu-id="7a668-257">b.</span></span> <span data-ttu-id="7a668-258">Merhaba, **Soyadı** metin kutusuna, türü hello Soyadı Simon.</span><span class="sxs-lookup"><span data-stu-id="7a668-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="7a668-259">c.</span><span class="sxs-lookup"><span data-stu-id="7a668-259">c.</span></span> <span data-ttu-id="7a668-260">Merhaba, **e-posta kimliği** metin kutusuna, Britta Simon hesabının hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="7a668-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="7a668-261">d.</span><span class="sxs-lookup"><span data-stu-id="7a668-261">d.</span></span> <span data-ttu-id="7a668-262">Merhaba, **bölge** açılan listesinde, bölge için select hello değer.</span><span class="sxs-lookup"><span data-stu-id="7a668-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="7a668-263">e.</span><span class="sxs-lookup"><span data-stu-id="7a668-263">e.</span></span> <span data-ttu-id="7a668-264">Merhaba, **bölme** açılan listesinde, bölme için select hello değer.</span><span class="sxs-lookup"><span data-stu-id="7a668-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="7a668-265">f.</span><span class="sxs-lookup"><span data-stu-id="7a668-265">f.</span></span> <span data-ttu-id="7a668-266">Merhaba, **departmanı** açılan listesinde, departman için select hello değer.</span><span class="sxs-lookup"><span data-stu-id="7a668-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="7a668-267">g.</span><span class="sxs-lookup"><span data-stu-id="7a668-267">g.</span></span> <span data-ttu-id="7a668-268">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7a668-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a668-269">Seçerek kayıt posta toouser gönderebilirsiniz **kayıt posta Gönder** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a668-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7a668-270">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="7a668-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7a668-271">Bu bölümde, kendi erişim tooiLMS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7a668-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="7a668-273">**tooassign Britta Simon tooiLMS hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7a668-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a668-274">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7a668-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7a668-276">Merhaba uygulamalar listesinde **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="7a668-276">In hello applications list, select **iLMS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="7a668-278">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7a668-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="7a668-280">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7a668-280">Click **Add** button.</span></span> <span data-ttu-id="7a668-281">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a668-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="7a668-283">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7a668-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7a668-284">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a668-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a668-285">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7a668-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a668-286">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7a668-286">Testing single sign-on</span></span>

<span data-ttu-id="7a668-287">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="7a668-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7a668-288">Merhaba erişim paneli iLMS döşeme hello tıkladığınızda, otomatik olarak oturum açma tooyour iLMS uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a668-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a668-289">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7a668-289">Additional resources</span></span>

* [<span data-ttu-id="7a668-290">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7a668-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a668-291">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7a668-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

