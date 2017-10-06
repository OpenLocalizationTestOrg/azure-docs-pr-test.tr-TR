---
title: "Öğretici: Azure Active Directory Tümleştirme ile ScreenSteps | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ScreenSteps arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="6f465-103">Öğretici: Azure Active Directory Tümleştirme ScreenSteps ile</span><span class="sxs-lookup"><span data-stu-id="6f465-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="6f465-104">Bu öğreticide, bilgi nasıl toointegrate ScreenSteps Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f465-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f465-105">ScreenSteps Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6f465-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f465-106">Erişim tooScreenSteps sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f465-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="6f465-107">Kullanıcıların tooautomatically get açan tooScreenSteps (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f465-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6f465-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="6f465-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6f465-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f465-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f465-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6f465-110">Prerequisites</span></span>

<span data-ttu-id="6f465-111">tooconfigure ScreenSteps ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f465-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="6f465-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6f465-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f465-113">Bir ScreenSteps çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6f465-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f465-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6f465-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f465-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f465-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f465-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6f465-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f465-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f465-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f465-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6f465-118">Scenario description</span></span>
<span data-ttu-id="6f465-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6f465-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f465-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6f465-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f465-121">Merhaba Galerisi'nden ScreenSteps ekleme</span><span class="sxs-lookup"><span data-stu-id="6f465-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="6f465-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f465-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="6f465-123">Merhaba Galerisi'nden ScreenSteps ekleme</span><span class="sxs-lookup"><span data-stu-id="6f465-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="6f465-124">Azure AD'ye tooconfigure hello tümleştirme ScreenSteps, tooadd ScreenSteps hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f465-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f465-125">**tooadd ScreenSteps hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f465-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f465-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f465-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="6f465-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6f465-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f465-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f465-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="6f465-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f465-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="6f465-133">Merhaba arama kutusuna yazın **ScreenSteps**seçin **ScreenSteps** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6f465-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6f465-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6f465-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6f465-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ScreenSteps sınayın.</span><span class="sxs-lookup"><span data-stu-id="6f465-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f465-137">Tek toowork'ın oturum açma hangi hello karşılık gelen ScreenSteps içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f465-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="6f465-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ScreenSteps hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f465-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="6f465-139">Merhaba hello değeri ScreenSteps içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="6f465-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f465-140">tooconfigure ve ScreenSteps ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f465-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f465-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="6f465-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f465-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="6f465-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f465-143">**[ScreenSteps test kullanıcısı oluşturma](#create-a-screensteps-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ScreenSteps içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="6f465-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f465-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6f465-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f465-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="6f465-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6f465-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6f465-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6f465-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ScreenSteps uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6f465-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="6f465-148">**tooconfigure Azure AD çoklu oturum açma ile ScreenSteps, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f465-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f465-149">Hello hello üzerinde Azure portal'ın **ScreenSteps** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6f465-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="6f465-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="6f465-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="6f465-153">Merhaba üzerinde **ScreenSteps etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f465-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![ScreenSteps etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="6f465-155">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="6f465-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f465-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="6f465-156">This value is not real.</span></span> <span data-ttu-id="6f465-157">Bu değer ile Merhaba güncelleştirme gerçek oturum açma, bu öğreticinin ilerleyen bölümlerinde açıklanan URL.</span><span class="sxs-lookup"><span data-stu-id="6f465-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="6f465-158">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6f465-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="6f465-160">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f465-160">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f465-162">Merhaba üzerinde **ScreenSteps yapılandırma** 'yi tıklatın **yapılandırma ScreenSteps** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6f465-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6f465-163">Kopya hello **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6f465-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ScreenSteps yapılandırma](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="6f465-165">Farklı web tarayıcısı penceresinde ScreenSteps şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6f465-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="6f465-166">Tıklatın **hesap ayarları**.</span><span class="sxs-lookup"><span data-stu-id="6f465-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="6f465-167">![Hesap Yönetimi](./media/active-directory-saas-screensteps-tutorial/ic778523.png "hesap yönetimi")</span><span class="sxs-lookup"><span data-stu-id="6f465-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="6f465-168">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6f465-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="6f465-169">![Uzaktan kimlik doğrulama](./media/active-directory-saas-screensteps-tutorial/ic778524.png "uzaktan kimlik doğrulama")</span><span class="sxs-lookup"><span data-stu-id="6f465-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="6f465-170">Tıklatın **tek oturum açma uç noktası oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6f465-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="6f465-171">![Uzaktan kimlik doğrulama](./media/active-directory-saas-screensteps-tutorial/ic778525.png "uzaktan kimlik doğrulama")</span><span class="sxs-lookup"><span data-stu-id="6f465-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="6f465-172">Merhaba, **oluşturmak tek oturum açma uç noktası** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f465-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="6f465-173">![Bir kimlik doğrulama uç noktası oluşturma](./media/active-directory-saas-screensteps-tutorial/ic778526.png "bir kimlik doğrulama uç noktası oluşturma")</span><span class="sxs-lookup"><span data-stu-id="6f465-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="6f465-174">a.</span><span class="sxs-lookup"><span data-stu-id="6f465-174">a.</span></span> <span data-ttu-id="6f465-175">Merhaba, **başlık** metin kutusuna, bir başlık yazın.</span><span class="sxs-lookup"><span data-stu-id="6f465-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="6f465-176">b.</span><span class="sxs-lookup"><span data-stu-id="6f465-176">b.</span></span> <span data-ttu-id="6f465-177">Merhaba gelen **modu** listesinde **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6f465-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="6f465-178">c.</span><span class="sxs-lookup"><span data-stu-id="6f465-178">c.</span></span> <span data-ttu-id="6f465-179">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f465-179">Click **Create**.</span></span>

12. <span data-ttu-id="6f465-180">**Düzen** yeni uç nokta hello.</span><span class="sxs-lookup"><span data-stu-id="6f465-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="6f465-181">![Uç noktayı Düzenle](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Düzenle uç noktası")</span><span class="sxs-lookup"><span data-stu-id="6f465-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="6f465-182">Merhaba, **Düzenle tek oturum açma uç noktası** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f465-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="6f465-183">![Uzaktan kimlik doğrulama uç noktası](./media/active-directory-saas-screensteps-tutorial/ic778527.png "uzaktan kimlik doğrulama uç noktası")</span><span class="sxs-lookup"><span data-stu-id="6f465-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="6f465-184">a.</span><span class="sxs-lookup"><span data-stu-id="6f465-184">a.</span></span> <span data-ttu-id="6f465-185">Tıklatın **yeni SAML sertifika dosyası karşıya yükleme**ve Azure portalından indirdikten sonra karşıya yükleme hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="6f465-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="6f465-186">b.</span><span class="sxs-lookup"><span data-stu-id="6f465-186">b.</span></span> <span data-ttu-id="6f465-187">Yapıştır **SAML çoklu oturum açma hizmet URL'si** hello hello Azure portal ' kopyaladığınız değeri **uzaktan oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f465-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="6f465-188">c.</span><span class="sxs-lookup"><span data-stu-id="6f465-188">c.</span></span> <span data-ttu-id="6f465-189">Yapıştır **Sign-Out URL** hello hello Azure portal ' kopyaladığınız değeri **oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f465-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="6f465-190">d.</span><span class="sxs-lookup"><span data-stu-id="6f465-190">d.</span></span> <span data-ttu-id="6f465-191">Seçin bir **grup** tooassign kullanıcılar toowhen sağlandı.</span><span class="sxs-lookup"><span data-stu-id="6f465-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="6f465-192">e.</span><span class="sxs-lookup"><span data-stu-id="6f465-192">e.</span></span> <span data-ttu-id="6f465-193">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="6f465-193">Click **Update**.</span></span>

    <span data-ttu-id="6f465-194">f.</span><span class="sxs-lookup"><span data-stu-id="6f465-194">f.</span></span> <span data-ttu-id="6f465-195">Kopya hello **SAML tüketici URL** toohello Pano toohello içinde Yapıştır **oturum açma URL'si** metin kutusuna **ScreenSteps etki alanı ve URL'leri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="6f465-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="6f465-196">g.</span><span class="sxs-lookup"><span data-stu-id="6f465-196">g.</span></span> <span data-ttu-id="6f465-197">Toohello iade **Düzenle tek oturum açma uç noktası**.</span><span class="sxs-lookup"><span data-stu-id="6f465-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="6f465-198">h.</span><span class="sxs-lookup"><span data-stu-id="6f465-198">h.</span></span> <span data-ttu-id="6f465-199">Hello'ı tıklatın **olun hesabı için varsayılan** toouse ScreenSteps oturum tüm kullanıcılar için bu uç nokta düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f465-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="6f465-200">Alternatif olarak, hello tıklatabilirsiniz **tooSite ekleme** toouse belirli sitelerin Bu uç nokta düğmesini **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="6f465-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="6f465-201">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6f465-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f465-202">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="6f465-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f465-203">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f465-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6f465-204">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f465-204">Create an Azure AD test user</span></span>

<span data-ttu-id="6f465-205">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="6f465-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="6f465-207">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f465-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f465-208">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f465-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6f465-210">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6f465-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6f465-212">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f465-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6f465-214">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f465-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6f465-216">a.</span><span class="sxs-lookup"><span data-stu-id="6f465-216">a.</span></span> <span data-ttu-id="6f465-217">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f465-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f465-218">b.</span><span class="sxs-lookup"><span data-stu-id="6f465-218">b.</span></span> <span data-ttu-id="6f465-219">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="6f465-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6f465-220">c.</span><span class="sxs-lookup"><span data-stu-id="6f465-220">c.</span></span> <span data-ttu-id="6f465-221">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="6f465-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6f465-222">d.</span><span class="sxs-lookup"><span data-stu-id="6f465-222">d.</span></span> <span data-ttu-id="6f465-223">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f465-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="6f465-224">ScreenSteps test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f465-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="6f465-225">Bu bölümde, ScreenSteps içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f465-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="6f465-226">Çalışmak [ScreenSteps istemci destek ekibi](https://www.screensteps.com/contact) hello ScreenSteps platform hello kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="6f465-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="6f465-227">Kullanıcıların oluşturulan ve çoklu oturum açma kullanmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="6f465-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6f465-228">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="6f465-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6f465-229">Bu bölümde, erişim tooScreenSteps vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f465-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="6f465-231">**tooassign Britta Simon tooScreenSteps hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f465-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f465-232">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f465-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6f465-234">Merhaba uygulamalar listesinde **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="6f465-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![Merhaba ScreenSteps bağlantı hello uygulamalar listesinde](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="6f465-236">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6f465-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="6f465-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f465-238">Click **Add** button.</span></span> <span data-ttu-id="6f465-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f465-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="6f465-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6f465-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f465-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f465-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f465-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f465-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6f465-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="6f465-244">Test single sign-on</span></span>

<span data-ttu-id="6f465-245">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="6f465-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f465-246">Hello erişim paneli ScreenSteps döşeme hello tıkladığınızda, otomatik olarak oturum açma ScreenSteps uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f465-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="6f465-247">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f465-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6f465-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6f465-248">Additional resources</span></span>

* [<span data-ttu-id="6f465-249">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6f465-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f465-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6f465-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

