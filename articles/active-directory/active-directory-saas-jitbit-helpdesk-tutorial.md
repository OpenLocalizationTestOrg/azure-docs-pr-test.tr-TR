---
title: "Öğretici: Azure Active Directory Tümleştirme Jitbit Yardım Masası ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Jitbit Yardım Masası arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="2cad9-103">Öğretici: Azure Active Directory Tümleştirme Jitbit Yardım Masası ile</span><span class="sxs-lookup"><span data-stu-id="2cad9-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="2cad9-104">Bu öğreticide, bilgi nasıl toointegrate Jitbit Yardım Masası Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2cad9-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2cad9-105">Jitbit Yardım Masası Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2cad9-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2cad9-106">Erişim tooJitbit Yardım Masası sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2cad9-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="2cad9-107">Kullanıcıların tooautomatically get açan tooJitbit Yardım Masası (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2cad9-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2cad9-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2cad9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2cad9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2cad9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cad9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2cad9-110">Prerequisites</span></span>

<span data-ttu-id="2cad9-111">tooconfigure Jitbit Yardım Masası ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cad9-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="2cad9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2cad9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2cad9-113">Bir Jitbit Yardım Masası çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2cad9-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2cad9-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2cad9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2cad9-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cad9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2cad9-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2cad9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2cad9-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2cad9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2cad9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2cad9-118">Scenario description</span></span>
<span data-ttu-id="2cad9-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2cad9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2cad9-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2cad9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2cad9-121">Merhaba Galerisi'nden Jitbit Yardım Masası ekleme</span><span class="sxs-lookup"><span data-stu-id="2cad9-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="2cad9-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2cad9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="2cad9-123">Merhaba Galerisi'nden Jitbit Yardım Masası ekleme</span><span class="sxs-lookup"><span data-stu-id="2cad9-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="2cad9-124">Azure AD'ye tooconfigure hello tümleştirme Jitbit Yardım Masası, tooadd Jitbit Yardım Masası hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cad9-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2cad9-125">**tooadd Jitbit Yardım Masası hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cad9-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cad9-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2cad9-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2cad9-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2cad9-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2cad9-133">Merhaba arama kutusuna yazın **Jitbit Yardım Masası**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="2cad9-135">Merhaba Sonuçlar panelinde seçin **Jitbit Yardım Masası**ve ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2cad9-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2cad9-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2cad9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2cad9-138">Bu bölümde, yapılandırmanız ve Jitbit Yardım Masası ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="2cad9-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2cad9-139">Tek toowork'ın oturum açma hangi hello karşılık gelen Jitbit Yardım Masası içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cad9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="2cad9-140">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Jitbit Yardım Masası hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cad9-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="2cad9-141">Merhaba hello değeri Jitbit Yardım Masası içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2cad9-142">tooconfigure ve Jitbit Yardım Masası ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2cad9-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2cad9-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2cad9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2cad9-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2cad9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2cad9-145">**[Jitbit Yardım Masası test kullanıcısı oluşturma](#creating-a-jitbit-helpdesk-test-user)**  -toohave Britta Simon bağlantılı toohello Azure AD kullanıcı gösterimini Jitbit Yardım Masası'nda, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2cad9-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2cad9-146">**[Atama hello Azure AD test kullanıcısı](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2cad9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2cad9-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2cad9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2cad9-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2cad9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2cad9-149">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Jitbit Yardım Masası uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2cad9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="2cad9-150">**tooconfigure Azure AD çoklu oturum açma Jitbit Yardım Masası ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cad9-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cad9-151">Hello hello üzerinde Azure portal'ın **Jitbit Yardım Masası** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2cad9-153">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2cad9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="2cad9-155">Merhaba üzerinde **Jitbit Yardım Masası etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2cad9-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="2cad9-157">a.</span><span class="sxs-lookup"><span data-stu-id="2cad9-157">a.</span></span> <span data-ttu-id="2cad9-158">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="2cad9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="2cad9-159">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="2cad9-159">This value is not real.</span></span> <span data-ttu-id="2cad9-160">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="2cad9-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2cad9-161">Kişi [Jitbit Yardım Masası istemci destek ekibi](https://www.jitbit.com/support/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="2cad9-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="2cad9-162">b.</span><span class="sxs-lookup"><span data-stu-id="2cad9-162">b.</span></span>  <span data-ttu-id="2cad9-163">Merhaba, **tanımlayıcısı** metin kutusuna, şu URL'yi yazın:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="2cad9-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="2cad9-164">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2cad9-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="2cad9-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2cad9-168">Merhaba üzerinde **Jitbit Yardım Masası yapılandırma** 'yi tıklatın **yapılandırma Jitbit Yardım Masası** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2cad9-169">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2cad9-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="2cad9-171">Farklı web tarayıcısı penceresinde Jitbit Yardım Masası şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2cad9-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="2cad9-172">Merhaba üstte Hello araç çubuğunda **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="2cad9-173">![Yönetim](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="2cad9-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="2cad9-174">Tıklatın **genel ayarları**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="2cad9-175">![Kullanıcılar, şirketler ve izinleri](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "kullanıcıları, şirketler ve izinleri")</span><span class="sxs-lookup"><span data-stu-id="2cad9-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="2cad9-176">Merhaba, **kimlik doğrulama ayarlarını** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2cad9-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2cad9-177">![Kimlik doğrulama ayarlarını](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "kimlik doğrulama ayarları")</span><span class="sxs-lookup"><span data-stu-id="2cad9-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="2cad9-178">a.</span><span class="sxs-lookup"><span data-stu-id="2cad9-178">a.</span></span> <span data-ttu-id="2cad9-179">Seçin **SAML 2.0 tek etkinleştirmek oturum**, çoklu oturum açma (SSO), ile kullanarak toosign **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="2cad9-180">b.</span><span class="sxs-lookup"><span data-stu-id="2cad9-180">b.</span></span> <span data-ttu-id="2cad9-181">Merhaba, **uç nokta URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="2cad9-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2cad9-182">c.</span><span class="sxs-lookup"><span data-stu-id="2cad9-182">c.</span></span> <span data-ttu-id="2cad9-183">Açık, **base-64** kodlanmış sertifika Not Defteri'nde, kopyalama hello panonuza bunu içerik ve toohello yapıştırın **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="2cad9-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="2cad9-184">d.</span><span class="sxs-lookup"><span data-stu-id="2cad9-184">d.</span></span> <span data-ttu-id="2cad9-185">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2cad9-186">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2cad9-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2cad9-187">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2cad9-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2cad9-188">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2cad9-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2cad9-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cad9-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="2cad9-190">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2cad9-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2cad9-192">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cad9-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cad9-193">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2cad9-195">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2cad9-197">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cad9-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2cad9-199">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2cad9-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2cad9-201">a.</span><span class="sxs-lookup"><span data-stu-id="2cad9-201">a.</span></span> <span data-ttu-id="2cad9-202">Merhaba, **adı** metin kutusuna, tür adı olarak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="2cad9-203">b.</span><span class="sxs-lookup"><span data-stu-id="2cad9-203">b.</span></span> <span data-ttu-id="2cad9-204">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2cad9-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2cad9-205">c.</span><span class="sxs-lookup"><span data-stu-id="2cad9-205">c.</span></span> <span data-ttu-id="2cad9-206">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2cad9-207">d.</span><span class="sxs-lookup"><span data-stu-id="2cad9-207">d.</span></span> <span data-ttu-id="2cad9-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2cad9-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="2cad9-209">Jitbit Yardım Masası test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cad9-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="2cad9-210">Jitbit Yardım Masası uygulamasına sipariş tooenable Azure AD kullanıcıların toolog bunlar Jitbit Yardım Masası sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2cad9-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="2cad9-211">Jitbit Yardım Masası Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2cad9-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="2cad9-212">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cad9-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cad9-213">İçinde tooyour oturum **Jitbit Yardım Masası** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="2cad9-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="2cad9-214">Hello içinde hello üst menüsünde **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="2cad9-215">![Yönetim](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="2cad9-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="2cad9-216">Tıklatın **kullanıcıları, şirketler ve izinleri**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="2cad9-217">![Kullanıcılar, şirketler ve izinleri](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "kullanıcıları, şirketler ve izinleri")</span><span class="sxs-lookup"><span data-stu-id="2cad9-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="2cad9-218">Tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="2cad9-219">![Kullanıcı Ekle](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="2cad9-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="2cad9-220">Hello Oluştur bölümünde, tooprovision gibi istediğiniz hello Azure AD hesabının hello veri türü:</span><span class="sxs-lookup"><span data-stu-id="2cad9-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="2cad9-221">![Oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="2cad9-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="2cad9-222">a.</span><span class="sxs-lookup"><span data-stu-id="2cad9-222">a.</span></span> <span data-ttu-id="2cad9-223">Merhaba, **kullanıcıadı** metin kutusuna, türü **BrittaSimon**, hello Azure portal olduğu gibi hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="2cad9-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="2cad9-224">b.</span><span class="sxs-lookup"><span data-stu-id="2cad9-224">b.</span></span> <span data-ttu-id="2cad9-225">Merhaba, **e-posta** hello kullanıcının e-posta metin kutusuna, ister  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2cad9-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="2cad9-226">c.</span><span class="sxs-lookup"><span data-stu-id="2cad9-226">c.</span></span> <span data-ttu-id="2cad9-227">Merhaba, **ad** metin kutusuna, tür ilk gibi hello kullanıcı adını **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="2cad9-228">d.</span><span class="sxs-lookup"><span data-stu-id="2cad9-228">d.</span></span> <span data-ttu-id="2cad9-229">Merhaba, **Soyadı** metin kutusuna, türü hello kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="2cad9-230">e.</span><span class="sxs-lookup"><span data-stu-id="2cad9-230">e.</span></span> <span data-ttu-id="2cad9-231">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2cad9-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="2cad9-232">API'leri, Azure AD kullanıcı hesapları Jitbit Yardım Masası tooprovision tarafından sağlanan veya herhangi diğer Jitbit Yardım Masası kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cad9-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2cad9-233">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2cad9-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2cad9-234">Bu bölümde, erişim tooJitbit Yardım Masası vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2cad9-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2cad9-236">**tooassign Britta Simon tooJitbit Yardım Masası, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2cad9-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cad9-237">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2cad9-239">Merhaba uygulamalar listesinde **Jitbit Yardım Masası**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="2cad9-241">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2cad9-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2cad9-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2cad9-243">Click **Add** button.</span></span> <span data-ttu-id="2cad9-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cad9-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2cad9-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2cad9-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2cad9-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cad9-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2cad9-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2cad9-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2cad9-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2cad9-249">Testing single sign-on</span></span>

<span data-ttu-id="2cad9-250">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2cad9-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2cad9-251">Jitbit Yardım Masası döşeme hello erişim paneli hello tıkladığınızda, oturum açma sayfasına Jitbit Yardım Masası uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2cad9-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="2cad9-252">Merhaba erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2cad9-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2cad9-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2cad9-253">Additional resources</span></span>

* [<span data-ttu-id="2cad9-254">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2cad9-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2cad9-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2cad9-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

