---
title: "Öğretici: Azure Active Directory Tümleştirme ile Sprinklr | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Sprinklr arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="b5a45-103">Öğretici: Azure Active Directory Tümleştirme Sprinklr ile</span><span class="sxs-lookup"><span data-stu-id="b5a45-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="b5a45-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Sprinklr tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b5a45-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5a45-105">Sprinklr Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="b5a45-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b5a45-106">Sprinklr erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b5a45-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="b5a45-107">Otomatik olarak için Sprinklr (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b5a45-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5a45-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="b5a45-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b5a45-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5a45-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5a45-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b5a45-110">Prerequisites</span></span>

<span data-ttu-id="b5a45-111">Azure AD tümleştirme Sprinklr ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5a45-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="b5a45-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="b5a45-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5a45-113">Bir Sprinklr çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="b5a45-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5a45-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="b5a45-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5a45-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5a45-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5a45-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5a45-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5a45-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5a45-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="b5a45-118">Scenario description</span></span>
<span data-ttu-id="b5a45-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="b5a45-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5a45-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="b5a45-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5a45-121">Galeriden Sprinklr ekleme</span><span class="sxs-lookup"><span data-stu-id="b5a45-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="b5a45-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b5a45-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="b5a45-123">Galeriden Sprinklr ekleme</span><span class="sxs-lookup"><span data-stu-id="b5a45-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="b5a45-124">Azure AD Sprinklr tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Sprinklr eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5a45-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5a45-125">**Galeriden Sprinklr eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5a45-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5a45-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5a45-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b5a45-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="b5a45-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="b5a45-133">Arama kutusuna **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-133">In the search box, type **Sprinklr**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="b5a45-135">Sonuçlar panelinde seçin **Sprinklr**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5a45-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="b5a45-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5a45-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Sprinklr ile test etme</span><span class="sxs-lookup"><span data-stu-id="b5a45-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b5a45-139">Tekli çalışmaya oturum için Azure AD Sprinklr karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="b5a45-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="b5a45-140">Diğer bir deyişle, bir Azure AD kullanıcısının Sprinklr ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5a45-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="b5a45-141">Sprinklr içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b5a45-142">Yapılandırma ve Azure AD çoklu oturum açma Sprinklr ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5a45-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5a45-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5a45-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5a45-145">**[Sprinklr test kullanıcısı oluşturma](#creating-a-sprinklr-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Sprinklr sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5a45-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5a45-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5a45-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b5a45-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5a45-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Sprinklr uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="b5a45-150">**Azure AD çoklu oturum açma ile Sprinklr yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5a45-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="b5a45-151">Azure portalında üzerinde **Sprinklr** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="b5a45-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="b5a45-155">Üzerinde **Sprinklr etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5a45-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="b5a45-157">a.</span><span class="sxs-lookup"><span data-stu-id="b5a45-157">a.</span></span> <span data-ttu-id="b5a45-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="b5a45-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="b5a45-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5a45-159">b.</span></span> <span data-ttu-id="b5a45-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="b5a45-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5a45-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="b5a45-161">These values are not real.</span></span> <span data-ttu-id="b5a45-162">Gerçek oturum açma URL'si ve tanımlayıcı değeri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5a45-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b5a45-163">Kişi [Sprinklr istemci destek ekibi](https://www.sprinklr.com/contact-us/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="b5a45-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="b5a45-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b5a45-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="b5a45-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b5a45-168">Üzerinde **Sprinklr yapılandırma** 'yi tıklatın **yapılandırma Sprinklr** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b5a45-169">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="b5a45-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="b5a45-170">Farklı web tarayıcısı penceresinde Sprinklr şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="b5a45-171">Git **Yönetim \> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="b5a45-172">![Yönetim](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="b5a45-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="b5a45-173">Git **iş ortağı yönetme \> çoklu oturum açma** üzerinde sol bölmeden.</span><span class="sxs-lookup"><span data-stu-id="b5a45-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="b5a45-174">![İş ortağı yönetme](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "iş ortağı yönetme")</span><span class="sxs-lookup"><span data-stu-id="b5a45-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="b5a45-175">Tıklatın **+ çoklu oturum açmaların eklemek**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="b5a45-176">![Çoklu oturum açmaların](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "çoklu oturum açmaların")</span><span class="sxs-lookup"><span data-stu-id="b5a45-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="b5a45-177">Üzerinde **çoklu oturum açma** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5a45-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="b5a45-178">![Çoklu oturum açmaların](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "çoklu oturum açmaların")</span><span class="sxs-lookup"><span data-stu-id="b5a45-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="b5a45-179">a.</span><span class="sxs-lookup"><span data-stu-id="b5a45-179">a.</span></span> <span data-ttu-id="b5a45-180">İçinde **adı** metin kutusuna, yapılandırmanız için bir ad yazın (örneğin: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="b5a45-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="b5a45-181">b.</span><span class="sxs-lookup"><span data-stu-id="b5a45-181">b.</span></span> <span data-ttu-id="b5a45-182">Seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-182">Select **Enabled**.</span></span>

    <span data-ttu-id="b5a45-183">c.</span><span class="sxs-lookup"><span data-stu-id="b5a45-183">c.</span></span> <span data-ttu-id="b5a45-184">Seçin **yeni SSO sertifikayı kullanmak**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="b5a45-185">e.</span><span class="sxs-lookup"><span data-stu-id="b5a45-185">e.</span></span> <span data-ttu-id="b5a45-186">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **kimlik sağlayıcısı sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b5a45-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="b5a45-187">f.</span><span class="sxs-lookup"><span data-stu-id="b5a45-187">f.</span></span> <span data-ttu-id="b5a45-188">Yapıştır **SAML varlık kimliği** Azure portalından kopyaladığınız değeri **varlık kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b5a45-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="b5a45-189">g.</span><span class="sxs-lookup"><span data-stu-id="b5a45-189">g.</span></span> <span data-ttu-id="b5a45-190">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b5a45-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="b5a45-191">h.</span><span class="sxs-lookup"><span data-stu-id="b5a45-191">h.</span></span> <span data-ttu-id="b5a45-192">Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="b5a45-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="b5a45-193">ı.</span><span class="sxs-lookup"><span data-stu-id="b5a45-193">i.</span></span> <span data-ttu-id="b5a45-194">Olarak **SAML kullanıcı kimliği türü**seçin **onaylamayı içeren kullanıcı "s sprinklr.com kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="b5a45-195">j.</span><span class="sxs-lookup"><span data-stu-id="b5a45-195">j.</span></span> <span data-ttu-id="b5a45-196">Olarak **SAML kullanıcı kimliği konumu**seçin **kullanıcı kimliğidir konu deyim ad tanımlayıcısı öğesinde**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="b5a45-197">k.</span><span class="sxs-lookup"><span data-stu-id="b5a45-197">k.</span></span> <span data-ttu-id="b5a45-198">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-198">Click **Save**.</span></span>
       
    <span data-ttu-id="b5a45-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="b5a45-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="b5a45-200">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="b5a45-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b5a45-201">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="b5a45-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b5a45-202">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5a45-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5a45-203">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5a45-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5a45-204">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b5a45-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="b5a45-206">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5a45-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5a45-207">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5a45-209">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5a45-211">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="b5a45-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5a45-213">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5a45-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5a45-215">a.</span><span class="sxs-lookup"><span data-stu-id="b5a45-215">a.</span></span> <span data-ttu-id="b5a45-216">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5a45-217">b.</span><span class="sxs-lookup"><span data-stu-id="b5a45-217">b.</span></span> <span data-ttu-id="b5a45-218">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="b5a45-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5a45-219">c.</span><span class="sxs-lookup"><span data-stu-id="b5a45-219">c.</span></span> <span data-ttu-id="b5a45-220">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b5a45-221">d.</span><span class="sxs-lookup"><span data-stu-id="b5a45-221">d.</span></span> <span data-ttu-id="b5a45-222">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="b5a45-223">Sprinklr test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5a45-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="b5a45-224">Sprinklr şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="b5a45-225">Git **Yönetim \> ayarları**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="b5a45-226">![Yönetim](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="b5a45-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="b5a45-227">Git **yönetmek istemci \> kullanıcılar** sol bölmeden.</span><span class="sxs-lookup"><span data-stu-id="b5a45-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="b5a45-228">![Ayarları](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="b5a45-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="b5a45-229">Tıklatın **kullanıcı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="b5a45-230">![Ayarları](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="b5a45-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="b5a45-231">Üzerinde **düzenleme kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5a45-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b5a45-232">![Kullanıcı düzenleme](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "düzenleme kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="b5a45-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="b5a45-233">a.</span><span class="sxs-lookup"><span data-stu-id="b5a45-233">a.</span></span> <span data-ttu-id="b5a45-234">İçinde **e-posta**, **ad** ve **Soyadı** metin kutuları, sağlamak istediğiniz bir Azure AD kullanıcı hesabı bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="b5a45-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="b5a45-235">b.</span><span class="sxs-lookup"><span data-stu-id="b5a45-235">b.</span></span> <span data-ttu-id="b5a45-236">Seçin **parola devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="b5a45-237">c.</span><span class="sxs-lookup"><span data-stu-id="b5a45-237">c.</span></span> <span data-ttu-id="b5a45-238">Seçin **dil**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-238">Select **Language**.</span></span>

    <span data-ttu-id="b5a45-239">d.</span><span class="sxs-lookup"><span data-stu-id="b5a45-239">d.</span></span> <span data-ttu-id="b5a45-240">Seçin **kullanıcı türü**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-240">Select **User Type**.</span></span>

    <span data-ttu-id="b5a45-241">e.</span><span class="sxs-lookup"><span data-stu-id="b5a45-241">e.</span></span> <span data-ttu-id="b5a45-242">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="b5a45-243">**Parola devre dışı** bir kimlik sağlayıcısı oturum açma kullanıcı seçilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5a45-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="b5a45-244">Git **rol**ve ardından aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b5a45-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="b5a45-245">![İş ortağı rolleri](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "ortak rolleri")</span><span class="sxs-lookup"><span data-stu-id="b5a45-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="b5a45-246">a.</span><span class="sxs-lookup"><span data-stu-id="b5a45-246">a.</span></span> <span data-ttu-id="b5a45-247">Gelen **Global** listesinde **tüm\_izinleri**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="b5a45-248">b.</span><span class="sxs-lookup"><span data-stu-id="b5a45-248">b.</span></span> <span data-ttu-id="b5a45-249">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="b5a45-250">API Azure AD kullanıcı hesaplarını sağlamak için Sprinklr tarafından sağlanan veya herhangi diğer Sprinklr kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5a45-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b5a45-251">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="b5a45-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b5a45-252">Bu bölümde, Britta Sprinklr için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5a45-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="b5a45-254">**Sprinklr için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="b5a45-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="b5a45-255">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="b5a45-257">Uygulamalar listesinde **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-257">In the applications list, select **Sprinklr**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="b5a45-259">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="b5a45-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="b5a45-261">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b5a45-261">Click **Add** button.</span></span> <span data-ttu-id="b5a45-262">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5a45-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="b5a45-264">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="b5a45-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b5a45-265">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5a45-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5a45-266">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="b5a45-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5a45-267">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="b5a45-267">Testing single sign-on</span></span>

<span data-ttu-id="b5a45-268">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="b5a45-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b5a45-269">Erişim paneli Sprinklr parçasında tıkladığınızda, erişim paneli hakkında daha fazla bilgi için bkz, otomatik olarak Sprinklr uygulamanıza açan almalısınız [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5a45-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b5a45-270">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b5a45-270">Additional resources</span></span>

* [<span data-ttu-id="b5a45-271">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="b5a45-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5a45-272">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="b5a45-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

