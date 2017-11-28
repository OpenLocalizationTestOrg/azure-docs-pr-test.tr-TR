---
title: "Öğretici: Azure Active Directory Tümleştirme ile Workday | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile iş günü arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="86159-103">Öğretici: Azure Active Directory Tümleştirme ile iş günü</span><span class="sxs-lookup"><span data-stu-id="86159-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="86159-104">Bu öğreticide, bilgi nasıl toointegrate Workday Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86159-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86159-105">Workday Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="86159-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86159-106">Erişim tooWorkday sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="86159-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="86159-107">Kullanıcıların tooautomatically get açan tooWorkday (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="86159-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86159-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="86159-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86159-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86159-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86159-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="86159-110">Prerequisites</span></span>

<span data-ttu-id="86159-111">tooconfigure Workday ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="86159-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="86159-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="86159-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86159-113">Bir iş günü çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="86159-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86159-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="86159-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86159-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="86159-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86159-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="86159-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86159-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86159-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86159-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="86159-118">Scenario description</span></span>
<span data-ttu-id="86159-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="86159-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86159-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="86159-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86159-121">Workday hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="86159-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="86159-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="86159-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="86159-123">Workday hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="86159-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="86159-124">Azure AD'ye tooconfigure hello tümleştirme gününün hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd Workday gerekir.</span><span class="sxs-lookup"><span data-stu-id="86159-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86159-125">**tooadd Workday hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86159-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86159-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="86159-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86159-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="86159-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86159-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="86159-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="86159-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86159-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="86159-133">Merhaba arama kutusuna yazın **Workday**.</span><span class="sxs-lookup"><span data-stu-id="86159-133">In hello search box, type **Workday**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="86159-135">Merhaba Sonuçlar panelinde seçin **Workday**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="86159-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86159-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="86159-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86159-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Workday ile test etme</span><span class="sxs-lookup"><span data-stu-id="86159-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86159-139">Tek toowork'ın oturum açma hangi hello karşılık gelen iş günü içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="86159-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="86159-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve iş günü içinde hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="86159-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="86159-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** iş günü içinde.</span><span class="sxs-lookup"><span data-stu-id="86159-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="86159-142">tooconfigure ve Workday ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="86159-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86159-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="86159-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86159-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="86159-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86159-145">**[Bir iş günü test kullanıcısı oluşturma](#creating-a-workday-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir iş günü içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="86159-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86159-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="86159-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86159-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="86159-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86159-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="86159-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86159-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Workday uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="86159-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="86159-150">**tooconfigure Azure AD çoklu oturum açma ile iş günü, başlangıç aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86159-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="86159-151">Merhaba hello üzerinde Azure portal'ın **Workday** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="86159-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="86159-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="86159-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="86159-155">Merhaba üzerinde **Workday etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="86159-157">a.</span><span class="sxs-lookup"><span data-stu-id="86159-157">a.</span></span> <span data-ttu-id="86159-158">Merhaba, **oturum açma URL'si** metin kutusuna, türü hello değeri olarak:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="86159-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="86159-159">b.</span><span class="sxs-lookup"><span data-stu-id="86159-159">b.</span></span> <span data-ttu-id="86159-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="86159-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86159-161">Bu değerler hello gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="86159-161">These values are not hello real.</span></span> <span data-ttu-id="86159-162">Bu değerler, oturum açma hello gerçek URL'si ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="86159-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="86159-163">Yanıt URL'si bir alt etki alanı gibi olmalıdır: www, wd2, wd3, wd3 impl, wd5, wd5 impl).</span><span class="sxs-lookup"><span data-stu-id="86159-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="86159-164">Aşağıdakine benzer kullanarak "*http://www.myworkday.com*" çalışır, ancak "*http://myworkday.com*" desteklemez.</span><span class="sxs-lookup"><span data-stu-id="86159-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="86159-165">Kişi [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="86159-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="86159-166">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="86159-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="86159-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86159-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86159-170">Merhaba üzerinde **Workday yapılandırma** 'yi tıklatın **yapılandırma Workday** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="86159-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="86159-171">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="86159-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="86159-172">![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="86159-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="86159-173">Farklı web tarayıcısı penceresinde tooyour Workday şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="86159-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="86159-174">Çok Git**menü \> çalışma ekranı**.</span><span class="sxs-lookup"><span data-stu-id="86159-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="86159-175">![Çalışma ekranı](./media/active-directory-saas-workday-tutorial/IC782923.png "çalışma ekranı")</span><span class="sxs-lookup"><span data-stu-id="86159-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="86159-176">Çok Git**hesap yönetimini**.</span><span class="sxs-lookup"><span data-stu-id="86159-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="86159-177">![Hesap Yönetimi](./media/active-directory-saas-workday-tutorial/IC782924.png "hesap yönetimi")</span><span class="sxs-lookup"><span data-stu-id="86159-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="86159-178">Çok Git**Kiracı kurulumunu Düzenle – güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="86159-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="86159-179">![Kiracı Güvenliği Düzenle](./media/active-directory-saas-workday-tutorial/IC782925.png "Kiracı güvenlik Düzenle")</span><span class="sxs-lookup"><span data-stu-id="86159-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="86159-180">Merhaba, **yönlendirme URL'lerini** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="86159-181">![Yönlendirme URL'lerini](./media/active-directory-saas-workday-tutorial/IC7829581.png "yeniden yönlendirme URL'leri")</span><span class="sxs-lookup"><span data-stu-id="86159-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="86159-182">a.</span><span class="sxs-lookup"><span data-stu-id="86159-182">a.</span></span> <span data-ttu-id="86159-183">Tıklatın **Satır Ekle**.</span><span class="sxs-lookup"><span data-stu-id="86159-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="86159-184">b.</span><span class="sxs-lookup"><span data-stu-id="86159-184">b.</span></span> <span data-ttu-id="86159-185">Merhaba, **oturum açma yeniden yönlendirme URL'si** textbox ve hello **mobil yeniden yönlendirme URL'sini** metin kutusuna, türü hello **oturum açma URL'si** üzerinde hello girdiğiniz **Workday etki alanı ve URL'leri** hello Azure portalı bölümü.</span><span class="sxs-lookup"><span data-stu-id="86159-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="86159-186">c.</span><span class="sxs-lookup"><span data-stu-id="86159-186">c.</span></span> <span data-ttu-id="86159-187">Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **Sign-Out URL**ve hello yapıştırma **oturumu kapatıp tekrar yönlendirme URL'sini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="86159-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="86159-188">d.</span><span class="sxs-lookup"><span data-stu-id="86159-188">d.</span></span>  <span data-ttu-id="86159-189">İçinde **ortam** metin kutusuna, türü hello ortam adı.</span><span class="sxs-lookup"><span data-stu-id="86159-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="86159-190">Merhaba hello ortamı özniteliğinin değeri bağlı hello Kiracı URL toohello değeri:</span><span class="sxs-lookup"><span data-stu-id="86159-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="86159-191">-Hello Workday kiracısı URL'si hello etki alanı adı ile impl örneğin başlayıp başlamadığını: *https://impl.workday.com/\<Kiracı\>/login-saml2.htmld*), hello **ortam** öznitelik tooImplementation ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86159-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="86159-192">-Hello etki alanı adı başka bir şey ile başlayan, toocontact gerekir [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello eşleşen **ortam** değeri.</span><span class="sxs-lookup"><span data-stu-id="86159-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="86159-193">Merhaba, **SAML Kurulumu** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="86159-194">![SAML Kurulumu](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="86159-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="86159-195">a.</span><span class="sxs-lookup"><span data-stu-id="86159-195">a.</span></span>  <span data-ttu-id="86159-196">Seçin **SAML kimlik doğrulamasını etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="86159-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="86159-197">b.</span><span class="sxs-lookup"><span data-stu-id="86159-197">b.</span></span>  <span data-ttu-id="86159-198">Tıklatın **Satır Ekle**.</span><span class="sxs-lookup"><span data-stu-id="86159-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="86159-199">Hello SAML kimlik sağlayıcısı bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="86159-200">![SAML kimlik sağlayıcısı](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML kimlik sağlayıcısı")</span><span class="sxs-lookup"><span data-stu-id="86159-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="86159-201">a.</span><span class="sxs-lookup"><span data-stu-id="86159-201">a.</span></span> <span data-ttu-id="86159-202">Merhaba kimlik sağlayıcı adı metin kutusuna bir sağlayıcı adı yazın (örneğin: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="86159-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="86159-203">b.</span><span class="sxs-lookup"><span data-stu-id="86159-203">b.</span></span> <span data-ttu-id="86159-204">Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **SAML varlık kimliği** değer ve hello yapıştırma **veren** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="86159-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="86159-205">c.</span><span class="sxs-lookup"><span data-stu-id="86159-205">c.</span></span> <span data-ttu-id="86159-206">Seçin **etkinleştirmek iş günü başlatılan oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="86159-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="86159-207">d.</span><span class="sxs-lookup"><span data-stu-id="86159-207">d.</span></span> <span data-ttu-id="86159-208">Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **Sign-Out URL** değer ve hello yapıştırma **oturum kapatma istek URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="86159-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="86159-209">e.</span><span class="sxs-lookup"><span data-stu-id="86159-209">e.</span></span> <span data-ttu-id="86159-210">Tıklatın **kimlik sağlayıcısı ortak anahtar sertifikası**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="86159-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="86159-211">![Oluşturma](./media/active-directory-saas-workday-tutorial/IC782928.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="86159-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="86159-212">f.</span><span class="sxs-lookup"><span data-stu-id="86159-212">f.</span></span> <span data-ttu-id="86159-213">Tıklatın **x509 oluşturma ortak anahtar**.</span><span class="sxs-lookup"><span data-stu-id="86159-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="86159-214">![Oluşturma](./media/active-directory-saas-workday-tutorial/IC782929.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="86159-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="86159-215">Merhaba, **görünüm x509 ortak anahtar** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="86159-216">![Görünüm x509 ortak anahtar](./media/active-directory-saas-workday-tutorial/IC782930.png "görünüm x509 ortak anahtar")</span><span class="sxs-lookup"><span data-stu-id="86159-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="86159-217">a.</span><span class="sxs-lookup"><span data-stu-id="86159-217">a.</span></span> <span data-ttu-id="86159-218">Merhaba, **adı** metin kutusuna, sertifikanızı için bir ad yazın (örneğin: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="86159-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="86159-219">b.</span><span class="sxs-lookup"><span data-stu-id="86159-219">b.</span></span> <span data-ttu-id="86159-220">Merhaba, **geçerlilik başlangıcı** metin kutusuna, türü hello sertifikanızı öznitelik değerinden geçerli.</span><span class="sxs-lookup"><span data-stu-id="86159-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="86159-221">c.</span><span class="sxs-lookup"><span data-stu-id="86159-221">c.</span></span>  <span data-ttu-id="86159-222">Merhaba, **için geçerli** metin kutusuna, sertifikanızı tür hello geçerli tooattribute değeri.</span><span class="sxs-lookup"><span data-stu-id="86159-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="86159-223">Merhaba tarihinden itibaren geçerli alın ve çift tıklatarak indirilen hello sertifikasından geçerli toodate hello.</span><span class="sxs-lookup"><span data-stu-id="86159-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="86159-224">Merhaba tarihleri hello altında listelenen **ayrıntıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="86159-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="86159-225">d.</span><span class="sxs-lookup"><span data-stu-id="86159-225">d.</span></span>  <span data-ttu-id="86159-226">Base-64 kodlanmış sertifikanızı not defteri sonra bunu içerik kopyalama hello açın.</span><span class="sxs-lookup"><span data-stu-id="86159-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="86159-227">e.</span><span class="sxs-lookup"><span data-stu-id="86159-227">e.</span></span>  <span data-ttu-id="86159-228">Merhaba, **sertifika** metin kutusuna, panonuza Yapıştır Merhaba içeriğine.</span><span class="sxs-lookup"><span data-stu-id="86159-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="86159-229">f.</span><span class="sxs-lookup"><span data-stu-id="86159-229">f.</span></span>  <span data-ttu-id="86159-230">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="86159-230">Click **OK**.</span></span>

15. <span data-ttu-id="86159-231">Merhaba aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="86159-232">![SSO yapılandırma](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="86159-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="86159-233">a.</span><span class="sxs-lookup"><span data-stu-id="86159-233">a.</span></span>  <span data-ttu-id="86159-234">Merhaba etkinleştirmek **x509 özel anahtar çifti**.</span><span class="sxs-lookup"><span data-stu-id="86159-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="86159-235">b.</span><span class="sxs-lookup"><span data-stu-id="86159-235">b.</span></span>  <span data-ttu-id="86159-236">Merhaba, **hizmet sağlayıcı kimliği** metin kutusuna, türü **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="86159-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="86159-237">c.</span><span class="sxs-lookup"><span data-stu-id="86159-237">c.</span></span>  <span data-ttu-id="86159-238">Seçin **etkinleştir SP tarafından başlatılan SAML kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="86159-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="86159-239">d.</span><span class="sxs-lookup"><span data-stu-id="86159-239">d.</span></span>  <span data-ttu-id="86159-240">Merhaba hello üzerinde Azure portal'ın **yapılandırma oturum açma** penceresinde, kopyalama hello **SAML çoklu oturum açma hizmet URL'si** değer ve hello yapıştırma **IDP SSO hizmet URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="86159-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="86159-241">e.</span><span class="sxs-lookup"><span data-stu-id="86159-241">e.</span></span> <span data-ttu-id="86159-242">Seçin **SP tarafından başlatılan kimlik doğrulama isteği Deflate değil**.</span><span class="sxs-lookup"><span data-stu-id="86159-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="86159-243">f.</span><span class="sxs-lookup"><span data-stu-id="86159-243">f.</span></span> <span data-ttu-id="86159-244">Olarak **kimlik doğrulama isteği imza yöntemi**seçin **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="86159-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="86159-245">![Kimlik doğrulama isteği imza yöntemi](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "kimlik doğrulama isteği imza yöntemi")</span><span class="sxs-lookup"><span data-stu-id="86159-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="86159-246">g.</span><span class="sxs-lookup"><span data-stu-id="86159-246">g.</span></span> <span data-ttu-id="86159-247">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="86159-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="86159-248">![TAMAM](./media/active-directory-saas-workday-tutorial/IC782933.png "TAMAM")
<CE></span><span class="sxs-lookup"><span data-stu-id="86159-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="86159-249">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="86159-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86159-250">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="86159-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86159-251">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86159-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86159-252">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="86159-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="86159-253">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="86159-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="86159-255">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86159-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86159-256">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="86159-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86159-258">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="86159-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86159-260">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="86159-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86159-262">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="86159-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86159-264">a.</span><span class="sxs-lookup"><span data-stu-id="86159-264">a.</span></span> <span data-ttu-id="86159-265">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86159-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86159-266">b.</span><span class="sxs-lookup"><span data-stu-id="86159-266">b.</span></span> <span data-ttu-id="86159-267">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="86159-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86159-268">c.</span><span class="sxs-lookup"><span data-stu-id="86159-268">c.</span></span> <span data-ttu-id="86159-269">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="86159-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86159-270">d.</span><span class="sxs-lookup"><span data-stu-id="86159-270">d.</span></span> <span data-ttu-id="86159-271">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="86159-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="86159-272">Bir iş günü test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="86159-272">Creating a Workday test user</span></span>

<span data-ttu-id="86159-273">tooget iş günü içinde sağlanan bir sınama kullanıcısı, gereksinim duyduğunuz toocontact hello [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="86159-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="86159-274">Merhaba [Workday istemci destek ekibi](https://www.workday.com/en-us/partners-services/services/support.html) hello kullanıcı sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86159-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86159-275">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="86159-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86159-276">Bu bölümde, erişim tooWorkday vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="86159-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="86159-278">**tooassign Britta Simon tooWorkday hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="86159-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="86159-279">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="86159-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="86159-281">Merhaba uygulamalar listesinde **Workday**.</span><span class="sxs-lookup"><span data-stu-id="86159-281">In hello applications list, select **Workday**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="86159-283">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="86159-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="86159-285">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="86159-285">Click **Add** button.</span></span> <span data-ttu-id="86159-286">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="86159-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="86159-288">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="86159-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86159-289">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="86159-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86159-290">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="86159-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86159-291">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="86159-291">Testing single sign-on</span></span>

<span data-ttu-id="86159-292">Çoklu oturum açma ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="86159-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="86159-293">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86159-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86159-294">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="86159-294">Additional resources</span></span>

* [<span data-ttu-id="86159-295">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="86159-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86159-296">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="86159-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="86159-297">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="86159-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

