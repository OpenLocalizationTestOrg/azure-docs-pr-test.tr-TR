---
title: "Öğretici: Azure Active Directory Tümleştirme Bambu Kantega SSO | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve bambu Kantega SSO arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="2f53e-103">Öğretici: Azure Active Directory Tümleştirme Bambu Kantega SSO</span><span class="sxs-lookup"><span data-stu-id="2f53e-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="2f53e-104">Bu öğreticide, bilgi nasıl toointegrate Kantega SSO Azure Active Directory (Azure AD) ile Bambu için.</span><span class="sxs-lookup"><span data-stu-id="2f53e-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f53e-105">Kantega SSO Bambu için Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2f53e-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f53e-106">Erişim tooKantega SSO Bambu için olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f53e-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="2f53e-107">Kullanıcıların tooautomatically get açan tooKantega SSO (çoklu oturum açma) Bambu için Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2f53e-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f53e-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2f53e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f53e-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f53e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f53e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f53e-110">Prerequisites</span></span>

<span data-ttu-id="2f53e-111">tooconfigure Bambu Kantega SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f53e-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="2f53e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2f53e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f53e-113">Abonelik Kantega SSO Bambu çoklu oturum açma için etkin</span><span class="sxs-lookup"><span data-stu-id="2f53e-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f53e-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2f53e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f53e-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f53e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f53e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f53e-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f53e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f53e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2f53e-118">Scenario description</span></span>
<span data-ttu-id="2f53e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2f53e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f53e-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2f53e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f53e-121">Merhaba Galerisi'nden Kantega SSO Bambu için ekleme</span><span class="sxs-lookup"><span data-stu-id="2f53e-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="2f53e-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f53e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="2f53e-123">Merhaba Galerisi'nden Kantega SSO Bambu için ekleme</span><span class="sxs-lookup"><span data-stu-id="2f53e-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="2f53e-124">Azure AD'ye tooconfigure hello tümleştirme Bambu Kantega sso'nun tooadd Kantega SSO hello galeri tooyour listesinden yönetilen SaaS uygulamaları için Bambu gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f53e-125">**tooadd Kantega SSO hello galerisinden Bambu için hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f53e-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f53e-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f53e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f53e-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f53e-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2f53e-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f53e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2f53e-133">Merhaba arama kutusuna yazın **Kantega SSO Bambu için**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="2f53e-135">Merhaba Sonuçlar panelinde seçin **Kantega SSO Bambu için**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2f53e-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f53e-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2f53e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f53e-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Bambu Kantega SSO ile test etme.</span><span class="sxs-lookup"><span data-stu-id="2f53e-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f53e-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Bambu Kantega SSO tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="2f53e-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve bambu Kantega SSO hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="2f53e-141">Merhaba hello değeri Bambu için Kantega SSO içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2f53e-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f53e-142">tooconfigure ve Azure AD çoklu oturum açma ile test Kantega SSO Bambu için yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f53e-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f53e-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2f53e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f53e-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2f53e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f53e-145">**[Kantega SSO Bambu test kullanıcısı için oluşturma](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave Britta Simon Kantega SSO kullanıcı bağlantılı toohello Azure AD gösterimidir Bambu için karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2f53e-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f53e-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2f53e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f53e-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2f53e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f53e-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f53e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f53e-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve, Kantega SSO Bambu uygulama için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="2f53e-150">**Azure AD çoklu oturum açma tooconfigure Bambu, Kantega SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f53e-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f53e-151">Merhaba hello üzerinde Azure portal'ın **Kantega SSO Bambu için** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2f53e-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2f53e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="2f53e-155">İçinde **IDP** hello modunda başlatılan **Kantega SSO Bambu etki alanı ve URL'ler için** bölümünde adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="2f53e-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-157">a.</span></span> <span data-ttu-id="2f53e-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2f53e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="2f53e-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-159">b.</span></span> <span data-ttu-id="2f53e-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2f53e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="2f53e-161">İçinde **SP** başlatılan modu, onay **Göster Gelişmiş URL ayarları** ve adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="2f53e-163">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2f53e-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2f53e-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-164">These values are not real.</span></span> <span data-ttu-id="2f53e-165">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="2f53e-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2f53e-166">Bu değerleri hello öğreticinin ilerleyen bölümlerinde açıklanan Bambu eklentisi hello yapılandırması sırasında alınır.</span><span class="sxs-lookup"><span data-stu-id="2f53e-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="2f53e-167">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2f53e-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="2f53e-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f53e-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2f53e-171">Farklı web tarayıcısı penceresinde tooyour Bambu içi sunucuda yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="2f53e-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="2f53e-172">Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="2f53e-174">Eklentiler sekmesi bölümü altında tıklatın **Bul yeni eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="2f53e-175">Arama **Kantega SSO Bambu (SAML & Kerberos) için** tıklatıp **yükleme** düğmesini tooinstall hello yeni SAML eklentisini.</span><span class="sxs-lookup"><span data-stu-id="2f53e-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="2f53e-177">Merhaba eklentisi yükleme başlar.</span><span class="sxs-lookup"><span data-stu-id="2f53e-177">hello plugin installation will start.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="2f53e-179">Merhaba yüklemesi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="2f53e-179">Once hello installation is complete.</span></span> <span data-ttu-id="2f53e-180">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-180">Click **Close**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="2f53e-182">**Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-182">Click **Manage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="2f53e-184">Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.</span><span class="sxs-lookup"><span data-stu-id="2f53e-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="2f53e-186">Merhaba, **SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2f53e-186">In hello **SAML** section.</span></span> <span data-ttu-id="2f53e-187">Seçin **Azure Active Directory (Azure AD)** hello gelen **Ekle kimlik sağlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="2f53e-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="2f53e-189">Abonelik düzeyi olarak **temel**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-189">Select subscription level as **Basic**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="2f53e-191">Merhaba üzerinde **uygulama özellikleri** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-191">On hello **App properties** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="2f53e-193">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-193">a.</span></span> <span data-ttu-id="2f53e-194">Kopya hello **uygulama kimliği URI'si** değer ve olarak kullanmak **tanımlayıcısı, yanıt URL'si ve oturum açma URL'si** hello üzerinde **Kantega SSO Bambu etki alanı ve URL'ler için** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="2f53e-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2f53e-195">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-195">b.</span></span> <span data-ttu-id="2f53e-196">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-196">Click **Next**.</span></span>

17. <span data-ttu-id="2f53e-197">Merhaba üzerinde **meta veri içeri aktarma** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="2f53e-199">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-199">a.</span></span> <span data-ttu-id="2f53e-200">Seçin **meta veri dosyası bilgisayarımda**ve Azure portalından karşıdan yükleme meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="2f53e-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2f53e-201">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-201">b.</span></span> <span data-ttu-id="2f53e-202">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-202">Click **Next**.</span></span>

18. <span data-ttu-id="2f53e-203">Merhaba üzerinde **adı ve SSO konumunu** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="2f53e-205">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-205">a.</span></span> <span data-ttu-id="2f53e-206">Merhaba kimlik sağlayıcısı adını ekleyin, **kimlik sağlayıcı adı** textbox (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f53e-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="2f53e-207">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-207">b.</span></span> <span data-ttu-id="2f53e-208">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-208">Click **Next**.</span></span>

19. <span data-ttu-id="2f53e-209">Merhaba imzalama sertifikası doğrulayın ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="2f53e-211">Merhaba üzerinde **Bambu kullanıcı hesapları** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="2f53e-213">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-213">a.</span></span> <span data-ttu-id="2f53e-214">Seçin **gerekirse Bambu'nın iç dizinde kullanıcılar oluşturma** ve kullanıcıların hello grubunun adı uygun hello girin (olabilir birden çok yok.</span><span class="sxs-lookup"><span data-stu-id="2f53e-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="2f53e-215">virgülle ayrılmış grupları).</span><span class="sxs-lookup"><span data-stu-id="2f53e-215">of groups separated by comma).</span></span>

    <span data-ttu-id="2f53e-216">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-216">b.</span></span> <span data-ttu-id="2f53e-217">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-217">Click **Next**.</span></span>

21. <span data-ttu-id="2f53e-218">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-218">Click **Finish**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="2f53e-220">Merhaba üzerinde **için Azure AD etki alanları bilinen** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="2f53e-222">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-222">a.</span></span> <span data-ttu-id="2f53e-223">Seçin **etki alanları bilinen** hello sayfasının sol hello panelinden.</span><span class="sxs-lookup"><span data-stu-id="2f53e-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="2f53e-224">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-224">b.</span></span> <span data-ttu-id="2f53e-225">Hello etki alanı adı girin **etki alanları bilinen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2f53e-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="2f53e-226">c.</span><span class="sxs-lookup"><span data-stu-id="2f53e-226">c.</span></span> <span data-ttu-id="2f53e-227">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2f53e-228">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2f53e-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f53e-229">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2f53e-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f53e-230">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f53e-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f53e-231">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f53e-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f53e-232">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2f53e-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2f53e-234">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f53e-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f53e-235">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2f53e-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f53e-237">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f53e-239">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f53e-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f53e-241">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f53e-243">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-243">a.</span></span> <span data-ttu-id="2f53e-244">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f53e-245">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-245">b.</span></span> <span data-ttu-id="2f53e-246">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2f53e-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f53e-247">c.</span><span class="sxs-lookup"><span data-stu-id="2f53e-247">c.</span></span> <span data-ttu-id="2f53e-248">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f53e-249">d.</span><span class="sxs-lookup"><span data-stu-id="2f53e-249">d.</span></span> <span data-ttu-id="2f53e-250">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="2f53e-251">Kantega SSO Bambu test kullanıcısı için oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f53e-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="2f53e-252">tooenable Azure AD kullanıcıların toolog tooBamboo bunların Bambu sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="2f53e-253">İçinde Kantega SSO Bambu için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="2f53e-254">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f53e-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f53e-255">Tooyour Bambu içi sunucuda, yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="2f53e-256">Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-256">Hover on cog and click hello **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="2f53e-258">**Kullanıcılar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-258">Click **Users**.</span></span> <span data-ttu-id="2f53e-259">Merhaba altında **Kullanıcı Ekle** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2f53e-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="2f53e-261">a.</span><span class="sxs-lookup"><span data-stu-id="2f53e-261">a.</span></span> <span data-ttu-id="2f53e-262">Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2f53e-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2f53e-263">b.</span><span class="sxs-lookup"><span data-stu-id="2f53e-263">b.</span></span> <span data-ttu-id="2f53e-264">Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="2f53e-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="2f53e-265">c.</span><span class="sxs-lookup"><span data-stu-id="2f53e-265">c.</span></span> <span data-ttu-id="2f53e-266">Merhaba, **parolayı onayla** metin kutusuna, kullanıcının parolasını hello.</span><span class="sxs-lookup"><span data-stu-id="2f53e-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="2f53e-267">d.</span><span class="sxs-lookup"><span data-stu-id="2f53e-267">d.</span></span> <span data-ttu-id="2f53e-268">Merhaba, **tam adı** metin kutusuna, Britta Simon gibi hello kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="2f53e-269">e.</span><span class="sxs-lookup"><span data-stu-id="2f53e-269">e.</span></span> <span data-ttu-id="2f53e-270">Merhaba, **e-posta** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2f53e-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2f53e-271">f.</span><span class="sxs-lookup"><span data-stu-id="2f53e-271">f.</span></span> <span data-ttu-id="2f53e-272">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f53e-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f53e-273">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2f53e-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f53e-274">Bu bölümde, erişim tooKantega Bambu SSO vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2f53e-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2f53e-276">**tooassign Britta Simon tooKantega Bambu, SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2f53e-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f53e-277">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2f53e-279">Merhaba uygulamalar listesinde **Kantega SSO Bambu için**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="2f53e-281">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2f53e-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2f53e-283">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f53e-283">Click **Add** button.</span></span> <span data-ttu-id="2f53e-284">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f53e-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2f53e-286">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2f53e-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f53e-287">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f53e-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f53e-288">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2f53e-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f53e-289">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2f53e-289">Testing single sign-on</span></span>

<span data-ttu-id="2f53e-290">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2f53e-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f53e-291">Merhaba Kantega SSO hello erişim paneli Bambu parçasında tıkladığınızda, Bambu uygulaması için otomatik olarak oturum açma Kantega SSO tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f53e-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="2f53e-292">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f53e-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2f53e-293">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2f53e-293">Additional resources</span></span>

* [<span data-ttu-id="2f53e-294">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2f53e-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f53e-295">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2f53e-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

