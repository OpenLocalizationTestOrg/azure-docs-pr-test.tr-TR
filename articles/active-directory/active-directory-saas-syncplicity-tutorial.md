---
title: "Öğretici: Azure Active Directory Tümleştirme ile Syncplicity | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Syncplicity arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="be068-103">Öğretici: Syncplicity Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="be068-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="be068-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Syncplicity tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="be068-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be068-105">Syncplicity Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="be068-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be068-106">Syncplicity erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="be068-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="be068-107">Otomatik olarak için Syncplicity (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="be068-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be068-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="be068-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="be068-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be068-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be068-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="be068-110">Prerequisites</span></span>

<span data-ttu-id="be068-111">Azure AD tümleştirme Syncplicity ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="be068-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="be068-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="be068-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be068-113">Bir Syncplicity çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="be068-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be068-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="be068-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be068-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="be068-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be068-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="be068-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be068-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be068-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be068-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="be068-118">Scenario description</span></span>
<span data-ttu-id="be068-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="be068-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be068-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="be068-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be068-121">Syncplicity Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="be068-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="be068-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="be068-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="be068-123">Syncplicity Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="be068-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="be068-124">Azure AD Syncplicity tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Syncplicity eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be068-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be068-125">**Syncplicity Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be068-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be068-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="be068-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be068-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="be068-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be068-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="be068-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="be068-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be068-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="be068-133">Arama kutusuna **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="be068-133">In the search box, type **Syncplicity**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="be068-135">Sonuçlar panelinde seçin **Syncplicity**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be068-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be068-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="be068-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be068-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Syncplicity ile test etme</span><span class="sxs-lookup"><span data-stu-id="be068-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be068-139">Tekli çalışmaya oturum için Azure AD Syncplicity karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="be068-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="be068-140">Diğer bir deyişle, bir Azure AD kullanıcısının Syncplicity ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be068-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="be068-141">Syncplicity içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="be068-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="be068-142">Yapılandırma ve Azure AD çoklu oturum açma Syncplicity ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="be068-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be068-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="be068-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be068-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="be068-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be068-145">**[Syncplicity test kullanıcısı oluşturma](#creating-a-syncplicity-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Syncplicity sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="be068-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="be068-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="be068-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be068-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="be068-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be068-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="be068-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be068-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Syncplicity uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be068-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="be068-150">**Azure AD çoklu oturum açma ile Syncplicity yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be068-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="be068-151">Azure portalında üzerinde **Syncplicity** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="be068-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="be068-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="be068-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="be068-155">Üzerinde **Syncplicity etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be068-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="be068-157">a.</span><span class="sxs-lookup"><span data-stu-id="be068-157">a.</span></span> <span data-ttu-id="be068-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="be068-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="be068-159">b.</span><span class="sxs-lookup"><span data-stu-id="be068-159">b.</span></span> <span data-ttu-id="be068-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="be068-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="be068-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="be068-161">These values are not real.</span></span> <span data-ttu-id="be068-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="be068-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="be068-163">Kişi [Syncplicity istemci destek ekibi](https://www.syncplicity.com/contact-us) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="be068-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="be068-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be068-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="be068-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be068-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be068-168">Üzerinde **Syncplicity yapılandırma** 'yi tıklatın **yapılandırma Syncplicity** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="be068-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="be068-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="be068-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="be068-171">Oturum açın, **Syncplicity** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="be068-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="be068-172">Üstteki menüde tıklatın **yönetici**seçin **ayarları**ve ardından **özel etki alanı ve çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="be068-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="be068-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="be068-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="be068-174">Üzerinde **çoklu oturum açma (SSO)** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be068-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="be068-175">![Çoklu oturum açma \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="be068-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="be068-176">a.</span><span class="sxs-lookup"><span data-stu-id="be068-176">a.</span></span> <span data-ttu-id="be068-177">İçinde **özel etki alanı** metin kutusuna, etki alanınızın adını yazın.</span><span class="sxs-lookup"><span data-stu-id="be068-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="be068-178">b.</span><span class="sxs-lookup"><span data-stu-id="be068-178">b.</span></span> <span data-ttu-id="be068-179">Seçin **etkin** olarak **tek oturum açma durumu**.</span><span class="sxs-lookup"><span data-stu-id="be068-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="be068-180">c.</span><span class="sxs-lookup"><span data-stu-id="be068-180">c.</span></span> <span data-ttu-id="be068-181">İçinde **varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="be068-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="be068-182">d.</span><span class="sxs-lookup"><span data-stu-id="be068-182">d.</span></span> <span data-ttu-id="be068-183">İçinde **oturum açma sayfası URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="be068-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="be068-184">e.</span><span class="sxs-lookup"><span data-stu-id="be068-184">e.</span></span> <span data-ttu-id="be068-185">İçinde **oturum kapatma sayfası URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="be068-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="be068-186">f.</span><span class="sxs-lookup"><span data-stu-id="be068-186">f.</span></span> <span data-ttu-id="be068-187">İçinde **kimlik sağlayıcısı sertifikası**, tıklatın **Dosya Seç**ve Azure Portalı'ndan indirilen sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="be068-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="be068-188">g.</span><span class="sxs-lookup"><span data-stu-id="be068-188">g.</span></span> <span data-ttu-id="be068-189">Tıklatın **değişiklikleri kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="be068-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="be068-190">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="be068-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="be068-191">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="be068-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="be068-192">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be068-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be068-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be068-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="be068-194">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="be068-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="be068-196">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be068-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be068-197">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="be068-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be068-199">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="be068-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be068-201">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="be068-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be068-203">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="be068-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be068-205">a.</span><span class="sxs-lookup"><span data-stu-id="be068-205">a.</span></span> <span data-ttu-id="be068-206">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be068-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be068-207">b.</span><span class="sxs-lookup"><span data-stu-id="be068-207">b.</span></span> <span data-ttu-id="be068-208">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="be068-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be068-209">c.</span><span class="sxs-lookup"><span data-stu-id="be068-209">c.</span></span> <span data-ttu-id="be068-210">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="be068-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="be068-211">d.</span><span class="sxs-lookup"><span data-stu-id="be068-211">d.</span></span> <span data-ttu-id="be068-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="be068-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="be068-213">Syncplicity test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="be068-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="be068-214">AAD kullanıcıların oturum açabilmesi için bunlar Syncplicity uygulama sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="be068-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="be068-215">Bu bölümde, AAD kullanıcı hesaplarının Syncplicity içinde nasıl oluşturulacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="be068-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="be068-216">**Bir kullanıcı hesabına Syncplicity sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be068-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="be068-217">Oturum, **Syncplicity** Kiracı (örneğin: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="be068-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="be068-218">Tıklatın **yönetici** seçip **kullanıcı hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="be068-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="be068-219">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="be068-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="be068-220">![Kullanıcıları yönetme](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "kullanıcıları yönetme")</span><span class="sxs-lookup"><span data-stu-id="be068-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="be068-221">Tür **e-posta addressess** sağlamak istediğiniz bir AAD hesabıyla seçin **kullanıcı** olarak **rol**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be068-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="be068-222">![Hesap bilgileri](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "hesap bilgileri")</span><span class="sxs-lookup"><span data-stu-id="be068-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="be068-223">AAD hesap sahibi onaylayın ve hesabını etkinleştirmek için bir bağlantı içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="be068-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="be068-224">Yeni kullanıcı bir üyesi haline gelir ve ardından, şirketinizde bir grup seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be068-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="be068-225">![Grup üyelikleri](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "grup üyelikleri")</span><span class="sxs-lookup"><span data-stu-id="be068-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="be068-226">Listelenen hiçbir grup varsa tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be068-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="be068-227">Kullanıcının bilgisayarında Syncplicity'nın denetimindeki yerleştirin ve ardından istediğiniz klasörleri seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="be068-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="be068-228">![Syncplicity klasörleri](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity klasörleri")</span><span class="sxs-lookup"><span data-stu-id="be068-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="be068-229">API sağlama AAD kullanıcı hesaplarına Syncplicity tarafından sağlanan veya herhangi diğer Syncplicity kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be068-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="be068-230">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="be068-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="be068-231">Bu bölümde, Britta Syncplicity için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="be068-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="be068-233">**Syncplicity için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="be068-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="be068-234">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="be068-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="be068-236">Uygulamalar listesinde **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="be068-236">In the applications list, select **Syncplicity**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="be068-238">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="be068-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="be068-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="be068-240">Click **Add** button.</span></span> <span data-ttu-id="be068-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be068-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="be068-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="be068-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be068-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be068-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be068-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="be068-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be068-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="be068-246">Testing single sign-on</span></span>

<span data-ttu-id="be068-247">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="be068-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="be068-248">Erişim paneli Syncplicity parçasında tıklattığınızda, otomatik olarak Syncplicity uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="be068-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="be068-249">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="be068-249">Additional resources</span></span>

* [<span data-ttu-id="be068-250">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="be068-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be068-251">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="be068-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

