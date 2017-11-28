---
title: "Öğretici: Azure Active Directory Tümleştirme ile Yardım Scout | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory Yardımı Scout arasındaki yapılandırmayı öğrenin."
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
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="4081e-103">Öğretici: Yardım Scout Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="4081e-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="4081e-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Yardım Scout tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4081e-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4081e-105">Azure AD ile Yardım Scout tümleştirme aşağıdaki yararları alın:</span><span class="sxs-lookup"><span data-stu-id="4081e-105">You get the following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="4081e-106">Azure AD'de kimlerin erişebileceğini Scout yardımcı olmak için kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4081e-106">In Azure AD, you can control who has access to Help Scout.</span></span>
- <span data-ttu-id="4081e-107">Otomatik olarak yardımcı Scout kullanıcılarınıza, çoklu oturum açma ve bir kullanıcının Azure AD hesabı kullanarak oturum.</span><span class="sxs-lookup"><span data-stu-id="4081e-107">You can automatically sign in your users to Help Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="4081e-108">Hesaplarınızı tek, merkezi bir konumda, Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="4081e-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="4081e-109">Azure AD ile hizmet (SaaS) uygulaması tümleştirme olarak yazılım hakkında daha fazla bilgi edinmek için [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4081e-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4081e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4081e-110">Prerequisites</span></span>

<span data-ttu-id="4081e-111">Yardım Scout ile Azure AD tümleştirmeyi ayarlamak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4081e-111">To set up Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="4081e-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4081e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4081e-113">Bir Yardım Scout aboneliğiyle, çoklu oturum açık açma</span><span class="sxs-lookup"><span data-stu-id="4081e-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="4081e-114">Bu öğreticide adımları test ederseniz, bunları bir üretim ortamında sınamanızı yok öneririz.</span><span class="sxs-lookup"><span data-stu-id="4081e-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="4081e-115">Bu öğreticide adımları test etmek için öneriler:</span><span class="sxs-lookup"><span data-stu-id="4081e-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="4081e-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4081e-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="4081e-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4081e-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4081e-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4081e-118">Scenario description</span></span>
<span data-ttu-id="4081e-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4081e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="4081e-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4081e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4081e-121">Yardım Scout Galeriden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4081e-121">Add Help Scout from the gallery.</span></span>
2. <span data-ttu-id="4081e-122">Ayarlama ve Azure AD çoklu oturum açmayı test edin.</span><span class="sxs-lookup"><span data-stu-id="4081e-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-the-gallery"></a><span data-ttu-id="4081e-123">Galeriden Yardım Scout ekleme</span><span class="sxs-lookup"><span data-stu-id="4081e-123">Add Help Scout from the gallery</span></span>
<span data-ttu-id="4081e-124">Galeride Yardım Scout Azure AD ile tümleştirmeyi ayarlamak için Yardım Scout yönetilen SaaS uygulamaları listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4081e-124">To set up the integration of Help Scout with Azure AD, in the gallery, add Help Scout to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4081e-125">Galeriden Yardım Scout eklemek için:</span><span class="sxs-lookup"><span data-stu-id="4081e-125">To add Help Scout from the gallery:</span></span>

1. <span data-ttu-id="4081e-126">İçinde [Azure portal](https://portal.azure.com), soldaki menüde seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4081e-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="4081e-128">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4081e-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kurumsal uygulamalar sayfası][2]
    
3. <span data-ttu-id="4081e-130">Yeni bir uygulama eklemek için seçin **yeni uygulama**.</span><span class="sxs-lookup"><span data-stu-id="4081e-130">To add a new application, select **New application**.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="4081e-132">Arama kutusuna **Yardım Scout**.</span><span class="sxs-lookup"><span data-stu-id="4081e-132">In the search box, enter **Help Scout**.</span></span> <span data-ttu-id="4081e-133">Arama sonuçlarında seçin **Yardım Scout**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4081e-133">In the search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Sonuçlar listesinde Scout Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4081e-135">Ayarlama ve Azure AD çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="4081e-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="4081e-136">Bu bölümde, ayarladığınız ve Yardım Scout ile Azure AD çoklu oturum açmayı test adlı bir test kullanıcı tabanlı *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="4081e-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="4081e-137">Tekli çalışmaya oturum için Azure AD Yardım Scout Azure AD karşılık gelen kullanıcı bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4081e-137">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="4081e-138">Bir Azure AD kullanıcısının Yardım Scout ilgili kullanıcı arasında bir bağlantı ilişkisi kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4081e-138">A link relationship between an Azure AD user and the related user in Help Scout must be established.</span></span>

<span data-ttu-id="4081e-139">İçin Yardım Scout içinde bağlantı ilişkisi kurmak için **kullanıcıadı**, değeri atayın **kullanıcı adı** Azure AD'de.</span><span class="sxs-lookup"><span data-stu-id="4081e-139">To establish the link relationship, in Help Scout, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="4081e-140">Yapılandırma ve Azure AD çoklu oturum açma Yardımı Scout ile test etmek için aşağıdaki görevleri tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="4081e-140">To configure and test Azure AD single sign-on with Help Scout, complete the following tasks:</span></span>

1. <span data-ttu-id="4081e-141">[Azure AD çoklu oturum açmayı ayarlama](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4081e-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="4081e-142">Bir kullanıcı bu özelliği kullanmak için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4081e-142">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="4081e-143">[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="4081e-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="4081e-144">Testleri Azure AD çoklu oturum açma Britta Simon kullanıcıyla.</span><span class="sxs-lookup"><span data-stu-id="4081e-144">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="4081e-145">[Yardım Scout test kullanıcısı oluşturma](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="4081e-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="4081e-146">Karşılık gelen Britta Simon, kullanıcının Azure AD gösterimini bağlı Yardım Scout oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4081e-146">Creates a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="4081e-147">[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="4081e-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="4081e-148">Çoklu oturum açmayı Britta Azure AD kullanılacak Simon ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4081e-148">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4081e-149">[Test çoklu oturum açma](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4081e-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="4081e-150">Yapılandırma çalıştığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="4081e-150">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="4081e-151">Azure AD çoklu oturum açmayı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4081e-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="4081e-152">Bu bölümde, Azure AD çoklu oturum açma Azure portalında ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="4081e-152">In this section, you set up Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="4081e-153">Sonra tek oturum açma Yardımı Scout uygulamanızda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4081e-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="4081e-154">Azure AD çoklu oturum açma Yardımı Scout ile ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="4081e-154">To set up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="4081e-155">Azure portalında üzerinde **Yardım Scout** uygulama tümleştirmesi sayfasında, **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4081e-155">In the Azure portal, on the **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Oturum açma tek bağlantı ayarlama][4]

2. <span data-ttu-id="4081e-157">Üzerinde **çoklu oturum açma** sayfası için **modu**seçin **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4081e-157">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="4081e-159">Altında **Yardım Scout etki alanı ve URL'leri**, uygulama, aşağıdaki adımları IDP başlatılan modunda, tam ayarlama istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="4081e-159">Under **Help Scout Domain and URLs**, if you want to set up the application in IDP-initiated mode, complete the following steps:</span></span>

    1. <span data-ttu-id="4081e-160">İçinde **tanımlayıcısı** kutusunda, aşağıdaki desen bir URL girin:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="4081e-160">In the **Identifier** box, enter a URL that has the following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="4081e-161">İçinde **yanıt URL'si** kutusunda, aşağıdaki desen bir URL girin:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="4081e-161">In the **Reply URL** box, enter a URL that has the following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="4081e-163">SP tarafından başlatılan modunda uygulama ayarlamak isteyip istemediğinizi seçin **Göster Gelişmiş URL ayarları** onay kutusunu işaretleyin ve ardından aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="4081e-163">If you want to set up the application in SP-initiated mode, select the **Show advanced URL settings** check box, and then do the following:</span></span>

    * <span data-ttu-id="4081e-164">İçinde **URL üzerinde oturum** kutusunda, aşağıdaki biçimde bir URL girin:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="4081e-164">In the **Sign on URL** box, enter a URL that has the following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Scout etki alanı ve URL'leri tek oturum açma bilgileri Yardım](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="4081e-166">Bu URL'leri yalnızca tanıtım değerler.</span><span class="sxs-lookup"><span data-stu-id="4081e-166">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="4081e-167">Yanıt URL'si ve gerçek tanımlayıcı URL'si ile değerlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4081e-167">Update the values with the actual identifier URL and reply URL.</span></span> <span data-ttu-id="4081e-168">Bu değerleri almak için başvurun [Yardım Scout destek ekibi](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="4081e-168">To get these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="4081e-169">Altında **SAML imzalama sertifikası**seçin **meta veri XML**ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4081e-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="4081e-171">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4081e-171">Select **Save**.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4081e-173">Çoklu oturum açma Yardımı Scout tarafında ayarlamak için indirilen meta veri XML dosyasına göndermek [Yardım Scout destek ekibi](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="4081e-173">To set up single sign-on on the Help Scout side, send the downloaded metadata XML file to the [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="4081e-174">Oturum açma SAML tek bağlantı iki tarafta da düzgün ayarlandığından emin Yardım Scout destek ekibi bu ayar uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4081e-174">The Help Scout support team applies this setting so that the SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4081e-175">Bu yönergelerde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulamanızı ayarlama yaparken!</span><span class="sxs-lookup"><span data-stu-id="4081e-175">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="4081e-176">Seçerek uygulama ekledikten sonra **Active Directory** > **kurumsal uygulamalar**seçin **çoklu oturum açma** sekmesi. Katıştırılmış belgelerde erişebilirsiniz **yapılandırma** bölümünde, sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="4081e-176">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="4081e-177">Daha fazla bilgi için bkz: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4081e-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4081e-178">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4081e-178">Create an Azure AD test user</span></span>

<span data-ttu-id="4081e-179">Bu bölümde, Azure portalında Britta Simon adlı bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4081e-179">In this section, in the Azure portal, you create a test user named Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="4081e-181">Azure AD'de bir test kullanıcı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="4081e-181">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="4081e-182">Azure portalında soldaki menüde seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4081e-182">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4081e-184">Kullanıcıların listesini görüntülemek için seçin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4081e-184">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Kullanıcıları ve grupları seçin ve ardından tüm kullanıcıları seçin](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4081e-186">Açmak için **kullanıcı** en üstündeki iletişim kutusu **tüm kullanıcılar** sayfasında, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4081e-186">To open the **User** dialog box, at the top of the **All Users** page, select **Add**.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4081e-188">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="4081e-188">In the **User** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="4081e-189">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4081e-189">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="4081e-190">İçinde **kullanıcı adı** kutusuna, kullanıcının Britta Simon e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="4081e-190">In the **User name** box, enter the email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="4081e-191">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="4081e-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="4081e-192">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="4081e-192">Select **Create**.</span></span>

        ![Kullanıcı iletişim kutusu](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="4081e-194">Yardım Scout test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4081e-194">Create a Help Scout test user</span></span>

<span data-ttu-id="4081e-195">Bu bölümde nesnesinin Britta Simon Yardım Scout içinde adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4081e-195">The object of this section is to create a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="4081e-196">Yardım Scout tam zamanında (JIT) sağlama, varsayılan olarak açıktır destekler.</span><span class="sxs-lookup"><span data-stu-id="4081e-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="4081e-197">Bu bölümde, eylem veya görevinin tamamlanması için yoktur.</span><span class="sxs-lookup"><span data-stu-id="4081e-197">In this section, there's no action or task to complete.</span></span> <span data-ttu-id="4081e-198">Bir kullanıcı Yardımı Scout içinde zaten yoksa, Yardım Scout erişmeyi denediğinde yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4081e-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4081e-199">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="4081e-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="4081e-200">Bu bölümde, kullanıcı Britta Scout yardımcı olmak için kullanıcı hesabı erişimi verilmesi tarafından Azure AD çoklu oturum açma kullanılacak Simon izin verin.</span><span class="sxs-lookup"><span data-stu-id="4081e-200">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to Help Scout.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="4081e-202">Yardım Scout Britta Simon atamak için:</span><span class="sxs-lookup"><span data-stu-id="4081e-202">To assign Britta Simon to Help Scout:</span></span>

1. <span data-ttu-id="4081e-203">Azure Portalı'ndaki uygulamaları görünümünü açın ve dizin görünümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="4081e-203">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="4081e-204">Seçin **kurumsal uygulamalar**ve ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4081e-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4081e-206">Uygulamalar listesinde **Yardım Scout**.</span><span class="sxs-lookup"><span data-stu-id="4081e-206">In the applications list, select **Help Scout**.</span></span>

    ![Uygulamalar listesinde Yardım Scout bağlantı](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="4081e-208">Soldaki menüde seçin **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4081e-208">In the left menu, select **Users and groups**.</span></span>

    ![Kullanıcılar ve gruplar bağlantı][202]

4. <span data-ttu-id="4081e-210">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4081e-210">Select **Add**.</span></span> <span data-ttu-id="4081e-211">Ardından **eklemek atama** sayfasında, **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4081e-211">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="4081e-213">Üzerinde **kullanıcılar ve gruplar** sayfasında, kullanıcıların, seçim listesinde **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4081e-213">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="4081e-214">Üzerinde **kullanıcılar ve gruplar** sayfasında, **seçin**.</span><span class="sxs-lookup"><span data-stu-id="4081e-214">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="4081e-215">Üzerinde **eklemek atama** sayfasında, **atamak**.</span><span class="sxs-lookup"><span data-stu-id="4081e-215">On the **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4081e-216">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="4081e-216">Test single sign-on</span></span>

<span data-ttu-id="4081e-217">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test.</span><span class="sxs-lookup"><span data-stu-id="4081e-217">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="4081e-218">Erişim panelinde Yardım Scout döşeme seçtiğinizde, otomatik olarak yardımcı Scout uygulamanıza oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="4081e-218">When you select the Help Scout tile in the access panel, you should be automatically signed in to your Help Scout application.</span></span>

<span data-ttu-id="4081e-219">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4081e-219">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4081e-220">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4081e-220">Additional resources</span></span>

* [<span data-ttu-id="4081e-221">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4081e-221">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4081e-222">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4081e-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

