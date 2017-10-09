---
title: "Öğretici: Azure Active Directory Tümleştirme ile Ceridian Dayforce HCM | Microsoft Docs"
description: "Tooconfigure nasıl çoklu oturum açma öğrenin Azure Active Directory ile Ceridian Dayforce HCM arasında."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="d0c74-103">Öğretici: Azure Active Directory Tümleştirme Ceridian Dayforce HCM ile</span><span class="sxs-lookup"><span data-stu-id="d0c74-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="d0c74-104">Bu öğreticide, bilgi nasıl toointegrate Ceridian Dayforce HCM Azure Active Directory'ye (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0c74-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0c74-105">Ceridian Dayforce HCM Azure AD ile tümleştirme ile Merhaba aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d0c74-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0c74-106">Erişim tooCeridian Dayforce HCM sahip Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c74-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="d0c74-107">Azure AD hesaplarına ile kullanıcılar tooautomatically get açan tooCeridian Dayforce HCM (çoklu oturum açma) etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0c74-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d0c74-108">Hesaplarınızı bir merkezi konumda - hello Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d0c74-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı tooknow istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c74-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0c74-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d0c74-110">Prerequisites</span></span>

<span data-ttu-id="d0c74-111">tooconfigure Ceridian Dayforce HCM ile Azure AD tümleştirme, aşağıdaki öğelerindeki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0c74-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="d0c74-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d0c74-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0c74-113">Bir Ceridian Dayforce HCM çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="d0c74-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0c74-114">tootest hello bu öğreticideki adımlar, bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d0c74-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0c74-115">Bu öğreticide tootest hello adımları, bu önerileri izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0c74-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0c74-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d0c74-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0c74-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0c74-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0c74-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d0c74-118">Scenario description</span></span>
<span data-ttu-id="d0c74-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d0c74-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0c74-120">Bu öğreticide gösterilen hello senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d0c74-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0c74-121">Merhaba Galerisi'nden Ceridian Dayforce HCM ekleme</span><span class="sxs-lookup"><span data-stu-id="d0c74-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="d0c74-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d0c74-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="d0c74-123">Merhaba Galerisi'nden Ceridian Dayforce HCM ekleme</span><span class="sxs-lookup"><span data-stu-id="d0c74-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="d0c74-124">Azure AD'ye tooconfigure hello tümleştirme Ceridian Dayforce HCM, tooadd Ceridian Dayforce HCM hello galeri tooyour listesinden yönetilen SaaS uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0c74-125">**tooadd Ceridian Dayforce HCM hello galerisinden hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d0c74-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c74-126">Merhaba,  **[Azure portal](https://portal.azure.com)**, üzerinde sol gezinti bölmesini Merhaba, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Hello Azure Active Directory düğmesi][1]

2. <span data-ttu-id="d0c74-128">Çok gidin**kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0c74-129">Çok Git**tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-129">Then go too**All applications**.</span></span>

    ![Merhaba kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="d0c74-131">tooadd yeni uygulama tıklatın **yeni uygulama** iletişim hello üstte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Merhaba yeni uygulama düğmesi][3]

4. <span data-ttu-id="d0c74-133">Merhaba arama kutusuna yazın **Ceridian Dayforce HCM**seçin **Ceridian Dayforce HCM** sonuç panelinden ardından **Ekle** düğmesini tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d0c74-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ceridian Dayforce HCM hello sonuçları listesinde](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d0c74-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d0c74-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d0c74-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Ceridian Dayforce "Britta Simon" adlı bir test kullanıcı tabanlı HCM ile test etme.</span><span class="sxs-lookup"><span data-stu-id="d0c74-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0c74-137">Tek toowork'ın oturum açma hangi hello karşılık gelen Ceridian Dayforce HCM içinde tooa kullanıcı Azure AD içinde olduğu Azure AD tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="d0c74-138">Diğer bir deyişle, bir Azure AD kullanıcı ve ilgili kullanıcı Ceridian Dayforce HCM hello arasında bir bağlantı ilişkisi kurulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="d0c74-139">Merhaba hello değeri Ceridian Dayforce HCM içinde atayın **kullanıcı adı** hello hello değeri olarak Azure AD'de **kullanıcıadı** tooestablish hello bağlantı ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d0c74-140">tooconfigure ve Ceridian Dayforce HCM ile Azure AD çoklu oturum açmayı test, yapı taşları aşağıdaki toocomplete hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0c74-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0c74-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  -tooenable kullanıcılar toouse bu özellik.</span><span class="sxs-lookup"><span data-stu-id="d0c74-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0c74-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  -tootest Azure AD çoklu oturum açma Britta Simon ile.</span><span class="sxs-lookup"><span data-stu-id="d0c74-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0c74-143">**[Ceridian Dayforce HCM test kullanıcısı oluşturma](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave Britta Simon kullanıcı bağlantılı toohello Azure AD gösterimidir Ceridian Dayforce HCM içinde karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="d0c74-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0c74-144">**[Hello Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d0c74-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0c74-145">**[Test çoklu oturum açma](#test-single-sign-on)**  -tooverify olup hello yapılandırma çalışır.</span><span class="sxs-lookup"><span data-stu-id="d0c74-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d0c74-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d0c74-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d0c74-147">Bu bölümde, Azure AD çoklu oturum açma hello Azure portal'ın etkinleştirin ve çoklu oturum açma Ceridian Dayforce HCM uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d0c74-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="d0c74-148">**Azure AD çoklu oturum açma tooconfigure Ceridian Dayforce HCM ile Merhaba aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d0c74-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c74-149">Hello hello üzerinde Azure portal'ın **Ceridian Dayforce HCM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="d0c74-151">Merhaba üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** tooenable çoklu oturum açma.</span><span class="sxs-lookup"><span data-stu-id="d0c74-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="d0c74-153">Merhaba üzerinde **Ceridian Dayforce HCM etki alanı ve URL'leri** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d0c74-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="d0c74-155">a.</span><span class="sxs-lookup"><span data-stu-id="d0c74-155">a.</span></span> <span data-ttu-id="d0c74-156">Merhaba, **oturum üzerinde URL'si** metin kutusuna, türü hello URL, kullanıcıların toosign üzerinde tooyour tarafından Ceridian Dayforce HCM uygulama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0c74-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="d0c74-157">Ortam</span><span class="sxs-lookup"><span data-stu-id="d0c74-157">Environment</span></span> | <span data-ttu-id="d0c74-158">URL</span><span class="sxs-lookup"><span data-stu-id="d0c74-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="d0c74-159">Üretim için</span><span class="sxs-lookup"><span data-stu-id="d0c74-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="d0c74-160">Test için</span><span class="sxs-lookup"><span data-stu-id="d0c74-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="d0c74-161">b.</span><span class="sxs-lookup"><span data-stu-id="d0c74-161">b.</span></span> <span data-ttu-id="d0c74-162">Merhaba, **tanımlayıcısı** metin kutusuna, bir desen aşağıdaki hello kullanarak URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="d0c74-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="d0c74-163">Ortam</span><span class="sxs-lookup"><span data-stu-id="d0c74-163">Environment</span></span> | <span data-ttu-id="d0c74-164">URL</span><span class="sxs-lookup"><span data-stu-id="d0c74-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="d0c74-165">Üretim için</span><span class="sxs-lookup"><span data-stu-id="d0c74-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="d0c74-166">Test için</span><span class="sxs-lookup"><span data-stu-id="d0c74-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="d0c74-167">c.</span><span class="sxs-lookup"><span data-stu-id="d0c74-167">c.</span></span> <span data-ttu-id="d0c74-168">Merhaba, **yanıt URL'si** metin kutusuna, Azure AD toopost hello yanıt tarafından kullanılan türü hello URL.</span><span class="sxs-lookup"><span data-stu-id="d0c74-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="d0c74-169">Ortam</span><span class="sxs-lookup"><span data-stu-id="d0c74-169">Environment</span></span> | <span data-ttu-id="d0c74-170">URL</span><span class="sxs-lookup"><span data-stu-id="d0c74-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="d0c74-171">Üretim için</span><span class="sxs-lookup"><span data-stu-id="d0c74-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="d0c74-172">Test için</span><span class="sxs-lookup"><span data-stu-id="d0c74-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="d0c74-173">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-173">These values are not real.</span></span> <span data-ttu-id="d0c74-174">Bu güncelleştirme tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile Merhaba gerçek değerler.</span><span class="sxs-lookup"><span data-stu-id="d0c74-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="d0c74-175">Kişi [Ceridian Dayforce HCM istemci destek ekibi](https://www.ceridian.com/contact-us/index.html) tooget bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d0c74-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="d0c74-176">Merhaba üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve hello meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d0c74-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Merhaba sertifika indirme bağlantısı](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="d0c74-178">Ceridian Dayforce HCM uygulamanızı belirli bir biçimde hello SAML onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="d0c74-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="d0c74-179">Çalışmak [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html) ilk tooidentify hello doğru kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d0c74-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="d0c74-180">Microsoft önerir hello kullanarak **"name"** kullanıcı tanımlayıcısı olarak özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d0c74-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="d0c74-181">Hello başlangıç değerleri bu özniteliklerin yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="d0c74-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="d0c74-182">Ekran aşağıdaki hello bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-182">hello following screenshot shows an example for this.</span></span>  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="d0c74-184">Merhaba, **kullanıcı öznitelikleri** hello bölüm **çoklu oturum açma** iletişim kutusunda, SAML belirteci özniteliği yukarıdaki hello resimde gösterildiği gibi yapılandırmak ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d0c74-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d0c74-185">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="d0c74-185">Attribute Name</span></span>  | <span data-ttu-id="d0c74-186">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="d0c74-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="d0c74-187">ad</span><span class="sxs-lookup"><span data-stu-id="d0c74-187">name</span></span>  | <span data-ttu-id="d0c74-188">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="d0c74-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="d0c74-189">a.</span><span class="sxs-lookup"><span data-stu-id="d0c74-189">a.</span></span> <span data-ttu-id="d0c74-190">Tıklatın **Ekle özniteliği** tooopen hello **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d0c74-193">b.</span><span class="sxs-lookup"><span data-stu-id="d0c74-193">b.</span></span> <span data-ttu-id="d0c74-194">Merhaba, **adı** metin kutusuna, ilgili satır için gösterilen türü hello öznitelik adı.</span><span class="sxs-lookup"><span data-stu-id="d0c74-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="d0c74-195">c.</span><span class="sxs-lookup"><span data-stu-id="d0c74-195">c.</span></span> <span data-ttu-id="d0c74-196">Merhaba, **değeri** listesi, uygulamanız için kullanmak istediğiniz toouse select hello kullanıcı özniteliği.</span><span class="sxs-lookup"><span data-stu-id="d0c74-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="d0c74-197">Örneğin, toouse hello benzersiz kullanıcı tanımlayıcısı olarak EmployeeID istiyorsanız ve hello ExtensionAttribute2 hello öznitelik değeri depoladığınız seçip **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="d0c74-198">d.</span><span class="sxs-lookup"><span data-stu-id="d0c74-198">d.</span></span> <span data-ttu-id="d0c74-199">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0c74-199">Click **Ok**.</span></span>

7. <span data-ttu-id="d0c74-200">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-200">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="d0c74-202">Merhaba üzerinde **Ceridian Dayforce HCM yapılandırma** 'yi tıklatın **yapılandırma Ceridian Dayforce HCM** tooopen **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d0c74-203">Kopya hello **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** hello gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d0c74-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM yapılandırma](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="d0c74-205">tooconfigure çoklu oturum açma üzerinde **Ceridian Dayforce HCM** yan, indirilen toosend hello ihtiyacınız **meta veri XML** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** çok[Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="d0c74-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="d0c74-206">Şimdi bu yönergeleri hello içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)hello uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d0c74-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0c74-207">Bu uygulamayı hello ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, hello tıklamanız yeterlidir **çoklu oturum açma** sekmesi ve erişim hello katıştırılmış hello aracılığıyla belgelere  **Yapılandırma** hello alt kısmına.</span><span class="sxs-lookup"><span data-stu-id="d0c74-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0c74-208">Daha fazla bilgiyi burada hello embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0c74-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d0c74-209">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0c74-209">Create an Azure AD test user</span></span>

<span data-ttu-id="d0c74-210">Bu bölümde Hello amacı toocreate hello Azure portal Britta Simon adlı bir test kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="d0c74-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="d0c74-212">**Azure AD'de bir sınama kullanıcısı toocreate hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d0c74-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c74-213">Merhaba hello sol bölmede Azure portal hello tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Hello Azure Active Directory düğmesi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d0c74-215">Kullanıcılar, toodisplay hello listesi gidin çok**kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" Merhaba "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d0c74-217">tooopen hello **kullanıcı** iletişim kutusu, tıklatın **Ekle** hello hello üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="d0c74-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Merhaba Ekle düğmesi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d0c74-219">Merhaba, **kullanıcı** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d0c74-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Merhaba kullanıcı iletişim kutusu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d0c74-221">a.</span><span class="sxs-lookup"><span data-stu-id="d0c74-221">a.</span></span> <span data-ttu-id="d0c74-222">Merhaba, **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0c74-223">b.</span><span class="sxs-lookup"><span data-stu-id="d0c74-223">b.</span></span> <span data-ttu-id="d0c74-224">Merhaba, **kullanıcı adı** kutusuna, kullanıcının Britta Simon hello e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="d0c74-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d0c74-225">c.</span><span class="sxs-lookup"><span data-stu-id="d0c74-225">c.</span></span> <span data-ttu-id="d0c74-226">Select hello **Göster parola** onay kutusunu işaretleyin ve ardından hello görüntülenen hello değerini aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="d0c74-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d0c74-227">d.</span><span class="sxs-lookup"><span data-stu-id="d0c74-227">d.</span></span> <span data-ttu-id="d0c74-228">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0c74-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="d0c74-229">Ceridian Dayforce HCM test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0c74-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="d0c74-230">Bu bölümde Hello amacı toocreate Ceridian Dayforce HCM Britta Simon adlı bir kullanıcı var.</span><span class="sxs-lookup"><span data-stu-id="d0c74-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="d0c74-231">İş ile Merhaba [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html) tooget kullanıcılar hello Ceridian Dayforce HCM uygulama eklendi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0c74-232">Hello Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d0c74-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0c74-233">Bu bölümde, erişim tooCeridian Dayforce HCM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d0c74-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d0c74-235">**tooassign Britta Simon tooCeridian Dayforce HCM hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d0c74-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c74-236">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d0c74-238">Merhaba uygulamalar listesinde **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="d0c74-240">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d0c74-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-242">Click **Add** button.</span></span> <span data-ttu-id="d0c74-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d0c74-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d0c74-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0c74-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0c74-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d0c74-248">Hello Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="d0c74-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d0c74-249">Bu bölümde, erişim tooCeridian Dayforce HCM vererek Britta Simon toouse Azure çoklu oturum açmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d0c74-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Merhaba kullanıcı rolü atayın][200] 

<span data-ttu-id="d0c74-251">**tooassign Britta Simon tooCeridian Dayforce HCM hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d0c74-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c74-252">Hello Azure portal, hello uygulamaları görünümü Aç ve ardından toohello dizin görünümüne gidin ve çok Git**kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d0c74-254">Merhaba uygulamalar listesinde **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Merhaba Ceridian Dayforce HCM bağlantı hello uygulamalar listesinde](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="d0c74-256">Merhaba soldaki Hello menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d0c74-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Merhaba "Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="d0c74-258">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0c74-258">Click **Add** button.</span></span> <span data-ttu-id="d0c74-259">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Merhaba eklemek atama bölmesi][203]

5. <span data-ttu-id="d0c74-261">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** hello kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d0c74-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0c74-262">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0c74-263">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0c74-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d0c74-264">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="d0c74-264">Test single sign-on</span></span>

<span data-ttu-id="d0c74-265">Bu bölümde Hello amacı olan tootest hello erişim paneli, Azure AD çoklu oturum açma Yapılandırması'nı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d0c74-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="d0c74-266">Merhaba Ceridian Dayforce HCM hello erişim paneli parçasında tıkladığınızda, otomatik olarak oturum açma tooyour Ceridian Dayforce HCM uygulama almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0c74-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0c74-267">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d0c74-267">Additional resources</span></span>

* [<span data-ttu-id="d0c74-268">İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları</span><span class="sxs-lookup"><span data-stu-id="d0c74-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0c74-269">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d0c74-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

