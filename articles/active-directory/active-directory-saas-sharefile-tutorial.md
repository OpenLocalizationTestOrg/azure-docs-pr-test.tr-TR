---
title: "Öğretici: Azure Active Directory Tümleştirme ile Citrix ShareFile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Citrix ShareFile arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="e8c5b-103">Öğretici: Citrix ShareFile Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e8c5b-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="e8c5b-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Citrix ShareFile tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8c5b-105">Citrix ShareFile Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8c5b-106">Citrix ShareFile erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="e8c5b-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Citrix ShareFile açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e8c5b-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e8c5b-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8c5b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8c5b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e8c5b-110">Prerequisites</span></span>

<span data-ttu-id="e8c5b-111">Azure AD tümleştirme Citrix ShareFile ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="e8c5b-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e8c5b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8c5b-113">Bir Citrix ShareFile çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e8c5b-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8c5b-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8c5b-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8c5b-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8c5b-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8c5b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8c5b-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e8c5b-118">Scenario description</span></span>
<span data-ttu-id="e8c5b-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8c5b-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8c5b-121">Citrix ShareFile Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e8c5b-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="e8c5b-122">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e8c5b-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="e8c5b-123">Citrix ShareFile Galerisi'nden ekleme</span><span class="sxs-lookup"><span data-stu-id="e8c5b-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="e8c5b-124">Azure AD Citrix ShareFile tümleştirilmesi yapılandırmak için Citrix ShareFile Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8c5b-125">**Galeriden Citrix ShareFile eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8c5b-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c5b-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="e8c5b-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8c5b-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="e8c5b-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="e8c5b-133">Arama kutusuna **Citrix ShareFile**seçin **Citrix ShareFile** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e8c5b-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e8c5b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e8c5b-136">Bu bölümde, yapılandırmanız ve Citrix ShareFile ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8c5b-137">Tekli çalışmaya oturum için Azure AD Citrix ShareFile karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="e8c5b-138">Diğer bir deyişle, bir Azure AD kullanıcısının ve Citrix ShareFile ilgili kullanıcı arasındaki bağlantıyı ilişki kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="e8c5b-139">Citrix ShareFile içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e8c5b-140">Yapılandırma ve Azure AD çoklu oturum açma Citrix ShareFile ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8c5b-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e8c5b-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8c5b-143">**[Citrix ShareFile test kullanıcısı oluşturma](#create-a-citrix-sharefile-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Citrix ShareFile sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8c5b-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8c5b-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e8c5b-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e8c5b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e8c5b-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Citrix ShareFile uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="e8c5b-148">**Azure AD çoklu oturum açma ile Citrix ShareFile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8c5b-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c5b-149">Azure portalında üzerinde **Citrix ShareFile** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="e8c5b-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="e8c5b-153">Üzerinde **Citrix ShareFile etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Citrix ShareFile etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="e8c5b-155">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="e8c5b-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8c5b-156">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-156">This value is not real.</span></span> <span data-ttu-id="e8c5b-157">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e8c5b-158">Kişi [Citrix ShareFile istemci destek ekibi](https://www.citrix.co.in/products/sharefile/support.html) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="e8c5b-159">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="e8c5b-161">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-161">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8c5b-163">Üzerinde **Citrix ShareFile yapılandırma** 'yi tıklatın **yapılandırma Citrix ShareFile** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e8c5b-164">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e8c5b-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Citrix ShareFile yapılandırma](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="e8c5b-166">Farklı web tarayıcısı penceresinde oturum açın, **Citrix ShareFile** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="e8c5b-167">Üstteki araç çubuğunda tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="e8c5b-168">Sol gezinti bölmesinde seçin **yapılandırma çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="e8c5b-169">![Hesap Yönetimi](./media/active-directory-saas-sharefile-tutorial/ic773627.png "hesap yönetimi")</span><span class="sxs-lookup"><span data-stu-id="e8c5b-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="e8c5b-170">Üzerinde **çoklu oturum açma / SAML 2.0 yapılandırma** iletişim sayfasında altında **temel ayarları**, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="e8c5b-171">![Çoklu oturum açma](./media/active-directory-saas-sharefile-tutorial/ic773628.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="e8c5b-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="e8c5b-172">a.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-172">a.</span></span> <span data-ttu-id="e8c5b-173">Tıklatın **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="e8c5b-174">b.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-174">b.</span></span> <span data-ttu-id="e8c5b-175">İçinde **bilgisayarınızı IDP veren / varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8c5b-176">c.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-176">c.</span></span> <span data-ttu-id="e8c5b-177">Tıklatın **değişiklik** yanına **X.509 sertifikası** alan ve Azure portalından indirdiğiniz sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="e8c5b-178">d.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-178">d.</span></span> <span data-ttu-id="e8c5b-179">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="e8c5b-180">e.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-180">e.</span></span> <span data-ttu-id="e8c5b-181">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="e8c5b-182">Tıklatın **kaydetmek** Citrix ShareFile Yönetim Portalı.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="e8c5b-183">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e8c5b-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e8c5b-184">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e8c5b-185">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8c5b-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e8c5b-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8c5b-186">Create an Azure AD test user</span></span>

<span data-ttu-id="e8c5b-187">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="e8c5b-189">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8c5b-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c5b-190">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e8c5b-192">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e8c5b-194">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e8c5b-196">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-196">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e8c5b-198">a.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-198">a.</span></span> <span data-ttu-id="e8c5b-199">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8c5b-200">b.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-200">b.</span></span> <span data-ttu-id="e8c5b-201">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e8c5b-202">c.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-202">c.</span></span> <span data-ttu-id="e8c5b-203">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e8c5b-204">d.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-204">d.</span></span> <span data-ttu-id="e8c5b-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="e8c5b-206">Citrix ShareFile test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8c5b-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="e8c5b-207">Azure AD kullanıcıların Citrix ShareFile oturum etkinleştirmek için bunların Citrix ShareFile sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="e8c5b-208">Citrix ShareFile söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="e8c5b-209">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8c5b-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c5b-210">Oturum, **Citrix ShareFile** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="e8c5b-211">Tıklatın **kullanıcıları yönetme \> kullanıcıların giriş yönetmek \> + çalışan oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="e8c5b-212">![Çalışan oluşturma](./media/active-directory-saas-sharefile-tutorial/IC781050.png "çalışan oluşturma")</span><span class="sxs-lookup"><span data-stu-id="e8c5b-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="e8c5b-213">Üzerinde **temel bilgileri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e8c5b-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="e8c5b-214">![Temel bilgileri](./media/active-directory-saas-sharefile-tutorial/IC799951.png "temel bilgileri")</span><span class="sxs-lookup"><span data-stu-id="e8c5b-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="e8c5b-215">a.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-215">a.</span></span> <span data-ttu-id="e8c5b-216">İçinde **e-posta adresi** metin kutusuna, Britta Simon e-posta adresini yazın  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e8c5b-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="e8c5b-217">b.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-217">b.</span></span> <span data-ttu-id="e8c5b-218">İçinde **ad** metin kutusuna, türü **ad** kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="e8c5b-219">c.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-219">c.</span></span> <span data-ttu-id="e8c5b-220">İçinde **Soyadı** metin kutusuna, türü **Soyadı** kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="e8c5b-221">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="e8c5b-222">Azure AD hesap sahibi bir e-posta almak ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izleyin. Azure AD kullanıcı hesaplarını sağlamak için herhangi bir Citrix ShareFile kullanıcı hesabı oluşturma araçlarını veya Citrix ShareFile tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e8c5b-223">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="e8c5b-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="e8c5b-224">Bu bölümde, Britta Citrix ShareFile erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="e8c5b-226">**Citrix ShareFile Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e8c5b-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="e8c5b-227">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e8c5b-229">Uygulamalar listesinde **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![Uygulamalar listesinde Citrix ShareFile bağlantı](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="e8c5b-231">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-231">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="e8c5b-233">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-233">Click **Add** button.</span></span> <span data-ttu-id="e8c5b-234">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="e8c5b-236">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e8c5b-237">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8c5b-238">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e8c5b-239">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="e8c5b-239">Test single sign-on</span></span>

<span data-ttu-id="e8c5b-240">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e8c5b-241">Erişim paneli Citrix ShareFile parçasında tıklattığınızda, otomatik olarak Citrix ShareFile uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e8c5b-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="e8c5b-242">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e8c5b-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e8c5b-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e8c5b-243">Additional resources</span></span>

* [<span data-ttu-id="e8c5b-244">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e8c5b-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8c5b-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e8c5b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

