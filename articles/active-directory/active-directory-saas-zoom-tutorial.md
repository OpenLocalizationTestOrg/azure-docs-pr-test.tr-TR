---
title: "Öğretici: Azure Active Directory Tümleştirme yakınlaştırma ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve yakınlaştırma arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="26d3a-103">Öğretici: Yakınlaştırma Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="26d3a-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="26d3a-104">Bu öğreticide, bilgi nasıl toointegrate yakınlaştırma Azure Active Directory (Azure AD) ile.</span><span class="sxs-lookup"><span data-stu-id="26d3a-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26d3a-105">Yakınlaştırma Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="26d3a-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="26d3a-106">Erişim tooZoom sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26d3a-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="26d3a-107">Kullanıcıların tooautomatically get açan tooZoom (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26d3a-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="26d3a-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="26d3a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="26d3a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26d3a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26d3a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="26d3a-110">Prerequisites</span></span>

<span data-ttu-id="26d3a-111">Yakınlaştırma ile tooconfigure Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="26d3a-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="26d3a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="26d3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26d3a-113">Bir yakınlaştırma çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="26d3a-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26d3a-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="26d3a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26d3a-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="26d3a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26d3a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26d3a-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26d3a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26d3a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="26d3a-118">Scenario description</span></span>
<span data-ttu-id="26d3a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="26d3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26d3a-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="26d3a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26d3a-121">Yakınlaştırma hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="26d3a-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="26d3a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="26d3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="26d3a-123">Yakınlaştırma hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="26d3a-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="26d3a-124">Azure AD'ye yakınlaştırma tooconfigure hello tümleştirilmesi, tooadd yakınlaştırma hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="26d3a-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="26d3a-125">**tooadd hello galerisinden yakınlaştırma hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26d3a-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="26d3a-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="26d3a-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="26d3a-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="26d3a-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="26d3a-133">Merhaba arama kutusuna yazın **yakınlaştırma**seçin **yakınlaştırma** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="26d3a-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçlar listesinde Yakınlaştır](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26d3a-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="26d3a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="26d3a-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı yakınlaştırma ile test etme.</span><span class="sxs-lookup"><span data-stu-id="26d3a-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26d3a-137">Tek toowork'ın oturum açma hangi hello karşılık gelen yakınlaştırır tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="26d3a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="26d3a-138">Diğer bir deyişle, bir bağlantı bir Azure AD kullanıcı ve kullanıcı arasındaki ilişki hello ilgili kurulan yakınlaştırma gereksinimlerini toobe içinde.</span><span class="sxs-lookup"><span data-stu-id="26d3a-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="26d3a-139">Yakınlaştırma, hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="26d3a-140">tooconfigure ve yakınlaştırma ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="26d3a-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="26d3a-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="26d3a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="26d3a-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="26d3a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26d3a-143">**[Yakınlaştırma test kullanıcısı oluşturma](#create-a-zoom-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir yakınlaştırır, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="26d3a-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="26d3a-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="26d3a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26d3a-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="26d3a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26d3a-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="26d3a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="26d3a-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma yakınlaştırma uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="26d3a-148">**Yakınlaştırma ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26d3a-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="26d3a-149">Merhaba hello üzerinde Azure portal'ın **yakınlaştırma** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="26d3a-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="26d3a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="26d3a-153">Merhaba üzerinde **yakınlaştırma etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26d3a-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Etki alanı ve URL'leri tek oturum açma bilgilerini Yakınlaştır](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="26d3a-155">a.</span><span class="sxs-lookup"><span data-stu-id="26d3a-155">a.</span></span> <span data-ttu-id="26d3a-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="26d3a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="26d3a-157">b.</span><span class="sxs-lookup"><span data-stu-id="26d3a-157">b.</span></span> <span data-ttu-id="26d3a-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="26d3a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26d3a-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="26d3a-159">These values are not real.</span></span> <span data-ttu-id="26d3a-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="26d3a-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="26d3a-161">Kişi [yakınlaştırma istemci destek ekibi](https://support.zoom.us/hc) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="26d3a-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="26d3a-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="26d3a-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="26d3a-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26d3a-166">Merhaba üzerinde **yakınlaştırma yapılandırma** 'yi tıklatın **yapılandırma yakınlaştırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="26d3a-167">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="26d3a-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Yakınlaştırma yapılandırma](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="26d3a-169">Farklı web tarayıcısı penceresinde tooyour yakınlaştırma şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="26d3a-170">Merhaba tıklatın **çoklu oturum açma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="26d3a-171">![Oturum açma tek sekme](./media/active-directory-saas-zoom-tutorial/IC784700.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="26d3a-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="26d3a-172">Hello tıklatın **güvenlik denetimi** sekmesini tıklatın ve ardından toohello Git **çoklu oturum açma** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="26d3a-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="26d3a-173">Hello çoklu oturum açma bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26d3a-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="26d3a-174">![Çoklu oturum açma bölüm](./media/active-directory-saas-zoom-tutorial/IC784701.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="26d3a-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="26d3a-175">a.</span><span class="sxs-lookup"><span data-stu-id="26d3a-175">a.</span></span> <span data-ttu-id="26d3a-176">Merhaba, **oturum açma sayfası URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="26d3a-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="26d3a-177">b.</span><span class="sxs-lookup"><span data-stu-id="26d3a-177">b.</span></span> <span data-ttu-id="26d3a-178">Merhaba, **oturum kapatma sayfası URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="26d3a-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="26d3a-179">c.</span><span class="sxs-lookup"><span data-stu-id="26d3a-179">c.</span></span> <span data-ttu-id="26d3a-180">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="26d3a-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="26d3a-181">d.</span><span class="sxs-lookup"><span data-stu-id="26d3a-181">d.</span></span> <span data-ttu-id="26d3a-182">Merhaba, **veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="26d3a-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="26d3a-183">e.</span><span class="sxs-lookup"><span data-stu-id="26d3a-183">e.</span></span> <span data-ttu-id="26d3a-184">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="26d3a-185">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="26d3a-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="26d3a-186">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="26d3a-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="26d3a-187">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26d3a-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26d3a-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26d3a-188">Create an Azure AD test user</span></span>

<span data-ttu-id="26d3a-189">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="26d3a-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="26d3a-191">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26d3a-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="26d3a-192">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="26d3a-194">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="26d3a-196">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="26d3a-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="26d3a-198">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26d3a-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="26d3a-200">a.</span><span class="sxs-lookup"><span data-stu-id="26d3a-200">a.</span></span> <span data-ttu-id="26d3a-201">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26d3a-202">b.</span><span class="sxs-lookup"><span data-stu-id="26d3a-202">b.</span></span> <span data-ttu-id="26d3a-203">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="26d3a-204">c.</span><span class="sxs-lookup"><span data-stu-id="26d3a-204">c.</span></span> <span data-ttu-id="26d3a-205">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="26d3a-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="26d3a-206">d.</span><span class="sxs-lookup"><span data-stu-id="26d3a-206">d.</span></span> <span data-ttu-id="26d3a-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="26d3a-208">Yakınlaştırma test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="26d3a-208">Create a Zoom test user</span></span>

<span data-ttu-id="26d3a-209">Sipariş tooenable Azure AD kullanıcıların toolog içinde tooZoom içinde bunların yakınlaştırma sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26d3a-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="26d3a-210">Yakınlaştırma Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="26d3a-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="26d3a-211">bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26d3a-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="26d3a-212">İçinde tooyour oturum **yakınlaştırma** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="26d3a-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="26d3a-213">Merhaba tıklatın **hesap yönetimi** sekmesini ve ardından **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="26d3a-214">Hello kullanıcı yönetimi bölümü, tıklatın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="26d3a-215">![Kullanıcı Yönetimi](./media/active-directory-saas-zoom-tutorial/IC784703.png "kullanıcı yönetimi")</span><span class="sxs-lookup"><span data-stu-id="26d3a-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="26d3a-216">Merhaba üzerinde **kullanıcıları eklemek** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="26d3a-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="26d3a-217">![Kullanıcıları ekleme](./media/active-directory-saas-zoom-tutorial/IC784704.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="26d3a-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="26d3a-218">a.</span><span class="sxs-lookup"><span data-stu-id="26d3a-218">a.</span></span> <span data-ttu-id="26d3a-219">Olarak **kullanıcı türü**seçin **temel**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="26d3a-220">b.</span><span class="sxs-lookup"><span data-stu-id="26d3a-220">b.</span></span> <span data-ttu-id="26d3a-221">Merhaba, **e-postaları** metin kutusuna, türü hello e-posta adresi geçerli bir Azure tooprovision istediğiniz AD hesabı.</span><span class="sxs-lookup"><span data-stu-id="26d3a-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="26d3a-222">c.</span><span class="sxs-lookup"><span data-stu-id="26d3a-222">c.</span></span> <span data-ttu-id="26d3a-223">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="26d3a-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="26d3a-224">API, kullanıcı hesaplarını yakınlaştırma tooprovision Azure Active Directory tarafından sağlanan veya herhangi diğer yakınlaştırma kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26d3a-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="26d3a-225">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="26d3a-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="26d3a-226">Bu bölümde, erişim tooZoom vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="26d3a-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="26d3a-228">**tooassign Britta Simon tooZoom hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="26d3a-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="26d3a-229">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="26d3a-231">Merhaba uygulamalar listesinde **yakınlaştırma**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-231">In hello applications list, select **Zoom**.</span></span>

    ![Merhaba yakınlaştırma bağlantı hello uygulamalar listesinde](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="26d3a-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="26d3a-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="26d3a-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="26d3a-235">Click **Add** button.</span></span> <span data-ttu-id="26d3a-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26d3a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="26d3a-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="26d3a-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="26d3a-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26d3a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26d3a-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="26d3a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="26d3a-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="26d3a-241">Test single sign-on</span></span>

<span data-ttu-id="26d3a-242">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="26d3a-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="26d3a-243">Merhaba yakınlaştırma hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour yakınlaştırma uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26d3a-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26d3a-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="26d3a-244">Additional resources</span></span>

* [<span data-ttu-id="26d3a-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="26d3a-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26d3a-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="26d3a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

