---
title: "Öğretici: Azure Active Directory Tümleştirme ile haberci | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile haberci arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="ece95-103">Öğretici: Azure Active Directory Tümleştirme haberci ile</span><span class="sxs-lookup"><span data-stu-id="ece95-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="ece95-104">Bu öğreticide, bilgi nasıl toointegrate haberci Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ece95-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ece95-105">Haberci Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ece95-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ece95-106">Erişim tooEnvoy sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece95-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="ece95-107">Kullanıcıların tooautomatically get açan tooEnvoy (çoklu oturum açma) Azure AD hesaplarına ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ece95-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ece95-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="ece95-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ece95-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ece95-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ece95-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ece95-110">Prerequisites</span></span>

<span data-ttu-id="ece95-111">tooconfigure haberci ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ece95-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="ece95-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="ece95-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ece95-113">Bir haberci çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="ece95-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ece95-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ece95-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ece95-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ece95-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ece95-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ece95-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ece95-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ece95-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ece95-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="ece95-118">Scenario description</span></span>
<span data-ttu-id="ece95-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="ece95-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ece95-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="ece95-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ece95-121">Merhaba Galerisi'nden haberci ekleme</span><span class="sxs-lookup"><span data-stu-id="ece95-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="ece95-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="ece95-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="ece95-123">Merhaba Galerisi'nden haberci ekleme</span><span class="sxs-lookup"><span data-stu-id="ece95-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="ece95-124">Azure AD'ye tooconfigure hello tümleştirme haberci, tooadd haberci hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ece95-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ece95-125">**tooadd haberci hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ece95-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ece95-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="ece95-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="ece95-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="ece95-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ece95-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ece95-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="ece95-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ece95-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="ece95-133">Merhaba arama kutusuna yazın **haberci**seçin **haberci** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ece95-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde haberci](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ece95-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="ece95-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ece95-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı haberci sınayın.</span><span class="sxs-lookup"><span data-stu-id="ece95-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ece95-137">Tek toowork'ın oturum açma hangi hello karşılık gelen haberci içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="ece95-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="ece95-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı haberci hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ece95-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="ece95-139">Merhaba hello değeri haberci içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="ece95-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ece95-140">tooconfigure ve haberci ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ece95-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ece95-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="ece95-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ece95-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="ece95-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ece95-143">**[Bir haberci test kullanıcısı oluşturma](#create-an-envoy-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir haberci içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="ece95-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ece95-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ece95-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ece95-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="ece95-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ece95-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ece95-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ece95-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma haberci uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ece95-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="ece95-148">**tooconfigure Azure AD çoklu oturum açma ile haberci, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ece95-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="ece95-149">Hello hello üzerinde Azure portal'ın **haberci** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="ece95-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="ece95-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="ece95-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="ece95-153">Merhaba üzerinde **haberci etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ece95-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Haberci etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="ece95-155">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="ece95-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ece95-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="ece95-156">This value is not real.</span></span> <span data-ttu-id="ece95-157">Bu değer ile Merhaba güncelleştirme gerçek oturum açma URL'si.</span><span class="sxs-lookup"><span data-stu-id="ece95-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ece95-158">Kişi [haberci istemci destek ekibi](https://envoy.com/contact/) tooget bu değer.</span><span class="sxs-lookup"><span data-stu-id="ece95-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="ece95-159">Merhaba üzerinde **SAML imzalama sertifikası** bölümü, kopyalama hello **parmak İZİ** sertifika değerini...</span><span class="sxs-lookup"><span data-stu-id="ece95-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="ece95-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ece95-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ece95-163">Merhaba üzerinde **haberci yapılandırma** 'yi tıklatın **yapılandırma haberci** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="ece95-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ece95-164">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="ece95-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Haberci yapılandırma](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="ece95-166">Farklı web tarayıcısı penceresinde haberci şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ece95-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="ece95-167">Merhaba üstte Hello araç çubuğunda **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ece95-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="ece95-168">![Haberci](./media/active-directory-saas-envoy-tutorial/ic776782.png "haberci")</span><span class="sxs-lookup"><span data-stu-id="ece95-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="ece95-169">Tıklatın **şirket**.</span><span class="sxs-lookup"><span data-stu-id="ece95-169">Click **Company**.</span></span>

    <span data-ttu-id="ece95-170">![Şirket](./media/active-directory-saas-envoy-tutorial/ic776783.png "şirket")</span><span class="sxs-lookup"><span data-stu-id="ece95-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="ece95-171">Tıklatın **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ece95-171">Click **SAML**.</span></span>

    <span data-ttu-id="ece95-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="ece95-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="ece95-173">Merhaba, **SAML kimlik doğrulaması** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ece95-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="ece95-174">![SAML kimlik doğrulaması](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="ece95-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="ece95-175">Hello hello denetim merkezini konum kimliği için hello uygulama tarafından üretilen otomatik bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="ece95-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="ece95-176">a.</span><span class="sxs-lookup"><span data-stu-id="ece95-176">a.</span></span> <span data-ttu-id="ece95-177">İçinde **parmak izi** metin kutusuna, Yapıştır hello **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="ece95-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ece95-178">b.</span><span class="sxs-lookup"><span data-stu-id="ece95-178">b.</span></span> <span data-ttu-id="ece95-179">Yapıştır **SAML çoklu oturum açma hizmet URL'si** kopyaladığınız değeri form hello Azure portal hello içine **kimlik SAĞLAYICISI HTTP SAML URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="ece95-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="ece95-180">c.</span><span class="sxs-lookup"><span data-stu-id="ece95-180">c.</span></span> <span data-ttu-id="ece95-181">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ece95-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ece95-182">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="ece95-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ece95-183">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="ece95-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ece95-184">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ece95-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ece95-185">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ece95-185">Create an Azure AD test user</span></span>

<span data-ttu-id="ece95-186">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="ece95-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="ece95-188">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ece95-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ece95-189">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ece95-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ece95-191">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="ece95-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ece95-193">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="ece95-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ece95-195">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ece95-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ece95-197">a.</span><span class="sxs-lookup"><span data-stu-id="ece95-197">a.</span></span> <span data-ttu-id="ece95-198">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ece95-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ece95-199">b.</span><span class="sxs-lookup"><span data-stu-id="ece95-199">b.</span></span> <span data-ttu-id="ece95-200">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="ece95-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ece95-201">c.</span><span class="sxs-lookup"><span data-stu-id="ece95-201">c.</span></span> <span data-ttu-id="ece95-202">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="ece95-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ece95-203">d.</span><span class="sxs-lookup"><span data-stu-id="ece95-203">d.</span></span> <span data-ttu-id="ece95-204">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ece95-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="ece95-205">Bir haberci test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ece95-205">Create an Envoy test user</span></span>

<span data-ttu-id="ece95-206">TooEnvoy sağlama, tooconfigure kullanıcı için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="ece95-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="ece95-207">Atanmış bir kullanıcı hello erişim paneli kullanılarak haberci toolog çalıştığında haberci hello kullanıcı var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="ece95-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="ece95-208">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, haberci tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ece95-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ece95-209">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="ece95-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ece95-210">Bu bölümde, erişim tooEnvoy vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ece95-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="ece95-212">**tooassign Britta Simon tooEnvoy hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ece95-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="ece95-213">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="ece95-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="ece95-215">Merhaba uygulamalar listesinde **haberci**.</span><span class="sxs-lookup"><span data-stu-id="ece95-215">In hello applications list, select **Envoy**.</span></span>

    ![Merhaba haberci bağlantı hello uygulamalar listesinde](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="ece95-217">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="ece95-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="ece95-219">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ece95-219">Click **Add** button.</span></span> <span data-ttu-id="ece95-220">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ece95-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="ece95-222">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="ece95-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ece95-223">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ece95-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ece95-224">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ece95-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ece95-225">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="ece95-225">Test single sign-on</span></span>

<span data-ttu-id="ece95-226">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="ece95-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ece95-227">Merhaba haberci hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour haberci uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ece95-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="ece95-228">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ece95-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ece95-229">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ece95-229">Additional resources</span></span>

* [<span data-ttu-id="ece95-230">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="ece95-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ece95-231">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="ece95-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

