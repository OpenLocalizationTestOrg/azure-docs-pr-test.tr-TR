---
title: "Öğretici: Azure Active Directory Tümleştirme ile Panorama9 | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Panorama9 arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="732f4-103">Öğretici: Azure Active Directory Tümleştirme Panorama9 ile</span><span class="sxs-lookup"><span data-stu-id="732f4-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="732f4-104">Bu öğreticide, bilgi nasıl toointegrate Panorama9 Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="732f4-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="732f4-105">Panorama9 Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="732f4-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="732f4-106">Erişim tooPanorama9 sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="732f4-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="732f4-107">Oturum açma, kullanıcıların tooautomatically get tooPanorama9 etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="732f4-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="732f4-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="732f4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="732f4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="732f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="732f4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="732f4-110">Prerequisites</span></span>

<span data-ttu-id="732f4-111">tooconfigure Panorama9 ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="732f4-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="732f4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="732f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="732f4-113">Bir Panorama9 çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="732f4-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="732f4-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="732f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="732f4-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="732f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="732f4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="732f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="732f4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="732f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="732f4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="732f4-118">Scenario description</span></span>
<span data-ttu-id="732f4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="732f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="732f4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="732f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="732f4-121">Merhaba Galerisi'nden Panorama9 ekleme</span><span class="sxs-lookup"><span data-stu-id="732f4-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="732f4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="732f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="732f4-123">Merhaba Galerisi'nden Panorama9 ekleme</span><span class="sxs-lookup"><span data-stu-id="732f4-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="732f4-124">Azure AD'ye tooconfigure hello tümleştirme Panorama9, tooadd Panorama9 hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="732f4-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="732f4-125">**tooadd Panorama9 hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="732f4-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="732f4-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="732f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="732f4-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="732f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="732f4-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="732f4-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="732f4-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="732f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="732f4-133">Merhaba arama kutusuna yazın **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="732f4-133">In hello search box, type **Panorama9**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="732f4-135">Merhaba Sonuçlar panelinde seçin **Panorama9**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="732f4-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="732f4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="732f4-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="732f4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Panorama9 ile test etme</span><span class="sxs-lookup"><span data-stu-id="732f4-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="732f4-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Panorama9 içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="732f4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="732f4-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Panorama9 hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="732f4-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="732f4-141">Merhaba hello değeri Panorama9 içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="732f4-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="732f4-142">tooconfigure ve Panorama9 ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="732f4-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="732f4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="732f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="732f4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="732f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="732f4-145">**[Panorama9 test kullanıcısı oluşturma](#creating-a-panorama9-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Panorama9 içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="732f4-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="732f4-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="732f4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="732f4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="732f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="732f4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="732f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="732f4-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Panorama9 uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="732f4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="732f4-150">**tooconfigure Azure AD çoklu oturum açma ile Panorama9, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="732f4-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="732f4-151">Hello hello üzerinde Azure portal'ın **Panorama9** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="732f4-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="732f4-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="732f4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="732f4-155">Merhaba üzerinde **Panorama9 etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="732f4-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="732f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="732f4-157">a.</span></span> <span data-ttu-id="732f4-158">Merhaba, **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="732f4-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="732f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="732f4-159">b.</span></span> <span data-ttu-id="732f4-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="732f4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="732f4-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="732f4-161">These values are not real.</span></span> <span data-ttu-id="732f4-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="732f4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="732f4-163">Kişi [Panorama9 istemci destek ekibi](https://support.panorama9.com) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="732f4-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="732f4-164">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="732f4-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="732f4-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="732f4-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="732f4-168">Merhaba üzerinde **Panorama9 yapılandırma** 'yi tıklatın **yapılandırma Panorama9** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="732f4-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="732f4-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="732f4-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="732f4-171">Farklı web tarayıcısı penceresinde Panorama9 şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="732f4-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="732f4-172">Merhaba üstte Hello araç çubuğunda **Yönet**ve ardından **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="732f4-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="732f4-173">![Uzantıları](./media/active-directory-saas-panorama9-tutorial/ic790023.png "uzantıları")</span><span class="sxs-lookup"><span data-stu-id="732f4-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="732f4-174">Merhaba üzerinde **uzantıları** iletişim kutusunda, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="732f4-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="732f4-175">![Çoklu oturum açma](./media/active-directory-saas-panorama9-tutorial/ic790024.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="732f4-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="732f4-176">Merhaba, **ayarları** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="732f4-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="732f4-177">![Ayarları](./media/active-directory-saas-panorama9-tutorial/ic790025.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="732f4-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="732f4-178">a.</span><span class="sxs-lookup"><span data-stu-id="732f4-178">a.</span></span> <span data-ttu-id="732f4-179">İçinde **kimlik sağlayıcısı URL'si** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="732f4-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="732f4-180">b.</span><span class="sxs-lookup"><span data-stu-id="732f4-180">b.</span></span> <span data-ttu-id="732f4-181">İçinde **sertifika parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="732f4-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="732f4-182">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="732f4-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="732f4-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="732f4-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="732f4-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="732f4-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="732f4-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="732f4-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="732f4-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="732f4-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="732f4-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="732f4-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="732f4-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="732f4-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="732f4-190">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="732f4-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="732f4-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="732f4-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="732f4-194">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="732f4-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="732f4-196">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="732f4-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="732f4-198">a.</span><span class="sxs-lookup"><span data-stu-id="732f4-198">a.</span></span> <span data-ttu-id="732f4-199">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="732f4-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="732f4-200">b.</span><span class="sxs-lookup"><span data-stu-id="732f4-200">b.</span></span> <span data-ttu-id="732f4-201">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="732f4-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="732f4-202">c.</span><span class="sxs-lookup"><span data-stu-id="732f4-202">c.</span></span> <span data-ttu-id="732f4-203">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="732f4-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="732f4-204">d.</span><span class="sxs-lookup"><span data-stu-id="732f4-204">d.</span></span> <span data-ttu-id="732f4-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="732f4-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="732f4-206">Panorama9 test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="732f4-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="732f4-207">Panorama9 içine sipariş tooenable Azure AD kullanıcıların toolog bunların Panorama9 sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="732f4-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="732f4-208">Panorama9 Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="732f4-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="732f4-209">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="732f4-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="732f4-210">İçinde tooyour oturum **Panorama9** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="732f4-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="732f4-211">Hello içinde hello üst menüsünde **Yönet**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="732f4-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="732f4-212">![Kullanıcıların](./media/active-directory-saas-panorama9-tutorial/ic790027.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="732f4-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="732f4-213">Hello kullanıcılar bölümü, tıklatın  **+**  tooadd yeni kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="732f4-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="732f4-214">![Kullanıcıların](./media/active-directory-saas-panorama9-tutorial/ic790028.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="732f4-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="732f4-215">Git toohello kullanıcı veri bölümü, türü hello e-posta adresini istediğiniz geçerli bir Azure Active Directory kullanıcı tooprovision hello **e-posta** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="732f4-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="732f4-216">Kullanıcılar bölümünde, tıklatın toohello gelen **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="732f4-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="732f4-217">Hello Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce bir bağlantı tooconfirm hesaplarında izler.</span><span class="sxs-lookup"><span data-stu-id="732f4-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="732f4-218">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="732f4-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="732f4-219">Bu bölümde, erişim tooPanorama9 vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="732f4-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="732f4-221">**tooassign Britta Simon tooPanorama9 hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="732f4-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="732f4-222">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="732f4-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="732f4-224">Merhaba uygulamalar listesinde **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="732f4-224">In hello applications list, select **Panorama9**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="732f4-226">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="732f4-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="732f4-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="732f4-228">Click **Add** button.</span></span> <span data-ttu-id="732f4-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="732f4-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="732f4-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="732f4-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="732f4-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="732f4-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="732f4-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="732f4-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="732f4-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="732f4-234">Testing single sign-on</span></span>

<span data-ttu-id="732f4-235">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="732f4-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="732f4-236">Merhaba erişim paneli hello Panorama9 parçasında tıkladığınızda, otomatik olarak oturum açma tooPanorama9 uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="732f4-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="732f4-237">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="732f4-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="732f4-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="732f4-238">Additional resources</span></span>

* [<span data-ttu-id="732f4-239">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="732f4-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="732f4-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="732f4-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

