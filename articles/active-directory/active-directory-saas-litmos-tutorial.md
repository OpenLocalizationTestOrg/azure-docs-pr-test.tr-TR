---
title: "Öğretici: Azure Active Directory Tümleştirme ile Litmos | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Litmos arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="7b9fd-103">Öğretici: Azure Active Directory Tümleştirme Litmos ile</span><span class="sxs-lookup"><span data-stu-id="7b9fd-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="7b9fd-104">Bu öğreticide, bilgi nasıl toointegrate Litmos Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b9fd-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b9fd-105">Litmos Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b9fd-106">Erişim tooLitmos sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="7b9fd-107">Kullanıcıların tooautomatically get açan tooLitmos (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7b9fd-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7b9fd-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b9fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b9fd-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7b9fd-110">Prerequisites</span></span>

<span data-ttu-id="7b9fd-111">tooconfigure Litmos ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="7b9fd-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="7b9fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b9fd-113">Bir Litmos çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="7b9fd-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b9fd-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b9fd-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b9fd-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b9fd-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b9fd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b9fd-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="7b9fd-118">Scenario description</span></span>
<span data-ttu-id="7b9fd-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b9fd-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b9fd-121">Merhaba Galerisi'nden Litmos ekleme</span><span class="sxs-lookup"><span data-stu-id="7b9fd-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="7b9fd-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="7b9fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="7b9fd-123">Merhaba Galerisi'nden Litmos ekleme</span><span class="sxs-lookup"><span data-stu-id="7b9fd-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="7b9fd-124">Azure AD'ye tooconfigure hello tümleştirme Litmos, tooadd Litmos hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b9fd-125">**tooadd Litmos hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b9fd-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b9fd-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="7b9fd-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b9fd-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="7b9fd-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="7b9fd-133">Merhaba arama kutusuna yazın **Litmos**seçin **Litmos** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b9fd-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="7b9fd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7b9fd-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Litmos sınayın.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b9fd-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Litmos içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="7b9fd-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Litmos hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="7b9fd-139">Merhaba hello değeri Litmos içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b9fd-140">tooconfigure ve Litmos ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b9fd-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b9fd-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b9fd-143">**[Litmos test kullanıcısı oluşturma](#create-a-litmos-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Litmos içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b9fd-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b9fd-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b9fd-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="7b9fd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b9fd-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Litmos uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="7b9fd-148">**tooconfigure Azure AD çoklu oturum açma ile Litmos, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b9fd-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b9fd-149">Hello hello üzerinde Azure portal'ın **Litmos** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="7b9fd-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="7b9fd-153">Merhaba üzerinde **Litmos etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Litmos etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="7b9fd-155">a.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-155">a.</span></span> <span data-ttu-id="7b9fd-156">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="7b9fd-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="7b9fd-157">b.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-157">b.</span></span> <span data-ttu-id="7b9fd-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="7b9fd-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b9fd-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-159">These values are not real.</span></span> <span data-ttu-id="7b9fd-160">Bu değerleri hello gerçek tanımlayıcısı ve yanıt URL'si ile daha sonra öğreticide veya kişi açıklanacak güncelleştirmek [Litmos destek ekibi](https://www.litmos.com/contact-us/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="7b9fd-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="7b9fd-163">Merhaba yapılandırmasının bir parçası olarak toocustomize hello gereksinim **SAML belirteci öznitelikleri** Litmos uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Öznitelik bölümü](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="7b9fd-165">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="7b9fd-165">Attribute Name</span></span>   | <span data-ttu-id="7b9fd-166">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="7b9fd-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="7b9fd-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="7b9fd-167">FirstName</span></span> |<span data-ttu-id="7b9fd-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="7b9fd-168">user.givenname</span></span> |
    | <span data-ttu-id="7b9fd-169">Soyadı</span><span class="sxs-lookup"><span data-stu-id="7b9fd-169">LastName</span></span>  |<span data-ttu-id="7b9fd-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="7b9fd-170">user.surname</span></span> |
    | <span data-ttu-id="7b9fd-171">E-posta</span><span class="sxs-lookup"><span data-stu-id="7b9fd-171">Email</span></span> |<span data-ttu-id="7b9fd-172">User.Mail</span><span class="sxs-lookup"><span data-stu-id="7b9fd-172">user.mail</span></span> |

    <span data-ttu-id="7b9fd-173">a.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-173">a.</span></span> <span data-ttu-id="7b9fd-174">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Öznitelik Ekle](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Öznitelik Dailog Ekle](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7b9fd-177">b.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-177">b.</span></span> <span data-ttu-id="7b9fd-178">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7b9fd-179">c.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-179">c.</span></span> <span data-ttu-id="7b9fd-180">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7b9fd-181">d.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-181">d.</span></span> <span data-ttu-id="7b9fd-182">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="7b9fd-183">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-183">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7b9fd-185">Farklı bir tarayıcı penceresinde yönetici olarak oturum açma tooyour Litmos şirket site.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="7b9fd-186">Merhaba gezinti çubuğunda hello sol tarafında tıklayın **hesapları**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Uygulama tarafında hesaplar bölümü][22] 

9. <span data-ttu-id="7b9fd-188">Merhaba tıklatın **tümleştirmeler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-188">Click hello **Integrations** tab.</span></span>
   
    ![Tümleştirme sekmesi][23] 

10. <span data-ttu-id="7b9fd-190">Merhaba üzerinde **tümleştirmeler** sekmesinde, aşağı çok kaydırma**3 taraf tümleştirmeler**ve ardından **SAML 2.0** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 bölümü][24] 

11. <span data-ttu-id="7b9fd-192">Altında Hello değerini kopyalayın **litmos için SAML endpoint hello:** ve hello yapıştırma **yanıt URL'si** metin kutusuna hello **Litmos etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML uç noktası][26] 

12. <span data-ttu-id="7b9fd-194">İçinde **Litmos** uygulama hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Litmos uygulama][25] 
     
     <span data-ttu-id="7b9fd-196">a.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-196">a.</span></span> <span data-ttu-id="7b9fd-197">Tıklatın **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="7b9fd-198">b.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-198">b.</span></span> <span data-ttu-id="7b9fd-199">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **SAML X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="7b9fd-200">c.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-200">c.</span></span> <span data-ttu-id="7b9fd-201">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7b9fd-202">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="7b9fd-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b9fd-203">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b9fd-204">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b9fd-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b9fd-205">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b9fd-205">Create an Azure AD test user</span></span>

<span data-ttu-id="7b9fd-206">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="7b9fd-208">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b9fd-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b9fd-209">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7b9fd-211">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7b9fd-213">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7b9fd-215">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7b9fd-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7b9fd-217">a.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-217">a.</span></span> <span data-ttu-id="7b9fd-218">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b9fd-219">b.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-219">b.</span></span> <span data-ttu-id="7b9fd-220">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7b9fd-221">c.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-221">c.</span></span> <span data-ttu-id="7b9fd-222">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7b9fd-223">d.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-223">d.</span></span> <span data-ttu-id="7b9fd-224">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="7b9fd-225">Litmos test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b9fd-225">Create a Litmos test user</span></span>

<span data-ttu-id="7b9fd-226">Bu bölümde Hello amacı toocreate Britta Simon içinde Litmos adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="7b9fd-227">Merhaba Litmos uygulama destekleyen zaman içinde sadece sağlama.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="7b9fd-228">Bunun anlamı bir kullanıcı hesabı otomatik olarak gerekirse hello erişim paneli kullanma girişimi tooaccess hello sırasında bir uygulama oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="7b9fd-229">**toocreate Litmos içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b9fd-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b9fd-230">Farklı bir tarayıcı penceresinde yönetici olarak oturum açma tooyour Litmos şirket site.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="7b9fd-231">Merhaba gezinti çubuğunda hello sol tarafında tıklayın **hesapları**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Uygulama tarafında hesaplar bölümü][22] 

3. <span data-ttu-id="7b9fd-233">Merhaba tıklatın **tümleştirmeler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-233">Click hello **Integrations** tab.</span></span>
   
    ![Tümleştirmeler sekmesi][23] 

4. <span data-ttu-id="7b9fd-235">Merhaba üzerinde **tümleştirmeler** sekmesinde, aşağı çok kaydırma**3 taraf tümleştirmeler**ve ardından **SAML 2.0** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="7b9fd-237">Seçin **otomatik olarak üret kullanıcılar**</span><span class="sxs-lookup"><span data-stu-id="7b9fd-237">Select **Autogenerate Users**</span></span>
   
    ![Otomatik olarak üret kullanıcılar][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7b9fd-239">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="7b9fd-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7b9fd-240">Bu bölümde, erişim tooLitmos vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="7b9fd-242">**tooassign Britta Simon tooLitmos hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="7b9fd-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b9fd-243">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="7b9fd-245">Merhaba uygulamalar listesinde **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-245">In hello applications list, select **Litmos**.</span></span>

    ![Merhaba Litmos bağlantı hello uygulamalar listesinde](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="7b9fd-247">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="7b9fd-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-249">Click **Add** button.</span></span> <span data-ttu-id="7b9fd-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="7b9fd-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b9fd-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b9fd-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b9fd-255">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="7b9fd-255">Test single sign-on</span></span>

<span data-ttu-id="7b9fd-256">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="7b9fd-257">Hello erişim paneli Litmos döşeme hello tıkladığınızda, otomatik olarak oturum açma Litmos uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b9fd-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b9fd-258">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7b9fd-258">Additional resources</span></span>

* [<span data-ttu-id="7b9fd-259">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="7b9fd-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b9fd-260">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="7b9fd-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

