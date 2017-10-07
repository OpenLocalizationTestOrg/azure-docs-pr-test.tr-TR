---
title: "Öğretici: Azure Active Directory Tümleştirme kayma ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Slack'e arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="a6a74-103">Öğretici: Azure Active Directory Tümleştirme kayma ile</span><span class="sxs-lookup"><span data-stu-id="a6a74-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="a6a74-104">Bu öğreticide, bilgi nasıl toointegrate boşluk Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="a6a74-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6a74-105">Kayma Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a6a74-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6a74-106">Erişim tooSlack sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a6a74-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="a6a74-107">Kullanıcıların tooautomatically get açan tooSlack (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a6a74-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6a74-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="a6a74-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a6a74-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6a74-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6a74-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a6a74-110">Prerequisites</span></span>

<span data-ttu-id="a6a74-111">tooconfigure kayma ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a6a74-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="a6a74-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="a6a74-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6a74-113">Bir Slack çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="a6a74-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6a74-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a6a74-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6a74-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a6a74-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6a74-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6a74-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6a74-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6a74-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="a6a74-118">Scenario description</span></span>
<span data-ttu-id="a6a74-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="a6a74-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6a74-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="a6a74-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6a74-121">Kayma hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="a6a74-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="a6a74-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a6a74-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="a6a74-123">Kayma hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="a6a74-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="a6a74-124">Azure AD'ye kayma tooconfigure hello tümleştirilmesi, tooadd kayma hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6a74-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6a74-125">**tooadd hello galerisinden kayma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a6a74-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6a74-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6a74-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a6a74-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="a6a74-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="a6a74-133">Merhaba arama kutusuna yazın **Slack'e**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-133">In hello search box, type **Slack**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="a6a74-135">Merhaba Sonuçlar panelinde seçin **Slack'e**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a6a74-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6a74-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="a6a74-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6a74-138">Bu bölümde, yapılandırmak ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı kayma sınayın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a6a74-139">Tek toowork'ın oturum açma hangi hello karşılık gelen kayma içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6a74-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="a6a74-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı kayma hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6a74-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="a6a74-141">Kayma içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a6a74-142">tooconfigure ve boşluk ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a6a74-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a6a74-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="a6a74-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6a74-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="a6a74-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6a74-145">**[Slack test kullanıcısı oluşturma](#creating-a-slack-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir kayma içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="a6a74-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6a74-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a6a74-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6a74-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="a6a74-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6a74-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a6a74-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6a74-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Slack uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="a6a74-150">**tooconfigure Azure AD çoklu oturum açma kayma ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a6a74-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6a74-151">Merhaba hello üzerinde Azure portal'ın **Slack'e** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="a6a74-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="a6a74-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="a6a74-155">Merhaba üzerinde **kayma etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a6a74-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="a6a74-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6a74-157">a.</span></span> <span data-ttu-id="a6a74-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="a6a74-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="a6a74-159">b.</span><span class="sxs-lookup"><span data-stu-id="a6a74-159">b.</span></span> <span data-ttu-id="a6a74-160">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="a6a74-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6a74-161">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="a6a74-161">hello value is not real.</span></span> <span data-ttu-id="a6a74-162">Üzerinde gerçek oturum URL'si hello tooupdate hello değeri var.</span><span class="sxs-lookup"><span data-stu-id="a6a74-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="a6a74-163">Kişi [Slack destek ekibi](https://slack.com/help/contact) tooget hello değeri</span><span class="sxs-lookup"><span data-stu-id="a6a74-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="a6a74-164">Slack uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="a6a74-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a6a74-165">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="a6a74-166">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="a6a74-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a6a74-167">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6a74-167">hello following screenshot shows an example for this.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="a6a74-169">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda **user.mail** olarak **kullanıcı tanımlayıcısı** ve gösterilen her satır için Merhaba aşağıdaki tabloda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a6a74-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="a6a74-170">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="a6a74-170">Attribute Name</span></span> | <span data-ttu-id="a6a74-171">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="a6a74-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a6a74-172">ilk_ad</span><span class="sxs-lookup"><span data-stu-id="a6a74-172">first_name</span></span> | <span data-ttu-id="a6a74-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="a6a74-173">user.givenname</span></span> |
    | <span data-ttu-id="a6a74-174">Soyadı</span><span class="sxs-lookup"><span data-stu-id="a6a74-174">last_name</span></span> | <span data-ttu-id="a6a74-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="a6a74-175">user.surname</span></span> |
    | <span data-ttu-id="a6a74-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="a6a74-176">User.Email</span></span> | <span data-ttu-id="a6a74-177">User.Mail</span><span class="sxs-lookup"><span data-stu-id="a6a74-177">user.mail</span></span> |  
    | <span data-ttu-id="a6a74-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="a6a74-178">User.Username</span></span> | <span data-ttu-id="a6a74-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="a6a74-179">user.userprincipalname</span></span> |

    <span data-ttu-id="a6a74-180">a.</span><span class="sxs-lookup"><span data-stu-id="a6a74-180">a.</span></span> <span data-ttu-id="a6a74-181">Tıklayın **özniteliği** tooopen **öznitelik Düzenle** iletişim kutusu ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a6a74-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="a6a74-183">a.</span><span class="sxs-lookup"><span data-stu-id="a6a74-183">a.</span></span> <span data-ttu-id="a6a74-184">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="a6a74-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="a6a74-185">b.</span><span class="sxs-lookup"><span data-stu-id="a6a74-185">b.</span></span> <span data-ttu-id="a6a74-186">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen select hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="a6a74-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a6a74-187">c.</span><span class="sxs-lookup"><span data-stu-id="a6a74-187">c.</span></span> <span data-ttu-id="a6a74-188">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-188">Click **OK**</span></span>

6. <span data-ttu-id="a6a74-189">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a6a74-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="a6a74-191">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-191">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a6a74-193">Merhaba üzerinde **kayma yapılandırma** 'yi tıklatın **yapılandırma kayma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a6a74-194">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="a6a74-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="a6a74-196">Farklı web tarayıcısı penceresinde tooyour Slack şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="a6a74-197">Çok gidin**Microsoft Azure AD** çok Git**takım ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="a6a74-199">Merhaba, **takım ayarları** bölümünde, hello tıklatın **kimlik doğrulaması** sekmesini ve ardından **ayarlarını değiştir**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="a6a74-201">Merhaba üzerinde **SAML kimlik doğrulaması ayarlarını** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a6a74-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="a6a74-203">a.</span><span class="sxs-lookup"><span data-stu-id="a6a74-203">a.</span></span>  <span data-ttu-id="a6a74-204">Merhaba, **SAML 2.0 uç noktası (HTTP)** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a6a74-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a6a74-205">b.</span><span class="sxs-lookup"><span data-stu-id="a6a74-205">b.</span></span>  <span data-ttu-id="a6a74-206">Merhaba, **kimlik sağlayıcısı veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="a6a74-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a6a74-207">c.</span><span class="sxs-lookup"><span data-stu-id="a6a74-207">c.</span></span>  <span data-ttu-id="a6a74-208">İndirilen sertifika dosyanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **ortak sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a6a74-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="a6a74-209">d.</span><span class="sxs-lookup"><span data-stu-id="a6a74-209">d.</span></span> <span data-ttu-id="a6a74-210">Yukarıdaki üç ayarları Hello Slack ekibiniz için uygun şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="a6a74-211">Hello ayarları hakkında daha fazla bilgi için lütfen hello bulur **Slack'e'nın SSO Yapılandırma Kılavuzu'nda** burada.</span><span class="sxs-lookup"><span data-stu-id="a6a74-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="a6a74-212">e.</span><span class="sxs-lookup"><span data-stu-id="a6a74-212">e.</span></span>  <span data-ttu-id="a6a74-213">Tıklatın **yapılandırmasını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="a6a74-214">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="a6a74-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a6a74-215">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="a6a74-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a6a74-216">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6a74-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6a74-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6a74-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6a74-218">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="a6a74-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="a6a74-220">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a6a74-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6a74-221">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6a74-223">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6a74-225">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="a6a74-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6a74-227">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a6a74-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6a74-229">a.</span><span class="sxs-lookup"><span data-stu-id="a6a74-229">a.</span></span> <span data-ttu-id="a6a74-230">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6a74-231">b.</span><span class="sxs-lookup"><span data-stu-id="a6a74-231">b.</span></span> <span data-ttu-id="a6a74-232">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="a6a74-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6a74-233">c.</span><span class="sxs-lookup"><span data-stu-id="a6a74-233">c.</span></span> <span data-ttu-id="a6a74-234">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a6a74-235">d.</span><span class="sxs-lookup"><span data-stu-id="a6a74-235">d.</span></span> <span data-ttu-id="a6a74-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a6a74-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="a6a74-237">Slack test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6a74-237">Creating a Slack test user</span></span>

<span data-ttu-id="a6a74-238">Bu bölümde Hello amacı toocreate Britta Simon içinde kayma adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6a74-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="a6a74-239">Kayma yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="a6a74-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a6a74-240">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="a6a74-240">There is no action item for you in this section.</span></span> <span data-ttu-id="a6a74-241">Henüz yoksa yeni bir kullanıcı bir girişim tooaccess kayma sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a6a74-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="a6a74-242">Toocreate kullanıcı el ile gerekiyorsa, tooContact gerek [Slack destek ekibi](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="a6a74-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a6a74-243">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="a6a74-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a6a74-244">Bu bölümde, erişim tooSlack vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a6a74-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="a6a74-246">**tooassign Britta Simon tooSlack hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="a6a74-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6a74-247">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="a6a74-249">Merhaba uygulamalar listesinde **Slack'e**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-249">In hello applications list, select **Slack**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="a6a74-251">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="a6a74-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="a6a74-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a6a74-253">Click **Add** button.</span></span> <span data-ttu-id="a6a74-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a6a74-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="a6a74-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="a6a74-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a6a74-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a6a74-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6a74-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="a6a74-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6a74-259">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="a6a74-259">Testing single sign-on</span></span>

<span data-ttu-id="a6a74-260">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="a6a74-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a6a74-261">Merhaba Slack kutucuğa tıkladığınızda de erişim paneli Merhaba, otomatik olarak oturum açma tooyour Slack uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6a74-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6a74-262">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a6a74-262">Additional resources</span></span>

* [<span data-ttu-id="a6a74-263">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a6a74-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6a74-264">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="a6a74-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

