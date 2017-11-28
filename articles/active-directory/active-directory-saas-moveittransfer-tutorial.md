---
title: "Öğretici: Azure Active Directory Tümleştirme MOVEit Transfer - Azure AD Tümleştirmesi ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile MOVEit Transfer - Azure AD tümleştirme arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="e1e00-103">Öğretici: Azure Active Directory Tümleştirme ile MOVEit Transfer - Azure AD tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e1e00-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="e1e00-104">Bu öğreticide, bilgi nasıl toointegrate MOVEit Transfer - Azure Active Directory (Azure AD) ile Azure AD tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="e1e00-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1e00-105">MOVEit Transfer - Azure AD tümleştirme Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1e00-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1e00-106">Erişim tooMOVEit Transfer - Azure AD tümleştirme sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e00-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="e1e00-107">Kullanıcıların tooautomatically get açan tooMOVEit Transfer - Azure AD hesaplarına ile Azure AD tümleştirme (çoklu oturum açma) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e00-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e1e00-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="e1e00-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e1e00-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1e00-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1e00-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1e00-110">Prerequisites</span></span>

<span data-ttu-id="e1e00-111">tooconfigure MOVEit Transfer - Azure AD Tümleştirmesi ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1e00-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="e1e00-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1e00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1e00-113">MOVEit Transfer - Azure AD tümleştirme çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e1e00-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1e00-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1e00-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1e00-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1e00-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1e00-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1e00-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1e00-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1e00-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1e00-118">Scenario description</span></span>
<span data-ttu-id="e1e00-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1e00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1e00-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1e00-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1e00-121">MOVEit Transfer - Azure AD tümleştirme hello galerisinden ekleme</span><span class="sxs-lookup"><span data-stu-id="e1e00-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="e1e00-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1e00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="e1e00-123">MOVEit Transfer - Azure AD tümleştirme hello galerisinden ekleme</span><span class="sxs-lookup"><span data-stu-id="e1e00-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="e1e00-124">tooconfigure hello tümleştirme MOVEit aktarım - Azure AD, Azure AD tümleştirmeye tooadd MOVEit Transfer - yönetilen SaaS uygulamalarının Azure AD tümleştirme hello galeri tooyour listeden gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1e00-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1e00-125">**tooadd MOVEit Transfer - Azure AD tümleştirme hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1e00-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1e00-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="e1e00-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1e00-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="e1e00-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="e1e00-133">Merhaba arama kutusuna yazın **MOVEit Transfer - Azure AD tümleştirme**seçin **MOVEit Transfer - Azure AD tümleştirme** sonuç panelinden ardından **Ekle** düğmesini tooadd hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="e1e00-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![MOVEit Transfer - Azure AD tümleştirme hello sonuçları listesinde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e1e00-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1e00-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e1e00-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma MOVEit Transfer - "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD Tümleştirmesi ile test etme.</span><span class="sxs-lookup"><span data-stu-id="e1e00-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1e00-137">Çoklu oturum açma toowork, Azure AD tooknow MOVEit aktarımı hangi hello karşılık gelen kullanıcı gereken - Azure AD içinde Azure AD tümleştirme tooa kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="e1e00-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="e1e00-138">Diğer bir deyişle, bir bağlantı ilişkisi Azure AD kullanıcısının hello ilgili kullanıcı MOVEit transfer - Azure AD tümleştirme kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1e00-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="e1e00-139">Merhaba hello değeri MOVEit Transfer - Azure AD tümleştirme atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1e00-140">tooconfigure ve Azure AD çoklu oturum açmayı test MOVEit Transfer - Azure AD Tümleştirmesi ile yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1e00-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1e00-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e1e00-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1e00-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e1e00-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1e00-143">**[MOVEit Transfer - Azure AD tümleştirme test kullanıcısı oluşturma](#create-a-moveit-transfer---azure-ad-integration-test-user)**  kullanıcı bağlantılı toohello Azure AD gösterimidir - toohave Britta Simon MOVEit transfer, karşılık gelen - Azure AD tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="e1e00-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1e00-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1e00-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1e00-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e1e00-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e1e00-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e1e00-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e1e00-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, MOVEit Transfer - Azure AD tümleştirme uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="e1e00-148">**tooconfigure Azure AD çoklu oturum açma MOVEit Transfer - Azure AD Tümleştirmesi ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1e00-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1e00-149">Merhaba hello üzerinde Azure portal'ın **MOVEit Transfer - Azure AD tümleştirme** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="e1e00-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e1e00-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="e1e00-153">Merhaba üzerinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1e00-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="e1e00-155">a.</span><span class="sxs-lookup"><span data-stu-id="e1e00-155">a.</span></span> <span data-ttu-id="e1e00-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="e1e00-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="e1e00-157">b.</span><span class="sxs-lookup"><span data-stu-id="e1e00-157">b.</span></span> <span data-ttu-id="e1e00-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="e1e00-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="e1e00-159">c.</span><span class="sxs-lookup"><span data-stu-id="e1e00-159">c.</span></span> <span data-ttu-id="e1e00-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="e1e00-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="e1e00-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e1e00-161">These values are not real.</span></span> <span data-ttu-id="e1e00-162">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="e1e00-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e1e00-163">Bu değerleri daha sonra da başvurabilir **servis sağlayıcı meta verileri URL'sini** bölüm veya kişi [MOVEit Transfer - Azure AD tümleştirme istemci destek ekibi](https://community.ipswitch.com/s/support) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="e1e00-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="e1e00-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1e00-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="e1e00-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-166">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="e1e00-168">Üzerinde tooyour MOVEit aktarımı Kiracı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="e1e00-169">Merhaba sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Ayarları bölümü üzerinde uygulama yan](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="e1e00-171">Tıklatın **tek oturum açma** altındaki bağlantı **kullanıcı kimlik doğrulama -> güvenlik ilkelerini**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Güvenlik ilkeleri üzerinde uygulama yan](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="e1e00-173">Merhaba meta veri URL'sini bağlantı toodownload hello meta veri belgesi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![Hizmet sağlayıcısı meta veri URL'si](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="e1e00-175">Doğrulayın **Entityıd** eşleşen **tanımlayıcısı** hello içinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e1e00-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="e1e00-176">Doğrulayın **AssertionConsumerService** konumu URL ile eşleşip **yanıt URL'si** hello içinde **MOVEit aktarım - Azure AD tümleştirme etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e1e00-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="e1e00-178">Tıklatın **kimlik sağlayıcı Ekle** tooadd yeni bir Federasyon kimlik sağlayıcısı düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Kimlik sağlayıcısı ekleyin](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="e1e00-180">Tıklatın **Gözat...**  tooselect hello Azure Portalı'ndan indirilen meta veri dosyası ve ardından **kimlik sağlayıcı Ekle** tooupload hello indirilen dosya.</span><span class="sxs-lookup"><span data-stu-id="e1e00-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![SAML kimlik sağlayıcısı](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="e1e00-182">Seçin "**Evet**" olarak **etkin** hello içinde **federe kimlik sağlayıcı ayarları Düzenle...**  sayfasında ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Federe kimlik sağlayıcı ayarları](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="e1e00-184">Merhaba, **federe kimlik sağlayıcısı kullanıcı ayarlarını Düzenle** sayfasında, hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1e00-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Federe kimlik sağlayıcı ayarları Düzenle](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="e1e00-186">a.</span><span class="sxs-lookup"><span data-stu-id="e1e00-186">a.</span></span> <span data-ttu-id="e1e00-187">Seçin **SAML NameID** olarak **oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="e1e00-188">b.</span><span class="sxs-lookup"><span data-stu-id="e1e00-188">b.</span></span> <span data-ttu-id="e1e00-189">Seçin **diğer** olarak **tam adı** ve hello **öznitelik adı** textbox hello değeri koyun: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="e1e00-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="e1e00-190">c.</span><span class="sxs-lookup"><span data-stu-id="e1e00-190">c.</span></span> <span data-ttu-id="e1e00-191">Seçin **diğer** olarak **e-posta** ve hello **öznitelik adı** textbox hello değeri koyun: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="e1e00-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="e1e00-192">d.</span><span class="sxs-lookup"><span data-stu-id="e1e00-192">d.</span></span> <span data-ttu-id="e1e00-193">Seçin **Evet** olarak **oturum açma hesabı otomatik olarak oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="e1e00-194">e.</span><span class="sxs-lookup"><span data-stu-id="e1e00-194">e.</span></span> <span data-ttu-id="e1e00-195">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="e1e00-196">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1e00-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1e00-197">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e1e00-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1e00-198">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1e00-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e1e00-199">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1e00-199">Create an Azure AD test user</span></span>

<span data-ttu-id="e1e00-200">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1e00-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="e1e00-202">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1e00-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1e00-203">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e1e00-205">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e1e00-207">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e1e00-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e1e00-209">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1e00-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e1e00-211">a.</span><span class="sxs-lookup"><span data-stu-id="e1e00-211">a.</span></span> <span data-ttu-id="e1e00-212">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1e00-213">b.</span><span class="sxs-lookup"><span data-stu-id="e1e00-213">b.</span></span> <span data-ttu-id="e1e00-214">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e1e00-215">c.</span><span class="sxs-lookup"><span data-stu-id="e1e00-215">c.</span></span> <span data-ttu-id="e1e00-216">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="e1e00-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e1e00-217">d.</span><span class="sxs-lookup"><span data-stu-id="e1e00-217">d.</span></span> <span data-ttu-id="e1e00-218">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1e00-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="e1e00-219">MOVEit Transfer - Azure AD tümleştirme test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1e00-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="e1e00-220">Bu bölümde Hello amacı toocreate Britta Simon MOVEit Transfer - Azure AD tümleştirme adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="e1e00-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="e1e00-221">MOVEit Transfer - Azure AD tümleştirme yalnızca zaman sağlama, hangi etkinleştirdiğiniz destekler.</span><span class="sxs-lookup"><span data-stu-id="e1e00-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="e1e00-222">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e1e00-222">There is no action item for you in this section.</span></span> <span data-ttu-id="e1e00-223">Yeni bir kullanıcı bir girişim tooaccess MOVEit Transfer - henüz yoksa Azure AD tümleştirme sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1e00-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e1e00-224">Toocreate kullanıcı el ile gerekiyorsa, toocontact hello gereksinim [MOVEit Transfer - Azure AD tümleştirme istemci destek ekibi](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="e1e00-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e1e00-225">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="e1e00-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e1e00-226">Bu bölümde, erişim tooMOVEit Transfer - Azure AD tümleştirme vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1e00-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="e1e00-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD tümleştirme hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1e00-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1e00-229">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1e00-231">Merhaba uygulamalar listesinde **MOVEit Transfer - Azure AD tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Merhaba MOVEit Transfer - Azure AD tümleştirme bağlantı hello uygulamalar listesinde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="e1e00-233">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1e00-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="e1e00-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1e00-235">Click **Add** button.</span></span> <span data-ttu-id="e1e00-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1e00-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="e1e00-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1e00-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1e00-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1e00-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1e00-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1e00-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e1e00-241">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="e1e00-241">Test single sign-on</span></span>

<span data-ttu-id="e1e00-242">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD SSO yapılandırmayı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e1e00-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1e00-243">Merhaba MOVEit Transfer - Azure AD tümleştirme kutucuğuna tıkladığınızda hello erişim paneli, otomatik olarak oturum açma tooyour MOVEit Transfer - Azure AD tümleştirme uygulaması almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1e00-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e1e00-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1e00-244">Additional resources</span></span>

* [<span data-ttu-id="e1e00-245">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e1e00-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1e00-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1e00-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

