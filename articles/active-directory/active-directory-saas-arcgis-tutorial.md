---
title: "Öğretici: Azure Active Directory Tümleştirme ArcGIS Online ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ArcGIS Online arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="e4a49-103">Öğretici: Azure Active Directory Tümleştirme ArcGIS Online ile</span><span class="sxs-lookup"><span data-stu-id="e4a49-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="e4a49-104">Bu öğreticide, bilgi nasıl toointegrate ArcGIS çevrimiçi Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e4a49-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4a49-105">ArcGIS çevrimiçi Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e4a49-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e4a49-106">Erişim tooArcGIS çevrimiçi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e4a49-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="e4a49-107">Kullanıcıların tooautomatically get açan tooArcGIS çevrimiçi (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e4a49-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4a49-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e4a49-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e4a49-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e4a49-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="e4a49-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e4a49-110">Prerequisites</span></span>

<span data-ttu-id="e4a49-111">tooconfigure ArcGIS Online ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4a49-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="e4a49-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e4a49-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4a49-113">Bir ArcGIS çevrimiçi çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e4a49-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4a49-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e4a49-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4a49-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4a49-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4a49-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e4a49-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4a49-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4a49-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4a49-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e4a49-118">Scenario description</span></span>
<span data-ttu-id="e4a49-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e4a49-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4a49-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e4a49-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4a49-121">ArcGIS çevrimiçi hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e4a49-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="e4a49-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e4a49-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="e4a49-123">ArcGIS çevrimiçi hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e4a49-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="e4a49-124">Azure AD'ye tooconfigure hello tümleştirme ArcGIS Online hello galeri tooyour yönetilen SaaS uygulamaları listesinden ArcGIS çevrimiçi tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4a49-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e4a49-125">**tooadd ArcGIS çevrimiçi hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e4a49-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4a49-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4a49-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e4a49-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e4a49-131">Tıklatın **yeni uygulama** hello iletişim tooadd yeni uygulamanın hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e4a49-133">Merhaba arama kutusuna yazın **ArcGIS çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="e4a49-135">Merhaba Sonuçlar panelinde seçin **ArcGIS çevrimiçi**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e4a49-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4a49-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e4a49-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4a49-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma ArcGIS "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Online ile test etme</span><span class="sxs-lookup"><span data-stu-id="e4a49-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e4a49-139">Tek toowork'ın oturum açma hangi hello karşılık gelen ArcGIS çevrimiçi tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4a49-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="e4a49-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ArcGIS çevrimiçi hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4a49-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="e4a49-141">Bu bağlantı ilişkisi hello hello değerini atayarak kurulur **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** ArcGIS çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="e4a49-142">tooconfigure ve ArcGIS Online ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4a49-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e4a49-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="e4a49-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e4a49-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="e4a49-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4a49-145">**[ArcGIS çevrimiçi bir test kullanıcısı oluşturma](#creating-an-arcgis-online-test-user) ** -toohave Britta Simon ArcGIS bağlantılı toohello Azure AD kullanıcı gösterimi olan Online'da, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="e4a49-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4a49-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e4a49-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4a49-147">**[Çoklu oturum açmayı test](#testing-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="e4a49-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4a49-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e4a49-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4a49-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ArcGIS çevrimiçi uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e4a49-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="e4a49-150">**tooconfigure Azure AD çoklu oturum açma ArcGIS Online ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e4a49-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4a49-151">Hello hello üzerinde Azure portal'ın **ArcGIS çevrimiçi** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e4a49-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e4a49-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="e4a49-155">Merhaba üzerinde **ArcGIS çevrimiçi etki alanı ve URL'leri** bölümünde, adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4a49-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="e4a49-157">Merhaba, **oturum açma URL'si** metin kutusuna, desen aşağıdaki hello kullanarak türü hello değeri:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="e4a49-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e4a49-158">Bu değer hello gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="e4a49-158">This value is not hello real.</span></span> <span data-ttu-id="e4a49-159">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="e4a49-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e4a49-160">Kişi [ArcGIS çevrimiçi istemci destek ekibi](http://support.esri.com/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="e4a49-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="e4a49-161">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e4a49-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="e4a49-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4a49-165">Farklı web tarayıcısı penceresinde ArcGIS şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e4a49-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="e4a49-166">Tıklatın **ayarları düzenleme**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="e4a49-167">![Ayarları Düzenle](./media/active-directory-saas-arcgis-tutorial/ic784742.png "ayarlarını Düzenle")</span><span class="sxs-lookup"><span data-stu-id="e4a49-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="e4a49-168">Tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-168">Click **Security**.</span></span>

    <span data-ttu-id="e4a49-169">![Güvenlik](./media/active-directory-saas-arcgis-tutorial/ic784743.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="e4a49-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="e4a49-170">Altında **Kurumsal oturum açma bilgileri**, tıklatın **AYARLANMIŞ kimlik sağlayıcı**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="e4a49-171">![Kurumsal oturum açma bilgileri](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Kurumsal oturum açmalar")</span><span class="sxs-lookup"><span data-stu-id="e4a49-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="e4a49-172">Merhaba üzerinde **ayarlanmış kimlik sağlayıcı** yapılandırma sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4a49-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e4a49-173">![Kimlik sağlayıcısı ayarlamak](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ayarlamak kimlik sağlayıcısı")</span><span class="sxs-lookup"><span data-stu-id="e4a49-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="e4a49-174">a.</span><span class="sxs-lookup"><span data-stu-id="e4a49-174">a.</span></span> <span data-ttu-id="e4a49-175">Merhaba, **adı** metin kutusuna, kuruluşunuzun adını yazın.</span><span class="sxs-lookup"><span data-stu-id="e4a49-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="e4a49-176">b.</span><span class="sxs-lookup"><span data-stu-id="e4a49-176">b.</span></span> <span data-ttu-id="e4a49-177">İçin **hello Kurumsal kimlik sağlayıcısı meta verileri sağlanan kullanarak**seçin **dosya**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="e4a49-178">c.</span><span class="sxs-lookup"><span data-stu-id="e4a49-178">c.</span></span> <span data-ttu-id="e4a49-179">tooupload, indirilen meta veri dosyası tıklatın **dosya**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="e4a49-180">d.</span><span class="sxs-lookup"><span data-stu-id="e4a49-180">d.</span></span> <span data-ttu-id="e4a49-181">Tıklatın **KÜMESİ kimlik SAĞLAYICISI**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="e4a49-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e4a49-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e4a49-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="e4a49-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e4a49-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e4a49-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4a49-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a49-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4a49-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="e4a49-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e4a49-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e4a49-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4a49-189">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4a49-191">Çok Git**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** toodisplay hello kullanıcılar listesi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4a49-193">Merhaba hello iletişim üstündeki **Ekle** tooopen hello **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e4a49-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4a49-195">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4a49-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4a49-197">a.</span><span class="sxs-lookup"><span data-stu-id="e4a49-197">a.</span></span> <span data-ttu-id="e4a49-198">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4a49-199">b.</span><span class="sxs-lookup"><span data-stu-id="e4a49-199">b.</span></span> <span data-ttu-id="e4a49-200">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** Britta Simon biri.</span><span class="sxs-lookup"><span data-stu-id="e4a49-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="e4a49-201">c.</span><span class="sxs-lookup"><span data-stu-id="e4a49-201">c.</span></span> <span data-ttu-id="e4a49-202">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e4a49-203">d.</span><span class="sxs-lookup"><span data-stu-id="e4a49-203">d.</span></span> <span data-ttu-id="e4a49-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e4a49-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="e4a49-205">ArcGIS çevrimiçi bir test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4a49-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="e4a49-206">İçine ArcGIS çevrimiçi sipariş tooenable Azure AD kullanıcıların toolog bunlar ArcGIS çevrimiçi sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e4a49-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="e4a49-207">ArcGIS Online Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e4a49-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="e4a49-208">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e4a49-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4a49-209">İçinde tooyour oturum **ArcGIS** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="e4a49-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="e4a49-210">Tıklatın **üye davet et**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="e4a49-211">![Üye davet](./media/active-directory-saas-arcgis-tutorial/ic784747.png "üye davet")</span><span class="sxs-lookup"><span data-stu-id="e4a49-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="e4a49-212">Seçin **üye otomatik olarak bir e-posta göndermeden eklemek**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="e4a49-213">![Üyeler otomatik olarak Ekle](./media/active-directory-saas-arcgis-tutorial/ic784748.png "üyeleri otomatik olarak Ekle")</span><span class="sxs-lookup"><span data-stu-id="e4a49-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="e4a49-214">Merhaba üzerinde **üyeleri** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e4a49-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="e4a49-215">![Ekleme ve gözden](./media/active-directory-saas-arcgis-tutorial/ic784749.png "ekleme ve gözden geçirme")</span><span class="sxs-lookup"><span data-stu-id="e4a49-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="e4a49-216">a.</span><span class="sxs-lookup"><span data-stu-id="e4a49-216">a.</span></span> <span data-ttu-id="e4a49-217">Merhaba girin **e-posta**, **ad**, ve **Soyadı** tooprovision istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="e4a49-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="e4a49-218">b.</span><span class="sxs-lookup"><span data-stu-id="e4a49-218">b.</span></span> <span data-ttu-id="e4a49-219">Tıklatın **ekleme ve gözden geçirme**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="e4a49-220">Girdiğiniz ve ardından hello verileri gözden **ADD MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="e4a49-221">![Üye Ekle](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Üye Ekle")</span><span class="sxs-lookup"><span data-stu-id="e4a49-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="e4a49-222">Hello Azure Active Directory hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin.</span><span class="sxs-lookup"><span data-stu-id="e4a49-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e4a49-223">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e4a49-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e4a49-224">Bu bölümde, çevrimiçi erişim tooArcGIS vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e4a49-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e4a49-226">**tooassign çevrimiçi Britta Simon tooArcGIS hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e4a49-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4a49-227">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e4a49-229">Merhaba uygulamalar listesinde **ArcGIS çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="e4a49-231">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e4a49-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e4a49-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e4a49-233">Click **Add** button.</span></span> <span data-ttu-id="e4a49-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e4a49-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e4a49-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e4a49-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e4a49-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e4a49-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4a49-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e4a49-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4a49-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e4a49-239">Testing single sign-on</span></span>

<span data-ttu-id="e4a49-240">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e4a49-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e4a49-241">Merhaba ArcGIS çevrimiçi hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ArcGIS çevrimiçi uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4a49-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="e4a49-242">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e4a49-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4a49-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e4a49-243">Additional resources</span></span>

* [<span data-ttu-id="e4a49-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e4a49-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4a49-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e4a49-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

