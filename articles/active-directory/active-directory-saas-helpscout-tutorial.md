---
title: "Öğretici: Azure Active Directory Tümleştirme ile Yardım Scout | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve Yardım Scout arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="9c7a4-103">Öğretici: Yardım Scout Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="9c7a4-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="9c7a4-104">Bu öğreticide, nasıl toointegrate yardımcı Azure Active Directory (Azure AD) ile Scout öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c7a4-105">Azure AD ile Yardım Scout tümleştirme avantajları aşağıdaki hello alın:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="9c7a4-106">Azure AD'de erişim tooHelp Scout olanların kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="9c7a4-107">Çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak otomatik olarak, kullanıcılar tooHelp Scout imzalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="9c7a4-108">Hesaplarınızı tek, merkezi bir konumda, hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="9c7a4-109">toolearn yazılım olarak Azure AD ile hizmet (SaaS) uygulama tümleştirmesi hakkında daha fazla bilgi görmek [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c7a4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9c7a4-110">Prerequisites</span></span>

<span data-ttu-id="9c7a4-111">tooset Yardım Scout ile Azure AD tümleştirme aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="9c7a4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9c7a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c7a4-113">Bir Yardım Scout aboneliğiyle, çoklu oturum açık açma</span><span class="sxs-lookup"><span data-stu-id="9c7a4-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="9c7a4-114">Bu öğreticide hello adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="9c7a4-115">Bu öğreticide hello adımları test etmek için öneriler:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="9c7a4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="9c7a4-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c7a4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9c7a4-118">Scenario description</span></span>
<span data-ttu-id="9c7a4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="9c7a4-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c7a4-121">Yardım Scout hello Galerisi'nden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="9c7a4-122">Ayarlama ve Azure AD çoklu oturum açmayı test edin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="9c7a4-123">Yardım Scout hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="9c7a4-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="9c7a4-124">Merhaba hello galerisinde Yardım Scout Azure AD ile tümleştirilmesi yukarı tooset Yardım Scout tooyour yönetilen SaaS uygulamaları listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9c7a4-125">tooadd Yardım Scout hello galerisinden:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="9c7a4-126">Merhaba, [Azure portal](https://portal.azure.com), buna hello soldaki menüden, seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="9c7a4-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar sayfası][2]
    
3. <span data-ttu-id="9c7a4-130">tooadd yeni bir uygulama seçin **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-130">tooadd a new application, select **New application**.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="9c7a4-132">Merhaba arama kutusuna **Yardım Scout**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="9c7a4-133">Merhaba arama sonuçlarında seçin **Yardım Scout**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Merhaba sonuçlar listesinde Scout Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9c7a4-135">Ayarlama ve Azure AD çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="9c7a4-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="9c7a4-136">Bu bölümde, ayarladığınız ve Yardım Scout ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="9c7a4-137">Tek toowork'ın oturum açma tooknow hello Azure AD karşılık gelen kullanıcı Yardımı Scout Azure AD gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="9c7a4-138">Bir Azure AD kullanıcı ve ilgili kullanıcı Yardımı Scout hello arasında bir bağlantı ilişkisi kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="9c7a4-139">tooestablish hello ilişkisinde Scout, yardımcı olmak için bağlantı **kullanıcıadı**, hello hello değerini atayın **kullanıcı adı** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="9c7a4-140">tooconfigure ve Azure AD çoklu oturum açmayı test Yardım Scout, görevleri aşağıdaki tam hello ile:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="9c7a4-141">[Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="9c7a4-142">Bu özellik bir kullanıcının toouse ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="9c7a4-143">[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="9c7a4-144">Testleri Azure AD çoklu oturum açma Britta Simon hello kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="9c7a4-145">[Yardım Scout test kullanıcısı oluşturma](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="9c7a4-146">Karşılık gelen Britta Simon, Yardım bağlantılı toohello hello kullanıcı Azure AD gösterimi olan Scout içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="9c7a4-147">[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="9c7a4-148">Azure AD çoklu oturum açma Britta Simon toouse ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c7a4-149">[Test çoklu oturum açma](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="9c7a4-150">Merhaba yapılandırmayı çalıştığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="9c7a4-151">Azure AD çoklu oturum açmayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9c7a4-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="9c7a4-152">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="9c7a4-153">Sonra tek oturum açma Yardımı Scout uygulamanızda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="9c7a4-154">Azure AD çoklu oturum açma Yardımı Scout ile yukarı tooset:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="9c7a4-155">Merhaba hello üzerinde Azure portal'ın **Yardım Scout** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Oturum açma tek bağlantı ayarlama][4]

2. <span data-ttu-id="9c7a4-157">Merhaba üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="9c7a4-159">Altında **Yardım Scout etki alanı ve URL'leri**IDP başlatılan modunda çalışırken, aşağıdaki adımları tam hello tooset Merhaba uygulaması yedeklemek istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="9c7a4-160">Merhaba, **tanımlayıcısı** kutusuna, desen aşağıdaki hello bir URL girin:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9c7a4-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="9c7a4-161">Merhaba, **yanıt URL'si** kutusuna, desen aşağıdaki hello bir URL girin:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9c7a4-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="9c7a4-163">SP tarafından başlatılan modunda tooset Merhaba uygulaması yedeklemek istiyorsanız hello seçin **Göster Gelişmiş URL ayarları** onay kutusunu işaretleyin ve ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="9c7a4-164">Merhaba, **URL üzerinde oturum** kutusuna, hello biçimini izleyen bir URL girin:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="9c7a4-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="9c7a4-166">Merhaba bu URL'leri yalnızca tanıtım değerler.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="9c7a4-167">Merhaba değerlerini hello gerçek tanımlayıcı URL'sini ve yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="9c7a4-168">Bu değerleri tooget başvurun [Yardım Scout destek ekibi](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="9c7a4-169">Altında **SAML imzalama sertifikası**seçin **meta veri XML**ve ardından hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="9c7a4-171">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-171">Select **Save**.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9c7a4-173">tek yukarı tooset hello Yardım Scout tarafında oturum açma, indirilen hello meta veri XML dosyası toohello Gönder [Yardım Scout destek ekibi](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="9c7a4-174">Böylece Hello SAML çoklu oturum açma bağlantısı iki tarafta da düzgün ayarlandığından hello Yardım Scout destek ekibi bu ayar uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9c7a4-175">Bu yönergelerde hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken!</span><span class="sxs-lookup"><span data-stu-id="9c7a4-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="9c7a4-176">Seçerek hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin hello **çoklu oturum açma** sekmesi. Merhaba katıştırılmış hello belgelerinde erişebilirsiniz **yapılandırma** kısmına hello sayfanın hello.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="9c7a4-177">Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9c7a4-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c7a4-178">Create an Azure AD test user</span></span>

<span data-ttu-id="9c7a4-179">Bu bölümde Azure portal hello Britta Simon adlı bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="9c7a4-181">toocreate Azure AD'de bir sınama kullanıcısı:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="9c7a4-182">Merhaba hello soldaki menüde Azure portal seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9c7a4-184">Kullanıcıların, select toodisplay hello listesini **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Kullanıcıları ve grupları seçin ve ardından tüm kullanıcıları seçin](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9c7a4-186">tooopen hello **kullanıcı** iletişim kutusu, hello hello üstündeki **tüm kullanıcılar** sayfasında, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9c7a4-188">Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="9c7a4-189">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="9c7a4-190">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="9c7a4-191">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="9c7a4-192">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-192">Select **Create**.</span></span>

        ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="9c7a4-194">Yardım Scout test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c7a4-194">Create a Help Scout test user</span></span>

<span data-ttu-id="9c7a4-195">Merhaba, bu bölümün toocreate Britta Simon Yardım Scout içinde adlı bir kullanıcı nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="9c7a4-196">Yardım Scout tam zamanında (JIT) sağlama, varsayılan olarak açıktır destekler.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="9c7a4-197">Bu bölümde, hiçbir eylem ya da görev toocomplete yoktur.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="9c7a4-198">Kullanıcı Yardım Scout içinde zaten mevcut değilse tooaccess Yardım Scout çalıştığınızda yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9c7a4-199">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="9c7a4-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9c7a4-200">Bu bölümde, hello kullanıcı Britta Simon toouse Azure AD çoklu oturum açma hello kullanıcı hesabı erişimi tooHelp Scout vererek sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="9c7a4-202">tooassign Britta Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="9c7a4-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="9c7a4-203">Hello Azure portal, hello uygulamaları görünümünü açın ve toohello dizini görünümü gidin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="9c7a4-204">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9c7a4-206">Merhaba uygulamalar listesinde **Yardım Scout**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-206">In hello applications list, select **Help Scout**.</span></span>

    ![Merhaba Yardım Scout bağlantı hello uygulamalar listesinde](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="9c7a4-208">Merhaba soldaki menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-208">In hello left menu, select **Users and groups**.</span></span>

    ![Merhaba kullanıcılar ve gruplar Bağla][202]

4. <span data-ttu-id="9c7a4-210">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-210">Select **Add**.</span></span> <span data-ttu-id="9c7a4-211">Ardından, hello **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="9c7a4-213">Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, select hello listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="9c7a4-214">Merhaba üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="9c7a4-215">Merhaba üzerinde **eklemek atama** sayfasında, **atamak**.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9c7a4-216">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="9c7a4-216">Test single sign-on</span></span>

<span data-ttu-id="9c7a4-217">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="9c7a4-218">Merhaba erişim panelinde hello Yardım Scout döşeme seçtiğinizde tooyour Yardım Scout uygulama otomatik olarak imzalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9c7a4-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="9c7a4-219">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c7a4-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9c7a4-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9c7a4-220">Additional resources</span></span>

* [<span data-ttu-id="9c7a4-221">İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9c7a4-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c7a4-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9c7a4-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

