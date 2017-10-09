---
title: "Öğretici: Azure Active Directory Tümleştirme IQNavigator VMs | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile IQNavigator VM'ler arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="1c4af-103">Öğretici: Azure Active Directory Tümleştirme IQNavigator VMs</span><span class="sxs-lookup"><span data-stu-id="1c4af-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="1c4af-104">Bu öğreticide, bilgi nasıl toointegrate IQNavigator VM'ler Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c4af-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c4af-105">IQNavigator VM'ler Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1c4af-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c4af-106">Erişim tooIQNavigator VM'ler sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1c4af-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="1c4af-107">Kullanıcıların tooautomatically get açan tooIQNavigator VM'ler (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1c4af-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c4af-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1c4af-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1c4af-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c4af-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c4af-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1c4af-110">Prerequisites</span></span>

<span data-ttu-id="1c4af-111">tooconfigure IQNavigator VM'ler ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c4af-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="1c4af-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1c4af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c4af-113">Bir IQNavigator VM'ler çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="1c4af-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c4af-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1c4af-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c4af-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c4af-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c4af-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1c4af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c4af-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c4af-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c4af-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1c4af-118">Scenario description</span></span>
<span data-ttu-id="1c4af-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1c4af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c4af-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1c4af-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c4af-121">Merhaba Galerisi'nden IQNavigator VM'ler ekleme</span><span class="sxs-lookup"><span data-stu-id="1c4af-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="1c4af-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1c4af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="1c4af-123">Merhaba Galerisi'nden IQNavigator VM'ler ekleme</span><span class="sxs-lookup"><span data-stu-id="1c4af-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="1c4af-124">Azure AD'ye tooconfigure hello tümleştirme IQNavigator VM'lerin tooadd IQNavigator VM'ler hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c4af-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c4af-125">**tooadd IQNavigator VM'ler hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1c4af-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4af-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c4af-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c4af-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1c4af-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1c4af-133">Merhaba arama kutusuna yazın **IQNavigator VM'ler**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="1c4af-135">Merhaba Sonuçlar panelinde seçin **IQNavigator VM'ler**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1c4af-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c4af-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1c4af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c4af-138">Bu bölümde, yapılandırmanız ve IQNavigator VM'ler ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="1c4af-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c4af-139">Tek toowork'ın oturum açma hangi hello karşılık gelen IQNavigator VM'ler içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c4af-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="1c4af-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı IQNavigator VM'ler arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c4af-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="1c4af-141">Merhaba hello değeri IQNavigator VM'LERDE atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1c4af-142">tooconfigure ve IQNavigator VM'ler ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c4af-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c4af-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="1c4af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c4af-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="1c4af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c4af-145">**[IQNavigator VM'ler test kullanıcısı oluşturma](#creating-a-iqnavigator-vms-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir IQNavigator VM'ler içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="1c4af-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c4af-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1c4af-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c4af-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="1c4af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c4af-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1c4af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c4af-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma IQNavigator VM'ler uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1c4af-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="1c4af-150">**tooconfigure Azure AD çoklu oturum açma IQNavigator VMs hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1c4af-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4af-151">Merhaba hello üzerinde Azure portal'ın **IQNavigator VM'ler** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1c4af-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1c4af-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="1c4af-155">Merhaba üzerinde **IQNavigator VM'ler etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1c4af-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="1c4af-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c4af-157">a.</span></span> <span data-ttu-id="1c4af-158">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="1c4af-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="1c4af-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c4af-159">b.</span></span> <span data-ttu-id="1c4af-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="1c4af-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="1c4af-161">Denetleme **Göster Gelişmiş URL ayarları**, adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1c4af-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="1c4af-163">Merhaba, **geçiş durumu** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="1c4af-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c4af-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="1c4af-164">These values are not real.</span></span> <span data-ttu-id="1c4af-165">Bu değerleri hello fiili yanıt URL'si ve geçiş durumu ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1c4af-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="1c4af-166">Kişi [IQNavigator VM'ler istemci destek ekibi](https://www.beeline.com/iqn-product-support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="1c4af-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="1c4af-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c4af-169">toogenerate hello **meta veri** url hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1c4af-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="1c4af-170">a.</span><span class="sxs-lookup"><span data-stu-id="1c4af-170">a.</span></span> <span data-ttu-id="1c4af-171">Tıklatın **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-171">Click **App registrations**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="1c4af-173">b.</span><span class="sxs-lookup"><span data-stu-id="1c4af-173">b.</span></span> <span data-ttu-id="1c4af-174">Tıklatın **uç noktaları** tooopen **uç noktaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="1c4af-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="1c4af-176">c.</span><span class="sxs-lookup"><span data-stu-id="1c4af-176">c.</span></span> <span data-ttu-id="1c4af-177">Merhaba Kopyala düğmesine toocopy tıklatın **FEDERASYON meta veri belgesi** URL'yi kopyalayıp Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c4af-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="1c4af-179">d.</span><span class="sxs-lookup"><span data-stu-id="1c4af-179">d.</span></span> <span data-ttu-id="1c4af-180">Şimdi toohello özellik sayfasında gidin **IQNavigator VM'ler** ve kopyalama hello **uygulama kimliği** kullanarak **kopyalama** düğmesine tıklayın ve Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="1c4af-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="1c4af-182">e.</span><span class="sxs-lookup"><span data-stu-id="1c4af-182">e.</span></span> <span data-ttu-id="1c4af-183">Merhaba oluşturmak **meta veri URL'sini** desen aşağıdaki hello kullanarak:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="1c4af-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="1c4af-184">IQNavigator uygulama hello ad tanımlayıcısı talep hello benzersiz kullanıcı kimliği değeri bekler.</span><span class="sxs-lookup"><span data-stu-id="1c4af-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="1c4af-185">Merhaba doğru değeri hello ad tanımlayıcısı talep için müşteri eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c4af-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="1c4af-186">Bu durumda biz hello kullanıcı eşledikten. UserPrincipalName hello Tanıtım amaçlı için.</span><span class="sxs-lookup"><span data-stu-id="1c4af-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="1c4af-187">Ancak kuruluş ayarları tooyour göre hello doğru değeri için eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c4af-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="1c4af-189">Merhaba üzerinde **IQNavigator VM'ler yapılandırma** 'yi tıklatın **yapılandırma IQNavigator VM'ler** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1c4af-190">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="1c4af-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="1c4af-192">tooconfigure çoklu oturum açma üzerinde **IQNavigator VM'ler** yan, gereksinim duyduğunuz toosend hello **meta veri URL'sini**, **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok [IQNavigator VM'ler destek ekibi](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="1c4af-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="1c4af-193">Bunlar, bu ayar toohave hello iki tarafta da ayarlamanızı SAML SSO bağlantı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1c4af-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1c4af-194">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1c4af-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c4af-195">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="1c4af-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c4af-196">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c4af-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c4af-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c4af-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c4af-198">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="1c4af-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1c4af-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1c4af-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4af-201">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c4af-203">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c4af-205">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="1c4af-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c4af-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1c4af-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c4af-209">a.</span><span class="sxs-lookup"><span data-stu-id="1c4af-209">a.</span></span> <span data-ttu-id="1c4af-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c4af-211">b.</span><span class="sxs-lookup"><span data-stu-id="1c4af-211">b.</span></span> <span data-ttu-id="1c4af-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1c4af-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c4af-213">c.</span><span class="sxs-lookup"><span data-stu-id="1c4af-213">c.</span></span> <span data-ttu-id="1c4af-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c4af-215">d.</span><span class="sxs-lookup"><span data-stu-id="1c4af-215">d.</span></span> <span data-ttu-id="1c4af-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c4af-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="1c4af-217">IQNavigator VM'ler test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c4af-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="1c4af-218">Bu bölümde Hello amacı toocreate IQNavigator VM'LERDE Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="1c4af-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="1c4af-219">Çalışmak [IQNavigator VM'ler destek ekibi](https://www.beeline.com/iqn-product-support/) hello IQNavigator VM'ler hesap tooadd hello kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="1c4af-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c4af-220">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1c4af-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c4af-221">Bu bölümde, erişim tooIQNavigator VM'ler vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1c4af-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1c4af-223">**tooassign Britta Simon tooIQNavigator VM'ler, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1c4af-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c4af-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1c4af-226">Merhaba uygulamalar listesinde **IQNavigator VM'ler**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="1c4af-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1c4af-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1c4af-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1c4af-230">Click **Add** button.</span></span> <span data-ttu-id="1c4af-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1c4af-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1c4af-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1c4af-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c4af-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1c4af-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c4af-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1c4af-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c4af-236">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1c4af-236">Testing single sign-on</span></span>

<span data-ttu-id="1c4af-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1c4af-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1c4af-238">Merhaba hello erişim paneli IQNavigator VM'ler parçasında tıkladığınızda, otomatik olarak oturum açma IQNavigator VM'ler uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c4af-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="1c4af-239">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c4af-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c4af-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1c4af-240">Additional resources</span></span>

* [<span data-ttu-id="1c4af-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="1c4af-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c4af-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1c4af-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

