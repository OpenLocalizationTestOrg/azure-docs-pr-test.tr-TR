---
title: "Öğretici: SAP Business ByDesign Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ve SAP Business ByDesign arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="9c9de-103">Öğretici: SAP Business ByDesign ile Azure Active Directory tümleştirme</span><span class="sxs-lookup"><span data-stu-id="9c9de-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="9c9de-104">Bu öğreticide, nasıl toointegrate SAP öğrenin iş ByDesign Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c9de-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c9de-105">SAP Business ByDesign Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9c9de-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9c9de-106">Erişim tooSAP iş ByDesign sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c9de-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="9c9de-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooSAP iş ByDesign (çoklu oturum açma) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c9de-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9c9de-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9c9de-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c9de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c9de-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9c9de-110">Prerequisites</span></span>

<span data-ttu-id="9c9de-111">SAP Business ByDesign ile Azure AD tümleştirme tooconfigure, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9c9de-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="9c9de-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9c9de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c9de-113">Bir SAP Business ByDesign çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="9c9de-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c9de-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9c9de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c9de-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9c9de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c9de-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9c9de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c9de-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c9de-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c9de-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9c9de-118">Scenario description</span></span>
<span data-ttu-id="9c9de-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c9de-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9c9de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c9de-121">SAP Business ByDesign hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="9c9de-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="9c9de-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9c9de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="9c9de-123">SAP Business ByDesign hello Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="9c9de-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="9c9de-124">Azure AD'ye tooconfigure hello tümleştirme SAP Business ByDesign, tooadd SAP Business ByDesign hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9c9de-125">**SAP Business ByDesign hello galerisinden tooadd hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9c9de-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c9de-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="9c9de-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9c9de-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="9c9de-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="9c9de-133">Merhaba arama kutusuna yazın **SAP Business ByDesign**seçin **SAP Business ByDesign** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9c9de-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign hello sonuçları listesinde](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9c9de-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9c9de-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9c9de-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma SAP Business "Britta Simon" adlı bir test kullanıcı tabanlı ByDesign ile test etme.</span><span class="sxs-lookup"><span data-stu-id="9c9de-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9c9de-137">Tek toowork'ın oturum açma hangi hello karşılık gelen SAP Business ByDesign içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="9c9de-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve SAP Business ByDesign hello ilgili kullanıcı arasındaki bağlantıyı ilişki kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="9c9de-139">SAP Business ByDesign içinde hello hello değerini atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9c9de-140">tooconfigure ve SAP Business ByDesign ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9c9de-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9c9de-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="9c9de-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9c9de-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="9c9de-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9c9de-143">**[SAP Business ByDesign test kullanıcısı oluşturma](#create-an-sap-business-bydesign-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir SAP Business ByDesign içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="9c9de-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9c9de-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9c9de-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c9de-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="9c9de-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9c9de-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9c9de-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9c9de-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma SAP Business ByDesign uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9c9de-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="9c9de-148">**SAP Business ByDesign ile Azure AD çoklu oturum açma tooconfigure hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9c9de-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c9de-149">Hello hello üzerinde Azure portal'ın **SAP Business ByDesign** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="9c9de-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9c9de-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="9c9de-153">Merhaba üzerinde **SAP Business ByDesign etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9c9de-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="9c9de-155">a.</span><span class="sxs-lookup"><span data-stu-id="9c9de-155">a.</span></span> <span data-ttu-id="9c9de-156">Merhaba, **oturum açma URL'si** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="9c9de-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="9c9de-157">b.</span><span class="sxs-lookup"><span data-stu-id="9c9de-157">b.</span></span> <span data-ttu-id="9c9de-158">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="9c9de-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9c9de-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-159">These values are not real.</span></span> <span data-ttu-id="9c9de-160">Bu güncelleştirme değerler ile Merhaba gerçek oturum açma URL'si ve tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9c9de-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9c9de-161">Kişi [SAP Business ByDesign istemci destek ekibi](https://www.sap.com/products/cloud-analytics.support.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="9c9de-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="9c9de-162">Merhaba üzerinde **kullanıcı öznitelikleri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9c9de-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign özniteliği bölümü](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="9c9de-164">a.</span><span class="sxs-lookup"><span data-stu-id="9c9de-164">a.</span></span> <span data-ttu-id="9c9de-165">İçinde **kullanıcı tanımlayıcısı** listesi, select hello **ExtractMailPrefix()** işlevi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="9c9de-166">b.</span><span class="sxs-lookup"><span data-stu-id="9c9de-166">b.</span></span> <span data-ttu-id="9c9de-167">Merhaba gelen **posta** listesi, uygulamanız için kullanmak istediğiniz toouse select hello kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9c9de-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="9c9de-168">Örneğin, toouse hello benzersiz kullanıcı tanımlayıcısı olarak EmployeeID istiyorsanız ve hello ExtensionAttribute2 hello öznitelik değeri depoladığınız ardından user.extensionattribute2 seçin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="9c9de-169">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="9c9de-171">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-171">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9c9de-173">Merhaba üzerinde **SAP Business ByDesign yapılandırma** 'yi tıklatın **yapılandırma SAP Business ByDesign** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9c9de-174">Kopya hello **SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="9c9de-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![SAP Business ByDesign yapılandırma](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="9c9de-176">tooget uygulamanız için yapılandırılmış SSO hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9c9de-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="9c9de-177">a.</span><span class="sxs-lookup"><span data-stu-id="9c9de-177">a.</span></span> <span data-ttu-id="9c9de-178">Yönetici haklarıyla tooyour SAP Business ByDesign Portal'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9c9de-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="9c9de-179">b.</span><span class="sxs-lookup"><span data-stu-id="9c9de-179">b.</span></span> <span data-ttu-id="9c9de-180">Çok gidin**uygulama ve kullanıcı yönetimi görevinin** hello tıklatıp **kimlik sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="9c9de-181">c.</span><span class="sxs-lookup"><span data-stu-id="9c9de-181">c.</span></span> <span data-ttu-id="9c9de-182">Tıklatın **yeni kimlik sağlayıcısı** ve hello Azure portal ' indirmiş select hello meta veri XML dosyası.</span><span class="sxs-lookup"><span data-stu-id="9c9de-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="9c9de-183">Merhaba meta verileri içe aktararak hello sistem otomatik olarak hello gerekli imza sertifikası ve şifreleme sertifikası karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="9c9de-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="9c9de-185">d.</span><span class="sxs-lookup"><span data-stu-id="9c9de-185">d.</span></span> <span data-ttu-id="9c9de-186">tooinclude hello **onaylama tüketici hizmeti URL'si** hello SAML isteği seçin **onaylama tüketici hizmeti URL'si dahil**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="9c9de-187">e.</span><span class="sxs-lookup"><span data-stu-id="9c9de-187">e.</span></span> <span data-ttu-id="9c9de-188">Tıklatın **çoklu oturum açmayı etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="9c9de-189">f.</span><span class="sxs-lookup"><span data-stu-id="9c9de-189">f.</span></span> <span data-ttu-id="9c9de-190">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-190">Save your changes.</span></span>
   
    <span data-ttu-id="9c9de-191">g.</span><span class="sxs-lookup"><span data-stu-id="9c9de-191">g.</span></span> <span data-ttu-id="9c9de-192">Merhaba tıklatın **My sistem** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-192">Click hello **My System** tab.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="9c9de-194">h.</span><span class="sxs-lookup"><span data-stu-id="9c9de-194">h.</span></span> <span data-ttu-id="9c9de-195">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, hangi hello Azure portal ' Merhaba, kopyaladığınız **Azure AD oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9c9de-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="9c9de-197">ı.</span><span class="sxs-lookup"><span data-stu-id="9c9de-197">i.</span></span> <span data-ttu-id="9c9de-198">Kullanıcı kimliği ve parola veya SSO ile seçerek oturum açma arasında Hello çalışan el ile seçip seçemeyeceğini belirtin **el ile kimlik sağlayıcısı seçimi**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="9c9de-199">j.</span><span class="sxs-lookup"><span data-stu-id="9c9de-199">j.</span></span> <span data-ttu-id="9c9de-200">Merhaba, **SSO URL** bölümünde, hello çalışan toologon toohello sistem tarafından kullanılması gereken hello URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="9c9de-201">Hello URL gönderilen tooEmployee açılır listesinde, aşağıdaki seçenekleri şu hello arasında seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c9de-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="9c9de-202">**SSO olmayan URL'si**</span><span class="sxs-lookup"><span data-stu-id="9c9de-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="9c9de-203">Merhaba sistemi yalnızca hello normal sistem URL toohello çalışan gönderir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="9c9de-204">Hello çalışan olamaz SSO kullanarak oturum açın ve parolayı kullanın veya gerekir bunun yerine sertifika.</span><span class="sxs-lookup"><span data-stu-id="9c9de-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="9c9de-205">**SSO URL'Sİ**</span><span class="sxs-lookup"><span data-stu-id="9c9de-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="9c9de-206">Merhaba sistemi yalnızca hello SSO URL toohello çalışan gönderir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="9c9de-207">Merhaba çalışan SSO kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="9c9de-208">Kimlik doğrulama isteği IDP hello yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="9c9de-209">**Otomatik Seçim**</span><span class="sxs-lookup"><span data-stu-id="9c9de-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="9c9de-210">SSO etkin değilse, hello sistem hello normal sistem URL toohello çalışan gönderir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="9c9de-211">SSO etkin değilse, hello sistem hello çalışan bir parolaya sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="9c9de-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="9c9de-212">Bir parola kullanılabilir durumdaysa, SSO URL'si ve olmayan SSO URL'si toohello çalışan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="9c9de-213">Bununla birlikte, Hello çalışan parolası yoksa, yalnızca hello SSO URL toohello çalışan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="9c9de-214">k.</span><span class="sxs-lookup"><span data-stu-id="9c9de-214">k.</span></span> <span data-ttu-id="9c9de-215">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="9c9de-216">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9c9de-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9c9de-217">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="9c9de-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9c9de-218">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c9de-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9c9de-219">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c9de-219">Create an Azure AD test user</span></span>

<span data-ttu-id="9c9de-220">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="9c9de-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="9c9de-222">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9c9de-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c9de-223">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9c9de-225">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9c9de-227">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="9c9de-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9c9de-229">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9c9de-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9c9de-231">a.</span><span class="sxs-lookup"><span data-stu-id="9c9de-231">a.</span></span> <span data-ttu-id="9c9de-232">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c9de-233">b.</span><span class="sxs-lookup"><span data-stu-id="9c9de-233">b.</span></span> <span data-ttu-id="9c9de-234">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="9c9de-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9c9de-235">c.</span><span class="sxs-lookup"><span data-stu-id="9c9de-235">c.</span></span> <span data-ttu-id="9c9de-236">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="9c9de-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9c9de-237">d.</span><span class="sxs-lookup"><span data-stu-id="9c9de-237">d.</span></span> <span data-ttu-id="9c9de-238">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9c9de-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="9c9de-239">SAP Business ByDesign test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c9de-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="9c9de-240">Bu bölümde, SAP Business ByDesign Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9c9de-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="9c9de-241">Lütfen çalışmak [SAP Business ByDesign istemci destek ekibi](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello kullanıcılar hello SAP Business ByDesign Platform.</span><span class="sxs-lookup"><span data-stu-id="9c9de-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="9c9de-242">Lütfen NameID değeri hello SAP Business ByDesign platform hello kullanıcıadı alanıyla eşleşmelidir emin olun.</span><span class="sxs-lookup"><span data-stu-id="9c9de-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9c9de-243">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="9c9de-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9c9de-244">Bu bölümde, erişim tooSAP iş ByDesign vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="9c9de-246">**tooassign Britta Simon tooSAP iş ByDesign hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9c9de-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c9de-247">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9c9de-249">Merhaba uygulamalar listesinde **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![Merhaba SAP Business ByDesign bağlantı hello uygulamalar listesinde](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="9c9de-251">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9c9de-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="9c9de-253">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9c9de-253">Click **Add** button.</span></span> <span data-ttu-id="9c9de-254">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9c9de-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="9c9de-256">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9c9de-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9c9de-257">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9c9de-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9c9de-258">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9c9de-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9c9de-259">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="9c9de-259">Test single sign-on</span></span>

<span data-ttu-id="9c9de-260">Bu bölümde, hello erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9c9de-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9c9de-261">Merhaba SAP Business ByDesign hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour SAP Business ByDesign uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c9de-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9c9de-262">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9c9de-262">Additional resources</span></span>

* [<span data-ttu-id="9c9de-263">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="9c9de-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c9de-264">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9c9de-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

