---
title: "Öğretici: Azure Active Directory Tümleştirme ile Gigya | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Gigya arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="5347b-103">Öğretici: Azure Active Directory Tümleştirme Gigya ile</span><span class="sxs-lookup"><span data-stu-id="5347b-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="5347b-104">Bu öğreticide, bilgi nasıl toointegrate Gigya Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5347b-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5347b-105">Gigya Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5347b-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5347b-106">Erişim tooGigya sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5347b-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="5347b-107">Kullanıcıların tooautomatically get açan tooGigya (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5347b-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5347b-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="5347b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5347b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5347b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5347b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5347b-110">Prerequisites</span></span>

<span data-ttu-id="5347b-111">tooconfigure Gigya ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5347b-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="5347b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5347b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5347b-113">Bir Gigya çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="5347b-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5347b-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5347b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5347b-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="5347b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5347b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5347b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5347b-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5347b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5347b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5347b-118">Scenario description</span></span>
<span data-ttu-id="5347b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5347b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5347b-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5347b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5347b-121">Merhaba Galerisi'nden Gigya ekleme</span><span class="sxs-lookup"><span data-stu-id="5347b-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="5347b-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5347b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="5347b-123">Merhaba Galerisi'nden Gigya ekleme</span><span class="sxs-lookup"><span data-stu-id="5347b-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="5347b-124">Azure AD'ye tooconfigure hello tümleştirme Gigya, tooadd Gigya hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="5347b-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5347b-125">**tooadd Gigya hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5347b-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5347b-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5347b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5347b-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5347b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5347b-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5347b-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="5347b-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5347b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="5347b-133">Merhaba arama kutusuna yazın **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="5347b-133">In hello search box, type **Gigya**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="5347b-135">Merhaba Sonuçlar panelinde seçin **Gigya**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5347b-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5347b-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5347b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5347b-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Gigya sınayın.</span><span class="sxs-lookup"><span data-stu-id="5347b-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5347b-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Gigya içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="5347b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="5347b-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Gigya hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5347b-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="5347b-141">Merhaba hello değeri Gigya içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="5347b-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5347b-142">tooconfigure ve Gigya ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5347b-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5347b-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="5347b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5347b-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="5347b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5347b-145">**[Gigya test kullanıcısı oluşturma](#creating-a-gigya-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Gigya içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="5347b-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5347b-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5347b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5347b-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="5347b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5347b-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5347b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5347b-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Gigya uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5347b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="5347b-150">**tooconfigure Azure AD çoklu oturum açma ile Gigya, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5347b-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="5347b-151">Hello hello üzerinde Azure portal'ın **Gigya** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5347b-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="5347b-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="5347b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="5347b-155">Merhaba üzerinde **Gigya etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5347b-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="5347b-157">a.</span><span class="sxs-lookup"><span data-stu-id="5347b-157">a.</span></span> <span data-ttu-id="5347b-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="5347b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="5347b-159">b.</span><span class="sxs-lookup"><span data-stu-id="5347b-159">b.</span></span> <span data-ttu-id="5347b-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5347b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5347b-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5347b-161">These values are not real.</span></span> <span data-ttu-id="5347b-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5347b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5347b-163">Kişi [Gigya istemci destek ekibi](https://www.gigya.com/support-policy/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="5347b-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5347b-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5347b-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="5347b-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5347b-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5347b-168">Merhaba üzerinde **Gigya yapılandırma** 'yi tıklatın **yapılandırma Gigya** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5347b-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5347b-169">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="5347b-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="5347b-171">Farklı web tarayıcısı penceresinde Gigya şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5347b-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="5347b-172">Çok Git**ayarları \> SAML oturum açma**ve ardından hello **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5347b-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="5347b-173">![SAML oturum açma](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML oturum açma")</span><span class="sxs-lookup"><span data-stu-id="5347b-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="5347b-174">Merhaba, **SAML oturum açma** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5347b-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5347b-175">![SAML Yapılandırması](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="5347b-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="5347b-176">a.</span><span class="sxs-lookup"><span data-stu-id="5347b-176">a.</span></span> <span data-ttu-id="5347b-177">Merhaba, **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="5347b-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="5347b-178">b.</span><span class="sxs-lookup"><span data-stu-id="5347b-178">b.</span></span> <span data-ttu-id="5347b-179">İçinde **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure Portalı'ndan kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="5347b-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="5347b-180">c.</span><span class="sxs-lookup"><span data-stu-id="5347b-180">c.</span></span> <span data-ttu-id="5347b-181">İçinde **çoklu oturum açma hizmet URL'si** metin kutusuna, Yapıştır hello değerini **çoklu oturum açma hizmet URL'si** Azure Portalı'ndan kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="5347b-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="5347b-182">d.</span><span class="sxs-lookup"><span data-stu-id="5347b-182">d.</span></span> <span data-ttu-id="5347b-183">İçinde **ad kimliği biçimi** metin kutusuna, Yapıştır hello değerini **ad tanımlayıcısı biçimi** Azure Portalı'ndan kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="5347b-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="5347b-184">e.</span><span class="sxs-lookup"><span data-stu-id="5347b-184">e.</span></span> <span data-ttu-id="5347b-185">Base-64 kodlanmış sertifikanızı Azure portalından kopyalama hello panonuza bunu içerik indirilen Not Defteri'nde açın ve toohello Yapıştır **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="5347b-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="5347b-186">f.</span><span class="sxs-lookup"><span data-stu-id="5347b-186">f.</span></span> <span data-ttu-id="5347b-187">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5347b-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5347b-188">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5347b-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5347b-189">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="5347b-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5347b-190">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5347b-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5347b-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5347b-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="5347b-192">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="5347b-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="5347b-194">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5347b-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5347b-195">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5347b-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5347b-197">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5347b-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5347b-199">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="5347b-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5347b-201">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5347b-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5347b-203">a.</span><span class="sxs-lookup"><span data-stu-id="5347b-203">a.</span></span> <span data-ttu-id="5347b-204">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5347b-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5347b-205">b.</span><span class="sxs-lookup"><span data-stu-id="5347b-205">b.</span></span> <span data-ttu-id="5347b-206">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5347b-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5347b-207">c.</span><span class="sxs-lookup"><span data-stu-id="5347b-207">c.</span></span> <span data-ttu-id="5347b-208">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5347b-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5347b-209">d.</span><span class="sxs-lookup"><span data-stu-id="5347b-209">d.</span></span> <span data-ttu-id="5347b-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5347b-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="5347b-211">Gigya test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5347b-211">Creating a Gigya test user</span></span>

<span data-ttu-id="5347b-212">Gigya içine sipariş tooenable Azure AD kullanıcıların toolog bunların Gigya sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5347b-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="5347b-213">Gigya Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5347b-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="5347b-214">bir kullanıcı hesapları tooprovision gerçekleştirmek hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5347b-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="5347b-215">İçinde tooyour oturum **Gigya** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="5347b-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="5347b-216">Çok Git**yönetici \> kullanıcıları yönetme**ve ardından **kullanıcıları davet**.</span><span class="sxs-lookup"><span data-stu-id="5347b-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="5347b-217">![Kullanıcıları yönetme](./media/active-directory-saas-gigya-tutorial/ic789535.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="5347b-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="5347b-218">Merhaba kullanıcıları davet iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5347b-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5347b-219">![Kullanıcıları davet](./media/active-directory-saas-gigya-tutorial/ic789536.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="5347b-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="5347b-220">a.</span><span class="sxs-lookup"><span data-stu-id="5347b-220">a.</span></span> <span data-ttu-id="5347b-221">Merhaba, **e-posta** metin kutusuna, tooprovision istediğiniz geçerli bir Azure Active Directory hesap türü hello e-posta diğer adı.</span><span class="sxs-lookup"><span data-stu-id="5347b-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="5347b-222">b.</span><span class="sxs-lookup"><span data-stu-id="5347b-222">b.</span></span> <span data-ttu-id="5347b-223">Tıklatın **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="5347b-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="5347b-224">Hello Azure Active Directory hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5347b-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5347b-225">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5347b-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5347b-226">Bu bölümde, erişim tooGigya vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5347b-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5347b-228">**tooassign Britta Simon tooGigya hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5347b-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="5347b-229">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5347b-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5347b-231">Merhaba uygulamalar listesinde **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="5347b-231">In hello applications list, select **Gigya**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="5347b-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5347b-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5347b-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5347b-235">Click **Add** button.</span></span> <span data-ttu-id="5347b-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5347b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5347b-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5347b-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5347b-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5347b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5347b-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5347b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5347b-241">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5347b-241">Testing single sign-on</span></span>

<span data-ttu-id="5347b-242">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5347b-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5347b-243">Merhaba Gigya hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Gigya uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5347b-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5347b-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5347b-244">Additional resources</span></span>

* [<span data-ttu-id="5347b-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5347b-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5347b-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5347b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

