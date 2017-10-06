---
title: "Öğretici: Azure Active Directory Tümleştirme ile Trello | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Trello arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="71207-103">Öğretici: Azure Active Directory Tümleştirme Trello ile</span><span class="sxs-lookup"><span data-stu-id="71207-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="71207-104">Bu öğreticide, bilgi nasıl toointegrate Trello Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71207-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71207-105">Trello Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="71207-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71207-106">Erişim tooTrello sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="71207-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="71207-107">Kullanıcıların tooautomatically get açan tooTrello (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="71207-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71207-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="71207-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="71207-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71207-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71207-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="71207-110">Prerequisites</span></span>

<span data-ttu-id="71207-111">tooconfigure Trello ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="71207-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="71207-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="71207-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71207-113">Bir Trello çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="71207-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71207-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="71207-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71207-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="71207-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71207-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="71207-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71207-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71207-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71207-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="71207-118">Scenario description</span></span>
<span data-ttu-id="71207-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="71207-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71207-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="71207-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71207-121">Merhaba Galerisi'nden Trello ekleme</span><span class="sxs-lookup"><span data-stu-id="71207-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="71207-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="71207-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="71207-123">Merhaba Galerisi'nden Trello ekleme</span><span class="sxs-lookup"><span data-stu-id="71207-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="71207-124">Azure AD'ye tooconfigure hello tümleştirme Trello, tooadd Trello hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="71207-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71207-125">**tooadd Trello hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71207-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71207-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="71207-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="71207-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="71207-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71207-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="71207-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="71207-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71207-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="71207-133">Merhaba arama kutusuna yazın **Trello**.</span><span class="sxs-lookup"><span data-stu-id="71207-133">In hello search box, type **Trello**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="71207-135">Merhaba Sonuçlar panelinde seçin **Trello**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="71207-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71207-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="71207-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71207-138">Bu bölümde, yapılandırmak ve Trello "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="71207-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71207-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Trello içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="71207-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="71207-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve Trello hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="71207-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="71207-141">Merhaba hello değeri Trello içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="71207-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="71207-142">tooconfigure ve Trello ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="71207-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71207-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="71207-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71207-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="71207-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71207-145">**[Trello test kullanıcısı oluşturma](#creating-a-trello-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Trello içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="71207-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71207-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="71207-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71207-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="71207-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71207-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71207-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71207-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Trello uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71207-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="71207-150">**tooconfigure Azure AD çoklu oturum açma ile Trello, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71207-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="71207-151">Hello hello üzerinde Azure portal'ın **Trello** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="71207-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="71207-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="71207-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="71207-155">Merhaba üzerinde **Trello etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **IDP başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71207-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="71207-157">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="71207-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="71207-158">Merhaba üzerinde **Trello etki alanı ve URL'leri** tooconfigure hello uygulamada isterseniz, bölümü **SP tarafından başlatılan modu**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71207-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="71207-160">a.</span><span class="sxs-lookup"><span data-stu-id="71207-160">a.</span></span> <span data-ttu-id="71207-161">Tıklatın hello üzerinde **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="71207-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="71207-162">b.</span><span class="sxs-lookup"><span data-stu-id="71207-162">b.</span></span> <span data-ttu-id="71207-163">Merhaba, **oturum üzerinde URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="71207-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="71207-164">Merhaba almalısınız  **\<Kurumsal\>**  Trello gelen başlık.</span><span class="sxs-lookup"><span data-stu-id="71207-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="71207-165">Merhaba başlık değer yoksa, kişi [Trello destek ekibi](mailto:support@trello.com) tooget hello başlık, kuruluş için.</span><span class="sxs-lookup"><span data-stu-id="71207-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="71207-166">Trello uygulama hello SAML onaylar toocontain özel öznitelikler bekler.</span><span class="sxs-lookup"><span data-stu-id="71207-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="71207-167">Bu uygulama için öznitelikler aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71207-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="71207-168">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **"Kullanıcı öznitelikleri"** hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="71207-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="71207-169">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="71207-169">hello following screenshot shows an example for this.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="71207-171">Merhaba üzerinde **SAML belirteci öznitelikleri** iletişim kutusunda, hello aşağıdaki tabloda, gösterilen her satır için gerçekleştirme adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="71207-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="71207-172">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="71207-172">Attribute Name</span></span> | <span data-ttu-id="71207-173">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="71207-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="71207-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="71207-174">User.Email</span></span> | <span data-ttu-id="71207-175">User.Mail</span><span class="sxs-lookup"><span data-stu-id="71207-175">user.mail</span></span> |
    | <span data-ttu-id="71207-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="71207-176">User.FirstName</span></span> | <span data-ttu-id="71207-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="71207-177">user.givenname</span></span> |
    | <span data-ttu-id="71207-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="71207-178">User.LastName</span></span> | <span data-ttu-id="71207-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="71207-179">user.surname</span></span> |

    <span data-ttu-id="71207-180">a.</span><span class="sxs-lookup"><span data-stu-id="71207-180">a.</span></span> <span data-ttu-id="71207-181">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71207-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="71207-184">b.</span><span class="sxs-lookup"><span data-stu-id="71207-184">b.</span></span> <span data-ttu-id="71207-185">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="71207-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="71207-186">c.</span><span class="sxs-lookup"><span data-stu-id="71207-186">c.</span></span> <span data-ttu-id="71207-187">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="71207-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="71207-188">d.</span><span class="sxs-lookup"><span data-stu-id="71207-188">d.</span></span> <span data-ttu-id="71207-189">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71207-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="71207-190">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="71207-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="71207-192">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71207-192">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71207-194">Merhaba üzerinde **Trello yapılandırma** 'yi tıklatın **yapılandırma Trello** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="71207-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="71207-195">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="71207-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="71207-197">tooget uygulamanız için yapılandırılmış SSO Git çok[Trello Kurumsal SSO yapılandırma](https://trello.com/sso-configuration) sayfa toosend [Trello destek ekibi](mailto:support@trello.com) hello **SAML çoklu oturum açma hizmet URL'si** ve Merhaba attach **sertifika (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="71207-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="71207-198">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="71207-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71207-199">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="71207-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71207-200">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71207-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71207-201">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71207-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="71207-202">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="71207-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="71207-204">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71207-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71207-205">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="71207-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71207-207">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="71207-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71207-209">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="71207-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71207-211">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71207-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71207-213">a.</span><span class="sxs-lookup"><span data-stu-id="71207-213">a.</span></span> <span data-ttu-id="71207-214">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71207-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71207-215">b.</span><span class="sxs-lookup"><span data-stu-id="71207-215">b.</span></span> <span data-ttu-id="71207-216">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="71207-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71207-217">c.</span><span class="sxs-lookup"><span data-stu-id="71207-217">c.</span></span> <span data-ttu-id="71207-218">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="71207-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="71207-219">d.</span><span class="sxs-lookup"><span data-stu-id="71207-219">d.</span></span> <span data-ttu-id="71207-220">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71207-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="71207-221">Trello test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71207-221">Creating a Trello test user</span></span>

<span data-ttu-id="71207-222">Bu bölümde, Trello içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71207-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="71207-223">Bu bölümde, Trello içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71207-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="71207-224">Yalnızca zaman sağlama Trello destekler ve yeni bir hesap hello Azure AD'den ilk kez oturum açtığınızda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="71207-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="71207-225">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="71207-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="71207-226">Bu bölümde, erişim tooTrello vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="71207-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="71207-228">**tooassign Britta Simon tooTrello hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="71207-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="71207-229">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="71207-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="71207-231">Merhaba uygulamalar listesinde **Trello**.</span><span class="sxs-lookup"><span data-stu-id="71207-231">In hello applications list, select **Trello**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="71207-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="71207-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="71207-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="71207-235">Click **Add** button.</span></span> <span data-ttu-id="71207-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71207-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="71207-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="71207-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71207-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71207-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71207-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="71207-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71207-241">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="71207-241">Testing single sign-on</span></span>

<span data-ttu-id="71207-242">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="71207-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="71207-243">Merhaba Trello hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Trello uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="71207-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71207-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="71207-244">Additional resources</span></span>

* [<span data-ttu-id="71207-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="71207-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71207-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="71207-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

