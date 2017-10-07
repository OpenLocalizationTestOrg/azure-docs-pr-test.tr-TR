---
title: "Öğretici: Azure Active Directory Tümleştirme ile Bonusly | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Bonusly arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="2ee9c-103">Öğretici: Azure Active Directory Tümleştirme Bonusly ile</span><span class="sxs-lookup"><span data-stu-id="2ee9c-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="2ee9c-104">Bu öğreticide, bilgi nasıl toointegrate Bonusly Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ee9c-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ee9c-105">Bonusly Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ee9c-106">Erişim tooBonusly sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2ee9c-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="2ee9c-107">Kullanıcıların tooautomatically get açan tooBonusly (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2ee9c-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ee9c-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2ee9c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ee9c-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ee9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ee9c-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ee9c-110">Prerequisites</span></span>

<span data-ttu-id="2ee9c-111">tooconfigure Bonusly ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="2ee9c-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2ee9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ee9c-113">Bir Bonusly çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2ee9c-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ee9c-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ee9c-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ee9c-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ee9c-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ee9c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ee9c-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2ee9c-118">Scenario description</span></span>
<span data-ttu-id="2ee9c-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ee9c-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ee9c-121">Merhaba Galerisi'nden Bonusly ekleme</span><span class="sxs-lookup"><span data-stu-id="2ee9c-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="2ee9c-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2ee9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="2ee9c-123">Merhaba Galerisi'nden Bonusly ekleme</span><span class="sxs-lookup"><span data-stu-id="2ee9c-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="2ee9c-124">Azure AD'ye tooconfigure hello tümleştirme Bonusly, tooadd Bonusly hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ee9c-125">**tooadd Bonusly hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee9c-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ee9c-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="2ee9c-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ee9c-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="2ee9c-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="2ee9c-133">Merhaba arama kutusuna yazın **Bonusly**seçin **Bonusly** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2ee9c-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2ee9c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2ee9c-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Bonusly sınayın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ee9c-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Bonusly içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="2ee9c-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Bonusly hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="2ee9c-139">Merhaba hello değeri Bonusly içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ee9c-140">tooconfigure ve Bonusly ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ee9c-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ee9c-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ee9c-143">**[Bonusly test kullanıcısı oluşturma](#create-a-bonusly-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Bonusly içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ee9c-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ee9c-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2ee9c-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2ee9c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2ee9c-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Bonusly uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="2ee9c-148">**tooconfigure Azure AD çoklu oturum açma ile Bonusly, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee9c-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ee9c-149">Hello hello üzerinde Azure portal'ın **Bonusly** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2ee9c-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="2ee9c-153">Merhaba üzerinde **Bonusly etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Oturum açma bilgileri bonusly etki alanı ve URL'leri tek](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="2ee9c-155">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="2ee9c-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ee9c-156">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-156">hello value is not real.</span></span> <span data-ttu-id="2ee9c-157">Güncelleştirme hello değerle hello gerçek yanıt URL'si.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="2ee9c-158">Kişi [Bonusly destek ekibi](https://Bonusly/contact) tooget hello değeri.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="2ee9c-159">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** hello sertifikasından değeri.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="2ee9c-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ee9c-163">Merhaba üzerinde **Bonusly yapılandırma** 'yi tıklatın **yapılandırma Bonusly** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2ee9c-164">Kopya hello **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2ee9c-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Bonusly yapılandırma](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="2ee9c-166">Farklı bir tarayıcı penceresinde tooyour içinde oturum **Bonusly** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="2ee9c-167">Merhaba üstte Hello araç çubuğunda **ayarları**ve ardından **tümleştirmeler ve uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="2ee9c-168">![Bonusly sosyal bölüm](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="2ee9c-169">Altında **çoklu oturum açma**seçin **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="2ee9c-170">Merhaba üzerinde **SAML** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2ee9c-171">![Bonusly Saml iletişim sayfa](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="2ee9c-172">a.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-172">a.</span></span> <span data-ttu-id="2ee9c-173">Merhaba, **IDP SSO hedef URL** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2ee9c-174">b.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-174">b.</span></span> <span data-ttu-id="2ee9c-175">Merhaba, **IDP veren** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2ee9c-176">c.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-176">c.</span></span> <span data-ttu-id="2ee9c-177">Merhaba, **IDP oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2ee9c-178">d.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-178">d.</span></span> <span data-ttu-id="2ee9c-179">Yapıştır **parmak izi** değeri hello Azure portalından kopyalanan **sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="2ee9c-180">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2ee9c-181">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2ee9c-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ee9c-182">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ee9c-183">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ee9c-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2ee9c-184">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee9c-184">Create an Azure AD test user</span></span>
<span data-ttu-id="2ee9c-185">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="2ee9c-187">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee9c-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ee9c-188">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ee9c-190">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ee9c-192">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ee9c-194">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ee9c-196">a.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-196">a.</span></span> <span data-ttu-id="2ee9c-197">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ee9c-198">b.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-198">b.</span></span> <span data-ttu-id="2ee9c-199">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ee9c-200">c.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-200">c.</span></span> <span data-ttu-id="2ee9c-201">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ee9c-202">d.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-202">d.</span></span> <span data-ttu-id="2ee9c-203">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="2ee9c-204">Bonusly test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee9c-204">Create a Bonusly test user</span></span>

<span data-ttu-id="2ee9c-205">TooBonusly içinde sipariş tooenable Azure AD kullanıcıların toolog bunların Bonusly sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="2ee9c-206">Bonusly Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="2ee9c-207">API, kullanıcı hesaplarını Bonusly tooprovision AAD tarafından sağlanan veya herhangi diğer Bonusly kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="2ee9c-208">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee9c-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ee9c-209">Bir web tarayıcısı penceresinde tooyour Bonusly kiracısı'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="2ee9c-210">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="2ee9c-211">![Ayarları](./media/active-directory-saas-bonus-tutorial/ic781041.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="2ee9c-212">Merhaba tıklatın **kullanıcılar ve İkramiyeler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="2ee9c-213">![Kullanıcılar ve İkramiyeler](./media/active-directory-saas-bonus-tutorial/ic781042.png "kullanıcılar ve İkramiyeler")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="2ee9c-214">Tıklatın **kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="2ee9c-215">![Kullanıcıları yönetme](./media/active-directory-saas-bonus-tutorial/ic781043.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="2ee9c-216">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="2ee9c-217">![Kullanıcı ekleme](./media/active-directory-saas-bonus-tutorial/ic781044.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="2ee9c-218">Merhaba üzerinde **Kullanıcı Ekle** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee9c-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="2ee9c-219">![Kullanıcı ekleme](./media/active-directory-saas-bonus-tutorial/ic781045.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="2ee9c-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="2ee9c-220">a.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-220">a.</span></span> <span data-ttu-id="2ee9c-221">Merhaba, **ad** metin kutusuna, hello ilk gibi kullanıcı adını girin **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="2ee9c-222">b.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-222">b.</span></span> <span data-ttu-id="2ee9c-223">Merhaba, **Soyadı** metin kutusuna, hello son gibi kullanıcı adını girin **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="2ee9c-224">c.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-224">c.</span></span> <span data-ttu-id="2ee9c-225">Merhaba, **e-posta** metin kutusuna, bir kullanıcı gibi hello e-posta girin  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2ee9c-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2ee9c-226">d.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-226">d.</span></span> <span data-ttu-id="2ee9c-227">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="2ee9c-228">Hello Azure AD hesap sahibi etkin hale önce bir bağlantı tooconfirm hello hesabını içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2ee9c-229">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="2ee9c-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2ee9c-230">Bu bölümde, erişim tooBonusly vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="2ee9c-232">**tooassign Britta Simon tooBonusly hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee9c-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ee9c-233">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2ee9c-235">Merhaba uygulamalar listesinde **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-235">In hello applications list, select **Bonusly**.</span></span>

    ![Merhaba Bonusly hello uygulamalar listesinde bağlantı](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="2ee9c-237">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="2ee9c-239">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-239">Click **Add** button.</span></span> <span data-ttu-id="2ee9c-240">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="2ee9c-242">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ee9c-243">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ee9c-244">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2ee9c-245">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="2ee9c-245">Test single sign-on</span></span>

<span data-ttu-id="2ee9c-246">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ee9c-247">Merhaba Bonusly kutucuğa tıkladığınızda de erişim paneli Merhaba, otomatik olarak oturum açma tooyour Bonusly uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee9c-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ee9c-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2ee9c-248">Additional resources</span></span>

* [<span data-ttu-id="2ee9c-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2ee9c-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ee9c-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2ee9c-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

