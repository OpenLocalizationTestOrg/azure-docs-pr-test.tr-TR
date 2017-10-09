---
title: "Öğretici: Azure Active Directory Tümleştirme ile Egnyte | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Egnyte arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="f86c5-103">Öğretici: Azure Active Directory Tümleştirme Egnyte ile</span><span class="sxs-lookup"><span data-stu-id="f86c5-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="f86c5-104">Bu öğreticide, bilgi nasıl toointegrate Egnyte Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f86c5-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f86c5-105">Egnyte Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f86c5-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f86c5-106">Erişim tooEgnyte sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f86c5-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="f86c5-107">Kullanıcıların tooautomatically get açan tooEgnyte (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f86c5-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f86c5-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f86c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f86c5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f86c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f86c5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f86c5-110">Prerequisites</span></span>

<span data-ttu-id="f86c5-111">tooconfigure Egnyte ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f86c5-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="f86c5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f86c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f86c5-113">Bir Egnyte çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f86c5-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f86c5-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f86c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f86c5-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f86c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f86c5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f86c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f86c5-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f86c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f86c5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f86c5-118">Scenario description</span></span>
<span data-ttu-id="f86c5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f86c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f86c5-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f86c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f86c5-121">Merhaba Galerisi'nden Egnyte ekleme</span><span class="sxs-lookup"><span data-stu-id="f86c5-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="f86c5-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f86c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="f86c5-123">Merhaba Galerisi'nden Egnyte ekleme</span><span class="sxs-lookup"><span data-stu-id="f86c5-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="f86c5-124">Azure AD'ye tooconfigure hello tümleştirme Egnyte, tooadd Egnyte hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f86c5-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f86c5-125">**tooadd Egnyte hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f86c5-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f86c5-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f86c5-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f86c5-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f86c5-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f86c5-133">Merhaba arama kutusuna yazın **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-133">In hello search box, type **Egnyte**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="f86c5-135">Merhaba Sonuçlar panelinde seçin **Egnyte**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f86c5-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f86c5-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f86c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f86c5-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Egnyte ile test etme</span><span class="sxs-lookup"><span data-stu-id="f86c5-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f86c5-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Egnyte içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="f86c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="f86c5-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Egnyte hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f86c5-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="f86c5-141">Merhaba hello değeri Egnyte içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f86c5-142">tooconfigure ve Egnyte ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f86c5-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f86c5-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="f86c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f86c5-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="f86c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f86c5-145">**[Bir Egnyte test kullanıcısı oluşturma](#creating-an-egnyte-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Egnyte içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="f86c5-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f86c5-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f86c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f86c5-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="f86c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f86c5-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f86c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f86c5-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Egnyte uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f86c5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="f86c5-150">**tooconfigure Azure AD çoklu oturum açma ile Egnyte, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f86c5-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="f86c5-151">Hello hello üzerinde Azure portal'ın **Egnyte** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f86c5-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="f86c5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="f86c5-155">Merhaba üzerinde **Egnyte etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f86c5-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="f86c5-157">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="f86c5-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f86c5-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="f86c5-158">This value is not real.</span></span> <span data-ttu-id="f86c5-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="f86c5-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f86c5-160">Kişi [Egnyte istemci destek ekibi](https://www.egnyte.com/corp/contact_egnyte.html) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="f86c5-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="f86c5-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f86c5-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="f86c5-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f86c5-165">Merhaba üzerinde **Egnyte yapılandırma** 'yi tıklatın **yapılandırma Egnyte** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f86c5-166">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f86c5-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="f86c5-168">Farklı web tarayıcısı penceresinde tooyour Egnyte şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f86c5-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="f86c5-169">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="f86c5-170">![Ayarları](./media/active-directory-saas-egnyte-tutorial/ic787819.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="f86c5-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="f86c5-171">Merhaba menüye tıklayın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="f86c5-172">![Ayarları](./media/active-directory-saas-egnyte-tutorial/ic787820.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="f86c5-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="f86c5-173">Merhaba tıklatın **yapılandırma** sekmesini ve ardından **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="f86c5-174">![Güvenlik](./media/active-directory-saas-egnyte-tutorial/ic787821.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="f86c5-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="f86c5-175">Merhaba, **çoklu oturum açma kimlik doğrulaması** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f86c5-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="f86c5-176">![Çoklu oturum açma kimlik doğrulaması](./media/active-directory-saas-egnyte-tutorial/ic787822.png "çoklu oturum açma kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="f86c5-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="f86c5-177">a.</span><span class="sxs-lookup"><span data-stu-id="f86c5-177">a.</span></span> <span data-ttu-id="f86c5-178">Olarak **çoklu oturum açma kimlik doğrulaması**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="f86c5-179">b.</span><span class="sxs-lookup"><span data-stu-id="f86c5-179">b.</span></span> <span data-ttu-id="f86c5-180">Olarak **kimlik sağlayıcısı**seçin **Azuread'i**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="f86c5-181">c.</span><span class="sxs-lookup"><span data-stu-id="f86c5-181">c.</span></span> <span data-ttu-id="f86c5-182">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello Azure portalından kopyalandığından **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f86c5-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="f86c5-183">d.</span><span class="sxs-lookup"><span data-stu-id="f86c5-183">d.</span></span> <span data-ttu-id="f86c5-184">Yapıştır **SAML varlık kimliği** hello Azure portalından kopyalanan **kimlik sağlayıcısı varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f86c5-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="f86c5-185">e.</span><span class="sxs-lookup"><span data-stu-id="f86c5-185">e.</span></span> <span data-ttu-id="f86c5-186">Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f86c5-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="f86c5-187">f.</span><span class="sxs-lookup"><span data-stu-id="f86c5-187">f.</span></span> <span data-ttu-id="f86c5-188">Olarak **kullanıcı eşlemesi varsayılan**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="f86c5-189">g.</span><span class="sxs-lookup"><span data-stu-id="f86c5-189">g.</span></span> <span data-ttu-id="f86c5-190">Olarak **etki alanına özgü veren değeriyle kullanın**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="f86c5-191">h.</span><span class="sxs-lookup"><span data-stu-id="f86c5-191">h.</span></span> <span data-ttu-id="f86c5-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f86c5-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f86c5-193">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f86c5-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f86c5-194">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="f86c5-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f86c5-195">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f86c5-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f86c5-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f86c5-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="f86c5-197">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f86c5-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f86c5-199">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f86c5-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f86c5-200">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f86c5-202">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f86c5-204">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="f86c5-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f86c5-206">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f86c5-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f86c5-208">a.</span><span class="sxs-lookup"><span data-stu-id="f86c5-208">a.</span></span> <span data-ttu-id="f86c5-209">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f86c5-210">b.</span><span class="sxs-lookup"><span data-stu-id="f86c5-210">b.</span></span> <span data-ttu-id="f86c5-211">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f86c5-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f86c5-212">c.</span><span class="sxs-lookup"><span data-stu-id="f86c5-212">c.</span></span> <span data-ttu-id="f86c5-213">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f86c5-214">d.</span><span class="sxs-lookup"><span data-stu-id="f86c5-214">d.</span></span> <span data-ttu-id="f86c5-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f86c5-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="f86c5-216">Bir Egnyte test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f86c5-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="f86c5-217">tooenable Azure AD kullanıcıların toolog tooEgnyte bunların Egnyte sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f86c5-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="f86c5-218">Egnyte Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f86c5-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="f86c5-219">**bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:**</span><span class="sxs-lookup"><span data-stu-id="f86c5-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f86c5-220">İçinde tooyour oturum **Egnyte** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="f86c5-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="f86c5-221">Çok Git**ayarları \> kullanıcıları ve grupları**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="f86c5-222">' I tıklatın **yeni kullanıcı Ekle**ve ardından hello türünü seçin kullanıcının tooadd istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="f86c5-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="f86c5-223">![Kullanıcıların](./media/active-directory-saas-egnyte-tutorial/ic787824.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="f86c5-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="f86c5-224">Merhaba, **yeni standart kullanıcı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f86c5-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f86c5-225">![Yeni standart kullanıcı](./media/active-directory-saas-egnyte-tutorial/ic787825.png "yeni standart kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="f86c5-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="f86c5-226">a.</span><span class="sxs-lookup"><span data-stu-id="f86c5-226">a.</span></span> <span data-ttu-id="f86c5-227">Türü hello **e-posta**, **kullanıcıadı**ve diğer ayrıntılarını tooprovision istediğiniz geçerli bir Azure Active Directory hesabı.</span><span class="sxs-lookup"><span data-stu-id="f86c5-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="f86c5-228">b.</span><span class="sxs-lookup"><span data-stu-id="f86c5-228">b.</span></span> <span data-ttu-id="f86c5-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f86c5-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="f86c5-230">Hello Azure Active Directory hesap sahibi bir bildirim e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f86c5-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="f86c5-231">API AAD kullanıcı hesaplarının Egnyte tooprovision tarafından sağlanan veya herhangi diğer Egnyte kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f86c5-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f86c5-232">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f86c5-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f86c5-233">Bu bölümde, erişim tooEgnyte vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f86c5-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f86c5-235">**tooassign Britta Simon tooEgnyte hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f86c5-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="f86c5-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f86c5-238">Merhaba uygulamalar listesinde **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-238">In hello applications list, select **Egnyte**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="f86c5-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f86c5-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f86c5-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f86c5-242">Click **Add** button.</span></span> <span data-ttu-id="f86c5-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f86c5-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f86c5-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f86c5-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f86c5-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f86c5-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f86c5-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f86c5-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f86c5-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f86c5-248">Testing single sign-on</span></span>

<span data-ttu-id="f86c5-249">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f86c5-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f86c5-250">Merhaba Egnyte hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Egnyte uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f86c5-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="f86c5-251">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f86c5-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f86c5-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f86c5-252">Additional resources</span></span>

* [<span data-ttu-id="f86c5-253">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f86c5-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f86c5-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f86c5-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

