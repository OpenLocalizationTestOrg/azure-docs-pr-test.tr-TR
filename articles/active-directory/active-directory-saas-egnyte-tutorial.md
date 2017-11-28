---
title: "Öğretici: Azure Active Directory Tümleştirme ile Egnyte | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Egnyte arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 62d01333b61e73c83588d2d1701c0c300df4ab1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="32a6a-103">Öğretici: Azure Active Directory Tümleştirme Egnyte ile</span><span class="sxs-lookup"><span data-stu-id="32a6a-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="32a6a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Egnyte tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-104">In this tutorial, you learn how to integrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32a6a-105">Egnyte Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="32a6a-105">Integrating Egnyte with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32a6a-106">Egnyte erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="32a6a-106">You can control in Azure AD who has access to Egnyte</span></span>
- <span data-ttu-id="32a6a-107">Otomatik olarak için Egnyte (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="32a6a-107">You can enable your users to automatically get signed-on to Egnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32a6a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="32a6a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32a6a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32a6a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32a6a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="32a6a-110">Prerequisites</span></span>

<span data-ttu-id="32a6a-111">Azure AD tümleştirme Egnyte ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="32a6a-111">To configure Azure AD integration with Egnyte, you need the following items:</span></span>

- <span data-ttu-id="32a6a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="32a6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32a6a-113">Bir Egnyte çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="32a6a-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32a6a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="32a6a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32a6a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="32a6a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32a6a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32a6a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32a6a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32a6a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="32a6a-118">Scenario description</span></span>
<span data-ttu-id="32a6a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32a6a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="32a6a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32a6a-121">Galeriden Egnyte ekleme</span><span class="sxs-lookup"><span data-stu-id="32a6a-121">Adding Egnyte from the gallery</span></span>
2. <span data-ttu-id="32a6a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="32a6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-the-gallery"></a><span data-ttu-id="32a6a-123">Galeriden Egnyte ekleme</span><span class="sxs-lookup"><span data-stu-id="32a6a-123">Adding Egnyte from the gallery</span></span>
<span data-ttu-id="32a6a-124">Azure AD Egnyte tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Egnyte eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="32a6a-124">To configure the integration of Egnyte into Azure AD, you need to add Egnyte from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32a6a-125">**Galeriden Egnyte eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32a6a-125">**To add Egnyte from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32a6a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32a6a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="32a6a-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="32a6a-133">Arama kutusuna **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-133">In the search box, type **Egnyte**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="32a6a-135">Sonuçlar panelinde seçin **Egnyte**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-135">In the results panel, select **Egnyte**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32a6a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="32a6a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32a6a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Egnyte ile test etme</span><span class="sxs-lookup"><span data-stu-id="32a6a-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32a6a-139">Tekli çalışmaya oturum için Azure AD Egnyte karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="32a6a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Egnyte is to a user in Azure AD.</span></span> <span data-ttu-id="32a6a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Egnyte ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="32a6a-140">In other words, a link relationship between an Azure AD user and the related user in Egnyte needs to be established.</span></span>

<span data-ttu-id="32a6a-141">Egnyte içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="32a6a-141">In Egnyte, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32a6a-142">Yapılandırma ve Azure AD çoklu oturum açma Egnyte ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="32a6a-142">To configure and test Azure AD single sign-on with Egnyte, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32a6a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="32a6a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32a6a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="32a6a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32a6a-145">**[Bir Egnyte test kullanıcısı oluşturma](#creating-an-egnyte-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Egnyte sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="32a6a-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - to have a counterpart of Britta Simon in Egnyte that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32a6a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="32a6a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32a6a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32a6a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="32a6a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32a6a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Egnyte uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="32a6a-150">**Azure AD çoklu oturum açma ile Egnyte yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32a6a-150">**To configure Azure AD single sign-on with Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6a-151">Azure portalında üzerinde **Egnyte** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-151">In the Azure portal, on the **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="32a6a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="32a6a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="32a6a-155">Üzerinde **Egnyte etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32a6a-155">On the **Egnyte Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="32a6a-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="32a6a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32a6a-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="32a6a-158">This value is not real.</span></span> <span data-ttu-id="32a6a-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="32a6a-160">Kişi [Egnyte istemci destek ekibi](https://www.egnyte.com/corp/contact_egnyte.html) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="32a6a-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) to get this value.</span></span> 
 
4. <span data-ttu-id="32a6a-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="32a6a-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32a6a-165">Üzerinde **Egnyte yapılandırma** 'yi tıklatın **yapılandırma Egnyte** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-165">On the **Egnyte Configuration** section, click **Configure Egnyte** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32a6a-166">Kopya **SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="32a6a-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="32a6a-168">Farklı web tarayıcısı penceresinde Egnyte şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-168">In a different web browser window, log in to your Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="32a6a-169">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="32a6a-170">![Ayarları](./media/active-directory-saas-egnyte-tutorial/ic787819.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="32a6a-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="32a6a-171">Menüye tıklayın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-171">In the menu, click **Settings**.</span></span>

   <span data-ttu-id="32a6a-172">![Ayarları](./media/active-directory-saas-egnyte-tutorial/ic787820.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="32a6a-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="32a6a-173">Tıklatın **yapılandırma** sekmesini ve ardından **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-173">Click the **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="32a6a-174">![Güvenlik](./media/active-directory-saas-egnyte-tutorial/ic787821.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="32a6a-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="32a6a-175">İçinde **çoklu oturum açma kimlik doğrulaması** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32a6a-175">In the **Single Sign-On Authentication** section, perform the following steps:</span></span>

    <span data-ttu-id="32a6a-176">![Çoklu oturum açma kimlik doğrulaması](./media/active-directory-saas-egnyte-tutorial/ic787822.png "çoklu oturum açma kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="32a6a-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="32a6a-177">a.</span><span class="sxs-lookup"><span data-stu-id="32a6a-177">a.</span></span> <span data-ttu-id="32a6a-178">Olarak **çoklu oturum açma kimlik doğrulaması**seçin **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="32a6a-179">b.</span><span class="sxs-lookup"><span data-stu-id="32a6a-179">b.</span></span> <span data-ttu-id="32a6a-180">Olarak **kimlik sağlayıcısı**seçin **Azuread'i**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="32a6a-181">c.</span><span class="sxs-lookup"><span data-stu-id="32a6a-181">c.</span></span> <span data-ttu-id="32a6a-182">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalına kopyalanan **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a6a-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into the **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="32a6a-183">d.</span><span class="sxs-lookup"><span data-stu-id="32a6a-183">d.</span></span> <span data-ttu-id="32a6a-184">Yapıştır **SAML varlık kimliği** Azure portalından kopyalanan **kimlik sağlayıcısı varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a6a-184">Paste **SAML Entity ID** which you have copied from Azure portal into the **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="32a6a-185">e.</span><span class="sxs-lookup"><span data-stu-id="32a6a-185">e.</span></span> <span data-ttu-id="32a6a-186">Base-64 kodlanmış sertifikanızı Azure portalından indirdiğiniz Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="32a6a-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="32a6a-187">f.</span><span class="sxs-lookup"><span data-stu-id="32a6a-187">f.</span></span> <span data-ttu-id="32a6a-188">Olarak **kullanıcı eşlemesi varsayılan**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="32a6a-189">g.</span><span class="sxs-lookup"><span data-stu-id="32a6a-189">g.</span></span> <span data-ttu-id="32a6a-190">Olarak **etki alanına özgü veren değeriyle kullanın**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="32a6a-191">h.</span><span class="sxs-lookup"><span data-stu-id="32a6a-191">h.</span></span> <span data-ttu-id="32a6a-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="32a6a-193">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="32a6a-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32a6a-194">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="32a6a-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32a6a-195">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32a6a-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32a6a-196">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32a6a-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="32a6a-197">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="32a6a-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="32a6a-199">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32a6a-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6a-200">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32a6a-202">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32a6a-204">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="32a6a-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32a6a-206">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32a6a-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32a6a-208">a.</span><span class="sxs-lookup"><span data-stu-id="32a6a-208">a.</span></span> <span data-ttu-id="32a6a-209">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32a6a-210">b.</span><span class="sxs-lookup"><span data-stu-id="32a6a-210">b.</span></span> <span data-ttu-id="32a6a-211">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="32a6a-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32a6a-212">c.</span><span class="sxs-lookup"><span data-stu-id="32a6a-212">c.</span></span> <span data-ttu-id="32a6a-213">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32a6a-214">d.</span><span class="sxs-lookup"><span data-stu-id="32a6a-214">d.</span></span> <span data-ttu-id="32a6a-215">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="32a6a-216">Bir Egnyte test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="32a6a-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="32a6a-217">Azure AD kullanıcıları için Egnyte oturum açmak etkinleştirmek için bunların Egnyte sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="32a6a-217">To enable Azure AD users to log in to Egnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="32a6a-218">Egnyte söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="32a6a-218">In the case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="32a6a-219">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32a6a-219">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6a-220">Oturum, **Egnyte** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="32a6a-220">Log in to your **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="32a6a-221">Git **ayarları \> kullanıcıları ve grupları**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-221">Go to **Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="32a6a-222">Tıklatın **yeni kullanıcı Ekle**ve ardından eklemek istediğiniz kullanıcı türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-222">Click **Add New User**, and then select the type of user you want to add.</span></span>
   
   <span data-ttu-id="32a6a-223">![Kullanıcıların](./media/active-directory-saas-egnyte-tutorial/ic787824.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="32a6a-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="32a6a-224">İçinde **yeni standart kullanıcı** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="32a6a-224">In the **New Standard User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="32a6a-225">![Yeni standart kullanıcı](./media/active-directory-saas-egnyte-tutorial/ic787825.png "yeni standart kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="32a6a-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="32a6a-226">a.</span><span class="sxs-lookup"><span data-stu-id="32a6a-226">a.</span></span> <span data-ttu-id="32a6a-227">Tür **e-posta**, **kullanıcıadı**ve diğer ayrıntılarını sağlamak istediğiniz geçerli bir Azure Active Directory hesabı.</span><span class="sxs-lookup"><span data-stu-id="32a6a-227">Type the **Email**, **Username**, and other details of a valid Azure Active Directory account you want to provision.</span></span>
   
   <span data-ttu-id="32a6a-228">b.</span><span class="sxs-lookup"><span data-stu-id="32a6a-228">b.</span></span> <span data-ttu-id="32a6a-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="32a6a-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="32a6a-230">Azure Active Directory hesap sahibi bir bildirim e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="32a6a-230">The Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="32a6a-231">API sağlama AAD kullanıcı hesaplarına Egnyte tarafından sağlanan veya herhangi diğer Egnyte kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32a6a-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32a6a-232">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="32a6a-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32a6a-233">Bu bölümde, Britta Egnyte için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Egnyte.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="32a6a-235">**Egnyte için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="32a6a-235">**To assign Britta Simon to Egnyte, perform the following steps:**</span></span>

1. <span data-ttu-id="32a6a-236">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="32a6a-238">Uygulamalar listesinde **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-238">In the applications list, select **Egnyte**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="32a6a-240">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="32a6a-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="32a6a-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="32a6a-242">Click **Add** button.</span></span> <span data-ttu-id="32a6a-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="32a6a-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="32a6a-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="32a6a-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32a6a-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="32a6a-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32a6a-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="32a6a-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32a6a-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="32a6a-248">Testing single sign-on</span></span>

<span data-ttu-id="32a6a-249">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="32a6a-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="32a6a-250">Erişim paneli Egnyte parçasında tıklattığınızda, otomatik olarak Egnyte uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="32a6a-250">When you click the Egnyte tile in the Access Panel, you should get automatically signed-on to your Egnyte application.</span></span>
<span data-ttu-id="32a6a-251">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32a6a-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="32a6a-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="32a6a-252">Additional resources</span></span>

* [<span data-ttu-id="32a6a-253">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="32a6a-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32a6a-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="32a6a-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

