---
title: "Öğretici: Azure Active Directory ile vxMaintain tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile vxMaintain arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="9d687-103">Öğretici: Azure Active Directory vxMaintain ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="9d687-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="9d687-104">Bu öğreticide, bilgi nasıl toointegrate vxMaintain Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d687-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d687-105">Bu tümleştirme birkaç önemli avantaj sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d687-105">This integration provides several important benefits.</span></span> <span data-ttu-id="9d687-106">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9d687-106">You can:</span></span>

- <span data-ttu-id="9d687-107">ToovxMaintain erişim denetimi olan Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="9d687-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="9d687-108">Kullanıcıların tooautomatically oturum açma toovxMaintain çoklu oturum açma (SSO) ile Azure AD hesaplarına kullanarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d687-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="9d687-109">Hesaplarınızı tek bir merkezi konumda yönetme: Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="9d687-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="9d687-110">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla toolearn bkz [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d687-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d687-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d687-111">Prerequisites</span></span>

<span data-ttu-id="9d687-112">tooconfigure vxMaintain ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d687-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="9d687-113">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9d687-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9d687-114">VxMaintain abonelik SSO'su etkin</span><span class="sxs-lookup"><span data-stu-id="9d687-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d687-115">Bu öğreticide hello adımları test ettiğinizde, bir üretim ortamında kullanmayın öneririz.</span><span class="sxs-lookup"><span data-stu-id="9d687-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="9d687-116">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="9d687-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9d687-117">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9d687-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d687-118">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d687-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d687-119">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9d687-119">Scenario description</span></span>
<span data-ttu-id="9d687-120">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9d687-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="9d687-121">Bu öğretici özetlenmektedir hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9d687-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="9d687-122">Merhaba Galerisi'nden vxMaintain ekleme</span><span class="sxs-lookup"><span data-stu-id="9d687-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="9d687-123">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9d687-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="9d687-124">Merhaba Galerisi'nden vxMaintain ekleme</span><span class="sxs-lookup"><span data-stu-id="9d687-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="9d687-125">Azure AD ile vxMaintain tooconfigure hello tümleştirilmesi, tooadd vxMaintain hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d687-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d687-126">Merhaba galerisinden tooadd vxMaintain hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9d687-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="9d687-127">Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d687-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="9d687-129">Seçin **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9d687-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Merhaba "Kurumsal uygulamalar" bölmesi][2]
    
3. <span data-ttu-id="9d687-131">bir uygulamada hello tooadd **tüm uygulamaları** iletişim kutusunda **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="9d687-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    !["Yeni uygulamayı" Merhaba düğmesi][3]

4. <span data-ttu-id="9d687-133">Merhaba arama kutusuna yazın **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="9d687-133">In hello search box, type **vxMaintain**.</span></span>

    ![Merhaba "Modu tek oturum açma" açılan liste](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="9d687-135">Merhaba sonuçları listesinden seçmek **vxMaintain**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9d687-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![Merhaba vxMaintain bağlantı](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9d687-137">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9d687-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9d687-138">Bu bölümde, yapılandırma ve Azure AD SSO "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı vxMaintain kullanarak test etme</span><span class="sxs-lookup"><span data-stu-id="9d687-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9d687-139">SSO toowork için Azure AD tooknow hello vxMaintain karşılık gelen toohello Azure AD kullanıcısının gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d687-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="9d687-140">Diğer bir deyişle, hello Azure AD kullanıcısının hello karşılık gelen vxMaintain kullanıcı arasında bir bağlantı ilişkisi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d687-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="9d687-141">tooestablish hello bağlantı ilişkisi, Ata hello vxMaintain **kullanıcı adı** değeri hello Azure AD olarak **kullanıcıadı** değeri.</span><span class="sxs-lookup"><span data-stu-id="9d687-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="9d687-142">tooconfigure ve test vxMaintain, yapı taşları aşağıdaki tam hello kullanarak Azure AD SSO.</span><span class="sxs-lookup"><span data-stu-id="9d687-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="9d687-143">Azure AD SSO yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9d687-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="9d687-144">Bu bölümde, hello Azure portalında Azure AD SSO'yu etkinleştirmek hem hello aşağıdakileri yaparak vxMaintain uygulamanızda SSO yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="9d687-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="9d687-145">Merhaba hello üzerinde Azure portal'ın **vxMaintain** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9d687-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![komutu "çoklu oturum açmayı" Merhaba][4]

2. <span data-ttu-id="9d687-147">Merhaba içinde SSO tooenable **tek oturum açma modu** aşağı açılan listesinden, **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9d687-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Merhaba "SAML tabanlı oturum açma" komutu](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="9d687-149">Altında **vxMaintain etki alanı ve URL'leri**, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9d687-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Merhaba vxMaintain etki alanı ve URL'ler bölümü](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="9d687-151">a.</span><span class="sxs-lookup"><span data-stu-id="9d687-151">a.</span></span> <span data-ttu-id="9d687-152">Merhaba, **tanımlayıcısı** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="9d687-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="9d687-153">b.</span><span class="sxs-lookup"><span data-stu-id="9d687-153">b.</span></span> <span data-ttu-id="9d687-154">Merhaba, **yanıt URL'si** kutusuna sözdizimi aşağıdaki hello sahip bir URL yazın:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="9d687-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d687-155">Merhaba önceki değerleri gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="9d687-155">hello preceding values are not real.</span></span> <span data-ttu-id="9d687-156">Merhaba gerçek tanımlayıcısı ile güncelleştirin ve URL yanıt.</span><span class="sxs-lookup"><span data-stu-id="9d687-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="9d687-157">tooobtain hello değerleri, kişi hello [vxMaintain destek ekibi](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9d687-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="9d687-158">Altında **SAML imzalama sertifikası**seçin **meta veri XML**ve ardından hello meta veri dosya tooyour bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9d687-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![Merhaba "SAML imzalama sertifikası" bölümü](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="9d687-160">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9d687-160">Select **Save**.</span></span>

    ![Merhaba Kaydet düğmesi](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d687-162">tooconfigure **vxMaintain** SSO, indirilen gönderme hello **meta veri XML** toohello dosya [vxMaintain destek ekibi](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9d687-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="9d687-163">Merhaba uygulama ayarlama gibi hello yönergeleri önceki hello kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d687-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d687-164">Hello hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümü, select hello **çoklu oturum açma** sekmesini ve ardından erişim hello Merhaba belgelerinden katıştırılmış **yapılandırma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9d687-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="9d687-165">toolearn hello embedded belgeler özelliği hakkında daha fazla bilgi görmek [Kurumsal uygulamaları için çoklu oturum açmayı yönetme](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9d687-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9d687-166">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d687-166">Create an Azure AD test user</span></span>
<span data-ttu-id="9d687-167">Bu bölümde, test kullanıcı Britta Simon hello Azure portal hello aşağıdakileri yaparak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9d687-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Hello Azure AD test kullanıcısı][100]

1. <span data-ttu-id="9d687-169">Merhaba, **Azure portal**, buna hello sol bölmesinde, seçin hello **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d687-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![Merhaba "Azure Active Directory" düğmesi](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d687-171">Kullanıcıların, listesini toodisplay Git çok**kullanıcılar ve gruplar** > **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9d687-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="9d687-172">![Merhaba "Tüm kullanıcılar" bağlantı](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="9d687-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="9d687-173">Merhaba **tüm kullanıcılar** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="9d687-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="9d687-174">tooopen hello **kullanıcı** iletişim kutusunda **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9d687-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d687-176">Merhaba, **kullanıcı** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9d687-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d687-178">a.</span><span class="sxs-lookup"><span data-stu-id="9d687-178">a.</span></span> <span data-ttu-id="9d687-179">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d687-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d687-180">b.</span><span class="sxs-lookup"><span data-stu-id="9d687-180">b.</span></span> <span data-ttu-id="9d687-181">Merhaba, **kullanıcı adı** kutusunda, test kullanıcısının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="9d687-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="9d687-182">c.</span><span class="sxs-lookup"><span data-stu-id="9d687-182">c.</span></span> <span data-ttu-id="9d687-183">Select hello **Göster parola** onay kutusunu ve ardından hello oluşturulan Not hello değeri **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="9d687-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="9d687-184">d.</span><span class="sxs-lookup"><span data-stu-id="9d687-184">d.</span></span> <span data-ttu-id="9d687-185">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="9d687-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="9d687-186">VxMaintain test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d687-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="9d687-187">Bu bölümde, test kullanıcı Britta Simon vxMaintain oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d687-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="9d687-188">Merhaba vxMaintain Platform tooadd kullanıcıların çalışması ile [vxMaintain destek ekibi](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9d687-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="9d687-189">SSO kullanmadan önce oluşturup hello kullanıcıları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d687-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9d687-190">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="9d687-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9d687-191">Bu bölümde, test kullanıcısı Britta Simon toouse Azure SSO erişimi toovxMaintain vererek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d687-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="9d687-192">toodo, bu nedenle, hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9d687-192">toodo so, do hello following:</span></span>

![Test kullanıcısı hello görünen ad listesinde][200] 

1. <span data-ttu-id="9d687-194">Hello Azure portal'ın **uygulamaları** görüntülemek için çok gidin**Directory** Görünüm > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9d687-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Merhaba "Tüm uygulamaları" bağlantı][201] 

2. <span data-ttu-id="9d687-196">Merhaba, **uygulamaları** listesinde **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="9d687-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![Merhaba vxMaintain bağlantı](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="9d687-198">Merhaba sol bölmesinde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9d687-198">In hello left pane, select **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="9d687-200">Seçin **Ekle** ve ardından hello **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9d687-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][203]

5. <span data-ttu-id="9d687-202">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinden, **Britta Simon**seçip hello **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d687-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="9d687-203">Merhaba, **eklemek atama** iletişim kutusunda **atamak**.</span><span class="sxs-lookup"><span data-stu-id="9d687-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="9d687-204">Azure AD çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="9d687-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="9d687-205">Bu bölümde, hello erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.</span><span class="sxs-lookup"><span data-stu-id="9d687-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="9d687-206">Seçme hello **vxMaintain** hello erişim paneli parçasında oturumunuzu tooyour vxMaintain uygulamada otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="9d687-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="9d687-207">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d687-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d687-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d687-208">Next steps</span></span>

* [<span data-ttu-id="9d687-209">Azure Active Directory ile SaaS uygulamalarını tümleştirme öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="9d687-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d687-210">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9d687-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

