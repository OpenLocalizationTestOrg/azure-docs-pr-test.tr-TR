---
title: "Öğretici: Azure Active Directory Tümleştirme ile AppDynamics | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile AppDynamics arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="fbbd8-103">Öğretici: Azure Active Directory Tümleştirme AppDynamics ile</span><span class="sxs-lookup"><span data-stu-id="fbbd8-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="fbbd8-104">Bu öğreticide, bilgi nasıl toointegrate AppDynamics Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbbd8-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbbd8-105">AppDynamics Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbbd8-106">Erişim tooAppDynamics sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fbbd8-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="fbbd8-107">Kullanıcıların tooautomatically get açan tooAppDynamics (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="fbbd8-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbbd8-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="fbbd8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fbbd8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbbd8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbbd8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fbbd8-110">Prerequisites</span></span>

<span data-ttu-id="fbbd8-111">tooconfigure AppDynamics ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="fbbd8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="fbbd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbbd8-113">Bir AppDynamics çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="fbbd8-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbbd8-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbbd8-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbbd8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbbd8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbbd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbbd8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="fbbd8-118">Scenario description</span></span>
<span data-ttu-id="fbbd8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbbd8-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbbd8-121">Merhaba Galerisi'nden AppDynamics ekleme</span><span class="sxs-lookup"><span data-stu-id="fbbd8-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="fbbd8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fbbd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="fbbd8-123">Merhaba Galerisi'nden AppDynamics ekleme</span><span class="sxs-lookup"><span data-stu-id="fbbd8-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="fbbd8-124">Azure AD'ye tooconfigure hello tümleştirme AppDynamics, tooadd AppDynamics hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbbd8-125">**tooadd AppDynamics hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbbd8-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbd8-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbbd8-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbbd8-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="fbbd8-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="fbbd8-133">Merhaba arama kutusuna yazın **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-133">In hello search box, type **AppDynamics**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="fbbd8-135">Merhaba Sonuçlar panelinde seçin **AppDynamics**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbbd8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="fbbd8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbbd8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı AppDynamics ile test etme</span><span class="sxs-lookup"><span data-stu-id="fbbd8-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fbbd8-139">Tek toowork'ın oturum açma hangi hello karşılık gelen AppDynamics içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="fbbd8-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı AppDynamics hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="fbbd8-141">Merhaba hello değeri AppDynamics içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fbbd8-142">tooconfigure ve AppDynamics ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbbd8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbbd8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbbd8-145">**[Bir AppDynamics test kullanıcısı oluşturma](#creating-an-appdynamics-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir AppDynamics içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbbd8-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbbd8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbbd8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbbd8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbbd8-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma AppDynamics uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="fbbd8-150">**tooconfigure Azure AD çoklu oturum açma ile AppDynamics, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbbd8-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbd8-151">Hello hello üzerinde Azure portal'ın **AppDynamics** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="fbbd8-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="fbbd8-155">Merhaba üzerinde **AppDynamics etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="fbbd8-157">a.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-157">a.</span></span> <span data-ttu-id="fbbd8-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="fbbd8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="fbbd8-159">b.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-159">b.</span></span> <span data-ttu-id="fbbd8-160">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="fbbd8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbbd8-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-161">These values are not real.</span></span> <span data-ttu-id="fbbd8-162">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fbbd8-163">Kişi [AppDynamics istemci destek ekibi](https://www.appdynamics.com/support/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="fbbd8-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="fbbd8-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbbd8-168">Merhaba üzerinde **AppDynamics yapılandırma** 'yi tıklatın **yapılandırma AppDynamics** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbbd8-169">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="fbbd8-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="fbbd8-171">Farklı web tarayıcısı penceresinde tooyour AppDynamics şirket sitede yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="fbbd8-172">Merhaba üstte Hello araç çubuğunda **ayarları**ve ardından **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="fbbd8-173">![Yönetim](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="fbbd8-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="fbbd8-174">Merhaba tıklatın **kimlik doğrulama sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="fbbd8-175">![Kimlik doğrulama sağlayıcısı](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "kimlik doğrulama sağlayıcısı")</span><span class="sxs-lookup"><span data-stu-id="fbbd8-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="fbbd8-176">Merhaba, **kimlik doğrulama sağlayıcısı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fbbd8-177">![SAML Yapılandırması](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="fbbd8-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="fbbd8-178">a.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-178">a.</span></span> <span data-ttu-id="fbbd8-179">Olarak **kimlik doğrulama sağlayıcısı**seçin **SAML**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="fbbd8-180">b.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-180">b.</span></span> <span data-ttu-id="fbbd8-181">Merhaba, **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fbbd8-182">c.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-182">c.</span></span> <span data-ttu-id="fbbd8-183">Merhaba, **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="fbbd8-184">d.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-184">d.</span></span> <span data-ttu-id="fbbd8-185">Base-64 kodlanmış sertifikanızı kopyalama hello panonuza bunu içerik Not Defteri'nde açın ve toohello yapıştırın **sertifika** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="fbbd8-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="fbbd8-186">e.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-186">e.</span></span> <span data-ttu-id="fbbd8-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-187">Click **Save**.</span></span>

     <span data-ttu-id="fbbd8-188">![Kaydet](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Kaydet")</span><span class="sxs-lookup"><span data-stu-id="fbbd8-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="fbbd8-189">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="fbbd8-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbbd8-190">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbbd8-191">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbbd8-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbbd8-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbbd8-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbbd8-193">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="fbbd8-195">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbbd8-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbd8-196">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbbd8-198">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbbd8-200">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbbd8-202">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbbd8-204">a.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-204">a.</span></span> <span data-ttu-id="fbbd8-205">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbbd8-206">b.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-206">b.</span></span> <span data-ttu-id="fbbd8-207">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbbd8-208">c.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-208">c.</span></span> <span data-ttu-id="fbbd8-209">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fbbd8-210">d.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-210">d.</span></span> <span data-ttu-id="fbbd8-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="fbbd8-212">Bir AppDynamics test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbbd8-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="fbbd8-213">tooenable Azure AD kullanıcıların toolog tooAppDynamics bunların AppDynamics sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="fbbd8-214">AppDynamics Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="fbbd8-215">**tooconfigure kullanıcı hazırlama, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbbd8-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbd8-216">İçinde tooyour AppDynamics şirket site yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="fbbd8-217">Çok Git**kullanıcılar**ve ardından  **+**  tooopen hello **kullanıcı oluştur** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="fbbd8-218">![Kullanıcıların](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="fbbd8-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="fbbd8-219">Merhaba, **kullanıcı oluştur** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fbbd8-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fbbd8-220">![Kullanıcı oluşturma](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="fbbd8-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="fbbd8-221">a.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-221">a.</span></span> <span data-ttu-id="fbbd8-222">Türü hello **kullanıcıadı**, **adı**, **e-posta**, **yeni parola**, **yineleyin yeni parola** geçerli bir AAD, Hesap hello tooprovision istiyorsanız ilgili metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="fbbd8-223">b.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-223">b.</span></span> <span data-ttu-id="fbbd8-224">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="fbbd8-225">API'leri, Azure AD kullanıcı hesapları AppDynamics tooprovision tarafından sağlanan veya herhangi diğer AppDynamics kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fbbd8-226">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="fbbd8-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fbbd8-227">Bu bölümde, erişim tooAppDynamics vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="fbbd8-229">**tooassign Britta Simon tooAppDynamics hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="fbbd8-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbbd8-230">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="fbbd8-232">Merhaba uygulamalar listesinde **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="fbbd8-234">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="fbbd8-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-236">Click **Add** button.</span></span> <span data-ttu-id="fbbd8-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="fbbd8-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbbd8-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbbd8-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbbd8-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="fbbd8-242">Testing single sign-on</span></span>

<span data-ttu-id="fbbd8-243">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbbd8-244">Hello erişim paneli AppDynamics döşeme hello tıkladığınızda, otomatik olarak oturum açma AppDynamics uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbbd8-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbbd8-245">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fbbd8-245">Additional resources</span></span>

* [<span data-ttu-id="fbbd8-246">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fbbd8-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbbd8-247">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="fbbd8-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

