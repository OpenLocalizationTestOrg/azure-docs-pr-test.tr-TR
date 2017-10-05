---
title: "Öğretici: Azure Active Directory Tümleştirme ile Freshservice | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Freshservice arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="e1652-103">Öğretici: Azure Active Directory Tümleştirme Freshservice ile</span><span class="sxs-lookup"><span data-stu-id="e1652-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="e1652-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Freshservice tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e1652-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1652-105">Freshservice Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1652-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1652-106">Freshservice erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1652-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="e1652-107">Otomatik olarak için Freshservice (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1652-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1652-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e1652-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1652-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1652-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1652-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1652-110">Prerequisites</span></span>

<span data-ttu-id="e1652-111">Azure AD tümleştirme Freshservice ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1652-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="e1652-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1652-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1652-113">Bir Freshservice çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="e1652-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1652-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1652-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1652-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1652-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1652-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1652-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1652-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1652-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1652-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1652-118">Scenario description</span></span>
<span data-ttu-id="e1652-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1652-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1652-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1652-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1652-121">Galeriden Freshservice ekleme</span><span class="sxs-lookup"><span data-stu-id="e1652-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="e1652-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1652-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="e1652-123">Galeriden Freshservice ekleme</span><span class="sxs-lookup"><span data-stu-id="e1652-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="e1652-124">Azure AD Freshservice tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Freshservice eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1652-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1652-125">**Galeriden Freshservice eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1652-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1652-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1652-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1652-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1652-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1652-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1652-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e1652-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1652-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e1652-133">Arama kutusuna **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="e1652-133">In the search box, type **Freshservice**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="e1652-135">Sonuçlar panelinde seçin **Freshservice**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1652-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1652-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1652-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1652-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Freshservice sınayın.</span><span class="sxs-lookup"><span data-stu-id="e1652-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1652-139">Tekli çalışmaya oturum için Azure AD Freshservice karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e1652-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="e1652-140">Diğer bir deyişle, bir Azure AD kullanıcısının Freshservice ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1652-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="e1652-141">Freshservice içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e1652-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1652-142">Yapılandırma ve Azure AD çoklu oturum açma Freshservice ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1652-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1652-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1652-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e1652-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e1652-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1652-145">**[Freshservice test kullanıcısı oluşturma](#creating-a-freshservice-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Freshservice sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e1652-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1652-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1652-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1652-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1652-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1652-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1652-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1652-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Freshservice uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1652-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="e1652-150">**Azure AD çoklu oturum açma ile Freshservice yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1652-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="e1652-151">Azure portalında üzerinde **Freshservice** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1652-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e1652-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1652-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="e1652-155">Üzerinde **Freshservice etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1652-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="e1652-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1652-157">a.</span></span> <span data-ttu-id="e1652-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="e1652-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="e1652-159">b.</span><span class="sxs-lookup"><span data-stu-id="e1652-159">b.</span></span> <span data-ttu-id="e1652-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="e1652-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1652-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e1652-161">These values are not real.</span></span> <span data-ttu-id="e1652-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1652-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1652-163">Kişi [Freshservice istemci destek ekibi](https://support.freshservice.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="e1652-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="e1652-164">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="e1652-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="e1652-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1652-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1652-168">Üzerinde **Freshservice yapılandırma** 'yi tıklatın **yapılandırma Freshservice** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e1652-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e1652-169">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="e1652-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="e1652-171">Farklı web tarayıcısı penceresinde Freshservice şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1652-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="e1652-172">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e1652-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="e1652-173">![Yönetici](./media/active-directory-saas-freshservice-tutorial/ic790814.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="e1652-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="e1652-174">İçinde **müşteri portalı**, tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="e1652-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="e1652-175">![Güvenlik](./media/active-directory-saas-freshservice-tutorial/ic790815.png "güvenlik")</span><span class="sxs-lookup"><span data-stu-id="e1652-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="e1652-176">İçinde **güvenlik** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1652-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e1652-177">![Çoklu oturum açmayı](./media/active-directory-saas-freshservice-tutorial/ic790816.png "çoklu oturum açmayı")</span><span class="sxs-lookup"><span data-stu-id="e1652-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="e1652-178">a.</span><span class="sxs-lookup"><span data-stu-id="e1652-178">a.</span></span> <span data-ttu-id="e1652-179">Anahtar **çoklu oturum açmayı**.</span><span class="sxs-lookup"><span data-stu-id="e1652-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="e1652-180">b.</span><span class="sxs-lookup"><span data-stu-id="e1652-180">b.</span></span> <span data-ttu-id="e1652-181">Seçin **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="e1652-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="e1652-182">c.</span><span class="sxs-lookup"><span data-stu-id="e1652-182">c.</span></span> <span data-ttu-id="e1652-183">İçinde **SAML oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e1652-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1652-184">d.</span><span class="sxs-lookup"><span data-stu-id="e1652-184">d.</span></span> <span data-ttu-id="e1652-185">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="e1652-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1652-186">e.</span><span class="sxs-lookup"><span data-stu-id="e1652-186">e.</span></span> <span data-ttu-id="e1652-187">İçinde **güvenlik sertifika parmak izi** metin kutusuna, Yapıştır **parmak İZİ** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="e1652-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1652-188">f.</span><span class="sxs-lookup"><span data-stu-id="e1652-188">f.</span></span> <span data-ttu-id="e1652-189">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="e1652-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="e1652-190">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1652-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1652-191">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e1652-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1652-192">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1652-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1652-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1652-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1652-194">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e1652-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e1652-196">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1652-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1652-197">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1652-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1652-199">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1652-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1652-201">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e1652-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1652-203">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1652-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1652-205">a.</span><span class="sxs-lookup"><span data-stu-id="e1652-205">a.</span></span> <span data-ttu-id="e1652-206">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1652-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1652-207">b.</span><span class="sxs-lookup"><span data-stu-id="e1652-207">b.</span></span> <span data-ttu-id="e1652-208">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e1652-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1652-209">c.</span><span class="sxs-lookup"><span data-stu-id="e1652-209">c.</span></span> <span data-ttu-id="e1652-210">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e1652-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1652-211">d.</span><span class="sxs-lookup"><span data-stu-id="e1652-211">d.</span></span> <span data-ttu-id="e1652-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1652-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="e1652-213">Freshservice test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1652-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="e1652-214">Azure AD kullanıcıları için FreshService oturum açmak etkinleştirmek için bunların FreshService sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e1652-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="e1652-215">FreshService söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="e1652-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="e1652-216">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1652-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e1652-217">Oturum, **FreshService** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="e1652-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="e1652-218">Üstteki menüde tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e1652-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="e1652-219">![Yönetici](./media/active-directory-saas-freshservice-tutorial/ic790814.png "yönetici")</span><span class="sxs-lookup"><span data-stu-id="e1652-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="e1652-220">İçinde **kullanıcı yönetimi** 'yi tıklatın **sahiplerini**.</span><span class="sxs-lookup"><span data-stu-id="e1652-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="e1652-221">![Sahiplerini](./media/active-directory-saas-freshservice-tutorial/ic790818.png "sahiplerini")</span><span class="sxs-lookup"><span data-stu-id="e1652-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="e1652-222">Tıklatın **yeni istek**.</span><span class="sxs-lookup"><span data-stu-id="e1652-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="e1652-223">![Yeni sahiplerini](./media/active-directory-saas-freshservice-tutorial/ic790819.png "yeni sahiplerini")</span><span class="sxs-lookup"><span data-stu-id="e1652-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="e1652-224">İçinde **yeni istek** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1652-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e1652-225">![Yeni İstek](./media/active-directory-saas-freshservice-tutorial/ic790820.png "yeni istek")</span><span class="sxs-lookup"><span data-stu-id="e1652-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="e1652-226">a.</span><span class="sxs-lookup"><span data-stu-id="e1652-226">a.</span></span> <span data-ttu-id="e1652-227">Girin **ad** ve **e-posta** istediğiniz ilgili metin kutularına sağlamayı geçerli bir Azure Active Directory hesabı öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="e1652-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="e1652-228">b.</span><span class="sxs-lookup"><span data-stu-id="e1652-228">b.</span></span> <span data-ttu-id="e1652-229">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1652-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e1652-230">Azure Active Directory hesap sahibi etkin duruma gelmesi hesabı onaylamak için bir bağlantı içeren bir e-posta alır</span><span class="sxs-lookup"><span data-stu-id="e1652-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="e1652-231">API sağlama AAD kullanıcı hesaplarına FreshService tarafından sağlanan veya herhangi diğer FreshService kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1652-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Kullanıcı atama][200] 

<span data-ttu-id="e1652-233">**Freshservice için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1652-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="e1652-234">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1652-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1652-236">Uygulamalar listesinde **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="e1652-236">In the applications list, select **Freshservice**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="e1652-238">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1652-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e1652-240">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1652-240">Click **Add** button.</span></span> <span data-ttu-id="e1652-241">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1652-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e1652-243">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1652-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e1652-244">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1652-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1652-245">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1652-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1652-246">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1652-246">Testing single sign-on</span></span>

<span data-ttu-id="e1652-247">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="e1652-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1652-248">Erişim paneli Freshservice parçasında tıklattığınızda, otomatik olarak Freshservice uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e1652-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1652-249">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1652-249">Additional resources</span></span>

* [<span data-ttu-id="e1652-250">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e1652-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1652-251">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1652-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

