---
title: "Öğretici: Azure Active Directory Tümleştirme ile TOPdesk - genel | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile TOPdesk - genel arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="759a2-103">Öğretici: Azure Active Directory Tümleştirme ile TOPdesk - genel</span><span class="sxs-lookup"><span data-stu-id="759a2-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="759a2-104">Bu öğreticide, bilgi nasıl toointegrate TOPdesk - Azure Active Directory (Azure AD) ile ortak.</span><span class="sxs-lookup"><span data-stu-id="759a2-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="759a2-105">TOPdesk - genel Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="759a2-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="759a2-106">Genel erişim tooTOPdesk - olan Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="759a2-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="759a2-107">Kullanıcıların tooautomatically get açan tooTOPdesk - Azure AD hesaplarına sahip (çoklu oturum açma) ortak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="759a2-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="759a2-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="759a2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="759a2-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="759a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="759a2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="759a2-110">Prerequisites</span></span>

<span data-ttu-id="759a2-111">tooconfigure TOPdesk ile-Azure AD tümleştirme genel, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="759a2-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="759a2-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="759a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="759a2-113">TOPdesk - genel çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="759a2-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="759a2-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="759a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="759a2-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="759a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="759a2-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="759a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="759a2-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="759a2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="759a2-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="759a2-118">Scenario description</span></span>
<span data-ttu-id="759a2-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="759a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="759a2-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="759a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="759a2-121">Ortak hello galerisinden TOPdesk - ekleme</span><span class="sxs-lookup"><span data-stu-id="759a2-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="759a2-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="759a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="759a2-123">Ortak hello galerisinden TOPdesk - ekleme</span><span class="sxs-lookup"><span data-stu-id="759a2-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="759a2-124">TOPdesk - Azure AD'ye ortak tooconfigure hello tümleştirilmesi tooadd TOPdesk - genel hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="759a2-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="759a2-125">**tooadd TOPdesk - hello galerisinden ortak hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="759a2-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="759a2-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="759a2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="759a2-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="759a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="759a2-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="759a2-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="759a2-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="759a2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="759a2-133">Merhaba arama kutusuna yazın **TOPdesk - genel**seçin **TOPdesk - genel** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="759a2-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TOPdesk - genel hello sonuçları listesinde](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="759a2-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="759a2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="759a2-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma TOPdesk ile test etme - genel "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="759a2-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="759a2-137">Çoklu oturum açma toowork, Azure AD tooknow TOPdesk hangi hello karşılık gelen kullanıcı gereken - Azure AD içinde ortak tooa kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="759a2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="759a2-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı TOPdesk - hello arasında bir bağlantı ilişkisi ortak kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="759a2-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="759a2-139">TOPdesk içinde-ortak, Ata hello hello değerini **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="759a2-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="759a2-140">tooconfigure ve Azure AD çoklu oturum açma ile TOPdesk - genel test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="759a2-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="759a2-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="759a2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="759a2-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="759a2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="759a2-143">**[TOPdesk - genel test kullanıcısı oluşturma](#create-a-topdesk---public-test-user)**  - toohave Britta Simon TOPdesk içinde karşılık gelen - kullanıcı bağlantılı toohello Azure AD gösterimidir ortak.</span><span class="sxs-lookup"><span data-stu-id="759a2-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="759a2-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="759a2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="759a2-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="759a2-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="759a2-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="759a2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="759a2-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma, TOPdesk - genel uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="759a2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="759a2-148">**Azure AD çoklu oturum açma tooconfigure TOPdesk ile-ortak hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="759a2-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="759a2-149">Merhaba hello üzerinde Azure portal'ın **TOPdesk - genel** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="759a2-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="759a2-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="759a2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="759a2-153">Merhaba üzerinde **TOPdesk - ortak etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![TOPdesk - ortak etki alanı ve URL'ler tek oturum açma bilgileri](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="759a2-155">a.</span><span class="sxs-lookup"><span data-stu-id="759a2-155">a.</span></span> <span data-ttu-id="759a2-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="759a2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="759a2-157">b.</span><span class="sxs-lookup"><span data-stu-id="759a2-157">b.</span></span> <span data-ttu-id="759a2-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="759a2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="759a2-159">c.</span><span class="sxs-lookup"><span data-stu-id="759a2-159">c.</span></span> <span data-ttu-id="759a2-160">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="759a2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="759a2-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="759a2-161">These values are not real.</span></span> <span data-ttu-id="759a2-162">Bu güncelleştirme tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="759a2-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="759a2-163">Yanıt açıklaması daha sonra öğreticide URL'dir.</span><span class="sxs-lookup"><span data-stu-id="759a2-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="759a2-164">Kişi [TOPdesk - ortak istemci destek ekibi](https://help.topdesk.com/saas/enterprise/user/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="759a2-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="759a2-165">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="759a2-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="759a2-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="759a2-167">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="759a2-169">Merhaba üzerinde **TOPdesk - genel yapılandırması** 'yi tıklatın **TOPdesk - ortak yapılandırma** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="759a2-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="759a2-170">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="759a2-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TOPdesk - genel yapılandırması](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="759a2-172">Tooyour üzerinde oturum **TOPdesk - genel** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="759a2-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="759a2-173">Merhaba, **TOPdesk** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="759a2-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="759a2-174">![Ayarları](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="759a2-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="759a2-175">Tıklatın **oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="759a2-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="759a2-176">![Oturum açma ayarları](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="759a2-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="759a2-177">Merhaba genişletin **oturum açma ayarları** menüsüne ve ardından **genel**.</span><span class="sxs-lookup"><span data-stu-id="759a2-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="759a2-178">![Genel](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "genel")</span><span class="sxs-lookup"><span data-stu-id="759a2-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="759a2-179">Merhaba, **ortak** hello bölümünü **SAML oturum açma** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="759a2-180">![Teknik ayarları](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "teknik ayarları")</span><span class="sxs-lookup"><span data-stu-id="759a2-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="759a2-181">a.</span><span class="sxs-lookup"><span data-stu-id="759a2-181">a.</span></span> <span data-ttu-id="759a2-182">Tıklatın **karşıdan** toodownload hello ortak meta veri dosyası ve bilgisayarınıza yerel olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="759a2-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="759a2-183">b.</span><span class="sxs-lookup"><span data-stu-id="759a2-183">b.</span></span> <span data-ttu-id="759a2-184">İndirilen hello meta veri dosyasını açın ve hello bulun **AssertionConsumerService** düğümü.</span><span class="sxs-lookup"><span data-stu-id="759a2-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="759a2-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="759a2-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="759a2-186">c.</span><span class="sxs-lookup"><span data-stu-id="759a2-186">c.</span></span> <span data-ttu-id="759a2-187">Kopya hello **AssertionConsumerService** değeri, bu değer hello yapıştırın **yanıt URL'si** metin kutusuna **TOPdesk - ortak etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="759a2-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="759a2-188">bir sertifika dosyası toocreate hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="759a2-189">![Sertifika](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "sertifika")</span><span class="sxs-lookup"><span data-stu-id="759a2-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="759a2-190">a.</span><span class="sxs-lookup"><span data-stu-id="759a2-190">a.</span></span> <span data-ttu-id="759a2-191">Açık hello Azure portalından meta veri dosyası indirilir.</span><span class="sxs-lookup"><span data-stu-id="759a2-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="759a2-192">b.</span><span class="sxs-lookup"><span data-stu-id="759a2-192">b.</span></span> <span data-ttu-id="759a2-193">Merhaba genişletin **RoleDescriptor** sahip düğümü bir **xsi: type** , **ssas'nin: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="759a2-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="759a2-194">c.</span><span class="sxs-lookup"><span data-stu-id="759a2-194">c.</span></span> <span data-ttu-id="759a2-195">Merhaba Hello değerini kopyalayın **X509Certificate** düğümü.</span><span class="sxs-lookup"><span data-stu-id="759a2-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="759a2-196">d.</span><span class="sxs-lookup"><span data-stu-id="759a2-196">d.</span></span> <span data-ttu-id="759a2-197">Kopyalanan Kaydet hello **X509Certificate** yerel olarak bilgisayarınızda bir dosyada değeri.</span><span class="sxs-lookup"><span data-stu-id="759a2-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="759a2-198">Merhaba, **ortak** 'yi tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="759a2-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="759a2-199">![SAML oturum açma](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML oturum açma")</span><span class="sxs-lookup"><span data-stu-id="759a2-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="759a2-200">Merhaba üzerinde **SAML Yapılandırması Yardımcısı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="759a2-201">![SAML Yapılandırması Yardımcısı](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Yapılandırması Yardımcısı")</span><span class="sxs-lookup"><span data-stu-id="759a2-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="759a2-202">a.</span><span class="sxs-lookup"><span data-stu-id="759a2-202">a.</span></span> <span data-ttu-id="759a2-203">tooupload indirilen meta verileriniz dosya Azure portalından altında **Federasyon meta verileri**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="759a2-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="759a2-204">b.</span><span class="sxs-lookup"><span data-stu-id="759a2-204">b.</span></span> <span data-ttu-id="759a2-205">altında sertifikanızı dosya tooupload **sertifika (RSA)**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="759a2-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="759a2-206">c.</span><span class="sxs-lookup"><span data-stu-id="759a2-206">c.</span></span> <span data-ttu-id="759a2-207">aldığınız hello TOPdesk destek ekibinden altında tooupload hello logo dosyası **Logo simgesini**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="759a2-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="759a2-208">d.</span><span class="sxs-lookup"><span data-stu-id="759a2-208">d.</span></span> <span data-ttu-id="759a2-209">Merhaba, **kullanıcı adı özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="759a2-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="759a2-210">e.</span><span class="sxs-lookup"><span data-stu-id="759a2-210">e.</span></span> <span data-ttu-id="759a2-211">Merhaba, **görünen adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="759a2-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="759a2-212">f.</span><span class="sxs-lookup"><span data-stu-id="759a2-212">f.</span></span> <span data-ttu-id="759a2-213">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="759a2-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="759a2-214">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="759a2-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="759a2-215">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="759a2-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="759a2-216">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="759a2-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="759a2-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="759a2-217">Create an Azure AD test user</span></span>

<span data-ttu-id="759a2-218">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="759a2-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="759a2-220">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="759a2-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="759a2-221">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="759a2-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="759a2-223">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="759a2-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="759a2-225">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="759a2-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="759a2-227">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="759a2-229">a.</span><span class="sxs-lookup"><span data-stu-id="759a2-229">a.</span></span> <span data-ttu-id="759a2-230">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="759a2-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="759a2-231">b.</span><span class="sxs-lookup"><span data-stu-id="759a2-231">b.</span></span> <span data-ttu-id="759a2-232">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="759a2-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="759a2-233">c.</span><span class="sxs-lookup"><span data-stu-id="759a2-233">c.</span></span> <span data-ttu-id="759a2-234">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="759a2-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="759a2-235">d.</span><span class="sxs-lookup"><span data-stu-id="759a2-235">d.</span></span> <span data-ttu-id="759a2-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="759a2-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="759a2-237">TOPdesk - genel test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="759a2-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="759a2-238">Sipariş tooenable Azure AD kullanıcıların toolog TOPdesk - içine içinde ortak, bunlar sağlanmalıdır TOPdesk - genel.</span><span class="sxs-lookup"><span data-stu-id="759a2-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="759a2-239">TOPdesk - hello durumda ortak, sağlama olduğunu el ile bir görev.</span><span class="sxs-lookup"><span data-stu-id="759a2-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="759a2-240">tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="759a2-241">Tooyour üzerinde oturum **TOPdesk - genel** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="759a2-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="759a2-242">Hello içinde hello üst menüsünde **TOPdesk \> yeni \> destek dosyalarını \> kişi**.</span><span class="sxs-lookup"><span data-stu-id="759a2-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="759a2-243">![Kişi](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "kişi")</span><span class="sxs-lookup"><span data-stu-id="759a2-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="759a2-244">Merhaba yeni bir kişiye iletişim kutusunda hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="759a2-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="759a2-245">![Yeni bir kişiye](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "yeni bir kişiye")</span><span class="sxs-lookup"><span data-stu-id="759a2-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="759a2-246">a.</span><span class="sxs-lookup"><span data-stu-id="759a2-246">a.</span></span> <span data-ttu-id="759a2-247">Merhaba Genel sekmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="759a2-247">Click hello General tab.</span></span>

    <span data-ttu-id="759a2-248">b.</span><span class="sxs-lookup"><span data-stu-id="759a2-248">b.</span></span> <span data-ttu-id="759a2-249">Merhaba, **Soyadı** metin kutusuna, Simon gibi hello kullanıcının soyadını yazın</span><span class="sxs-lookup"><span data-stu-id="759a2-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="759a2-250">c.</span><span class="sxs-lookup"><span data-stu-id="759a2-250">c.</span></span> <span data-ttu-id="759a2-251">Seçin bir **Site** hello hesabı.</span><span class="sxs-lookup"><span data-stu-id="759a2-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="759a2-252">d.</span><span class="sxs-lookup"><span data-stu-id="759a2-252">d.</span></span> <span data-ttu-id="759a2-253">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="759a2-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="759a2-254">Herhangi bir TOPdesk - genel kullanıcı hesabı oluşturma araçlarını veya TOPdesk - genel tooprovision Azure AD kullanıcı hesapları tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="759a2-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="759a2-255">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="759a2-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="759a2-256">Bu bölümde, erişim tooTOPdesk - genel vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="759a2-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="759a2-258">**tooassign Britta Simon tooTOPdesk - genel hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="759a2-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="759a2-259">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="759a2-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="759a2-261">Merhaba uygulamalar listesinde **TOPdesk - genel**.</span><span class="sxs-lookup"><span data-stu-id="759a2-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Merhaba TOPdesk - ortak bağlantı hello uygulamalar listesinde](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="759a2-263">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="759a2-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="759a2-265">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="759a2-265">Click **Add** button.</span></span> <span data-ttu-id="759a2-266">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="759a2-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="759a2-268">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="759a2-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="759a2-269">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="759a2-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="759a2-270">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="759a2-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="759a2-271">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="759a2-271">Test single sign-on</span></span>

<span data-ttu-id="759a2-272">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="759a2-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="759a2-273">Merhaba TOPdesk - tıklattığınızda genel kutucuğu hello erişim paneli, otomatik olarak oturum açma tooyour TOPdesk - genel uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="759a2-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="759a2-274">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="759a2-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="759a2-275">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="759a2-275">Additional resources</span></span>

* [<span data-ttu-id="759a2-276">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="759a2-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="759a2-277">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="759a2-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

