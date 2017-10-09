---
title: "Öğretici: Azure Active Directory Tümleştirme ile LogicMonitor | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile LogicMonitor arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="19b52-103">Öğretici: Azure Active Directory Tümleştirme LogicMonitor ile</span><span class="sxs-lookup"><span data-stu-id="19b52-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="19b52-104">Bu öğreticide, bilgi nasıl toointegrate LogicMonitor Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19b52-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19b52-105">LogicMonitor Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="19b52-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19b52-106">Erişim tooLogicMonitor sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="19b52-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="19b52-107">Kullanıcıların tooautomatically get açan tooLogicMonitor (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="19b52-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19b52-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="19b52-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="19b52-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19b52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19b52-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="19b52-110">Prerequisites</span></span>

<span data-ttu-id="19b52-111">tooconfigure LogicMonitor ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="19b52-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="19b52-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="19b52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19b52-113">Bir LogicMonitor çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="19b52-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19b52-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="19b52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19b52-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="19b52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19b52-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="19b52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19b52-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19b52-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19b52-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="19b52-118">Scenario description</span></span>
<span data-ttu-id="19b52-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="19b52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19b52-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="19b52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19b52-121">Merhaba Galerisi'nden LogicMonitor ekleme</span><span class="sxs-lookup"><span data-stu-id="19b52-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="19b52-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="19b52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="19b52-123">Merhaba Galerisi'nden LogicMonitor ekleme</span><span class="sxs-lookup"><span data-stu-id="19b52-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="19b52-124">Azure AD'ye tooconfigure hello tümleştirme LogicMonitor, tooadd LogicMonitor hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b52-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19b52-125">**tooadd LogicMonitor hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="19b52-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19b52-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="19b52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19b52-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="19b52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19b52-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="19b52-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="19b52-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="19b52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="19b52-133">Merhaba arama kutusuna yazın **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="19b52-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="19b52-135">Merhaba Sonuçlar panelinde seçin **LogicMonitor**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="19b52-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19b52-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="19b52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19b52-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LogicMonitor sınayın.</span><span class="sxs-lookup"><span data-stu-id="19b52-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19b52-139">Tek toowork'ın oturum açma hangi hello karşılık gelen LogicMonitor içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b52-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="19b52-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı LogicMonitor hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b52-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="19b52-141">Merhaba hello değeri LogicMonitor içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="19b52-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="19b52-142">tooconfigure ve LogicMonitor ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="19b52-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19b52-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="19b52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19b52-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="19b52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19b52-145">**[LogicMonitor test kullanıcısı oluşturma](#creating-a-logicmonitor-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir LogicMonitor içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="19b52-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="19b52-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="19b52-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19b52-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="19b52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19b52-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="19b52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19b52-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma LogicMonitor uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="19b52-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="19b52-150">**tooconfigure Azure AD çoklu oturum açma ile LogicMonitor, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="19b52-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="19b52-151">Hello hello üzerinde Azure portal'ın **LogicMonitor** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="19b52-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="19b52-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="19b52-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="19b52-155">Merhaba üzerinde **LogicMonitor etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="19b52-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="19b52-157">a.</span><span class="sxs-lookup"><span data-stu-id="19b52-157">a.</span></span> <span data-ttu-id="19b52-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="19b52-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="19b52-159">b.</span><span class="sxs-lookup"><span data-stu-id="19b52-159">b.</span></span> <span data-ttu-id="19b52-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="19b52-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="19b52-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="19b52-161">These values are not real.</span></span> <span data-ttu-id="19b52-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="19b52-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="19b52-163">Kişi [LogicMonitor istemci destek ekibi](https://www.logicmonitor.com/contact/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="19b52-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="19b52-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="19b52-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="19b52-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="19b52-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19b52-168">İçinde tooyour oturum **LogicMonitor** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="19b52-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="19b52-169">Hello içinde hello üst menüsünde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="19b52-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="19b52-170">![Ayarları](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="19b52-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="19b52-171">Merhaba gezinti .bat uzantılarını dener içinde hello sol tarafında, tıklatın **çoklu oturum açma**</span><span class="sxs-lookup"><span data-stu-id="19b52-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="19b52-172">![Çoklu oturum açma](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="19b52-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="19b52-173">Merhaba, **çoklu oturum açma (SSO) ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="19b52-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="19b52-174">![Çoklu oturum açma ayarları](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="19b52-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="19b52-175">a.</span><span class="sxs-lookup"><span data-stu-id="19b52-175">a.</span></span> <span data-ttu-id="19b52-176">Seçin **çoklu oturum açmayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="19b52-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="19b52-177">b.</span><span class="sxs-lookup"><span data-stu-id="19b52-177">b.</span></span> <span data-ttu-id="19b52-178">Olarak **varsayılan rol ataması**seçin **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="19b52-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="19b52-179">c.</span><span class="sxs-lookup"><span data-stu-id="19b52-179">c.</span></span> <span data-ttu-id="19b52-180">İndirilen hello meta veri dosyasını Not Defteri'nde açın ve hello dosyasının içeriği hello yapıştırın **kimlik sağlayıcısı meta verileri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="19b52-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="19b52-181">d.</span><span class="sxs-lookup"><span data-stu-id="19b52-181">d.</span></span> <span data-ttu-id="19b52-182">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="19b52-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="19b52-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="19b52-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="19b52-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="19b52-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="19b52-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19b52-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19b52-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19b52-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="19b52-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="19b52-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="19b52-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="19b52-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19b52-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="19b52-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19b52-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="19b52-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19b52-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="19b52-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19b52-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="19b52-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19b52-198">a.</span><span class="sxs-lookup"><span data-stu-id="19b52-198">a.</span></span> <span data-ttu-id="19b52-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19b52-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19b52-200">b.</span><span class="sxs-lookup"><span data-stu-id="19b52-200">b.</span></span> <span data-ttu-id="19b52-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="19b52-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19b52-202">c.</span><span class="sxs-lookup"><span data-stu-id="19b52-202">c.</span></span> <span data-ttu-id="19b52-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="19b52-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19b52-204">d.</span><span class="sxs-lookup"><span data-stu-id="19b52-204">d.</span></span> <span data-ttu-id="19b52-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19b52-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="19b52-206">LogicMonitor test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19b52-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="19b52-207">AAD kullanıcılar toobe mümkün toosign için bunların sağlanan toohello LogicMonitor uygulama Azure Active Directory kullanıcı adlarını kullanarak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b52-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="19b52-208">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="19b52-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="19b52-209">İçinde tooyour LogicMonitor şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="19b52-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="19b52-210">Hello içinde hello üst menüsünde **ayarları**ve ardından **rol ve kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="19b52-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="19b52-211">![Rol ve kullanıcı](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "rolleri ve kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="19b52-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="19b52-212">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19b52-212">Click **Add**.</span></span>

4. <span data-ttu-id="19b52-213">Merhaba, **Hesap Ekle** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="19b52-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="19b52-214">![Hesap Ekle](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Hesap Ekle")</span><span class="sxs-lookup"><span data-stu-id="19b52-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="19b52-215">a.</span><span class="sxs-lookup"><span data-stu-id="19b52-215">a.</span></span> <span data-ttu-id="19b52-216">Türü hello **kullanıcıadı**, **e-posta**, **parola**, ve **parolayı yeniden yazın parola** hello Azure Active Directory kullanıcı istediğiniz değerleri metin kutuları hello içine tooprovision ilgili.</span><span class="sxs-lookup"><span data-stu-id="19b52-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="19b52-217">b.</span><span class="sxs-lookup"><span data-stu-id="19b52-217">b.</span></span> <span data-ttu-id="19b52-218">Seçin **rolleri**, **görüntüleme izinleri**ve hello **durum**.</span><span class="sxs-lookup"><span data-stu-id="19b52-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="19b52-219">c.</span><span class="sxs-lookup"><span data-stu-id="19b52-219">c.</span></span> <span data-ttu-id="19b52-220">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="19b52-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="19b52-221">API, kullanıcı hesaplarını LogicMonitor tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer LogicMonitor kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b52-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="19b52-222">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="19b52-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="19b52-223">Bu bölümde, erişim tooLogicMonitor vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="19b52-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="19b52-225">**tooassign Britta Simon tooLogicMonitor hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="19b52-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="19b52-226">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="19b52-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="19b52-228">Merhaba uygulamalar listesinde **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="19b52-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="19b52-230">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="19b52-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="19b52-232">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="19b52-232">Click **Add** button.</span></span> <span data-ttu-id="19b52-233">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="19b52-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="19b52-235">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="19b52-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19b52-236">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="19b52-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19b52-237">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="19b52-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19b52-238">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="19b52-238">Testing single sign-on</span></span>

<span data-ttu-id="19b52-239">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="19b52-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="19b52-240">Merhaba LogicMonitor hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour LogicMonitor uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b52-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="19b52-241">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19b52-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="19b52-242">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="19b52-242">Additional resources</span></span>

* [<span data-ttu-id="19b52-243">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="19b52-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19b52-244">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="19b52-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

