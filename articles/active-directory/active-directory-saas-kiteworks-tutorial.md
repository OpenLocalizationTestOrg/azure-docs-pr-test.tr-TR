---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kiteworks | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Kiteworks arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="e7672-103">Öğretici: Azure Active Directory Tümleştirme Kiteworks ile</span><span class="sxs-lookup"><span data-stu-id="e7672-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="e7672-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Kiteworks tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e7672-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7672-105">Kiteworks Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e7672-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7672-106">Kiteworks erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e7672-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="e7672-107">Otomatik olarak için Kiteworks (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e7672-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7672-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e7672-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7672-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7672-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7672-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e7672-110">Prerequisites</span></span>

<span data-ttu-id="e7672-111">Azure AD tümleştirme Kiteworks ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7672-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="e7672-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e7672-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7672-113">Bir Kiteworks çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e7672-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7672-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e7672-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7672-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7672-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7672-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e7672-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7672-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7672-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7672-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e7672-118">Scenario description</span></span>
<span data-ttu-id="e7672-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e7672-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7672-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e7672-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7672-121">Galeriden Kiteworks ekleme</span><span class="sxs-lookup"><span data-stu-id="e7672-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="e7672-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e7672-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="e7672-123">Galeriden Kiteworks ekleme</span><span class="sxs-lookup"><span data-stu-id="e7672-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="e7672-124">Azure AD Kiteworks tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Kiteworks eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7672-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7672-125">**Galeriden Kiteworks eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7672-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7672-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e7672-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7672-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e7672-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7672-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e7672-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e7672-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7672-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e7672-133">Arama kutusuna **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="e7672-133">In the search box, type **Kiteworks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="e7672-135">Sonuçlar panelinde seçin **Kiteworks**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7672-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7672-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e7672-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7672-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kiteworks sınayın.</span><span class="sxs-lookup"><span data-stu-id="e7672-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7672-139">Tekli çalışmaya oturum için Azure AD Kiteworks karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e7672-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="e7672-140">Diğer bir deyişle, bir Azure AD kullanıcısının Kiteworks ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7672-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="e7672-141">Kiteworks içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e7672-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7672-142">Yapılandırma ve Azure AD çoklu oturum açma Kiteworks ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7672-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7672-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e7672-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7672-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e7672-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7672-145">**[Kiteworks test kullanıcısı oluşturma](#creating-a-kiteworks-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Kiteworks sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e7672-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7672-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e7672-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7672-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e7672-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7672-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e7672-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7672-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Kiteworks uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7672-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="e7672-150">**Azure AD çoklu oturum açma ile Kiteworks yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7672-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="e7672-151">Azure portalında üzerinde **Kiteworks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e7672-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e7672-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e7672-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="e7672-155">Üzerinde **Kiteworks etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7672-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="e7672-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7672-157">a.</span></span> <span data-ttu-id="e7672-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="e7672-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="e7672-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7672-159">b.</span></span> <span data-ttu-id="e7672-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="e7672-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7672-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e7672-161">These values are not real.</span></span> <span data-ttu-id="e7672-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7672-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e7672-163">Kişi [Kiteworks istemci destek ekibi](http://accellion.com/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="e7672-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="e7672-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e7672-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="e7672-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7672-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7672-168">Üzerinde **Kiteworks yapılandırma** 'yi tıklatın **yapılandırma Kiteworks** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e7672-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e7672-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e7672-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="e7672-171">Kiteworks şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="e7672-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="e7672-172">Üstteki araç çubuğunda tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e7672-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="e7672-174">İçinde **kimlik doğrulama ve yetkilendirme** 'yi tıklatın **SSO Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="e7672-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="e7672-176">SSO Kurulumu sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7672-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="e7672-178">a.</span><span class="sxs-lookup"><span data-stu-id="e7672-178">a.</span></span> <span data-ttu-id="e7672-179">Seçin **SSO kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="e7672-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="e7672-180">b.</span><span class="sxs-lookup"><span data-stu-id="e7672-180">b.</span></span> <span data-ttu-id="e7672-181">Seçin **başlatmak AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="e7672-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="e7672-182">c.</span><span class="sxs-lookup"><span data-stu-id="e7672-182">c.</span></span> <span data-ttu-id="e7672-183">İçinde **IDP varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e7672-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="e7672-184">d.</span><span class="sxs-lookup"><span data-stu-id="e7672-184">d.</span></span> <span data-ttu-id="e7672-185">İçinde **çoklu oturum açma hizmet URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e7672-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7672-186">e.</span><span class="sxs-lookup"><span data-stu-id="e7672-186">e.</span></span> <span data-ttu-id="e7672-187">İçinde **tek oturum kapatma hizmeti URL'si** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e7672-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7672-188">f.</span><span class="sxs-lookup"><span data-stu-id="e7672-188">f.</span></span> <span data-ttu-id="e7672-189">İndirilen sertifikanızı Not Defteri'nde açın, içeriği Kopyala ve ardından yapıştırın **RSA ortak anahtar sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e7672-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="e7672-190">g.</span><span class="sxs-lookup"><span data-stu-id="e7672-190">g.</span></span> <span data-ttu-id="e7672-191">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7672-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e7672-192">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e7672-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7672-193">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e7672-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7672-194">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7672-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7672-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7672-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7672-196">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e7672-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e7672-198">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7672-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7672-199">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e7672-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7672-201">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e7672-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7672-203">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e7672-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7672-205">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e7672-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7672-207">a.</span><span class="sxs-lookup"><span data-stu-id="e7672-207">a.</span></span> <span data-ttu-id="e7672-208">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7672-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7672-209">b.</span><span class="sxs-lookup"><span data-stu-id="e7672-209">b.</span></span> <span data-ttu-id="e7672-210">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e7672-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7672-211">c.</span><span class="sxs-lookup"><span data-stu-id="e7672-211">c.</span></span> <span data-ttu-id="e7672-212">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e7672-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7672-213">d.</span><span class="sxs-lookup"><span data-stu-id="e7672-213">d.</span></span> <span data-ttu-id="e7672-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7672-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="e7672-215">Kiteworks test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7672-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="e7672-216">Bu bölümün amacı Britta Simon içinde Kiteworks adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e7672-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="e7672-217">Kiteworks yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="e7672-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="e7672-218">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e7672-218">There is no action item for you in this section.</span></span> <span data-ttu-id="e7672-219">Yeni bir kullanıcı henüz yoksa Kitewors erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e7672-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="e7672-220">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [Kiteworks destek ekibi](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="e7672-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7672-221">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e7672-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7672-222">Bu bölümde, Britta Kiteworks için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7672-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e7672-224">**Kiteworks için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e7672-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="e7672-225">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e7672-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e7672-227">Uygulamalar listesinde **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="e7672-227">In the applications list, select **Kiteworks**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="e7672-229">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e7672-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e7672-231">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e7672-231">Click **Add** button.</span></span> <span data-ttu-id="e7672-232">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7672-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e7672-234">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e7672-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7672-235">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7672-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7672-236">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e7672-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7672-237">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e7672-237">Testing single sign-on</span></span>

<span data-ttu-id="e7672-238">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="e7672-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="e7672-239">Erişim paneli Kiteworks parçasında tıklattığınızda, otomatik olarak Kiteworks uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e7672-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7672-240">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e7672-240">Additional resources</span></span>

* [<span data-ttu-id="e7672-241">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e7672-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7672-242">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e7672-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

