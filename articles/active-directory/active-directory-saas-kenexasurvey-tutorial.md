---
title: "Öğretici: Azure Active Directory Tümleştirme ile IBM Kenexa anket Kurumsal | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile IBM Kenexa anket kuruluş arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="32f1b-103">Öğretici: Azure Active Directory Tümleştirme ile IBM Kenexa anket Enterprise</span><span class="sxs-lookup"><span data-stu-id="32f1b-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="32f1b-104">Bu öğreticide, bilgi nasıl toointegrate IBM Kenexa anket kuruluş Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32f1b-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32f1b-105">IBM Kenexa anket kuruluş Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="32f1b-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32f1b-106">Erişim tooIBM Kenexa anket Kurumsal sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32f1b-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="32f1b-107">Azure AD hesaplarına ile çoklu oturum açma (SSO) kullanarak, kullanıcılar tooautomatically oturum açma tooIBM Kenexa anket Kurumsal etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32f1b-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="32f1b-108">Hesaplarınızı tek bir merkezi konumda yönetebilirsiniz: Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="32f1b-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="32f1b-109">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak tooknow yazılım hakkında daha fazla bilgi istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32f1b-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32f1b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="32f1b-110">Prerequisites</span></span>

<span data-ttu-id="32f1b-111">IBM Kenexa anket Kurumsal ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="32f1b-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="32f1b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="32f1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32f1b-113">IBM Kenexa anket Kurumsal SSO etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="32f1b-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32f1b-114">Bu öğreticide hello adımları test ettiğinizde, bir üretim ortamında kullanmayın öneririz.</span><span class="sxs-lookup"><span data-stu-id="32f1b-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="32f1b-115">Bu öğreticide tootest hello adımları bu önerileri izleyin:</span><span class="sxs-lookup"><span data-stu-id="32f1b-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="32f1b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="32f1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32f1b-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32f1b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32f1b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="32f1b-118">Scenario description</span></span>
<span data-ttu-id="32f1b-119">Bu öğreticide, Azure AD SSO bir test ortamında test.</span><span class="sxs-lookup"><span data-stu-id="32f1b-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="32f1b-120">Merhaba öğreticide özetlenen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="32f1b-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="32f1b-121">IBM Kenexa anket Kurumsal hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="32f1b-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="32f1b-122">Yapılandırma ve Azure AD SSO test etme</span><span class="sxs-lookup"><span data-stu-id="32f1b-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="32f1b-123">IBM Kenexa anket Kurumsal hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="32f1b-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="32f1b-124">Azure AD'ye IBM Kenexa anket Enterprise tooconfigure hello tümleştirme hello galeri tooyour listesinden yönetilen SaaS uygulamaları IBM Kenexa anket Kurumsal ekleyin.</span><span class="sxs-lookup"><span data-stu-id="32f1b-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32f1b-125">tooadd IBM Kenexa anket Kurumsal hello galerisinden hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="32f1b-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="32f1b-126">Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="32f1b-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="32f1b-130">bir uygulama, tooadd tıklatın hello **yeni uygulama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-130">tooadd an application, click hello **New application** button.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="32f1b-132">Merhaba arama kutusuna yazın **IBM Kenexa anket Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="32f1b-134">Hello sonuçlar listesinde seçin **IBM Kenexa anket Kurumsal**ve ardından hello **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="32f1b-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa anket Kurumsal hello sonuçları listesinde](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="32f1b-136">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="32f1b-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="32f1b-137">Bu bölümde, yapılandırma ve Azure AD SSO IBM Kenexa anket "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı kuruluş ile test etme</span><span class="sxs-lookup"><span data-stu-id="32f1b-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32f1b-138">SSO toowork için Azure AD, Azure AD'de tooidentify hello IBM Kenexa anket Kurumsal kullanıcı karşılık gelen gerekir.</span><span class="sxs-lookup"><span data-stu-id="32f1b-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="32f1b-139">Diğer bir deyişle, Azure AD IBM Kenexa anket kuruluşta bir Azure AD kullanıcısının ve ilgili kullanıcı arasında bir bağlantı ilişkisi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="32f1b-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="32f1b-140">tooestablish hello bağlantı ilişkisi, Ata hello hello değerini **kullanıcı adı** kuruluştaki IBM Kenexa anket hello hello değeri olarak **kullanıcıadı** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="32f1b-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="32f1b-141">tooconfigure ve test IBM Kenexa anket Enterprise, tam ile Azure AD SSO hello sonraki iki bölümde yapı taşları hello.</span><span class="sxs-lookup"><span data-stu-id="32f1b-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="32f1b-142">Azure AD SSO yapılandırın</span><span class="sxs-lookup"><span data-stu-id="32f1b-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="32f1b-143">Bu bölümdeki hello Azure portalında Azure AD SSO'yu etkinleştirmek ve SSO hello aşağıdakileri yaparak IBM Kenexa anket Kurumsal uygulamanızda yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="32f1b-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="32f1b-144">Merhaba hello üzerinde Azure portal'ın **IBM Kenexa anket Kurumsal** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Oturum açma tek bağlantı IBM Kenexa anket Kurumsal yapılandırma][4]

2. <span data-ttu-id="32f1b-146">Merhaba, **çoklu oturum açma** iletişim kutusunda hello **modu** kutusunda **SAML tabanlı oturum açma** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="32f1b-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="32f1b-148">Merhaba, **IBM Kenexa anket kuruluş etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32f1b-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![IBM Kenexa anket kuruluş etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="32f1b-150">a.</span><span class="sxs-lookup"><span data-stu-id="32f1b-150">a.</span></span> <span data-ttu-id="32f1b-151">Merhaba, **tanımlayıcısı** metin kutusuna, desen aşağıdaki hello bir URL türüyle:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="32f1b-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="32f1b-152">b.</span><span class="sxs-lookup"><span data-stu-id="32f1b-152">b.</span></span> <span data-ttu-id="32f1b-153">Merhaba, **yanıt URL'si** metin kutusuna, desen aşağıdaki hello bir URL türüyle:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="32f1b-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32f1b-154">Merhaba önceki değerleri gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="32f1b-154">hello preceding values are not real.</span></span> <span data-ttu-id="32f1b-155">Merhaba gerçek tanımlayıcısı ile güncelleştirin ve URL yanıt.</span><span class="sxs-lookup"><span data-stu-id="32f1b-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="32f1b-156">tooobtain hello gerçek değerler, kişi hello [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="32f1b-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="32f1b-157">Altında **SAML imzalama sertifikası**, tıklatın **sertifika (Base64)**ve ardından hello sertifika dosya tooyour bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="32f1b-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![Merhaba sertifika (Base64) indirme bağlantısı](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="32f1b-159">Merhaba IBM Kenexa anket Kurumsal uygulama, tooadd özel öznitelik eşlemeleri toohello yapılandırması, SAML belirteci özniteliklerin gerektiren belirli bir biçimde, tooreceive hello güvenlik onaylar biçimlendirme dili (SAML) onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="32f1b-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="32f1b-160">Merhaba hello yanıt hello kullanıcı tanımlayıcısı talebin değeri hello hello Kenexa sistemde yapılandırılmış SSO kimliği eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="32f1b-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="32f1b-161">toomap kuruluşunuzdaki SSO Internet Veri Birimi Protokolü (IDP) olarak uygun kullanıcı tanımlayıcısı Merhaba, iş ile Merhaba [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="32f1b-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="32f1b-162">Varsayılan olarak, Azure AD hello kullanıcı tanımlayıcısı hello kullanıcı asıl adı (UPN) değeri olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="32f1b-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="32f1b-163">Merhaba bu değeri değiştirebilirsiniz **özniteliği** sekmesinde, aşağıdaki ekran görüntüsü hello gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="32f1b-164">yalnızca doğru eşleme hello tamamladıktan sonra hello tümleştirme çalışır.</span><span class="sxs-lookup"><span data-stu-id="32f1b-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![Merhaba kullanıcı öznitelikleri iletişim kutusu](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="32f1b-166">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32f1b-166">Click **Save**.</span></span>

    ![Merhaba yapılandırma çoklu oturum açma düğmesi Kaydet](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32f1b-168">tooopen hello **yapılandırma oturum açma** penceresi altında **IBM Kenexa anket Kurumsal yapılandırma**, tıklatın **IBM Kenexa anket Kurumsal yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![Merhaba IBM Kenexa anket Kurumsal yapılandırma bağlantısı](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="32f1b-170">Kopya hello **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** hello değerlerinden **hızlı başvuru** bölümü.</span><span class="sxs-lookup"><span data-stu-id="32f1b-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="32f1b-171">Merhaba, **yapılandırma oturum açma** penceresi altında **hızlı başvuru**, kopya hello **Sign-Out URL**, **SAML varlık kimliği**, ve  **SAML çoklu oturum açma hizmet URL'si** değerleri.</span><span class="sxs-lookup"><span data-stu-id="32f1b-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="32f1b-172">tooconfigure SSO hello üzerinde **IBM Kenexa anket Kurumsal** tarafı, indirilen hello Gönder **sertifika (Base64)**, **Sign-Out URL**, **SAML varlık kimliği**, ve **SAML çoklu oturum açma hizmet URL'si** toohello değerleri [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="32f1b-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="32f1b-173">Merhaba Bu yönergelerde kısa sürümü tooa başvurabilir [Azure portal](https://portal.azure.com) hello uygulaması kuruluyor sırada.</span><span class="sxs-lookup"><span data-stu-id="32f1b-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="32f1b-174">Hello hello uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesini tıklatın ve ardından erişim Merhaba katıştırılmış hello aracılığıyla belgelere **yapılandırma** hello sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="32f1b-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="32f1b-175">toolearn hello embedded belgeler özelliği hakkında daha fazla bilgi görmek [Azure AD embedded belgeler](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="32f1b-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="32f1b-176">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32f1b-176">Create an Azure AD test user</span></span>
<span data-ttu-id="32f1b-177">Bu bölümde, test kullanıcı Britta Simon hello Azure portal hello aşağıdakileri yaparak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="32f1b-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

1. <span data-ttu-id="32f1b-179">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32f1b-181">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32f1b-183">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="32f1b-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32f1b-185">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32f1b-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32f1b-187">a.</span><span class="sxs-lookup"><span data-stu-id="32f1b-187">a.</span></span> <span data-ttu-id="32f1b-188">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32f1b-189">b.</span><span class="sxs-lookup"><span data-stu-id="32f1b-189">b.</span></span> <span data-ttu-id="32f1b-190">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="32f1b-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="32f1b-191">c.</span><span class="sxs-lookup"><span data-stu-id="32f1b-191">c.</span></span> <span data-ttu-id="32f1b-192">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="32f1b-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="32f1b-193">d.</span><span class="sxs-lookup"><span data-stu-id="32f1b-193">d.</span></span> <span data-ttu-id="32f1b-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32f1b-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="32f1b-195">IBM Kenexa anket Kurumsal test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32f1b-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="32f1b-196">Bu bölümde, IBM Kenexa anket kuruluşta Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32f1b-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="32f1b-197">toocreate kullanıcılar hello IBM Kenexa anket Enterprise sistemi ve bunlar için harita hello SSO kimliği ile Merhaba çalışabilir [IBM Kenexa anket kurumsal destek ekibi](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="32f1b-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="32f1b-198">Bu SSO kimlik değeri ayrıca olmalıdır toohello kullanıcı tanımlayıcısı değeri Azure AD'den eşlenmiş.</span><span class="sxs-lookup"><span data-stu-id="32f1b-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="32f1b-199">Merhaba bu varsayılan ayarı değiştirebilirsiniz **özniteliği** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="32f1b-200">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="32f1b-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="32f1b-201">Bu bölümde, kullanıcı Britta Simon toouse Azure SSO erişimi tooIBM Kenexa anket Kurumsal vererek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="32f1b-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="32f1b-203">tooassign kullanıcı Britta Simon tooIBM Kenexa anket Kurumsal hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="32f1b-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="32f1b-204">Hello Azure portal, hello açın **uygulamaları** görüntülemek için Git toohello **dizin** görünümü, select **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Merhaba "Kurumsal uygulamalar" ve "Tüm uygulamaları" bağlantılar][201] 

2. <span data-ttu-id="32f1b-206">Merhaba, **uygulamaları** listesinde **IBM Kenexa anket Kurumsal**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![Merhaba IBM Kenexa anket Kurumsal bağlantı hello uygulamalar listesinde](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="32f1b-208">Merhaba sol bölmede **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-208">In hello left pane, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="32f1b-210">Merhaba tıklatın **Ekle** düğmesine ve ardından hello **eklemek atama** bölmesinde, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="32f1b-212">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda hello **kullanıcılar** listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="32f1b-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="32f1b-213">Merhaba, **kullanıcılar ve gruplar** iletişim kutusunda, hello **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="32f1b-214">Merhaba, **eklemek atama** iletişim hello kutusunda, **atamak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32f1b-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="32f1b-215">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="32f1b-215">Test single sign-on</span></span>

<span data-ttu-id="32f1b-216">Bu bölümde, hello erişim paneli kullanarak Azure AD SSO yapılandırmanızı sınayın.</span><span class="sxs-lookup"><span data-stu-id="32f1b-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="32f1b-217">Merhaba tıkladığınızda **IBM Kenexa anket Kurumsal** parçasında Merhaba erişim paneli, tooyour IBM Kenexa anket Kurumsal uygulama otomatik olarak imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="32f1b-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32f1b-218">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="32f1b-218">Additional resources</span></span>

* [<span data-ttu-id="32f1b-219">İlgili nasıl öğreticiler listesi Azure Active Directory ile toointegrate SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="32f1b-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32f1b-220">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="32f1b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
