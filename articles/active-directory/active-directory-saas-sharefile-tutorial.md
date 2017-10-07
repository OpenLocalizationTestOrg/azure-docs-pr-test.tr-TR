---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix ShareFile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Citrix ShareFile arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="079d0-103">Öğretici: Citrix ShareFile Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="079d0-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="079d0-104">Bu öğreticide, bilgi nasıl toointegrate Citrix ShareFile Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="079d0-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="079d0-105">Citrix ShareFile Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="079d0-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="079d0-106">Erişim tooCitrix ShareFile sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="079d0-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="079d0-107">Kullanıcıların tooautomatically get açan tooCitrix ShareFile (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="079d0-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="079d0-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="079d0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="079d0-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="079d0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="079d0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="079d0-110">Prerequisites</span></span>

<span data-ttu-id="079d0-111">tooconfigure Citrix ShareFile ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="079d0-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="079d0-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="079d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="079d0-113">Bir Citrix ShareFile çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="079d0-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="079d0-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="079d0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="079d0-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="079d0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="079d0-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="079d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="079d0-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="079d0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="079d0-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="079d0-118">Scenario description</span></span>
<span data-ttu-id="079d0-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="079d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="079d0-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="079d0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="079d0-121">Citrix ShareFile hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="079d0-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="079d0-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="079d0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="079d0-123">Citrix ShareFile hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="079d0-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="079d0-124">Azure AD'ye tooconfigure hello tümleştirme Citrix ShareFile, tooadd Citrix ShareFile hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="079d0-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="079d0-125">**tooadd Citrix ShareFile hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="079d0-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="079d0-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="079d0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="079d0-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="079d0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="079d0-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="079d0-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="079d0-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="079d0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="079d0-133">Merhaba arama kutusuna yazın **Citrix ShareFile**seçin **Citrix ShareFile** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="079d0-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba, Citrix ShareFile listesi sonuçları](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="079d0-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="079d0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="079d0-136">Bu bölümde, yapılandırmanız ve Citrix ShareFile ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="079d0-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="079d0-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Citrix ShareFile içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="079d0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="079d0-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Citrix ShareFile hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="079d0-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="079d0-139">Citrix ShareFile içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="079d0-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="079d0-140">tooconfigure ve Citrix ShareFile ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="079d0-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="079d0-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="079d0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="079d0-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="079d0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="079d0-143">**[Citrix ShareFile test kullanıcısı oluşturma](#create-a-citrix-sharefile-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Citrix ShareFile içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="079d0-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="079d0-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="079d0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="079d0-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="079d0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="079d0-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="079d0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="079d0-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Citrix ShareFile uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="079d0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="079d0-148">**tooconfigure Azure AD çoklu oturum açma Citrix ShareFile ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="079d0-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="079d0-149">Hello hello üzerinde Azure portal'ın **Citrix ShareFile** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="079d0-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="079d0-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="079d0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="079d0-153">Merhaba üzerinde **Citrix ShareFile etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="079d0-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Citrix ShareFile etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="079d0-155">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="079d0-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="079d0-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="079d0-156">This value is not real.</span></span> <span data-ttu-id="079d0-157">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="079d0-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="079d0-158">Kişi [Citrix ShareFile istemci destek ekibi](https://www.citrix.co.in/products/sharefile/support.html) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="079d0-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="079d0-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="079d0-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="079d0-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="079d0-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="079d0-163">Merhaba üzerinde **Citrix ShareFile yapılandırma** 'yi tıklatın **yapılandırma Citrix ShareFile** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="079d0-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="079d0-164">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="079d0-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Citrix ShareFile yapılandırma](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="079d0-166">Farklı web tarayıcısı penceresinde oturum açın, **Citrix ShareFile** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="079d0-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="079d0-167">Merhaba üstte Hello araç çubuğunda **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="079d0-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="079d0-168">Merhaba sol gezinti bölmesinde seçin **yapılandırma çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="079d0-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="079d0-169">![Hesap Yönetimi](./media/active-directory-saas-sharefile-tutorial/ic773627.png "hesap yönetimi")</span><span class="sxs-lookup"><span data-stu-id="079d0-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="079d0-170">Merhaba üzerinde **çoklu oturum açma / SAML 2.0 yapılandırma** iletişim sayfasında altında **temel ayarları**, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="079d0-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="079d0-171">![Çoklu oturum açma](./media/active-directory-saas-sharefile-tutorial/ic773628.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="079d0-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="079d0-172">a.</span><span class="sxs-lookup"><span data-stu-id="079d0-172">a.</span></span> <span data-ttu-id="079d0-173">Tıklatın **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="079d0-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="079d0-174">b.</span><span class="sxs-lookup"><span data-stu-id="079d0-174">b.</span></span> <span data-ttu-id="079d0-175">İçinde **bilgisayarınızı IDP veren / varlık kimliği** metin kutusuna, Yapıştır hello değerini **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="079d0-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="079d0-176">c.</span><span class="sxs-lookup"><span data-stu-id="079d0-176">c.</span></span> <span data-ttu-id="079d0-177">Tıklatın **değişiklik** sonraki toohello **X.509 sertifikası** alan ve karşıya yükleme hello sertifika'ndan indirilen hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="079d0-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="079d0-178">d.</span><span class="sxs-lookup"><span data-stu-id="079d0-178">d.</span></span> <span data-ttu-id="079d0-179">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır hello değerini **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="079d0-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="079d0-180">e.</span><span class="sxs-lookup"><span data-stu-id="079d0-180">e.</span></span> <span data-ttu-id="079d0-181">İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır hello değerini **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="079d0-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="079d0-182">Tıklatın **kaydetmek** hello Citrix ShareFile yönetim portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="079d0-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="079d0-183">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="079d0-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="079d0-184">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="079d0-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="079d0-185">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="079d0-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="079d0-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="079d0-186">Create an Azure AD test user</span></span>

<span data-ttu-id="079d0-187">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="079d0-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="079d0-189">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="079d0-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="079d0-190">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="079d0-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="079d0-192">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="079d0-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="079d0-194">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="079d0-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="079d0-196">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="079d0-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="079d0-198">a.</span><span class="sxs-lookup"><span data-stu-id="079d0-198">a.</span></span> <span data-ttu-id="079d0-199">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="079d0-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="079d0-200">b.</span><span class="sxs-lookup"><span data-stu-id="079d0-200">b.</span></span> <span data-ttu-id="079d0-201">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="079d0-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="079d0-202">c.</span><span class="sxs-lookup"><span data-stu-id="079d0-202">c.</span></span> <span data-ttu-id="079d0-203">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="079d0-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="079d0-204">d.</span><span class="sxs-lookup"><span data-stu-id="079d0-204">d.</span></span> <span data-ttu-id="079d0-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="079d0-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="079d0-206">Citrix ShareFile test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="079d0-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="079d0-207">Citrix ShareFile içine sipariş tooenable Azure AD kullanıcıların toolog bunlar Citrix ShareFile sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="079d0-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="079d0-208">Citrix ShareFile Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="079d0-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="079d0-209">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="079d0-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="079d0-210">İçinde tooyour oturum **Citrix ShareFile** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="079d0-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="079d0-211">Tıklatın **kullanıcıları yönetme \> kullanıcıların giriş yönetmek \> + çalışan oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="079d0-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="079d0-212">![Çalışan oluşturma](./media/active-directory-saas-sharefile-tutorial/IC781050.png "çalışan oluşturma")</span><span class="sxs-lookup"><span data-stu-id="079d0-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="079d0-213">Merhaba üzerinde **temel bilgileri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="079d0-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="079d0-214">![Temel bilgileri](./media/active-directory-saas-sharefile-tutorial/IC799951.png "temel bilgileri")</span><span class="sxs-lookup"><span data-stu-id="079d0-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="079d0-215">a.</span><span class="sxs-lookup"><span data-stu-id="079d0-215">a.</span></span> <span data-ttu-id="079d0-216">Merhaba, **e-posta adresi** metin kutusuna, türü hello e-posta adresi Britta Simon  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="079d0-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="079d0-217">b.</span><span class="sxs-lookup"><span data-stu-id="079d0-217">b.</span></span> <span data-ttu-id="079d0-218">Merhaba, **ad** metin kutusuna, türü **ad** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="079d0-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="079d0-219">c.</span><span class="sxs-lookup"><span data-stu-id="079d0-219">c.</span></span> <span data-ttu-id="079d0-220">Merhaba, **Soyadı** metin kutusuna, türü **Soyadı** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="079d0-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="079d0-221">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="079d0-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="079d0-222">Hello Azure AD hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce bağlantı tooconfirm hesaplarında izleyin. API'leri, Azure AD kullanıcı hesapları Citrix ShareFile tooprovision tarafından sağlanan veya herhangi diğer Citrix ShareFile kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="079d0-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="079d0-223">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="079d0-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="079d0-224">Bu bölümde, erişim tooCitrix ShareFile vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="079d0-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="079d0-226">**tooassign Britta Simon tooCitrix ShareFile, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="079d0-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="079d0-227">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="079d0-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="079d0-229">Merhaba uygulamalar listesinde **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="079d0-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Merhaba hello uygulamalar listesinde Citrix ShareFile bağlantı](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="079d0-231">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="079d0-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="079d0-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="079d0-233">Click **Add** button.</span></span> <span data-ttu-id="079d0-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="079d0-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="079d0-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="079d0-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="079d0-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="079d0-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="079d0-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="079d0-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="079d0-239">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="079d0-239">Test single sign-on</span></span>

<span data-ttu-id="079d0-240">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="079d0-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="079d0-241">Citrix ShareFile döşeme hello erişim paneli hello tıkladığınızda, otomatik olarak oturum açma Citrix ShareFile uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="079d0-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="079d0-242">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="079d0-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="079d0-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="079d0-243">Additional resources</span></span>

* [<span data-ttu-id="079d0-244">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="079d0-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="079d0-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="079d0-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

