---
title: "Öğretici: Azure Active Directory Tümleştirme LinkedIn yükseltmesine ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory arasındaki LinkedIn Yükselt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="18637-103">Öğretici: Azure Active Directory Tümleştirme LinkedIn yükseltmesine ile</span><span class="sxs-lookup"><span data-stu-id="18637-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="18637-104">Bu öğreticide, bilgi toointegrate LinkedIn yükseltmesine nasıl Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="18637-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18637-105">LinkedIn yükseltmesine Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="18637-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18637-106">Erişim tooLinkedIn yükseltme sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="18637-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="18637-107">Kullanıcıların tooautomatically get açan tooLinkedIn yükseltme (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="18637-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18637-108">Bir merkezi konumda - hello Azure Yönetim Portalı hesaplarınızı yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="18637-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="18637-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18637-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18637-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="18637-110">Prerequisites</span></span>

<span data-ttu-id="18637-111">tooconfigure LinkedIn yükseltmesine ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="18637-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="18637-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="18637-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18637-113">Bir LinkedIn yükseltmesine çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="18637-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18637-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="18637-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18637-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="18637-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18637-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18637-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="18637-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18637-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18637-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="18637-118">Scenario description</span></span>
<span data-ttu-id="18637-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="18637-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18637-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="18637-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18637-121">LinkedIn yükseltmesine hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="18637-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="18637-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="18637-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="18637-123">LinkedIn yükseltmesine hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="18637-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="18637-124">Azure AD'ye tooconfigure hello tümleştirme LinkedIn yükseltmesine, tooadd LinkedIn yükseltmesine hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="18637-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18637-125">**tooadd LinkedIn yükseltmesine hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18637-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18637-126">Merhaba,  **[Azure Yönetim Portalı](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="18637-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18637-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="18637-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18637-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="18637-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="18637-131">Tıklatın **Ekle** hello iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18637-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="18637-133">Merhaba arama kutusuna yazın **LinkedIn yükseltmesine**.</span><span class="sxs-lookup"><span data-stu-id="18637-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="18637-134">Sonuçları panelinden tıklatın **LinkedIn yükseltmesine** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="18637-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18637-136">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="18637-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18637-137">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı LinkedIn yükseltmesine ile test etme.</span><span class="sxs-lookup"><span data-stu-id="18637-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18637-138">Tek toowork'ın oturum açma hangi hello karşılık gelen LinkedIn yükseltmesine de tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="18637-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="18637-139">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı LinkedIn yükseltmesine arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="18637-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="18637-140">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcı adı** LinkedIn yükseltmesine içinde.</span><span class="sxs-lookup"><span data-stu-id="18637-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="18637-141">tooconfigure ve LinkedIn yükseltmesine ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="18637-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18637-142">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="18637-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18637-143">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="18637-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18637-144">**[Bir LinkedIn yükseltmesine test kullanıcısı oluşturma](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="18637-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="18637-145">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="18637-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18637-146">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="18637-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18637-147">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="18637-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18637-148">Bu bölümde, Azure AD çoklu oturum açma hello Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma LinkedIn yükseltmesine uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="18637-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="18637-149">**tooconfigure Azure AD çoklu oturum açma LinkedIn yükseltmesine ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18637-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="18637-150">Merhaba üzerinde hello Azure Yönetim Portalı'nda **LinkedIn yükseltmesine** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="18637-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="18637-152">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="18637-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="18637-154">Bir farklı web tarayıcısı penceresinde, bir yönetici olarak oturum açma tooyour LinkedIn yükseltmesine Kiracı.</span><span class="sxs-lookup"><span data-stu-id="18637-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="18637-155">İçinde **hesap Merkezi'nde**, tıklatın **genel ayarları** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="18637-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="18637-156">Ayrıca, seçin **yükseltme - AAD Test yükseltmesine** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="18637-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="18637-158">Tıklayın **veya burayı tıklatın tooload ve kopyalama tek tek alanların hello formundan** kopyalayıp **varlık kimliği** ve **onaylama tüketici erişim (ACS) URL'si**</span><span class="sxs-lookup"><span data-stu-id="18637-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="18637-160">Azure Portal'da altında **LinkedIn yükseltme etki alanı ve URL'leri**, hello tooconfigure SSO istiyorsanız aşağıdaki adımları gerçekleştirin içinde **IDP başlatılan** modu</span><span class="sxs-lookup"><span data-stu-id="18637-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="18637-162">a.</span><span class="sxs-lookup"><span data-stu-id="18637-162">a.</span></span> <span data-ttu-id="18637-163">Merhaba, **tanımlayıcısı** metin kutusuna, hello girin **varlık kimliği** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="18637-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="18637-164">b.</span><span class="sxs-lookup"><span data-stu-id="18637-164">b.</span></span> <span data-ttu-id="18637-165">Merhaba, **yanıt URL'si** metin kutusuna, hello girin **onaylama tüketici erişim (ACS) Url** LinkedIn portalından kopyalandığından</span><span class="sxs-lookup"><span data-stu-id="18637-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="18637-166">Tooconfigure SSO istiyorsanız içinde **SP tarafından başlatılan**, sonra hello yapılandırma bölümündeki Gelişmiş URL Göster ayarı seçeneğini tıklatın ve hello oturum URL deseni takip hello ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="18637-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="18637-168">LinkedIn yükseltmesine uygulamanızı hello SAML onaylar, tooadd özel öznitelik eşlemelerini tooyour SAML belirteci öznitelikleri yapılandırma gerektiren belirli bir biçimde, bekliyor.</span><span class="sxs-lookup"><span data-stu-id="18637-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="18637-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="18637-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="18637-170">Merhaba varsayılan değerini **kullanıcı tanımlayıcısı** olan **user.userprincipalname** ancak LinkedIn yükseltmesine hello kullanıcının e-posta adresiyle eşleşen bu toobe bekliyor.</span><span class="sxs-lookup"><span data-stu-id="18637-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="18637-171">Bunun için kullanabileceğiniz **user.mail** özniteliği hello listeden veya kuruluş yapılandırmanızı temel alarak hello uygun öznitelik değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="18637-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="18637-173">İçinde **kullanıcı öznitelikleri** 'yi tıklatın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** ve hello özniteliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="18637-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="18637-174">Adlı başka bir talep tooadd gerek **departmanı** ve hello değeri gereken çok eşlenen toobe**user.department**.</span><span class="sxs-lookup"><span data-stu-id="18637-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="18637-175">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="18637-175">Attribute Name</span></span> | <span data-ttu-id="18637-176">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="18637-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="18637-177">Bölüm</span><span class="sxs-lookup"><span data-stu-id="18637-177">department</span></span>| <span data-ttu-id="18637-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="18637-178">user.department</span></span> |

      ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="18637-180">a.</span><span class="sxs-lookup"><span data-stu-id="18637-180">a.</span></span> <span data-ttu-id="18637-181">Aşağıdaki - gösterildiği gibi hello departmanı özniteliği Ekle'ye tıklayın Ekle özniteliği tooopen hello özniteliği ayrıntılar sayfası</span><span class="sxs-lookup"><span data-stu-id="18637-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="18637-183">b.</span><span class="sxs-lookup"><span data-stu-id="18637-183">b.</span></span> <span data-ttu-id="18637-184">Tıklayın **Tamam** toosave hello özniteliği.</span><span class="sxs-lookup"><span data-stu-id="18637-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="18637-185">c.</span><span class="sxs-lookup"><span data-stu-id="18637-185">c.</span></span> <span data-ttu-id="18637-186">Değişiklik hello hello özniteliğin adını **emailaddress** çok**e-posta**.</span><span class="sxs-lookup"><span data-stu-id="18637-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="18637-187">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="18637-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="18637-189">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="18637-189">Click **Save**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="18637-191">Çok Git**LinkedIn yönetici ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="18637-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="18637-192">Yalnızca XML karşıya dosya seçeneği hello üzerinde tıklayarak hello Azure portal ' yüklenen hello XML dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="18637-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="18637-194">Tıklatın **üzerinde** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="18637-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="18637-195">SSO durum değişecektir **bağlı** çok**bağlandı**</span><span class="sxs-lookup"><span data-stu-id="18637-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18637-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18637-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="18637-198">Bu bölümde Hello amacı toocreate Britta Simon adlı hello Azure Yönetim Portalı'nda bir sınama kullanıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="18637-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="18637-200">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18637-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18637-201">Merhaba, **Azure Yönetim Portalı**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="18637-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18637-203">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="18637-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18637-205">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18637-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18637-207">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="18637-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18637-209">a.</span><span class="sxs-lookup"><span data-stu-id="18637-209">a.</span></span> <span data-ttu-id="18637-210">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18637-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18637-211">b.</span><span class="sxs-lookup"><span data-stu-id="18637-211">b.</span></span> <span data-ttu-id="18637-212">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="18637-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18637-213">c.</span><span class="sxs-lookup"><span data-stu-id="18637-213">c.</span></span> <span data-ttu-id="18637-214">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="18637-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18637-215">d.</span><span class="sxs-lookup"><span data-stu-id="18637-215">d.</span></span> <span data-ttu-id="18637-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="18637-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="18637-217">Bir LinkedIn yükseltmesine test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18637-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="18637-218">Bağlantılı yükseltmesine uygulama zaman kullanıcı sağlama ve kimlik doğrulama kullanıcılar hello uygulamada otomatik olarak oluşturulacak sonra hemen destekler.</span><span class="sxs-lookup"><span data-stu-id="18637-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="18637-219">Merhaba yönetici ayarları sayfasında hello LinkedIn yükseltmesine portal Çevir hello anahtar **otomatik olarak ata lisansları** zaman sağlama sadece tooactive tooenable ve bu ayrıca atamak lisans toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="18637-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18637-221">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="18637-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18637-222">Bu bölümde, kendi erişim tooLinkedIn yükseltme vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="18637-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="18637-224">**tooassign Britta Simon tooLinkedIn yükseltme, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="18637-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="18637-225">Hello uygulamaları görünümü, Hello Azure Yönetim Portalı'nda açın ve ardından toohello dizin görünümüne gidin ve çok gidin**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="18637-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="18637-227">Merhaba uygulamalar listesinde **LinkedIn yükseltmesine**.</span><span class="sxs-lookup"><span data-stu-id="18637-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="18637-229">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="18637-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="18637-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="18637-231">Click **Add** button.</span></span> <span data-ttu-id="18637-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18637-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="18637-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="18637-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18637-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18637-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18637-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="18637-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18637-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="18637-237">Testing single sign-on</span></span>

<span data-ttu-id="18637-238">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="18637-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18637-239">Merhaba LinkedIn yükseltmesine döşemeyi hello erişim paneli tıklattığınızda hello Azure oturum açma sayfasına almanız gerekir ve üzerinde başarılı oturum açma sonra bunu LinkedIn yükseltmesine uygulamanıza almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18637-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18637-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="18637-240">Additional resources</span></span>

* [<span data-ttu-id="18637-241">Öğretici: LinkedIn yükseltmesine otomatik kullanıcı hazırlama Azure Active Directory ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="18637-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="18637-242">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="18637-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18637-243">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="18637-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
