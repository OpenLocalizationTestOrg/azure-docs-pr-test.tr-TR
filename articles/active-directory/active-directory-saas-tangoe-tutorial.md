---
title: "Öğretici: Azure Active Directory Tümleştirme Tangoe komutu Premium Mobile ile | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Tangoe komutu Premium mobil arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="2e7a5-103">Öğretici: Azure Active Directory Tümleştirme Tangoe komutu Premium Mobile ile</span><span class="sxs-lookup"><span data-stu-id="2e7a5-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="2e7a5-104">Bu öğreticide, bilgi nasıl toointegrate Tangoe komutu Premium mobil Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e7a5-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e7a5-105">Tangoe komutu Premium mobil Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e7a5-106">Erişim tooTangoe komutu Premium mobil sahip Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2e7a5-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="2e7a5-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooTangoe komutu Premium mobil (çoklu oturum açma) etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2e7a5-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e7a5-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2e7a5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2e7a5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e7a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e7a5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2e7a5-110">Prerequisites</span></span>

<span data-ttu-id="2e7a5-111">tooconfigure Tangoe komutu Premium Mobile ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="2e7a5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2e7a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e7a5-113">Bir Tangoe komutu Premium mobil çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2e7a5-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e7a5-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e7a5-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e7a5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e7a5-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e7a5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e7a5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2e7a5-118">Scenario description</span></span>
<span data-ttu-id="2e7a5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e7a5-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e7a5-121">Merhaba Galerisi'nden Tangoe komutu Premium mobil ekleme</span><span class="sxs-lookup"><span data-stu-id="2e7a5-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="2e7a5-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2e7a5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="2e7a5-123">Merhaba Galerisi'nden Tangoe komutu Premium mobil ekleme</span><span class="sxs-lookup"><span data-stu-id="2e7a5-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="2e7a5-124">Azure AD'ye tooconfigure hello tümleştirme Tangoe komutu Premium Mobile tooadd Tangoe komutu Premium mobil hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e7a5-125">**tooadd Tangoe komutu Premium mobil hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e7a5-126">Merhaba, ** [Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e7a5-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e7a5-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-129">Then go too**All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2e7a5-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2e7a5-133">Merhaba arama kutusuna yazın **Tangoe komutu Premium mobil**seçin **Tangoe komutu Premium mobil** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="2e7a5-134">Tangoe komutu Premium mobil Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="2e7a5-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e7a5-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2e7a5-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2e7a5-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Tangoe komutu Premium "Britta Simon" adlı bir test kullanıcı tabanlı Mobile ile test etme.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e7a5-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Tangoe komutu Premium Mobile'da tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="2e7a5-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Tangoe komutu Premium Mobile'da hello ilgili kullanıcı arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="2e7a5-139">Merhaba hello değeri Tangoe komutu Premium Mobile'da atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2e7a5-140">tooconfigure ve Tangoe komutu Premium Mobile ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e7a5-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on) ** -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e7a5-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user) ** -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e7a5-143">**[Tangoe komutu Premium mobil test kullanıcısı oluşturma](#create-a-tangoe-command-premium-mobile-test-user) ** -toohave Britta Simon Mobile'da Tangoe komutu Premium bağlantılı toohello Azure AD kullanıcı gösterimi olan, karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e7a5-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e7a5-145">**[Test çoklu oturum açma](#test-single-sign-on) ** -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e7a5-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2e7a5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2e7a5-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Tangoe komutu Premium mobil uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="2e7a5-148">**Azure AD çoklu oturum açma tooconfigure Tangoe komutu Premium Mobile ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e7a5-149">Merhaba hello üzerinde Azure portal'ın **Tangoe komutu Premium mobil** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2e7a5-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML tabanlı oturum açma](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="2e7a5-153">Merhaba üzerinde **Tangoe komutu Premium mobil etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Tangoe komutu Premium mobil etki alanı ve URL'leri](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="2e7a5-155">a.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-155">a.</span></span> <span data-ttu-id="2e7a5-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="2e7a5-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="2e7a5-157">b.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-157">b.</span></span> <span data-ttu-id="2e7a5-158">Merhaba, **yanıt URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="2e7a5-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e7a5-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-159">These values are not real.</span></span> <span data-ttu-id="2e7a5-160">Bu değerleri hello gerçek yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="2e7a5-161">Kişi [Tangoe komutu Premium mobil istemci destek ekibi](https://www.tangoe.com/contact-2/) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="2e7a5-162">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![SAML imzalama sertifikası bölümü](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="2e7a5-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-164">Click **Save** button.</span></span>

    ![Kaydet düğmesi](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="2e7a5-166">Merhaba üzerinde **Tangoe komutu Premium mobil yapılandırma** 'yi tıklatın **yapılandırma Tangoe komutu Premium mobil** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2e7a5-167">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Tangoe komutu Premium mobil yapılandırma bölümü](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="2e7a5-169">tooget SSO yapılandırılmış uygulamanızın, kişi, [Tangoe komutu Premium mobil istemci destek ekibi](https://www.tangoe.com/contact-2/) ve hello şunları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="2e7a5-170">Merhaba indirilen meta veri dosyası</span><span class="sxs-lookup"><span data-stu-id="2e7a5-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="2e7a5-171">Merhaba **SAML varlık kimliği**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="2e7a5-172">Merhaba **SAML çoklu oturum açma hizmet URL'si**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="2e7a5-173">Merhaba **Sign-Out URL'si**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="2e7a5-174">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2e7a5-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2e7a5-175">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere ** Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2e7a5-176">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e7a5-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e7a5-177">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e7a5-177">Create an Azure AD test user</span></span>
<span data-ttu-id="2e7a5-178">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2e7a5-180">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e7a5-181">Merhaba, **Azure portal**, üzerinde sol gezinti bölmesinde Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e7a5-183">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Kullanıcıların ve grupların tüm kullanıcılar ->](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e7a5-185">tooopen hello **kullanıcı** iletişim kutusunda, tıklatın **Ekle** hello üstteki hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Kullanıcı ekle](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e7a5-187">Merhaba üzerinde **kullanıcı** iletişim sayfasında, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2e7a5-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Kullanıcı iletişim sayfası](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e7a5-189">a.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-189">a.</span></span> <span data-ttu-id="2e7a5-190">Merhaba, **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e7a5-191">b.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-191">b.</span></span> <span data-ttu-id="2e7a5-192">Merhaba, **kullanıcı adı** metin kutusuna, türü hello **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e7a5-193">c.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-193">c.</span></span> <span data-ttu-id="2e7a5-194">Seçin **Göster parola** ve hello hello değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2e7a5-195">d.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-195">d.</span></span> <span data-ttu-id="2e7a5-196">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="2e7a5-197">Tangoe komutu Premium mobil test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e7a5-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="2e7a5-198">Bu bölümde, Britta Simon Tangoe komutu Premium Mobile'da adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="2e7a5-199">Çoklu oturum açma işleminden önce hello uygulamada sağlanan tüm hello kullanıcılar toobe Tangoe komutu Premium mobil uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="2e7a5-200">İş, bu nedenle Lütfen hello ile [Tangoe komutu Premium mobil istemci destek ekibi](https://www.tangoe.com/contact-2/) tooprovision bu kullanıcılar hello uygulamaya.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2e7a5-201">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="2e7a5-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2e7a5-202">Bu bölümde, erişim tooTangoe komutu Premium mobil vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2e7a5-204">**tooassign Britta Simon tooTangoe komutu Premium mobil hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2e7a5-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e7a5-205">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2e7a5-207">Merhaba uygulamalar listesinde **Tangoe komutu Premium mobil**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe komutu Premium mobil uygulama listesinde](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="2e7a5-209">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2e7a5-211">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-211">Click **Add** button.</span></span> <span data-ttu-id="2e7a5-212">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2e7a5-214">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e7a5-215">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e7a5-216">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2e7a5-217">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="2e7a5-217">Test single sign-on</span></span>

<span data-ttu-id="2e7a5-218">Bu bölümde, Azure AD SSO yapılandırmanızı hello erişim paneli kullanarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2e7a5-219">Merhaba Tangoe komutu Premium mobil hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma Tangoe komutu Premium mobil uygulama tooyour almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e7a5-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="2e7a5-220">Erişim paneli hakkında daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e7a5-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e7a5-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2e7a5-221">Additional resources</span></span>

* [<span data-ttu-id="2e7a5-222">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="2e7a5-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e7a5-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2e7a5-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

