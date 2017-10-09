---
title: "Öğretici: Azure Active Directory Tümleştirme Igloo yazılımıyla | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Igloo yazılımı arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="4d3e4-103">Öğretici: Azure Active Directory Tümleştirme Igloo yazılımıyla</span><span class="sxs-lookup"><span data-stu-id="4d3e4-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="4d3e4-104">Bu öğreticide, bilgi nasıl toointegrate Igloo yazılım Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4d3e4-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d3e4-105">Igloo yazılım Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d3e4-106">Erişim tooIgloo yazılım sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4d3e4-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="4d3e4-107">Kullanıcıların tooautomatically get açan tooIgloo yazılım (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4d3e4-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d3e4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4d3e4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4d3e4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d3e4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d3e4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4d3e4-110">Prerequisites</span></span>

<span data-ttu-id="4d3e4-111">tooconfigure Igloo yazılım ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="4d3e4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4d3e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d3e4-113">Bir Igloo yazılım çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="4d3e4-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d3e4-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d3e4-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d3e4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d3e4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d3e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d3e4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4d3e4-118">Scenario description</span></span>
<span data-ttu-id="4d3e4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d3e4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d3e4-121">Merhaba Galerisi'nden Igloo yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="4d3e4-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="4d3e4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4d3e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="4d3e4-123">Merhaba Galerisi'nden Igloo yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="4d3e4-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="4d3e4-124">Azure AD'ye tooconfigure hello tümleştirme Igloo yazılım tooadd Igloo yazılım hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d3e4-125">**tooadd Igloo yazılım hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d3e4-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d3e4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d3e4-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d3e4-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4d3e4-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4d3e4-133">Merhaba arama kutusuna yazın **Igloo yazılım**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-133">In hello search box, type **Igloo Software**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="4d3e4-135">Merhaba Sonuçlar panelinde seçin **Igloo yazılım**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d3e4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4d3e4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d3e4-138">Bu bölümde, yapılandırmak ve Igloo yazılım "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d3e4-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Igloo yazılım tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="4d3e4-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Igloo yazılım hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="4d3e4-141">Merhaba hello değeri Igloo yazılımda atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d3e4-142">tooconfigure ve Igloo yazılım ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d3e4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d3e4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d3e4-145">**[Bir Igloo yazılım test kullanıcısı oluşturma](#creating-an-igloo-software-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Igloo yazılım, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d3e4-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d3e4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d3e4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4d3e4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d3e4-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Igloo yazılım uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="4d3e4-150">**tooconfigure Azure AD çoklu oturum açma Igloo yazılımıyla hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d3e4-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d3e4-151">Hello hello üzerinde Azure portal'ın **Igloo yazılım** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4d3e4-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="4d3e4-155">Merhaba üzerinde **Igloo yazılım etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="4d3e4-157">a.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-157">a.</span></span> <span data-ttu-id="4d3e4-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="4d3e4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="4d3e4-159">b.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-159">b.</span></span> <span data-ttu-id="4d3e4-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="4d3e4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="4d3e4-161">c.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-161">c.</span></span> <span data-ttu-id="4d3e4-162">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="4d3e4-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d3e4-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-163">These values are not real.</span></span> <span data-ttu-id="4d3e4-164">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4d3e4-165">Kişi [Igloo yazılım istemci destek ekibi](https://www.igloosoftware.com/services/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="4d3e4-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="4d3e4-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4d3e4-170">Merhaba üzerinde **Igloo yazılım yapılandırma** 'yi tıklatın **Igloo yazılımı Yapılandır** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4d3e4-171">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="4d3e4-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="4d3e4-173">Farklı web tarayıcısı penceresinde tooyour Igloo yazılım şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="4d3e4-174">Toohello Git **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="4d3e4-175">![Denetim Masası](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Denetim Masası")</span><span class="sxs-lookup"><span data-stu-id="4d3e4-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="4d3e4-176">Merhaba, **üyelik** sekmesini tıklatın, **ayarları oturum**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="4d3e4-177">![Ayarları'nda oturum](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Ayarları'nda oturum açın")</span><span class="sxs-lookup"><span data-stu-id="4d3e4-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="4d3e4-178">Hello SAML yapılandırma bölümü, tıklatın **SAML kimlik doğrulaması yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="4d3e4-179">![SAML Yapılandırması](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="4d3e4-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="4d3e4-180">Merhaba, **genel yapılandırma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4d3e4-181">![Genel yapılandırma](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "genel yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="4d3e4-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="4d3e4-182">a.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-182">a.</span></span> <span data-ttu-id="4d3e4-183">Merhaba, **bağlantı adı** metin kutusuna, yapılandırmanız için özel bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="4d3e4-184">b.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-184">b.</span></span> <span data-ttu-id="4d3e4-185">Merhaba, **IDP oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4d3e4-186">c.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-186">c.</span></span> <span data-ttu-id="4d3e4-187">Merhaba, **IDP oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4d3e4-188">d.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-188">d.</span></span> <span data-ttu-id="4d3e4-189">Seçin **oturum kapatma yanıt ve İstek HTTP türü** olarak **POST**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="4d3e4-190">e.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-190">e.</span></span> <span data-ttu-id="4d3e4-191">Açık, **base-64** kodlanmış sertifika Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde ve toohello yapıştırın **ortak sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="4d3e4-192">Merhaba, **yanıt ve kimlik doğrulama Yapılandırması**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="4d3e4-193">![Yanıt ve kimlik doğrulama Yapılandırması](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "yanıt ve kimlik doğrulama yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="4d3e4-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="4d3e4-194">a.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-194">a.</span></span> <span data-ttu-id="4d3e4-195">Olarak **kimlik sağlayıcısı**seçin **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="4d3e4-196">b.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-196">b.</span></span> <span data-ttu-id="4d3e4-197">Olarak **tanımlayıcı türü**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="4d3e4-198">c.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-198">c.</span></span> <span data-ttu-id="4d3e4-199">Merhaba, **e-posta özniteliği** metin kutusuna, türü **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="4d3e4-200">d.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-200">d.</span></span> <span data-ttu-id="4d3e4-201">Merhaba, **ad özniteliği** metin kutusuna, türü **givenname**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="4d3e4-202">e.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-202">e.</span></span> <span data-ttu-id="4d3e4-203">Merhaba, **son Name özniteliği** metin kutusuna, türü **Soyadı**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="4d3e4-204">Aşağıdaki adımları toocomplete hello yapılandırma hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="4d3e4-205">![Oturum açma kullanıcı oluşturma](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "oturum açma kullanıcı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="4d3e4-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="4d3e4-206">a.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-206">a.</span></span> <span data-ttu-id="4d3e4-207">Olarak **oturum açma kullanıcı oluşturma**seçin **yeni bir kullanıcı oturum sitenizdeki oluşturduğunuzda**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="4d3e4-208">b.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-208">b.</span></span> <span data-ttu-id="4d3e4-209">Olarak **ayarlarında oturum**seçin **"Oturum" ekranında kullanım SAML düğmesini**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="4d3e4-210">c.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-210">c.</span></span> <span data-ttu-id="4d3e4-211">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4d3e4-212">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4d3e4-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d3e4-213">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d3e4-214">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d3e4-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d3e4-215">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d3e4-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d3e4-216">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4d3e4-218">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d3e4-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d3e4-219">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d3e4-221">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d3e4-223">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d3e4-225">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4d3e4-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d3e4-227">a.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-227">a.</span></span> <span data-ttu-id="4d3e4-228">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d3e4-229">b.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-229">b.</span></span> <span data-ttu-id="4d3e4-230">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d3e4-231">c.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-231">c.</span></span> <span data-ttu-id="4d3e4-232">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4d3e4-233">d.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-233">d.</span></span> <span data-ttu-id="4d3e4-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="4d3e4-235">Bir Igloo yazılım test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d3e4-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="4d3e4-236">TooIgloo yazılım sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="4d3e4-237">Yazılım tooIgloo kullanarak bir atanan kullanıcı çalıştığında toolog hello erişim paneli, Igloo yazılım hello kullanıcı var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="4d3e4-238">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Igloo yazılım tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4d3e4-239">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4d3e4-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4d3e4-240">Bu bölümde, erişim tooIgloo yazılım vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4d3e4-242">**tooassign Britta Simon tooIgloo yazılım, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4d3e4-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d3e4-243">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4d3e4-245">Merhaba uygulamalar listesinde **Igloo yazılım**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="4d3e4-247">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4d3e4-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-249">Click **Add** button.</span></span> <span data-ttu-id="4d3e4-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4d3e4-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d3e4-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d3e4-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d3e4-255">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4d3e4-255">Testing single sign-on</span></span>

<span data-ttu-id="4d3e4-256">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4d3e4-257">Merhaba Igloo yazılım hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Igloo yazılım uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d3e4-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="4d3e4-258">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d3e4-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d3e4-259">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4d3e4-259">Additional resources</span></span>

* [<span data-ttu-id="4d3e4-260">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="4d3e4-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d3e4-261">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4d3e4-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

