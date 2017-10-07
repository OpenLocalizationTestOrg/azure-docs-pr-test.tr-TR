---
title: "Öğretici: Azure Active Directory Tümleştirme FishEye/Crucible Kantega SSO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FishEye/Crucible Kantega SSO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="5a710-103">Öğretici: Azure Active Directory Tümleştirme FishEye/Crucible Kantega SSO</span><span class="sxs-lookup"><span data-stu-id="5a710-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="5a710-104">Bu öğreticide, bilgi nasıl toointegrate Kantega SSO FishEye/Crucible Azure Active Directory'ye (Azure AD) için.</span><span class="sxs-lookup"><span data-stu-id="5a710-104">In this tutorial, you learn how toointegrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a710-105">Kantega SSO FishEye/Crucible için Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5a710-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a710-106">FishEye/Crucible için erişim tooKantega SSO olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5a710-106">You can control in Azure AD who has access tooKantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="5a710-107">Kullanıcıların tooautomatically get açan tooKantega SSO (çoklu oturum açma) FishEye/Crucible için Azure AD hesaplarına etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5a710-107">You can enable your users tooautomatically get signed-on tooKantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a710-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="5a710-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5a710-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a710-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a710-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5a710-110">Prerequisites</span></span>

<span data-ttu-id="5a710-111">tooconfigure FishEye/Crucible Kantega SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a710-111">tooconfigure Azure AD integration with Kantega SSO for FishEye/Crucible, you need hello following items:</span></span>

- <span data-ttu-id="5a710-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5a710-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a710-113">Abonelik Kantega SSO FishEye/Crucible çoklu oturum açma için etkin</span><span class="sxs-lookup"><span data-stu-id="5a710-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a710-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5a710-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a710-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a710-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a710-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a710-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a710-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a710-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5a710-118">Scenario description</span></span>
<span data-ttu-id="5a710-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5a710-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a710-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5a710-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a710-121">Merhaba Galerisi'nden Kantega SSO FishEye/Crucible için ekleme</span><span class="sxs-lookup"><span data-stu-id="5a710-121">Adding Kantega SSO for FishEye/Crucible from hello gallery</span></span>
2. <span data-ttu-id="5a710-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5a710-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a><span data-ttu-id="5a710-123">Merhaba Galerisi'nden Kantega SSO FishEye/Crucible için ekleme</span><span class="sxs-lookup"><span data-stu-id="5a710-123">Adding Kantega SSO for FishEye/Crucible from hello gallery</span></span>
<span data-ttu-id="5a710-124">Azure AD'ye tooconfigure hello tümleştirme FishEye/Crucible Kantega sso'nun tooadd Kantega SSO hello galeri tooyour listesinden yönetilen SaaS uygulamaları FishEye/Crucible için gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a710-124">tooconfigure hello integration of Kantega SSO for FishEye/Crucible into Azure AD, you need tooadd Kantega SSO for FishEye/Crucible from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a710-125">**tooadd FishEye/Crucible hello galerisinden Kantega SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a710-125">**tooadd Kantega SSO for FishEye/Crucible from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a710-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5a710-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a710-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5a710-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a710-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5a710-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="5a710-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a710-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="5a710-133">Merhaba arama kutusuna yazın **Kantega SSO FishEye/Crucible için**.</span><span class="sxs-lookup"><span data-stu-id="5a710-133">In hello search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="5a710-135">Merhaba Sonuçlar panelinde seçin **Kantega SSO FishEye/Crucible için**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5a710-135">In hello results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a710-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5a710-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a710-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma FishEye/Crucible "Britta Simon" adlı bir test kullanıcı tabanlı Kantega SSO ile test etme.</span><span class="sxs-lookup"><span data-stu-id="5a710-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a710-139">Tek toowork'ın oturum açma hangi hello karşılık gelen FishEye/Crucible Kantega SSO tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a710-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for FishEye/Crucible is tooa user in Azure AD.</span></span> <span data-ttu-id="5a710-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve FishEye/Crucible Kantega SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a710-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for FishEye/Crucible needs toobe established.</span></span>

<span data-ttu-id="5a710-141">Merhaba hello değeri FishEye/Crucible için Kantega SSO içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="5a710-141">In Kantega SSO for FishEye/Crucible, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a710-142">tooconfigure ve Azure AD çoklu oturum açma FishEye/Crucible için test Kantega SSO, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a710-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a710-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5a710-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a710-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5a710-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a710-145">**[Kantega SSO FishEye/Crucible test kullanıcısı için oluşturma](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave Britta Simon Kantega SSO kullanıcı bağlantılı toohello Azure AD gösterimidir FishEye/Crucible için karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5a710-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a710-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5a710-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a710-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a710-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a710-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5a710-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a710-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve, Kantega SSO FishEye/Crucible uygulama için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a710-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="5a710-150">**Azure AD çoklu oturum açma tooconfigure FishEye/Crucible Kantega SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a710-150">**tooconfigure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a710-151">Merhaba hello üzerinde Azure portal'ın **Kantega SSO FishEye/Crucible için** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5a710-151">In hello Azure portal, on hello **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="5a710-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5a710-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="5a710-155">İçinde **IDP** hello modunda başlatılan **Kantega SSO FishEye/Crucible etki alanı ve URL'ler için** bölümünde adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-155">In **IDP** initiated mode, on hello **Kantega SSO for FishEye/Crucible Domain and URLs** section perform hello following step :</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="5a710-157">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-157">a.</span></span> <span data-ttu-id="5a710-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="5a710-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="5a710-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-159">b.</span></span> <span data-ttu-id="5a710-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="5a710-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="5a710-161">İçinde **SP** başlatılan modu, onay **Göster Gelişmiş URL ayarları** ve adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-161">In **SP** initiated mode, check **Show advanced URL settings** and perform hello following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="5a710-163">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="5a710-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5a710-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5a710-164">These values are not real.</span></span> <span data-ttu-id="5a710-165">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="5a710-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5a710-166">Bu değerleri hello öğreticinin ilerleyen bölümlerinde açıklanan FishEye/Crucible eklentisi hello yapılandırması sırasında alınır.</span><span class="sxs-lookup"><span data-stu-id="5a710-166">These values are recieved during hello configuration of FishEye/Crucible plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="5a710-167">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5a710-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="5a710-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a710-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="5a710-171">Farklı web tarayıcısı penceresinde tooyour FishEye/Crucible içi sunucuda yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="5a710-171">In a different web browser window, log in tooyour FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="5a710-172">Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="5a710-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="5a710-174">Sistem ayarları bölümü altında tıklatın **Bul yeni eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="5a710-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="5a710-176">Arama **Kantega SSO Crucible için** tıklatıp **yükleme** düğmesini tooinstall hello yeni SAML eklentisini.</span><span class="sxs-lookup"><span data-stu-id="5a710-176">Search **Kantega SSO for Crucible** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="5a710-178">Merhaba Eklentisi yüklemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="5a710-178">hello plugin installation starts.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="5a710-180">Merhaba yüklemesi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="5a710-180">Once hello installation is complete.</span></span> <span data-ttu-id="5a710-181">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-181">Click **Close**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="5a710-183">**Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-183">Click **Manage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="5a710-185">Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.</span><span class="sxs-lookup"><span data-stu-id="5a710-185">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="5a710-187">Merhaba, **SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5a710-187">In hello **SAML** section.</span></span> <span data-ttu-id="5a710-188">Seçin **Azure Active Directory (Azure AD)** hello gelen **Ekle kimlik sağlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="5a710-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="5a710-190">Abonelik düzeyi olarak **temel**.</span><span class="sxs-lookup"><span data-stu-id="5a710-190">Select subscription level as **Basic**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="5a710-192">Merhaba üzerinde **uygulama özellikleri** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-192">On hello **App properties** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="5a710-194">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-194">a.</span></span> <span data-ttu-id="5a710-195">Kopya hello **uygulama kimliği URI'si** değer ve olarak kullanmak **tanımlayıcısı, yanıt URL'si ve oturum açma URL'si** hello üzerinde **Kantega SSO FishEye/Crucible etki alanı ve URL'ler için** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="5a710-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="5a710-196">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-196">b.</span></span> <span data-ttu-id="5a710-197">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-197">Click **Next**.</span></span>

18. <span data-ttu-id="5a710-198">Merhaba üzerinde **meta veri içeri aktarma** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-198">On hello **Metadata import** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="5a710-200">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-200">a.</span></span> <span data-ttu-id="5a710-201">Seçin **meta veri dosyası bilgisayarımda**ve Azure portalından karşıdan yükleme meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="5a710-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="5a710-202">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-202">b.</span></span> <span data-ttu-id="5a710-203">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-203">Click **Next**.</span></span>

19. <span data-ttu-id="5a710-204">Merhaba üzerinde **adı ve SSO konumunu** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="5a710-206">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-206">a.</span></span> <span data-ttu-id="5a710-207">Merhaba kimlik sağlayıcısı adını ekleyin, **kimlik sağlayıcı adı** textbox (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a710-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="5a710-208">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-208">b.</span></span> <span data-ttu-id="5a710-209">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-209">Click **Next**.</span></span>

20. <span data-ttu-id="5a710-210">Merhaba imzalama sertifikası doğrulayın ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5a710-210">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="5a710-212">Merhaba üzerinde **balık gözü kullanıcı hesapları** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-212">On hello **FishEye user accounts** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="5a710-214">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-214">a.</span></span> <span data-ttu-id="5a710-215">Seçin **gerekirse FishEye'nın iç dizinde kullanıcılar oluşturma** ve kullanıcıların hello grubunun adı uygun hello girin (olabilir birden çok yok.</span><span class="sxs-lookup"><span data-stu-id="5a710-215">Select **Create users in FishEye's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="5a710-216">virgülle ayrılmış grupları).</span><span class="sxs-lookup"><span data-stu-id="5a710-216">of groups separated by comma).</span></span>

    <span data-ttu-id="5a710-217">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-217">b.</span></span> <span data-ttu-id="5a710-218">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-218">Click **Next**.</span></span>

22. <span data-ttu-id="5a710-219">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-219">Click **Finish**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="5a710-221">Merhaba üzerinde **için Azure AD etki alanları bilinen** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="5a710-223">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-223">a.</span></span> <span data-ttu-id="5a710-224">Seçin **etki alanları bilinen** hello sayfasının sol hello panelinden.</span><span class="sxs-lookup"><span data-stu-id="5a710-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="5a710-225">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-225">b.</span></span> <span data-ttu-id="5a710-226">Hello etki alanı adı girin **etki alanları bilinen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="5a710-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="5a710-227">c.</span><span class="sxs-lookup"><span data-stu-id="5a710-227">c.</span></span> <span data-ttu-id="5a710-228">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="5a710-229">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5a710-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a710-230">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="5a710-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a710-231">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a710-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a710-232">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a710-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a710-233">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5a710-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="5a710-235">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a710-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a710-236">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5a710-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a710-238">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5a710-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a710-240">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a710-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a710-242">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a710-244">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-244">a.</span></span> <span data-ttu-id="5a710-245">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a710-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a710-246">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-246">b.</span></span> <span data-ttu-id="5a710-247">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5a710-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a710-248">c.</span><span class="sxs-lookup"><span data-stu-id="5a710-248">c.</span></span> <span data-ttu-id="5a710-249">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5a710-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5a710-250">d.</span><span class="sxs-lookup"><span data-stu-id="5a710-250">d.</span></span> <span data-ttu-id="5a710-251">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="5a710-252">Kantega SSO FishEye/Crucible test kullanıcısı için oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a710-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="5a710-253">tooenable Azure AD kullanıcıların toolog tooFishEye/Crucible, bunlar FishEye/Crucible sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a710-253">tooenable Azure AD users toolog in tooFishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="5a710-254">SSO Kantega içinde FishEye/Crucible için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5a710-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="5a710-255">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a710-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a710-256">Tooyour Crucible içi sunucuda, yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5a710-256">Log in tooyour Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="5a710-257">Dişlisine üzerine gelin ve hello tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5a710-257">Hover on cog and click hello **Users**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="5a710-259">Altında **kullanıcılar** bölüm sekmesini tıklatın, **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5a710-259">Under **Users** tab section, click **Add user**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="5a710-261">Merhaba üzerinde **yeni kullanıcı Ekle** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a710-261">On hello **Add New User** dialog page, perform hello following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="5a710-263">a.</span><span class="sxs-lookup"><span data-stu-id="5a710-263">a.</span></span> <span data-ttu-id="5a710-264">Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5a710-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="5a710-265">b.</span><span class="sxs-lookup"><span data-stu-id="5a710-265">b.</span></span> <span data-ttu-id="5a710-266">Merhaba, **görünen adı** metin kutusuna, Britta Simon gibi hello kullanıcı türü görünen adı.</span><span class="sxs-lookup"><span data-stu-id="5a710-266">In hello **Display Name** textbox, type display name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="5a710-267">c.</span><span class="sxs-lookup"><span data-stu-id="5a710-267">c.</span></span> <span data-ttu-id="5a710-268">Merhaba, **e-posta adresi** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5a710-268">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="5a710-269">d.</span><span class="sxs-lookup"><span data-stu-id="5a710-269">d.</span></span> <span data-ttu-id="5a710-270">Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="5a710-270">In hello **Password** textbox, type hello password of user.</span></span>  

    <span data-ttu-id="5a710-271">e.</span><span class="sxs-lookup"><span data-stu-id="5a710-271">e.</span></span> <span data-ttu-id="5a710-272">Merhaba, **parolayı onayla** metin kutusuna, kullanıcının parolasını hello.</span><span class="sxs-lookup"><span data-stu-id="5a710-272">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>

    <span data-ttu-id="5a710-273">f.</span><span class="sxs-lookup"><span data-stu-id="5a710-273">f.</span></span> <span data-ttu-id="5a710-274">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a710-274">Click **Add**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5a710-275">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5a710-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5a710-276">Bu bölümde, FishEye/Crucible için erişim tooKantega SSO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5a710-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for FishEye/Crucible.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5a710-278">**tooassign Britta Simon tooKantega FishEye/Crucible için SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a710-278">**tooassign Britta Simon tooKantega SSO for FishEye/Crucible, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a710-279">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5a710-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5a710-281">Merhaba uygulamalar listesinde **Kantega SSO FishEye/Crucible için**.</span><span class="sxs-lookup"><span data-stu-id="5a710-281">In hello applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="5a710-283">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5a710-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5a710-285">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a710-285">Click **Add** button.</span></span> <span data-ttu-id="5a710-286">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a710-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5a710-288">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5a710-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a710-289">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a710-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a710-290">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a710-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a710-291">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5a710-291">Testing single sign-on</span></span>

<span data-ttu-id="5a710-292">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5a710-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a710-293">Merhaba Kantega SSO hello erişim paneli FishEye/Crucible parçasında tıkladığınızda, FishEye/Crucible uygulaması için otomatik olarak oturum açma Kantega SSO tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a710-293">When you click hello Kantega SSO for FishEye/Crucible tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="5a710-294">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a710-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5a710-295">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5a710-295">Additional resources</span></span>

* [<span data-ttu-id="5a710-296">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5a710-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a710-297">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5a710-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

