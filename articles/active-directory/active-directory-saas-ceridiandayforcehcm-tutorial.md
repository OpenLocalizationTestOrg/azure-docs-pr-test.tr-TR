---
title: "Öğretici: Azure Active Directory Tümleştirme ile Ceridian Dayforce HCM | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Ceridian Dayforce HCM arasında yapılandırmayı öğrenin."
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
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="5b715-103">Öğretici: Azure Active Directory Tümleştirme Ceridian Dayforce HCM ile</span><span class="sxs-lookup"><span data-stu-id="5b715-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="5b715-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Ceridian Dayforce HCM tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5b715-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b715-105">Ceridian Dayforce HCM Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5b715-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b715-106">Ceridian Dayforce HCM erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b715-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="5b715-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Ceridian Dayforce HCM açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b715-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5b715-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="5b715-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5b715-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b715-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b715-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5b715-110">Prerequisites</span></span>

<span data-ttu-id="5b715-111">Azure AD tümleştirme Ceridian Dayforce HCM ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b715-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="5b715-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5b715-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b715-113">Bir Ceridian Dayforce HCM çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="5b715-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b715-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5b715-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b715-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b715-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b715-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5b715-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b715-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b715-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b715-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5b715-118">Scenario description</span></span>
<span data-ttu-id="5b715-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5b715-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b715-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5b715-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b715-121">Galeriden Ceridian Dayforce HCM ekleme</span><span class="sxs-lookup"><span data-stu-id="5b715-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="5b715-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5b715-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="5b715-123">Galeriden Ceridian Dayforce HCM ekleme</span><span class="sxs-lookup"><span data-stu-id="5b715-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="5b715-124">Azure AD Ceridian Dayforce HCM tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Ceridian Dayforce HCM eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b715-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b715-125">**Galeriden Ceridian Dayforce HCM eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b715-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b715-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5b715-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="5b715-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5b715-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b715-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5b715-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="5b715-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b715-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="5b715-133">Arama kutusuna **Ceridian Dayforce HCM**seçin **Ceridian Dayforce HCM** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="5b715-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5b715-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5b715-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5b715-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Ceridian Dayforce "Britta Simon" adlı bir test kullanıcı tabanlı HCM ile test etme.</span><span class="sxs-lookup"><span data-stu-id="5b715-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b715-137">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Ceridian Dayforce HCM, bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="5b715-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="5b715-138">Diğer bir deyişle, bir Azure AD kullanıcısının Ceridian Dayforce HCM ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b715-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="5b715-139">Değeri Ceridian Dayforce HCM Ata **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5b715-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b715-140">Yapılandırma ve Azure AD çoklu oturum açma Ceridian Dayforce HCM ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b715-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b715-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5b715-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b715-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="5b715-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b715-143">**[Ceridian Dayforce HCM test kullanıcısı oluşturma](#create-a-ceridian-dayforce-hcm-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Ceridian Dayforce HCM sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="5b715-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b715-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5b715-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b715-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5b715-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5b715-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5b715-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5b715-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Ceridian Dayforce HCM uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5b715-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="5b715-148">**Azure AD çoklu oturum açma Ceridian Dayforce HCM ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b715-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="5b715-149">Azure portalında üzerinde **Ceridian Dayforce HCM** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5b715-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="5b715-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5b715-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="5b715-153">Üzerinde **Ceridian Dayforce HCM etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b715-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="5b715-155">a.</span><span class="sxs-lookup"><span data-stu-id="5b715-155">a.</span></span> <span data-ttu-id="5b715-156">İçinde **oturum üzerinde URL'si** metin kutusuna, türü URL kullanıcılarınıza oturum açma Ceridian Dayforce HCM uygulamanıza tarafından kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="5b715-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="5b715-157">Ortam</span><span class="sxs-lookup"><span data-stu-id="5b715-157">Environment</span></span> | <span data-ttu-id="5b715-158">URL</span><span class="sxs-lookup"><span data-stu-id="5b715-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="5b715-159">Üretim için</span><span class="sxs-lookup"><span data-stu-id="5b715-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="5b715-160">Test için</span><span class="sxs-lookup"><span data-stu-id="5b715-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="5b715-161">b.</span><span class="sxs-lookup"><span data-stu-id="5b715-161">b.</span></span> <span data-ttu-id="5b715-162">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="5b715-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="5b715-163">Ortam</span><span class="sxs-lookup"><span data-stu-id="5b715-163">Environment</span></span> | <span data-ttu-id="5b715-164">URL</span><span class="sxs-lookup"><span data-stu-id="5b715-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="5b715-165">Üretim için</span><span class="sxs-lookup"><span data-stu-id="5b715-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="5b715-166">Test için</span><span class="sxs-lookup"><span data-stu-id="5b715-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="5b715-167">c.</span><span class="sxs-lookup"><span data-stu-id="5b715-167">c.</span></span> <span data-ttu-id="5b715-168">İçinde **yanıt URL'si** metin kutusuna, türü URL kullanılan Azure AD tarafından yanıt gönderme.</span><span class="sxs-lookup"><span data-stu-id="5b715-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="5b715-169">Ortam</span><span class="sxs-lookup"><span data-stu-id="5b715-169">Environment</span></span> | <span data-ttu-id="5b715-170">URL</span><span class="sxs-lookup"><span data-stu-id="5b715-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="5b715-171">Üretim için</span><span class="sxs-lookup"><span data-stu-id="5b715-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="5b715-172">Test için</span><span class="sxs-lookup"><span data-stu-id="5b715-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="5b715-173">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5b715-173">These values are not real.</span></span> <span data-ttu-id="5b715-174">Bu değerleri gerçek tanımlayıcısı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5b715-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="5b715-175">Kişi [Ceridian Dayforce HCM istemci destek ekibi](https://www.ceridian.com/contact-us/index.html) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="5b715-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="5b715-176">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5b715-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="5b715-178">Ceridian Dayforce HCM uygulamanızı belirli bir biçimde SAML onaylar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="5b715-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5b715-179">Çalışmak [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html) doğru kullanıcı tanımlayıcısı belirlemek için öncelikle.</span><span class="sxs-lookup"><span data-stu-id="5b715-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="5b715-180">Microsoft önerir kullanarak **"name"** kullanıcı tanımlayıcısı olarak özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5b715-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="5b715-181">Bu öznitelik değerlerini yönetebilirsiniz **kullanıcı öznitelikleri** uygulama tümleştirmesi sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="5b715-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="5b715-182">Aşağıdaki ekran görüntüsünde bunun bir örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="5b715-182">The following screenshot shows an example for this.</span></span>  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="5b715-184">İçinde **kullanıcı öznitelikleri** bölümünde **çoklu oturum açma** iletişim kutusunda, yukarıdaki resimde gösterildiği gibi SAML belirteci özniteliği yapılandırın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b715-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="5b715-185">Öznitelik adı</span><span class="sxs-lookup"><span data-stu-id="5b715-185">Attribute Name</span></span>  | <span data-ttu-id="5b715-186">Öznitelik değeri</span><span class="sxs-lookup"><span data-stu-id="5b715-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="5b715-187">ad</span><span class="sxs-lookup"><span data-stu-id="5b715-187">name</span></span>  | <span data-ttu-id="5b715-188">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="5b715-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="5b715-189">a.</span><span class="sxs-lookup"><span data-stu-id="5b715-189">a.</span></span> <span data-ttu-id="5b715-190">Tıklatın **Ekle özniteliği** açmak için **özniteliği eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="5b715-193">b.</span><span class="sxs-lookup"><span data-stu-id="5b715-193">b.</span></span> <span data-ttu-id="5b715-194">İçinde **adı** metin kutusuna, ilgili satır için gösterilen öznitelik adı yazın.</span><span class="sxs-lookup"><span data-stu-id="5b715-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5b715-195">c.</span><span class="sxs-lookup"><span data-stu-id="5b715-195">c.</span></span> <span data-ttu-id="5b715-196">İçinde **değeri** listesinde, uygulamanız için kullanmak istediğiniz kullanıcı özniteliği seçin.</span><span class="sxs-lookup"><span data-stu-id="5b715-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="5b715-197">Örneğin, EmployeeID kullanmak istiyorsanız, benzersiz bir kullanıcı tanımlayıcısı ve öznitelik değeri ExtensionAttribute2 depoladığınız, ardından **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="5b715-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="5b715-198">d.</span><span class="sxs-lookup"><span data-stu-id="5b715-198">d.</span></span> <span data-ttu-id="5b715-199">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5b715-199">Click **Ok**.</span></span>

7. <span data-ttu-id="5b715-200">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b715-200">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="5b715-202">Üzerinde **Ceridian Dayforce HCM yapılandırma** 'yi tıklatın **yapılandırma Ceridian Dayforce HCM** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5b715-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5b715-203">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="5b715-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM yapılandırma](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="5b715-205">Çoklu oturum açma yapılandırmak için **Ceridian Dayforce HCM** yan, indirilen göndermek için ihtiyacınız **meta veri XML** ve **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** için [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="5b715-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="5b715-206">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5b715-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b715-207">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="5b715-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b715-208">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b715-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5b715-209">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b715-209">Create an Azure AD test user</span></span>

<span data-ttu-id="5b715-210">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="5b715-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="5b715-212">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b715-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b715-213">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b715-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5b715-215">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5b715-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5b715-217">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5b715-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5b715-219">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5b715-219">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5b715-221">a.</span><span class="sxs-lookup"><span data-stu-id="5b715-221">a.</span></span> <span data-ttu-id="5b715-222">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b715-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b715-223">b.</span><span class="sxs-lookup"><span data-stu-id="5b715-223">b.</span></span> <span data-ttu-id="5b715-224">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="5b715-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5b715-225">c.</span><span class="sxs-lookup"><span data-stu-id="5b715-225">c.</span></span> <span data-ttu-id="5b715-226">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="5b715-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5b715-227">d.</span><span class="sxs-lookup"><span data-stu-id="5b715-227">d.</span></span> <span data-ttu-id="5b715-228">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5b715-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="5b715-229">Ceridian Dayforce HCM test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b715-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="5b715-230">Bu bölümün amacı Britta Simon Ceridian Dayforce HCM adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="5b715-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="5b715-231">Çalışmak [Ceridian Dayforce HCM destek ekibi](https://www.ceridian.com/contact-us/index.html) Ceridian Dayforce HCM uygulamada eklenen kullanıcıları alınamadı.</span><span class="sxs-lookup"><span data-stu-id="5b715-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5b715-232">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5b715-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5b715-233">Bu bölümde, Britta Ceridian Dayforce HCM erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5b715-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5b715-235">**Ceridian Dayforce HCM Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b715-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="5b715-236">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5b715-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5b715-238">Uygulamalar listesinde **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="5b715-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="5b715-240">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5b715-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5b715-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b715-242">Click **Add** button.</span></span> <span data-ttu-id="5b715-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5b715-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5b715-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b715-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b715-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5b715-248">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="5b715-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="5b715-249">Bu bölümde, Britta Ceridian Dayforce HCM erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5b715-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="5b715-251">**Ceridian Dayforce HCM Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5b715-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="5b715-252">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5b715-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5b715-254">Uygulamalar listesinde **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="5b715-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Uygulamalar listesinde Ceridian Dayforce HCM bağlantı](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="5b715-256">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5b715-256">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="5b715-258">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b715-258">Click **Add** button.</span></span> <span data-ttu-id="5b715-259">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="5b715-261">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5b715-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b715-262">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b715-263">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5b715-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5b715-264">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="5b715-264">Test single sign-on</span></span>

<span data-ttu-id="5b715-265">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="5b715-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="5b715-266">Erişim paneli Ceridian Dayforce HCM parçasında tıklattığınızda, otomatik olarak Ceridian Dayforce HCM uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="5b715-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5b715-267">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5b715-267">Additional resources</span></span>

* [<span data-ttu-id="5b715-268">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="5b715-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b715-269">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5b715-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

