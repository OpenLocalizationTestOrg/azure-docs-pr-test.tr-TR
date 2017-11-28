---
title: "Öğretici: Azure Active Directory ile tümleştirme Jira için SAML SSO GmbH çözünürlüğün | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile SAML SSO GmbH çözünürlüğün Jira için arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="1afd6-103">Öğretici: Çözümleme GmbH Jira için SAML SSO Azure Active Directory Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="1afd6-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="1afd6-104">Bu öğreticide, bilgi nasıl toointegrate SAML SSO Jira için Azure Active Directory (Azure AD) ile GmbH çözünürlüğün.</span><span class="sxs-lookup"><span data-stu-id="1afd6-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1afd6-105">Azure AD ile GmbH çözünürlüğün SAML SSO Jira için tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1afd6-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1afd6-106">Erişim tooSAML SSO için Jira tarafından çözüldü GmbH sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1afd6-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="1afd6-107">Azure AD hesaplarına sahip (çoklu oturum açma) GmbH çözünürlüğün Jira için kullanıcılar tooautomatically get açan tooSAML SSO etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1afd6-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1afd6-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1afd6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1afd6-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1afd6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1afd6-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1afd6-110">Prerequisites</span></span>

<span data-ttu-id="1afd6-111">tooconfigure GmbH çözünürlüğün Jira için SAML SSO ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1afd6-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="1afd6-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1afd6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1afd6-113">SAML SSO etkin abonelik GmbH çoklu oturum çözünürlüğün Jira için</span><span class="sxs-lookup"><span data-stu-id="1afd6-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1afd6-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1afd6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1afd6-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1afd6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1afd6-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1afd6-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1afd6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1afd6-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1afd6-118">Scenario description</span></span>
<span data-ttu-id="1afd6-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1afd6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1afd6-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1afd6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1afd6-121">SAML SSO Jira için çözüm GmbH tarafından hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="1afd6-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="1afd6-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1afd6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="1afd6-123">SAML SSO Jira için çözüm GmbH tarafından hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="1afd6-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="1afd6-124">tooconfigure hello tümleştirilmesi Jira için SAML SSO GmbH çözünürlüğün Azure AD'ye, tooadd SAML SSO için Jira hello galeri tooyour yönetilen SaaS uygulamaları listesinden GmbH çözünürlüğün gerekir.</span><span class="sxs-lookup"><span data-stu-id="1afd6-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1afd6-125">**tooadd Jira için SAML SSO hello galerisinden GmbH çözünürlüğün hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1afd6-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1afd6-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1afd6-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1afd6-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1afd6-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1afd6-133">Merhaba arama kutusuna yazın **SAML SSO GmbH çözünürlüğün Jira için**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="1afd6-135">Merhaba Sonuçlar panelinde seçin **SAML SSO GmbH çözünürlüğün Jira için**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1afd6-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1afd6-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1afd6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1afd6-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Jira için SAML SSO GmbH "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı çözünürlüğün test etme</span><span class="sxs-lookup"><span data-stu-id="1afd6-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1afd6-139">Tek toowork'ın oturum açma Azure AD hangi hello karşılık gelen kullanıcı SAML SSO Jira için Azure AD içinde GmbH tooa kullanıcıdır çözünürlüğün tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="1afd6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="1afd6-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello çözünürlüğün SAML SSO Jira için ilgili kullanıcı arasında bir bağlantı ilişkisi GmbH kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1afd6-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="1afd6-141">Merhaba hello değeri GmbH çözünürlüğün Jira için SAML SSO içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1afd6-142">tooconfigure ve Azure AD çoklu oturum açma ile test SAML SSO Jira için GmbH çözünürlüğün, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1afd6-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1afd6-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="1afd6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1afd6-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="1afd6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1afd6-145">**[SAML SSO çözümleme GmbH test kullanıcı tarafından Jira için oluşturma](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave bir Britta Simon SAML SSO Jira için karşılık gelen kullanıcı bağlantılı toohello Azure AD gösterimidir GmbH çözünürlüğün.</span><span class="sxs-lookup"><span data-stu-id="1afd6-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1afd6-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1afd6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1afd6-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="1afd6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1afd6-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1afd6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1afd6-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, SAML SSO Jira için çözüm GmbH uygulama tarafından yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="1afd6-150">**Azure AD çoklu oturum açma GmbH, çözünürlüğün tooconfigure Jira için SAML SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1afd6-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="1afd6-151">Merhaba hello üzerinde Azure portal'ın **SAML SSO GmbH çözünürlüğün Jira için** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1afd6-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1afd6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="1afd6-155">Merhaba üzerinde **Jira GmbH etki alanı çözünürlüğün ve URL'ler için SAML SSO** tooconfigure hello uygulamada isterseniz, bölümü **IDP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="1afd6-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="1afd6-157">a.</span><span class="sxs-lookup"><span data-stu-id="1afd6-157">a.</span></span> <span data-ttu-id="1afd6-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1afd6-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="1afd6-159">b.</span><span class="sxs-lookup"><span data-stu-id="1afd6-159">b.</span></span> <span data-ttu-id="1afd6-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1afd6-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="1afd6-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1afd6-162">Tooconfigure hello uygulamada istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="1afd6-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="1afd6-164">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1afd6-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1afd6-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="1afd6-165">These values are not real.</span></span> <span data-ttu-id="1afd6-166">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="1afd6-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1afd6-167">Kişi [SAML SSO GmbH istemci çözünürlüğün Jira için destek ekibi](https://www.resolution.de/go/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="1afd6-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="1afd6-168">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1afd6-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="1afd6-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1afd6-172">Farklı web tarayıcısı penceresinde tooyour içinde oturum **SAML SSO çözümleme GmbH Yönetici portalı tarafından Jira için** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="1afd6-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="1afd6-173">Dişlisine üzerine gelin ve hello tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="1afd6-175">Yeniden yönlendirilen tooAdministrator erişim sayfası var.</span><span class="sxs-lookup"><span data-stu-id="1afd6-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="1afd6-176">Merhaba girin **parola** tıklatıp **Onayla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="1afd6-178">Eklentiler sekmesi bölümü altında tıklatın **Bul yeni eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="1afd6-179">Arama **SAML çoklu oturum açma (SSO) JIRA için** tıklatıp **yükleme** düğmesini tooinstall hello yeni SAML eklentisini.</span><span class="sxs-lookup"><span data-stu-id="1afd6-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="1afd6-181">Merhaba eklentisi yükleme başlar.</span><span class="sxs-lookup"><span data-stu-id="1afd6-181">hello plugin installation will start.</span></span> <span data-ttu-id="1afd6-182">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-182">Click **Close**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="1afd6-185">**Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-185">Click **Manage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="1afd6-187">Tıklatın **yapılandırma** tooconfigure hello yeni eklenti.</span><span class="sxs-lookup"><span data-stu-id="1afd6-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="1afd6-189">Üzerinde **SAML SingleSignOn eklentisi yapılandırma** sayfasında, **ek kimlik sağlayıcısı ekleyin** düğmesini tooconfigure hello ayarlarını kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1afd6-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="1afd6-191">Bu sayfada şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1afd6-191">Perform following steps on this page:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="1afd6-193">a.</span><span class="sxs-lookup"><span data-stu-id="1afd6-193">a.</span></span> <span data-ttu-id="1afd6-194">Ekleme **adı** hello kimlik sağlayıcısı (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1afd6-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="1afd6-195">b.</span><span class="sxs-lookup"><span data-stu-id="1afd6-195">b.</span></span> <span data-ttu-id="1afd6-196">Ekleme **açıklama** hello kimlik sağlayıcısı (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1afd6-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="1afd6-197">c.</span><span class="sxs-lookup"><span data-stu-id="1afd6-197">c.</span></span> <span data-ttu-id="1afd6-198">Tıklatın **XML** ve select hello **meta veri** Azure Portalı'ndan indirilen dosya.</span><span class="sxs-lookup"><span data-stu-id="1afd6-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1afd6-199">d.</span><span class="sxs-lookup"><span data-stu-id="1afd6-199">d.</span></span> <span data-ttu-id="1afd6-200">Tıklatın **yük** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-200">Click **Load** button.</span></span>

    <span data-ttu-id="1afd6-201">e.</span><span class="sxs-lookup"><span data-stu-id="1afd6-201">e.</span></span> <span data-ttu-id="1afd6-202">Merhaba IDP meta verileri okur ve hello alanlar hello ekran vurgulu olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="1afd6-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="1afd6-203">Tıklatın **Ayarları Kaydet** düğmesini toosave hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="1afd6-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="1afd6-205">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1afd6-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1afd6-206">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="1afd6-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1afd6-207">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1afd6-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1afd6-208">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1afd6-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="1afd6-209">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="1afd6-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1afd6-211">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1afd6-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1afd6-212">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1afd6-214">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1afd6-216">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="1afd6-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1afd6-218">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1afd6-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1afd6-220">a.</span><span class="sxs-lookup"><span data-stu-id="1afd6-220">a.</span></span> <span data-ttu-id="1afd6-221">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1afd6-222">b.</span><span class="sxs-lookup"><span data-stu-id="1afd6-222">b.</span></span> <span data-ttu-id="1afd6-223">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1afd6-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1afd6-224">c.</span><span class="sxs-lookup"><span data-stu-id="1afd6-224">c.</span></span> <span data-ttu-id="1afd6-225">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1afd6-226">d.</span><span class="sxs-lookup"><span data-stu-id="1afd6-226">d.</span></span> <span data-ttu-id="1afd6-227">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="1afd6-228">SAML SSO çözümleme GmbH test kullanıcı tarafından Jira için oluşturma</span><span class="sxs-lookup"><span data-stu-id="1afd6-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="1afd6-229">tooenable Azure AD kullanıcıların toolog Jira için SSO GmbH çözünürlüğün tooSAML bunlar Jira için SAML SSO içine GmbH çözümleme tarafından sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1afd6-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="1afd6-230">Jira GmbH çözünürlüğün için SAML SSO içinde sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="1afd6-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="1afd6-231">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1afd6-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1afd6-232">İçinde tooyour SAML SSO çözümleme GmbH şirket site tarafından Jira için yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="1afd6-233">Dişlisine üzerine gelin ve hello tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-233">Hover on cog and click hello **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="1afd6-235">Yeniden yönlendirilen tooAdministrator erişim sayfası tooenter olduğunuz **parola** tıklatıp **Onayla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="1afd6-237">Altında **kullanıcı yönetimi** bölüm sekmesini tıklatın, **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-237">Under **User management** tab section, click **create user**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="1afd6-239">Merhaba üzerinde **"Yeni kullanıcı oluştur"** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1afd6-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="1afd6-241">a.</span><span class="sxs-lookup"><span data-stu-id="1afd6-241">a.</span></span> <span data-ttu-id="1afd6-242">Merhaba, **e-posta adresi** türü hello kullanıcının e-posta adresi metin kutusuna, ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1afd6-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1afd6-243">b.</span><span class="sxs-lookup"><span data-stu-id="1afd6-243">b.</span></span> <span data-ttu-id="1afd6-244">Merhaba, **tam adı** metin kutusuna, Britta Simon gibi hello kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="1afd6-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="1afd6-245">c.</span><span class="sxs-lookup"><span data-stu-id="1afd6-245">c.</span></span> <span data-ttu-id="1afd6-246">Merhaba, **kullanıcıadı** metin kutusuna, kullanıcının türü hello e-posta ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1afd6-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1afd6-247">d.</span><span class="sxs-lookup"><span data-stu-id="1afd6-247">d.</span></span> <span data-ttu-id="1afd6-248">Merhaba, **parola** metin kutusuna, kullanıcının hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="1afd6-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="1afd6-249">e.</span><span class="sxs-lookup"><span data-stu-id="1afd6-249">e.</span></span> <span data-ttu-id="1afd6-250">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1afd6-251">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1afd6-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1afd6-252">Bu bölümde, erişim tooSAML SSO için Jira tarafından çözüldü GmbH vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1afd6-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1afd6-254">**tooassign GmbH, çözünürlüğün Britta Simon tooSAML Jira için SSO hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1afd6-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="1afd6-255">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1afd6-257">Merhaba uygulamalar listesinde **SAML SSO GmbH çözünürlüğün Jira için**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="1afd6-259">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1afd6-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1afd6-261">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1afd6-261">Click **Add** button.</span></span> <span data-ttu-id="1afd6-262">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1afd6-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1afd6-264">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1afd6-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1afd6-265">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1afd6-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1afd6-266">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1afd6-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1afd6-267">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1afd6-267">Testing single sign-on</span></span>

<span data-ttu-id="1afd6-268">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1afd6-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1afd6-269">Merhaba SAML SSO Jira için çözüm GmbH hello erişim paneli parçasında tarafından tıkladığınızda, çözümleme GmbH uygulama tarafından Jira için otomatik olarak oturum açma SAML SSO tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1afd6-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="1afd6-270">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1afd6-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1afd6-271">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1afd6-271">Additional resources</span></span>

* [<span data-ttu-id="1afd6-272">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="1afd6-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1afd6-273">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1afd6-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

