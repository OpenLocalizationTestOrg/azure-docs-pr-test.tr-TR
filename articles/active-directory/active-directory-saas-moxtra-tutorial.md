---
title: "Öğretici: Azure Active Directory Tümleştirme ile Moxtra | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Moxtra arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="6a792-103">Öğretici: Azure Active Directory Tümleştirme Moxtra ile</span><span class="sxs-lookup"><span data-stu-id="6a792-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="6a792-104">Bu öğreticide, bilgi nasıl toointegrate Moxtra Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a792-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a792-105">Moxtra Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6a792-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a792-106">Erişim tooMoxtra sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6a792-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="6a792-107">Kullanıcıların tooautomatically get açan tooMoxtra (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6a792-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a792-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6a792-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6a792-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a792-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a792-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6a792-110">Prerequisites</span></span>

<span data-ttu-id="6a792-111">tooconfigure Moxtra ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a792-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="6a792-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6a792-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a792-113">Bir Moxtra çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6a792-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a792-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6a792-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a792-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a792-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a792-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6a792-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a792-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a792-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a792-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6a792-118">Scenario description</span></span>
<span data-ttu-id="6a792-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6a792-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a792-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6a792-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a792-121">Merhaba Galerisi'nden Moxtra ekleme</span><span class="sxs-lookup"><span data-stu-id="6a792-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="6a792-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6a792-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="6a792-123">Merhaba Galerisi'nden Moxtra ekleme</span><span class="sxs-lookup"><span data-stu-id="6a792-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="6a792-124">Azure AD'ye tooconfigure hello tümleştirme Moxtra, tooadd Moxtra hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a792-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a792-125">**tooadd Moxtra hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a792-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a792-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6a792-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a792-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6a792-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a792-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6a792-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6a792-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a792-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6a792-133">Merhaba arama kutusuna yazın **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="6a792-133">In hello search box, type **Moxtra**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="6a792-135">Merhaba Sonuçlar panelinde seçin **Moxtra**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6a792-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a792-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6a792-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a792-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Moxtra sınayın.</span><span class="sxs-lookup"><span data-stu-id="6a792-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a792-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Moxtra içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a792-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="6a792-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Moxtra hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a792-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="6a792-141">Merhaba hello değeri Moxtra içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6a792-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a792-142">tooconfigure ve Moxtra ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a792-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a792-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6a792-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a792-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6a792-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a792-145">**[Moxtra test kullanıcısı oluşturma](#creating-a-moxtra-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Moxtra içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6a792-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a792-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6a792-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a792-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6a792-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a792-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6a792-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a792-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Moxtra uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6a792-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="6a792-150">**tooconfigure Azure AD çoklu oturum açma ile Moxtra, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a792-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a792-151">Hello hello üzerinde Azure portal'ın **Moxtra** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6a792-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6a792-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6a792-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="6a792-155">Merhaba üzerinde **Moxtra etki alanı ve URL'leri** bölümünde, adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a792-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="6a792-157">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="6a792-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="6a792-158">Moxtra uygulama hello SAML onaylar belirli bir biçimde bekler.</span><span class="sxs-lookup"><span data-stu-id="6a792-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6a792-159">Bu uygulama için talep aşağıdaki hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6a792-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="6a792-160">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz "**kullanıcı öznitelikleri**" uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="6a792-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6a792-161">Ekran aşağıdaki hello Bu yapılandırmanın bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="6a792-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="6a792-163">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği hello görüntüde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a792-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6a792-164">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="6a792-164">Attribute Name</span></span> | <span data-ttu-id="6a792-165">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="6a792-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6a792-166">FirstName</span><span class="sxs-lookup"><span data-stu-id="6a792-166">firstname</span></span> | <span data-ttu-id="6a792-167">User.givenName</span><span class="sxs-lookup"><span data-stu-id="6a792-167">user.givenname</span></span> |
    | <span data-ttu-id="6a792-168">Soyadı</span><span class="sxs-lookup"><span data-stu-id="6a792-168">lastname</span></span> | <span data-ttu-id="6a792-169">User.surname</span><span class="sxs-lookup"><span data-stu-id="6a792-169">user.surname</span></span> |
    | <span data-ttu-id="6a792-170">idpid</span><span class="sxs-lookup"><span data-stu-id="6a792-170">idpid</span></span>    | <span data-ttu-id="6a792-171">< SAML varlık kimliği ></span><span class="sxs-lookup"><span data-stu-id="6a792-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="6a792-172">Merhaba değerini **idpid** özniteliği gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="6a792-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="6a792-173">Merhaba gerçek değerinden alabilirsiniz **hızlı başvuru** altında bölümünde **Moxtra yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="6a792-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="6a792-174">a.</span><span class="sxs-lookup"><span data-stu-id="6a792-174">a.</span></span> <span data-ttu-id="6a792-175">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a792-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="6a792-177">b.</span><span class="sxs-lookup"><span data-stu-id="6a792-177">b.</span></span> <span data-ttu-id="6a792-178">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="6a792-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6a792-180">c.</span><span class="sxs-lookup"><span data-stu-id="6a792-180">c.</span></span> <span data-ttu-id="6a792-181">Merhaba gelen **değeri** listesinde, ilgili satır için gösterilen türü hello öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="6a792-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="6a792-182">d.</span><span class="sxs-lookup"><span data-stu-id="6a792-182">d.</span></span> <span data-ttu-id="6a792-183">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a792-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="6a792-184">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6a792-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="6a792-186">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a792-186">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6a792-188">Merhaba üzerinde **Moxtra yapılandırma** 'yi tıklatın **yapılandırma Moxtra** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6a792-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6a792-189">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6a792-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="6a792-191">Başka bir tarayıcı penceresinde tooyour Moxtra şirket sitesinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6a792-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="6a792-192">Merhaba soldaki Hello araç çubuğunda **Yönetici Konsolu > SAML çoklu oturum açma**ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="6a792-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="6a792-194">Merhaba üzerinde **SAML** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a792-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="6a792-196">a.</span><span class="sxs-lookup"><span data-stu-id="6a792-196">a.</span></span> <span data-ttu-id="6a792-197">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="6a792-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="6a792-198">b.</span><span class="sxs-lookup"><span data-stu-id="6a792-198">b.</span></span> <span data-ttu-id="6a792-199">Merhaba, **IDP varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6a792-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="6a792-200">c.</span><span class="sxs-lookup"><span data-stu-id="6a792-200">c.</span></span> <span data-ttu-id="6a792-201">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6a792-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="6a792-202">d.</span><span class="sxs-lookup"><span data-stu-id="6a792-202">d.</span></span> <span data-ttu-id="6a792-203">Merhaba, **AuthnContextClassRef** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="6a792-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="6a792-204">e.</span><span class="sxs-lookup"><span data-stu-id="6a792-204">e.</span></span> <span data-ttu-id="6a792-205">Merhaba, **NameID biçimi** metin kutusuna, türü **urn: OASIS: adları: tc: SAML:1.1:nameid-biçimi: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="6a792-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="6a792-206">f.</span><span class="sxs-lookup"><span data-stu-id="6a792-206">f.</span></span> <span data-ttu-id="6a792-207">Not Defteri'nde, Azure Portalı'ndan indirilen açık sertifika hello içeriği Kopyala ve hello yapıştırma **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6a792-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="6a792-208">g.</span><span class="sxs-lookup"><span data-stu-id="6a792-208">g.</span></span> <span data-ttu-id="6a792-209">SAML e-posta etki alanınızın Hello SAML e-posta etki alanı metin kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="6a792-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="6a792-210">toosee hello adımları tooverify hello etki alanı, hello tıklayın "**ı**" altında.</span><span class="sxs-lookup"><span data-stu-id="6a792-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="6a792-211">h.</span><span class="sxs-lookup"><span data-stu-id="6a792-211">h.</span></span> <span data-ttu-id="6a792-212">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="6a792-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="6a792-213">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6a792-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a792-214">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6a792-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a792-215">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a792-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a792-216">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a792-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a792-217">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6a792-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6a792-219">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a792-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a792-220">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6a792-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a792-222">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6a792-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a792-224">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a792-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a792-226">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a792-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a792-228">a.</span><span class="sxs-lookup"><span data-stu-id="6a792-228">a.</span></span> <span data-ttu-id="6a792-229">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a792-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a792-230">b.</span><span class="sxs-lookup"><span data-stu-id="6a792-230">b.</span></span> <span data-ttu-id="6a792-231">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6a792-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a792-232">c.</span><span class="sxs-lookup"><span data-stu-id="6a792-232">c.</span></span> <span data-ttu-id="6a792-233">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6a792-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6a792-234">d.</span><span class="sxs-lookup"><span data-stu-id="6a792-234">d.</span></span> <span data-ttu-id="6a792-235">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a792-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="6a792-236">Moxtra test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a792-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="6a792-237">Bu bölümde Hello amacı toocreate Britta Simon içinde Moxtra adlı bir kullanıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a792-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="6a792-238">**toocreate Moxtra içinde Britta Simon adlı bir kullanıcı hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a792-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a792-239">Üzerinde tooyour Moxtra şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6a792-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="6a792-240">Merhaba soldaki Hello araç çubuğunda **Yönetici Konsolu > Kullanıcı Yönetimi**ve ardından **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6a792-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="6a792-242">Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6a792-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="6a792-243">a.</span><span class="sxs-lookup"><span data-stu-id="6a792-243">a.</span></span> <span data-ttu-id="6a792-244">Merhaba, **ad** metin kutusuna, türü **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6a792-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="6a792-245">b.</span><span class="sxs-lookup"><span data-stu-id="6a792-245">b.</span></span> <span data-ttu-id="6a792-246">Merhaba, **Soyadı** metin kutusuna, türü **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6a792-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="6a792-247">c.</span><span class="sxs-lookup"><span data-stu-id="6a792-247">c.</span></span> <span data-ttu-id="6a792-248">Merhaba, **e-posta** metin kutusuna, Britta'nın e-posta adresi ile aynı Azure Portal'da türü.</span><span class="sxs-lookup"><span data-stu-id="6a792-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="6a792-249">d.</span><span class="sxs-lookup"><span data-stu-id="6a792-249">d.</span></span> <span data-ttu-id="6a792-250">Merhaba, **bölme** metin kutusuna, türü **geliştirme**.</span><span class="sxs-lookup"><span data-stu-id="6a792-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="6a792-251">e.</span><span class="sxs-lookup"><span data-stu-id="6a792-251">e.</span></span> <span data-ttu-id="6a792-252">Merhaba, **departmanı** metin kutusuna, türü **BT**.</span><span class="sxs-lookup"><span data-stu-id="6a792-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="6a792-253">f.</span><span class="sxs-lookup"><span data-stu-id="6a792-253">f.</span></span> <span data-ttu-id="6a792-254">Seçin **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="6a792-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="6a792-255">g.</span><span class="sxs-lookup"><span data-stu-id="6a792-255">g.</span></span> <span data-ttu-id="6a792-256">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a792-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6a792-257">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6a792-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6a792-258">Bu bölümde, erişim tooMoxtra vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6a792-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6a792-260">**tooassign Britta Simon tooMoxtra hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6a792-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a792-261">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6a792-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6a792-263">Merhaba uygulamalar listesinde **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="6a792-263">In hello applications list, select **Moxtra**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="6a792-265">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6a792-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6a792-267">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6a792-267">Click **Add** button.</span></span> <span data-ttu-id="6a792-268">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a792-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6a792-270">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6a792-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a792-271">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a792-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a792-272">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6a792-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a792-273">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6a792-273">Testing single sign-on</span></span>

<span data-ttu-id="6a792-274">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6a792-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6a792-275">Merhaba Moxtra hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Moxtra uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a792-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="6a792-276">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a792-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a792-277">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6a792-277">Additional resources</span></span>

* [<span data-ttu-id="6a792-278">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6a792-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a792-279">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6a792-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

