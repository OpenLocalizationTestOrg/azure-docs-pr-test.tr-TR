---
title: "Öğretici: Azure Active Directory Tümleştirme ile ClickTime | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile ClickTime arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="33fef-103">Öğretici: Azure Active Directory Tümleştirme ClickTime ile</span><span class="sxs-lookup"><span data-stu-id="33fef-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="33fef-104">Bu öğreticide, bilgi nasıl toointegrate ClickTime Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33fef-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33fef-105">ClickTime Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="33fef-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="33fef-106">Erişim tooClickTime sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="33fef-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="33fef-107">Kullanıcıların tooautomatically get açan tooClickTime (çoklu oturum açma) Azure AD hesaplarına sahip etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="33fef-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33fef-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="33fef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="33fef-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33fef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33fef-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="33fef-110">Prerequisites</span></span>

<span data-ttu-id="33fef-111">tooconfigure ClickTime ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="33fef-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="33fef-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="33fef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33fef-113">Bir ClickTime çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="33fef-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33fef-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="33fef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33fef-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="33fef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33fef-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="33fef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33fef-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33fef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33fef-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="33fef-118">Scenario description</span></span>
<span data-ttu-id="33fef-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="33fef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33fef-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="33fef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33fef-121">Merhaba Galerisi'nden ClickTime ekleme</span><span class="sxs-lookup"><span data-stu-id="33fef-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="33fef-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="33fef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="33fef-123">Merhaba Galerisi'nden ClickTime ekleme</span><span class="sxs-lookup"><span data-stu-id="33fef-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="33fef-124">Azure AD'ye tooconfigure hello tümleştirme ClickTime, tooadd ClickTime hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="33fef-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="33fef-125">**tooadd ClickTime hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="33fef-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="33fef-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="33fef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="33fef-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="33fef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="33fef-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="33fef-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="33fef-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="33fef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="33fef-133">Merhaba arama kutusuna yazın **ClickTime**seçin **ClickTime** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="33fef-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Merhaba sonuçları listesinde ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="33fef-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="33fef-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="33fef-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı ClickTime sınayın.</span><span class="sxs-lookup"><span data-stu-id="33fef-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33fef-137">Tek toowork'ın oturum açma hangi hello karşılık gelen ClickTime içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="33fef-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="33fef-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı ClickTime hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="33fef-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="33fef-139">Merhaba hello değeri ClickTime içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="33fef-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="33fef-140">tooconfigure ve ClickTime ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="33fef-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="33fef-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="33fef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="33fef-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="33fef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33fef-143">**[ClickTime test kullanıcısı oluşturma](#create-a-clicktime-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir ClickTime içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="33fef-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="33fef-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="33fef-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33fef-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="33fef-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="33fef-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="33fef-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="33fef-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma ClickTime uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="33fef-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="33fef-148">**tooconfigure Azure AD çoklu oturum açma ile ClickTime, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="33fef-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="33fef-149">Hello hello üzerinde Azure portal'ın **ClickTime** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="33fef-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="33fef-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="33fef-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="33fef-153">Merhaba üzerinde **ClickTime etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="33fef-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![ClickTime etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="33fef-155">a.</span><span class="sxs-lookup"><span data-stu-id="33fef-155">a.</span></span> <span data-ttu-id="33fef-156">Merhaba, **tanımlayıcısı** metin kutusuna, URL'yi yazın:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="33fef-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="33fef-157">b.</span><span class="sxs-lookup"><span data-stu-id="33fef-157">b.</span></span> <span data-ttu-id="33fef-158">Merhaba, **yanıt URL'si** metin kutusuna, türü aşağıdaki hello kullanarak bir URL düzenleri:</span><span class="sxs-lookup"><span data-stu-id="33fef-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="33fef-159">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve hello sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="33fef-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="33fef-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="33fef-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="33fef-163">Merhaba üzerinde **ClickTime yapılandırma** 'yi tıklatın **yapılandırma ClickTime** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="33fef-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="33fef-164">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="33fef-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ClickTime yapılandırma](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="33fef-166">Farklı web tarayıcısı penceresinde ClickTime şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="33fef-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="33fef-167">Merhaba üstte Hello araç çubuğunda **Tercihler**ve ardından **güvenlik ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="33fef-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="33fef-168">Merhaba, **tek oturum açma tercihleri** yapılandırma bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="33fef-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="33fef-169">![Güvenlik ayarları](./media/active-directory-saas-clicktime-tutorial/tic777280.png "güvenlik ayarları")</span><span class="sxs-lookup"><span data-stu-id="33fef-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="33fef-170">a.</span><span class="sxs-lookup"><span data-stu-id="33fef-170">a.</span></span>  <span data-ttu-id="33fef-171">Seçin **izin** çoklu oturum açma (SSO) ile kullanarak oturum açın **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="33fef-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="33fef-172">b.</span><span class="sxs-lookup"><span data-stu-id="33fef-172">b.</span></span> <span data-ttu-id="33fef-173">Merhaba, **kimlik sağlayıcısı Endpoint** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="33fef-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="33fef-174">c.</span><span class="sxs-lookup"><span data-stu-id="33fef-174">c.</span></span>  <span data-ttu-id="33fef-175">Açık hello **base-64 kodlamalı sertifika** Azure portalında indirilen **not defteri**hello içeriği Kopyala ve hello yapıştırma **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="33fef-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="33fef-176">d.</span><span class="sxs-lookup"><span data-stu-id="33fef-176">d.</span></span>  <span data-ttu-id="33fef-177">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33fef-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="33fef-178">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="33fef-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="33fef-179">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="33fef-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="33fef-180">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33fef-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="33fef-181">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="33fef-181">Create an Azure AD test user</span></span>
<span data-ttu-id="33fef-182">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="33fef-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="33fef-184">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="33fef-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="33fef-185">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="33fef-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33fef-187">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="33fef-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33fef-189">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="33fef-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![Merhaba Ekle düğmesi](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33fef-191">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="33fef-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33fef-193">a.</span><span class="sxs-lookup"><span data-stu-id="33fef-193">a.</span></span> <span data-ttu-id="33fef-194">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33fef-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33fef-195">b.</span><span class="sxs-lookup"><span data-stu-id="33fef-195">b.</span></span> <span data-ttu-id="33fef-196">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="33fef-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33fef-197">c.</span><span class="sxs-lookup"><span data-stu-id="33fef-197">c.</span></span> <span data-ttu-id="33fef-198">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="33fef-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="33fef-199">d.</span><span class="sxs-lookup"><span data-stu-id="33fef-199">d.</span></span> <span data-ttu-id="33fef-200">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33fef-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="33fef-201">ClickTime test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="33fef-201">Create a ClickTime test user</span></span>

<span data-ttu-id="33fef-202">ClickTime içine sipariş tooenable Azure AD kullanıcıların toolog bunların ClickTime sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="33fef-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="33fef-203">ClickTime Hello durumda sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="33fef-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="33fef-204">API'leri, Azure AD kullanıcı hesapları ClickTime tooprovision tarafından sağlanan veya herhangi diğer ClickTime kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33fef-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="33fef-205">**bir kullanıcı hesabı tooprovision hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="33fef-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="33fef-206">İçinde tooyour oturum **ClickTime** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="33fef-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="33fef-207">Merhaba üstte Hello araç çubuğunda **şirket**ve ardından **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="33fef-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="33fef-208">![Kişiler](./media/active-directory-saas-clicktime-tutorial/tic777282.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="33fef-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="33fef-209">Tıklatın **kişiyi ekler**.</span><span class="sxs-lookup"><span data-stu-id="33fef-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="33fef-210">![Kişi Ekle](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Kişi Ekle")</span><span class="sxs-lookup"><span data-stu-id="33fef-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="33fef-211">Hello yeni bir kişiye bölümü, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="33fef-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="33fef-212">![Kişiler](./media/active-directory-saas-clicktime-tutorial/tic777284.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="33fef-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="33fef-213">a.</span><span class="sxs-lookup"><span data-stu-id="33fef-213">a.</span></span>  <span data-ttu-id="33fef-214">Merhaba, **tam adı** metin kutusuna, tam ad kullanıcı türünü gibi **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="33fef-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="33fef-215">b.</span><span class="sxs-lookup"><span data-stu-id="33fef-215">b.</span></span>  <span data-ttu-id="33fef-216">Merhaba, **e-posta adresi** metin kutusuna, kullanıcının türü hello e-posta ister  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="33fef-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="33fef-217">İsterseniz, hello yeni kişi nesnesi ek özellikleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33fef-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="33fef-218">c.</span><span class="sxs-lookup"><span data-stu-id="33fef-218">c.</span></span>  <span data-ttu-id="33fef-219">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="33fef-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="33fef-220">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="33fef-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="33fef-221">Bu bölümde, erişim tooClickTime vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="33fef-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="33fef-223">**tooassign Britta Simon tooClickTime hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="33fef-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="33fef-224">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="33fef-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="33fef-226">Merhaba uygulamalar listesinde **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="33fef-226">In hello applications list, select **ClickTime**.</span></span>

    ![Merhaba uygulamalar listesinde ClickTimne bağlantı](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="33fef-228">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="33fef-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202] 

4. <span data-ttu-id="33fef-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="33fef-230">Click **Add** button.</span></span> <span data-ttu-id="33fef-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="33fef-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="33fef-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="33fef-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="33fef-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="33fef-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33fef-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="33fef-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="33fef-236">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="33fef-236">Test single sign-on</span></span>

<span data-ttu-id="33fef-237">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="33fef-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="33fef-238">Merhaba ClickTime hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour ClickTime uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="33fef-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="33fef-239">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="33fef-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="33fef-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="33fef-240">Additional resources</span></span>

* [<span data-ttu-id="33fef-241">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="33fef-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33fef-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="33fef-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

