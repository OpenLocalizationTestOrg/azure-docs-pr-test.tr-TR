---
title: "Öğretici: Azure Active Directory Tümleştirme ile Gigya | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Gigya arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="bb4bb-103">Öğretici: Azure Active Directory Tümleştirme Gigya ile</span><span class="sxs-lookup"><span data-stu-id="bb4bb-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="bb4bb-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Gigya tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb4bb-105">Gigya Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bb4bb-106">Gigya erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bb4bb-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="bb4bb-107">Otomatik olarak için Gigya (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bb4bb-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb4bb-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="bb4bb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bb4bb-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb4bb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb4bb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bb4bb-110">Prerequisites</span></span>

<span data-ttu-id="bb4bb-111">Azure AD tümleştirme Gigya ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="bb4bb-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="bb4bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb4bb-113">Bir Gigya çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="bb4bb-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb4bb-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb4bb-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb4bb-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb4bb-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb4bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb4bb-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="bb4bb-118">Scenario description</span></span>
<span data-ttu-id="bb4bb-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb4bb-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb4bb-121">Galeriden Gigya ekleme</span><span class="sxs-lookup"><span data-stu-id="bb4bb-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="bb4bb-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bb4bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="bb4bb-123">Galeriden Gigya ekleme</span><span class="sxs-lookup"><span data-stu-id="bb4bb-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="bb4bb-124">Azure AD Gigya tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Gigya eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bb4bb-125">**Galeriden Gigya eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bb4bb-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bb4bb-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb4bb-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bb4bb-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="bb4bb-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="bb4bb-133">Arama kutusuna **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-133">In the search box, type **Gigya**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="bb4bb-135">Sonuçlar panelinde seçin **Gigya**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb4bb-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="bb4bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb4bb-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Gigya sınayın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb4bb-139">Tekli çalışmaya oturum için Azure AD Gigya karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="bb4bb-140">Diğer bir deyişle, bir Azure AD kullanıcısının Gigya ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="bb4bb-141">Gigya içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bb4bb-142">Yapılandırma ve Azure AD çoklu oturum açma Gigya ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bb4bb-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bb4bb-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb4bb-145">**[Gigya test kullanıcısı oluşturma](#creating-a-gigya-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Gigya sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb4bb-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb4bb-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb4bb-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bb4bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb4bb-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Gigya uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="bb4bb-150">**Azure AD çoklu oturum açma ile Gigya yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bb4bb-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="bb4bb-151">Azure portalında üzerinde **Gigya** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="bb4bb-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="bb4bb-155">Üzerinde **Gigya etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="bb4bb-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-157">a.</span></span> <span data-ttu-id="bb4bb-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="bb4bb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="bb4bb-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-159">b.</span></span> <span data-ttu-id="bb4bb-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bb4bb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb4bb-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-161">These values are not real.</span></span> <span data-ttu-id="bb4bb-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bb4bb-163">Kişi [Gigya istemci destek ekibi](https://www.gigya.com/support-policy/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="bb4bb-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="bb4bb-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb4bb-168">Üzerinde **Gigya yapılandırma** 'yi tıklatın **yapılandırma Gigya** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bb4bb-169">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="bb4bb-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="bb4bb-171">Farklı web tarayıcısı penceresinde Gigya şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="bb4bb-172">Git **ayarları \> SAML oturum açma**ve ardından **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="bb4bb-173">![SAML oturum açma](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML oturum açma")</span><span class="sxs-lookup"><span data-stu-id="bb4bb-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="bb4bb-174">İçinde **SAML oturum açma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="bb4bb-175">![SAML Yapılandırması](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="bb4bb-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="bb4bb-176">a.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-176">a.</span></span> <span data-ttu-id="bb4bb-177">İçinde **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="bb4bb-178">b.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-178">b.</span></span> <span data-ttu-id="bb4bb-179">İçinde **veren** metin değerini yapıştırın **SAML varlık kimliği** Azure Portalı'ndan kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="bb4bb-180">c.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-180">c.</span></span> <span data-ttu-id="bb4bb-181">İçinde **çoklu oturum açma hizmet URL'si** metin değerini yapıştırın **çoklu oturum açma hizmet URL'si** Azure Portalı'ndan kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="bb4bb-182">d.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-182">d.</span></span> <span data-ttu-id="bb4bb-183">İçinde **ad kimliği biçimi** metin değerini yapıştırın **ad tanımlayıcısı biçimi** Azure Portalı'ndan kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="bb4bb-184">e.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-184">e.</span></span> <span data-ttu-id="bb4bb-185">Base-64 kodlanmış sertifikanızı Azure portalından indirdiğiniz Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **X.509 sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="bb4bb-186">f.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-186">f.</span></span> <span data-ttu-id="bb4bb-187">Tıklatın **ayarlarını kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="bb4bb-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="bb4bb-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bb4bb-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bb4bb-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb4bb-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb4bb-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb4bb-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="bb4bb-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="bb4bb-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bb4bb-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bb4bb-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb4bb-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb4bb-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb4bb-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb4bb-203">a.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-203">a.</span></span> <span data-ttu-id="bb4bb-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb4bb-205">b.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-205">b.</span></span> <span data-ttu-id="bb4bb-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb4bb-207">c.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-207">c.</span></span> <span data-ttu-id="bb4bb-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bb4bb-209">d.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-209">d.</span></span> <span data-ttu-id="bb4bb-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="bb4bb-211">Gigya test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb4bb-211">Creating a Gigya test user</span></span>

<span data-ttu-id="bb4bb-212">Azure AD kullanıcıların Gigya oturum etkinleştirmek için bunların Gigya sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="bb4bb-213">Gigya söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="bb4bb-214">Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="bb4bb-215">Oturum, **Gigya** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="bb4bb-216">Git **yönetici \> kullanıcıları yönetme**ve ardından **kullanıcıları davet**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="bb4bb-217">![Kullanıcıları yönetme](./media/active-directory-saas-gigya-tutorial/ic789535.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="bb4bb-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="bb4bb-218">Kullanıcıların davet iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bb4bb-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="bb4bb-219">![Kullanıcıları davet](./media/active-directory-saas-gigya-tutorial/ic789536.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="bb4bb-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="bb4bb-220">a.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-220">a.</span></span> <span data-ttu-id="bb4bb-221">İçinde **e-posta** metin kutusu, geçerli bir Azure Active Directory hesabı sağlamak istediğiniz e-posta diğer adı yazın.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="bb4bb-222">b.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-222">b.</span></span> <span data-ttu-id="bb4bb-223">Tıklatın **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="bb4bb-224">Azure Active Directory hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bb4bb-225">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="bb4bb-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bb4bb-226">Bu bölümde, Britta Gigya için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="bb4bb-228">**Gigya için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="bb4bb-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="bb4bb-229">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="bb4bb-231">Uygulamalar listesinde **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-231">In the applications list, select **Gigya**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="bb4bb-233">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="bb4bb-235">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-235">Click **Add** button.</span></span> <span data-ttu-id="bb4bb-236">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="bb4bb-238">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bb4bb-239">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb4bb-240">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb4bb-241">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="bb4bb-241">Testing single sign-on</span></span>

<span data-ttu-id="bb4bb-242">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bb4bb-243">Erişim paneli Gigya parçasında tıklattığınızda, otomatik olarak Gigya uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="bb4bb-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb4bb-244">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bb4bb-244">Additional resources</span></span>

* [<span data-ttu-id="bb4bb-245">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="bb4bb-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb4bb-246">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="bb4bb-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

