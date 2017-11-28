---
title: "Öğretici: Azure Active Directory Tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile algısına Amerika Birleşik Devletleri (Non-UltiPro) arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="fe2fa-103">Öğretici: Azure Active Directory Tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile</span><span class="sxs-lookup"><span data-stu-id="fe2fa-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="fe2fa-104">Bu öğreticide, bilgi nasıl toointegrate Azure Active Directory (Azure AD) ile algısına Amerika Birleşik Devletleri (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="fe2fa-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe2fa-105">Algısına Amerika Birleşik Devletleri (Non-UltiPro) Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fe2fa-106">Erişim tooPerception Amerika Birleşik Devletleri (UltiPro olmayan) sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="fe2fa-107">Kullanıcıların tooautomatically get açan tooPerception Amerika Birleşik Devletleri (Non-UltiPro) (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fe2fa-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fe2fa-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe2fa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe2fa-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe2fa-110">Prerequisites</span></span>

<span data-ttu-id="fe2fa-111">Azure AD tümleştirmesi algısına Amerika Birleşik Devletleri (Non-UltiPro) ile tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="fe2fa-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fe2fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe2fa-113">Bir algısına Amerika Birleşik Devletleri (Non-UltiPro) çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fe2fa-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe2fa-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe2fa-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe2fa-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe2fa-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe2fa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe2fa-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fe2fa-118">Scenario description</span></span>
<span data-ttu-id="fe2fa-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe2fa-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe2fa-121">Merhaba Galerisi'nden algısına Amerika Birleşik Devletleri (Non-UltiPro) ekleme</span><span class="sxs-lookup"><span data-stu-id="fe2fa-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="fe2fa-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fe2fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="fe2fa-123">Merhaba Galerisi'nden algısına Amerika Birleşik Devletleri (Non-UltiPro) ekleme</span><span class="sxs-lookup"><span data-stu-id="fe2fa-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="fe2fa-124">tooconfigure hello tümleştirmesi algısına Amerika Birleşik Devletleri (UltiPro olmayan), Azure AD'ye hello galeri tooyour listesinden yönetilen SaaS uygulamaları tooadd algısına Amerika Birleşik Devletleri (Non-UltiPro) gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fe2fa-125">**tooadd hello galerisinden algısına Amerika Birleşik Devletleri (Non-UltiPro) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fe2fa-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe2fa-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="fe2fa-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fe2fa-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="fe2fa-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="fe2fa-133">Merhaba arama kutusuna yazın **algısına Amerika Birleşik Devletleri (Non-UltiPro)**seçin **algısına Amerika Birleşik Devletleri (Non-UltiPro)** sonuç panelinden ardından **Ekle** düğmesi tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde algısına Amerika Birleşik Devletleri (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fe2fa-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fe2fa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fe2fa-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ile algısına "Britta Simon" adlı bir test kullanıcı tabanlı ABD (UltiPro olmayan) test etme.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe2fa-137">Tek toowork'ın oturum açma hangi hello karşılık gelen algısına Amerika Birleşik Devletleri (Non-UltiPro) içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="fe2fa-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve hello ilgili kullanıcı algısına Amerika Birleşik Devletleri (Non-UltiPro) içinde arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="fe2fa-139">Merhaba hello değerini algısına Amerika Birleşik Devletleri (UltiPro olmayan), Ata **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fe2fa-140">tooconfigure ve test algısına Amerika Birleşik Devletleri (Non-UltiPro) ile Azure AD çoklu oturum açma, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fe2fa-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fe2fa-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe2fa-143">**[Algısına Amerika Birleşik Devletleri (Non-UltiPro) test kullanıcısı oluşturma](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave Britta Simon içinde algısına bağlantılı toohello Azure AD kullanıcı gösterimi olan ABD (UltiPro olmayan), karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe2fa-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe2fa-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fe2fa-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fe2fa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fe2fa-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="fe2fa-148">**tooconfigure Azure AD çoklu oturum açma algısına Amerika Birleşik Devletleri (Non-UltiPro) ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fe2fa-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="fe2fa-149">Merhaba hello üzerinde Azure portal'ın **algısına Amerika Birleşik Devletleri (Non-UltiPro)** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="fe2fa-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="fe2fa-153">Merhaba üzerinde **algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="fe2fa-155">a.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-155">a.</span></span> <span data-ttu-id="fe2fa-156">Merhaba, **tanımlayıcısı** metin kutusuna, türü hello URL'si:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="fe2fa-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="fe2fa-157">b.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-157">b.</span></span> <span data-ttu-id="fe2fa-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="fe2fa-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fe2fa-159">Merhaba değeri gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-159">hello value is not real.</span></span> <span data-ttu-id="fe2fa-160">Merhaba değeri hello öğreticinin ilerleyen bölümlerinde açıklanan hello gerçek yanıt URL ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="fe2fa-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="fe2fa-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-163">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fe2fa-165">Merhaba üzerinde **algısına Amerika Birleşik Devletleri (Non-UltiPro) yapılandırma** 'yi tıklatın **yapılandırma algısına Amerika Birleşik Devletleri (Non-UltiPro)** tooopen **yapılandırma oturum açma** penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fe2fa-166">Kopya hello **SAML varlık kimliği** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fe2fa-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="fe2fa-167">a.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-167">a.</span></span> <span data-ttu-id="fe2fa-168">Merhaba **algısına Amerika Birleşik Devletleri (Non-UltiPro)** uygulama gerektirir hello **SAML varlık kimliği** kopyaladığınız, değer toobe URI kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="fe2fa-169">tooget hello kodlanmış URI değeri, kullanım hello aşağıdaki bağlantıda:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="fe2fa-170">b.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-170">b.</span></span> <span data-ttu-id="fe2fa-171">Merhaba URI edindikten sonra kodlanmış değeri birleştirmek, ile Merhaba **yanıt URL'si** aşağıdaki - belirtildiği gibi</span><span class="sxs-lookup"><span data-stu-id="fe2fa-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="fe2fa-172">c.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-172">c.</span></span> <span data-ttu-id="fe2fa-173">Merhaba değerinde yukarıda Yapıştır hello **yanıt URL'si** metin kutusuna **algısına Amerika Birleşik Devletleri (UltiPro olmayan) etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) yapılandırma](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="fe2fa-175">Başka bir tarayıcı penceresinde tooyour algısına Amerika Birleşik Devletleri (Non-UltiPro) şirket sitesinde yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="fe2fa-176">Merhaba ana araç çubuğunda **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Algısına Amerika Birleşik Devletleri (Non-UltiPro) kullanıcı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="fe2fa-178">Merhaba üzerinde **hesap ayarlarını** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Algısına Amerika Birleşik Devletleri (Non-UltiPro) kullanıcı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="fe2fa-180">a.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-180">a.</span></span> <span data-ttu-id="fe2fa-181">Merhaba, **şirket adı** metin kutusuna, tür hello hello adını **şirket**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="fe2fa-182">b.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-182">b.</span></span> <span data-ttu-id="fe2fa-183">Merhaba, **hesap adı** metin kutusuna, tür hello hello adını **hesap**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="fe2fa-184">c.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-184">c.</span></span> <span data-ttu-id="fe2fa-185">İçinde **varsayılan yanıt-tooEmail** metin kutusu, geçerli tür hello **e-posta**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="fe2fa-186">d.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-186">d.</span></span> <span data-ttu-id="fe2fa-187">Seçin **SSO kimlik sağlayıcısı** olarak **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="fe2fa-188">Merhaba üzerinde **SSO yapılandırma** sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Algısına Amerika Birleşik Devletleri (UltiPro olmayan) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="fe2fa-190">a.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-190">a.</span></span> <span data-ttu-id="fe2fa-191">Seçin **SAML NameID türü** olarak **e-posta**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="fe2fa-192">b.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-192">b.</span></span> <span data-ttu-id="fe2fa-193">Merhaba, **SSO yapılandırma adı** metin kutusuna, tür hello adını, **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="fe2fa-194">c.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-194">c.</span></span> <span data-ttu-id="fe2fa-195">İçinde **kimlik sağlayıcı adı** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="fe2fa-196">d.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-196">d.</span></span> <span data-ttu-id="fe2fa-197">İçinde **SAML etki alanı metin kutusu**, gibi hello etki alanını girin  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fe2fa-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="fe2fa-198">e.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-198">e.</span></span> <span data-ttu-id="fe2fa-199">Tıklayın **yeniden karşıya** tooupload hello **meta veri XML** dosya.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="fe2fa-200">f.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-200">f.</span></span> <span data-ttu-id="fe2fa-201">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="fe2fa-202">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fe2fa-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fe2fa-203">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fe2fa-204">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe2fa-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fe2fa-205">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe2fa-205">Create an Azure AD test user</span></span>

<span data-ttu-id="fe2fa-206">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="fe2fa-208">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fe2fa-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe2fa-209">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fe2fa-211">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fe2fa-213">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fe2fa-215">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fe2fa-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fe2fa-217">a.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-217">a.</span></span> <span data-ttu-id="fe2fa-218">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe2fa-219">b.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-219">b.</span></span> <span data-ttu-id="fe2fa-220">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fe2fa-221">c.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-221">c.</span></span> <span data-ttu-id="fe2fa-222">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fe2fa-223">d.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-223">d.</span></span> <span data-ttu-id="fe2fa-224">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="fe2fa-225">Algısına Amerika Birleşik Devletleri (Non-UltiPro) test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe2fa-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="fe2fa-226">Bu bölümde, Britta Simon algısına Amerika Birleşik Devletleri (Non-UltiPro) adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="fe2fa-227">Çalışmak [algısına Amerika Birleşik Devletleri (Non-UltiPro) destek ekibi](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello kullanıcılar hello algısına Amerika Birleşik Devletleri (Non-UltiPro) Platform.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fe2fa-228">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="fe2fa-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fe2fa-229">Bu bölümde, erişim tooPerception Amerika Birleşik Devletleri (Non-UltiPro) vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="fe2fa-231">**tooassign Britta Simon tooPerception Amerika Birleşik Devletleri (Non-UltiPro) hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fe2fa-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="fe2fa-232">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fe2fa-234">Merhaba uygulamalar listesinde **algısına Amerika Birleşik Devletleri (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![Merhaba uygulamalar listesinde Hello algısına Amerika Birleşik Devletleri (Non-UltiPro) bağlantısı](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="fe2fa-236">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="fe2fa-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-238">Click **Add** button.</span></span> <span data-ttu-id="fe2fa-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="fe2fa-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fe2fa-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe2fa-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fe2fa-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="fe2fa-244">Test single sign-on</span></span>

<span data-ttu-id="fe2fa-245">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fe2fa-246">Merhaba algısına Amerika Birleşik Devletleri (Non-UltiPro) hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma algısına Amerika Birleşik Devletleri (UltiPro olmayan) uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe2fa-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="fe2fa-247">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe2fa-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fe2fa-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fe2fa-248">Additional resources</span></span>

* [<span data-ttu-id="fe2fa-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fe2fa-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe2fa-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fe2fa-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

