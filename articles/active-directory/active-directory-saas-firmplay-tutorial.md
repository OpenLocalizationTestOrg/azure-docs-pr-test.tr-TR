---
title: "Öğretici: Azure Active Directory Tümleştirme FirmPlay - işe alma için çalışan hakları ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile FirmPlay - işe alma için çalışan hakları arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="1d8da-103">Öğretici: Azure Active Directory Tümleştirme ile FirmPlay - işe alma için çalışan hakları</span><span class="sxs-lookup"><span data-stu-id="1d8da-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="1d8da-104">Bu öğreticide, bilgi nasıl toointegrate FirmPlay - işe alma Azure Active Directory (Azure AD) ile çalışan hakları.</span><span class="sxs-lookup"><span data-stu-id="1d8da-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d8da-105">FirmPlay - Azure AD ile işe alma için çalışan hakları tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1d8da-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1d8da-106">İşe alma için çalışan hakları erişim tooFirmPlay - olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1d8da-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="1d8da-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooFirmPlay - işe alma (çoklu oturum açma) için çalışan hakları etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1d8da-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d8da-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1d8da-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="1d8da-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d8da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d8da-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1d8da-110">Prerequisites</span></span>

<span data-ttu-id="1d8da-111">tooconfigure FirmPlay - işe alma, çalışan hakları ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d8da-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="1d8da-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1d8da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d8da-113">FirmPlay - çoklu oturum açma etkin abonelik işe alma için çalışan hakları</span><span class="sxs-lookup"><span data-stu-id="1d8da-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="1d8da-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1d8da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1d8da-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d8da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d8da-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d8da-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1d8da-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d8da-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1d8da-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1d8da-118">Scenario description</span></span>
<span data-ttu-id="1d8da-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1d8da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d8da-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1d8da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d8da-121">İşe alma hello galerisinden çalışan hakları FirmPlay - ekleme</span><span class="sxs-lookup"><span data-stu-id="1d8da-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="1d8da-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1d8da-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="1d8da-123">İşe alma hello galerisinden çalışan hakları FirmPlay - ekleme</span><span class="sxs-lookup"><span data-stu-id="1d8da-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="1d8da-124">tooconfigure hello FirmPlay - Azure AD'ye işe alma için çalışan hakları tümleştirilmesi tooadd FirmPlay - işe alma hello galeri tooyour listesinden yönetilen SaaS uygulamaları için çalışan hakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d8da-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1d8da-125">**tooadd FirmPlay - işe alma hello galerisinden çalışan hakları hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1d8da-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d8da-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d8da-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1d8da-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1d8da-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1d8da-133">Merhaba arama kutusuna yazın **FirmPlay - işe alma için çalışan hakları**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="1d8da-135">Merhaba Sonuçlar panelinde seçin **FirmPlay - işe alma için çalışan hakları**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="1d8da-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d8da-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1d8da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d8da-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma FirmPlay - işe alma "Britta Simon" adlı bir test kullanıcıyı temel alarak çalışan hakları ile test etme.</span><span class="sxs-lookup"><span data-stu-id="1d8da-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d8da-139">Tek toowork'ın oturum açma, Azure AD'de FirmPlay - çalışan hakları işe alma için hangi hello karşılık gelen kullanıcı tooa kullanıcıdır tooknow Azure AD gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="1d8da-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="1d8da-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve FirmPlay - çalışan hakları işe alma için ilgili kullanıcı hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d8da-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="1d8da-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** FirmPlay - işe alma için çalışan hakları içinde.</span><span class="sxs-lookup"><span data-stu-id="1d8da-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="1d8da-142">tooconfigure ve Azure AD çoklu oturum açmayı test FirmPlay - işe alma, çalışan hakları ile yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d8da-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1d8da-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="1d8da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1d8da-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="1d8da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d8da-145">**[İşe alma test kullanıcısı için çalışan hakları FirmPlay - oluşturma](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave Britta Simon FirmPlay içinde karşılık gelen: çalışan başka bir deyişle işe alma için hakları bağlı her toohello Azure AD gösterimi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1d8da-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1d8da-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d8da-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="1d8da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d8da-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1d8da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d8da-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma FirmPlay - çalışan hakları işe alma uygulaması için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1d8da-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="1d8da-150">**Azure AD çoklu oturum açma tooconfigure FirmPlay - işe alma, çalışan hakları ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1d8da-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d8da-151">Hello üzerinde hello Azure Yönetim Portalı'nda **FirmPlay - çalışan hakları işe alma için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1d8da-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="1d8da-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="1d8da-155">Merhaba üzerinde **FirmPlay - işe alma etki alanı ve URL'ler için çalışan hakları** bölümünde hello **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="1d8da-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="1d8da-157">Lütfen bu hello gerçek değer olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1d8da-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="1d8da-158">Bu değeri hello gerçek ile oturum URL'yi tooupdate sahip.</span><span class="sxs-lookup"><span data-stu-id="1d8da-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="1d8da-159">Kişi [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="1d8da-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="1d8da-160">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="1d8da-162">Merhaba üzerinde **yeni sertifika oluştur** iletişim kutusunda, hello Takvim simgesine tıklayın ve bir **sona erme tarihi**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="1d8da-163">Ardından **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-163">Then click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="1d8da-165">Merhaba üzerinde **SAML imzalama sertifikası** bölümünde, select **yeni sertifika etkin hale getirin** tıklatıp **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="1d8da-167">Merhaba açılır pencere üzerinde **geçiş sertifikası** penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1d8da-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1d8da-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="1d8da-171">Merhaba üzerinde **FirmPlay - işe alma yapılandırması için çalışan hakları** 'yi tıklatın **FirmPlay - çalışan hakları işe alma için yapılandırma** tooopen **oturum açmaYapılandırma**iletişim.</span><span class="sxs-lookup"><span data-stu-id="1d8da-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="1d8da-174">tooget SSO yapılandırılmış uygulamanızın, kişi [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) ve ile Merhaba aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="1d8da-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="1d8da-175">• hello indirilen **sertifika dosyası**</span><span class="sxs-lookup"><span data-stu-id="1d8da-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="1d8da-176">• hello **SAML çoklu oturum açma hizmet URL'si**</span><span class="sxs-lookup"><span data-stu-id="1d8da-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="1d8da-177">• hello **SAML varlık kimliği**</span><span class="sxs-lookup"><span data-stu-id="1d8da-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="1d8da-178">• hello **Sign-Out URL'si**</span><span class="sxs-lookup"><span data-stu-id="1d8da-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d8da-179">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d8da-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d8da-180">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="1d8da-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1d8da-182">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1d8da-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d8da-183">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d8da-185">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d8da-187">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1d8da-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d8da-189">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1d8da-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d8da-191">a.</span><span class="sxs-lookup"><span data-stu-id="1d8da-191">a.</span></span> <span data-ttu-id="1d8da-192">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d8da-193">b.</span><span class="sxs-lookup"><span data-stu-id="1d8da-193">b.</span></span> <span data-ttu-id="1d8da-194">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1d8da-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d8da-195">c.</span><span class="sxs-lookup"><span data-stu-id="1d8da-195">c.</span></span> <span data-ttu-id="1d8da-196">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1d8da-197">d.</span><span class="sxs-lookup"><span data-stu-id="1d8da-197">d.</span></span> <span data-ttu-id="1d8da-198">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1d8da-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="1d8da-199">İşe alma test kullanıcısı için çalışan hakları FirmPlay - oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d8da-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="1d8da-200">Bu bölümde, Britta Simon FirmPlay - işe alma için çalışan hakları adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d8da-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="1d8da-201">Lütfen çalışmak [FirmPlay - işe alma destek ekibi için çalışan hakları](mailto:engineering@firmplay.com) tooadd hello kullanıcılar hello FirmPlay - işe alma platform için çalışan hakları.</span><span class="sxs-lookup"><span data-stu-id="1d8da-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1d8da-202">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1d8da-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1d8da-203">Bu bölümde, kendi erişim tooFirmPlay - işe alma için çalışan hakları vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d8da-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1d8da-205">**tooassign Britta Simon tooFirmPlay - işe alma, çalışan hakları hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1d8da-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d8da-206">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1d8da-208">Merhaba uygulamalar listesinde **FirmPlay - işe alma için çalışan hakları**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="1d8da-210">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1d8da-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1d8da-212">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1d8da-212">Click **Add** button.</span></span> <span data-ttu-id="1d8da-213">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1d8da-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1d8da-215">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1d8da-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1d8da-216">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1d8da-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d8da-217">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1d8da-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="1d8da-218">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1d8da-218">Testing single sign-on</span></span>

<span data-ttu-id="1d8da-219">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1d8da-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1d8da-220">Merhaba FirmPlay - hello erişim paneli, işe alma parçasında çalışan hakları tıkladığınızda otomatik olarak oturum açma tooyour FirmPlay - işe alma uygulaması için çalışan hakları almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1d8da-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1d8da-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1d8da-221">Additional resources</span></span>

* [<span data-ttu-id="1d8da-222">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="1d8da-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d8da-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1d8da-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png