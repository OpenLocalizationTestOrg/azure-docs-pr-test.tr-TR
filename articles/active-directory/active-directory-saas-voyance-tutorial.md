---
title: "Öğretici: Azure Active Directory Tümleştirme ile Voyance | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Voyance arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="89967-103">Öğretici: Azure Active Directory Tümleştirme Voyance ile</span><span class="sxs-lookup"><span data-stu-id="89967-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="89967-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Voyance tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="89967-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89967-105">Voyance Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="89967-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="89967-106">Voyance erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="89967-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="89967-107">Otomatik olarak için Voyance (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="89967-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89967-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="89967-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="89967-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89967-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89967-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89967-110">Prerequisites</span></span>

<span data-ttu-id="89967-111">Azure AD tümleştirme Voyance ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="89967-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="89967-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="89967-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89967-113">Bir Voyance çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="89967-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89967-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="89967-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89967-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="89967-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89967-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="89967-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89967-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89967-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89967-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="89967-118">Scenario description</span></span>
<span data-ttu-id="89967-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="89967-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89967-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="89967-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89967-121">Galeriden Voyance ekleme</span><span class="sxs-lookup"><span data-stu-id="89967-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="89967-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="89967-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="89967-123">Galeriden Voyance ekleme</span><span class="sxs-lookup"><span data-stu-id="89967-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="89967-124">Azure AD Voyance tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Voyance eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="89967-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="89967-125">**Galeriden Voyance eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89967-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="89967-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="89967-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="89967-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="89967-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="89967-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="89967-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="89967-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89967-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="89967-133">Arama kutusuna **Voyance**seçin **Voyance** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="89967-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89967-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="89967-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89967-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Voyance sınayın.</span><span class="sxs-lookup"><span data-stu-id="89967-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89967-137">Tekli çalışmaya oturum için Azure AD Voyance karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="89967-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="89967-138">Diğer bir deyişle, bir Azure AD kullanıcısının Voyance ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="89967-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="89967-139">Voyance içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="89967-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="89967-140">Yapılandırma ve Azure AD çoklu oturum açma Voyance ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="89967-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="89967-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="89967-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="89967-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="89967-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89967-143">**[Voyance test kullanıcısı oluşturma](#create-a-voyance-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Voyance sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="89967-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="89967-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="89967-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89967-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="89967-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89967-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="89967-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89967-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Voyance uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="89967-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="89967-148">**Azure AD çoklu oturum açma ile Voyance yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89967-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="89967-149">Azure portalında üzerinde **Voyance** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="89967-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="89967-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="89967-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="89967-153">Üzerinde **Voyance etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="89967-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Voyance etki alanı ve URL'leri tek oturum açma bilgilerini IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="89967-155">a.</span><span class="sxs-lookup"><span data-stu-id="89967-155">a.</span></span> <span data-ttu-id="89967-156">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="89967-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="89967-157">b.</span><span class="sxs-lookup"><span data-stu-id="89967-157">b.</span></span> <span data-ttu-id="89967-158">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="89967-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="89967-159">Denetleme **Göster Gelişmiş URL ayarları** ve uygulamada yapılandırmak istiyorsanız aşağıdaki adımı gerçekleştirin **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="89967-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Voyance etki alanı ve URL'leri tek oturum açma bilgilerini SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="89967-161">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="89967-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="89967-162">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="89967-162">These values are not real.</span></span> <span data-ttu-id="89967-163">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="89967-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="89967-164">Kişi [Voyance istemci destek ekibi](mailto:support@nyansa.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="89967-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="89967-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89967-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="89967-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89967-167">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="89967-169">Üzerinde **Voyance yapılandırma** 'yi tıklatın **yapılandırma Voyance** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="89967-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="89967-170">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="89967-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Voyance yapılandırma](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="89967-172">Farklı web tarayıcısı penceresinde Voyance kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="89967-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="89967-173">Gezinti çubuğu sağ üst köşesinde gidin ve bildiren açılan üzerinde tıklayın "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="89967-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Çoklu oturum açma uygulama yan Acme University üzerinde yapılandırma](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="89967-175">Tıklayın "**yönetici ayarları**".</span><span class="sxs-lookup"><span data-stu-id="89967-175">Click "**Admin Settings**".</span></span>

    ![Çoklu oturum açma uygulama yan yönetim ayarlarını yapılandır](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="89967-177">Tıklayın "**kullanıcı erişimini**" sekmesi.</span><span class="sxs-lookup"><span data-stu-id="89967-177">Click "**User Access**" tab.</span></span>

    ![Çoklu oturum açma uygulama yan kullanıcı erişimini yapılandırma](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="89967-179">Tıklayın "**SSO devre dışı**" Azure AD SAML 2.0 kullanan bir IDP yapılandırmak için düğmesini.</span><span class="sxs-lookup"><span data-stu-id="89967-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Yapılandırma çoklu oturum açma uygulama yan SSO devre dışı düğmesi](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="89967-181">Git **SAML v2** bölümünde ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="89967-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Çoklu oturum açma SAML uygulama tarafında yapılandırma v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="89967-183">a.</span><span class="sxs-lookup"><span data-stu-id="89967-183">a.</span></span> <span data-ttu-id="89967-184">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="89967-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="89967-185">b.</span><span class="sxs-lookup"><span data-stu-id="89967-185">b.</span></span> <span data-ttu-id="89967-186">Yapıştır **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan **IDP oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="89967-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="89967-187">c.</span><span class="sxs-lookup"><span data-stu-id="89967-187">c.</span></span> <span data-ttu-id="89967-188">İndirilen Base64 ile kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **IDP Cert** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="89967-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="89967-189">d.</span><span class="sxs-lookup"><span data-stu-id="89967-189">d.</span></span> <span data-ttu-id="89967-190">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89967-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="89967-191">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="89967-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="89967-192">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="89967-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="89967-193">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89967-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89967-194">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89967-194">Create an Azure AD test user</span></span>

<span data-ttu-id="89967-195">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="89967-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="89967-197">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89967-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="89967-198">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="89967-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89967-200">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="89967-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89967-202">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="89967-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89967-204">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="89967-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89967-206">a.</span><span class="sxs-lookup"><span data-stu-id="89967-206">a.</span></span> <span data-ttu-id="89967-207">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89967-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89967-208">b.</span><span class="sxs-lookup"><span data-stu-id="89967-208">b.</span></span> <span data-ttu-id="89967-209">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="89967-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89967-210">c.</span><span class="sxs-lookup"><span data-stu-id="89967-210">c.</span></span> <span data-ttu-id="89967-211">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="89967-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="89967-212">d.</span><span class="sxs-lookup"><span data-stu-id="89967-212">d.</span></span> <span data-ttu-id="89967-213">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89967-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="89967-214">Voyance test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89967-214">Create a Voyance test user</span></span>

<span data-ttu-id="89967-215">Bu bölümün amacı Britta Simon içinde Voyance adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="89967-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="89967-216">Voyance yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="89967-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="89967-217">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="89967-217">There is no action item for you in this section.</span></span> <span data-ttu-id="89967-218">Yeni bir kullanıcı henüz yoksa Voyance erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="89967-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="89967-219">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [Voyance destek ekibi](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="89967-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="89967-220">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="89967-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="89967-221">Bu bölümde, Britta Voyance için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="89967-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Kullanıcı rolü atayın][200]

<span data-ttu-id="89967-223">**Voyance için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="89967-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="89967-224">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="89967-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="89967-226">Uygulamalar listesinde **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="89967-226">In the applications list, select **Voyance**.</span></span>

    ![Uygulamalar listesinde Voyance bağlantı](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="89967-228">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="89967-228">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="89967-230">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="89967-230">Click **Add** button.</span></span> <span data-ttu-id="89967-231">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89967-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="89967-233">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="89967-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="89967-234">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89967-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89967-235">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89967-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89967-236">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="89967-236">Test single sign-on</span></span>

<span data-ttu-id="89967-237">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="89967-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="89967-238">Erişim paneli Voyance parçasında tıklattığınızda, otomatik olarak Voyance uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="89967-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89967-239">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="89967-239">Additional resources</span></span>

* [<span data-ttu-id="89967-240">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="89967-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89967-241">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="89967-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

