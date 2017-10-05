---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jobscience | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Jobscience arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="92c4d-103">Öğretici: Azure Active Directory Tümleştirme Jobscience ile</span><span class="sxs-lookup"><span data-stu-id="92c4d-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="92c4d-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Jobscience tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92c4d-105">Jobscience Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="92c4d-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92c4d-106">Jobscience erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="92c4d-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="92c4d-107">Otomatik olarak için Jobscience (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="92c4d-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92c4d-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="92c4d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92c4d-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92c4d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92c4d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="92c4d-110">Prerequisites</span></span>

<span data-ttu-id="92c4d-111">Azure AD tümleştirme Jobscience ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c4d-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="92c4d-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="92c4d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92c4d-113">Bir Jobscience çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="92c4d-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92c4d-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="92c4d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92c4d-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c4d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92c4d-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92c4d-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92c4d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92c4d-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="92c4d-118">Scenario description</span></span>
<span data-ttu-id="92c4d-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92c4d-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="92c4d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92c4d-121">Galeriden Jobscience ekleme</span><span class="sxs-lookup"><span data-stu-id="92c4d-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="92c4d-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="92c4d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="92c4d-123">Galeriden Jobscience ekleme</span><span class="sxs-lookup"><span data-stu-id="92c4d-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="92c4d-124">Azure AD Jobscience tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Jobscience eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c4d-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92c4d-125">**Galeriden Jobscience eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4d-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92c4d-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92c4d-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92c4d-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="92c4d-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="92c4d-133">Arama kutusuna **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-133">In the search box, type **Jobscience**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="92c4d-135">Sonuçlar panelinde seçin **Jobscience**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92c4d-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="92c4d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92c4d-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Jobscience ile test etme</span><span class="sxs-lookup"><span data-stu-id="92c4d-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="92c4d-139">Tekli çalışmaya oturum için Azure AD Jobscience karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="92c4d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="92c4d-140">Diğer bir deyişle, bir Azure AD kullanıcısının Jobscience ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c4d-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="92c4d-141">Jobscience içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92c4d-142">Yapılandırma ve Azure AD çoklu oturum açma Jobscience ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c4d-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92c4d-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92c4d-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92c4d-145">**[Jobscience test kullanıcısı oluşturma](#creating-a-jobscience-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Jobscience sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92c4d-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92c4d-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92c4d-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="92c4d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92c4d-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Jobscience uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="92c4d-150">**Azure AD çoklu oturum açma ile Jobscience yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4d-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="92c4d-151">Azure portalında üzerinde **Jobscience** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="92c4d-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="92c4d-155">Üzerinde **Jobscience etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4d-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="92c4d-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="92c4d-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="92c4d-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="92c4d-158">This value is not real.</span></span> <span data-ttu-id="92c4d-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="92c4d-160">Bu değer alma [Jobscience istemci destek ekibi](https://www.jobscience.com/support) veya SSO profilinden öğreticide daha sonra açıklanan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="92c4d-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="92c4d-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="92c4d-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92c4d-165">Üzerinde **Jobscience yapılandırma** 'yi tıklatın **yapılandırma Jobscience** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="92c4d-166">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="92c4d-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="92c4d-168">Jobscience şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="92c4d-169">Git **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="92c4d-170">![Kurulum](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="92c4d-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="92c4d-171">Sol gezinti bölmesinde, içinde **Yönet** 'yi tıklatın **etki alanı yönetimi** ilgili bölümü genişletin ve ardından **My etki alanı** açmak için **My etki alanı** sayfası.</span><span class="sxs-lookup"><span data-stu-id="92c4d-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="92c4d-172">![Etki alanım](./media/active-directory-saas-jobscience-tutorial/ic767825.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="92c4d-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="92c4d-173">Etki alanınızın doğru şekilde ayarlanmış olması gerektiğini doğrulamak için içinde olduğundan emin olun "**adım 4 dağıtılan kullanıcılara**" ve gözden geçirin, "**My etki alanı ayarları**".</span><span class="sxs-lookup"><span data-stu-id="92c4d-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="92c4d-174">![Etki alanı kullanıcıya dağıtılan](./media/active-directory-saas-jobscience-tutorial/ic784377.png "kullanıcıya dağıtılan etki alanı")</span><span class="sxs-lookup"><span data-stu-id="92c4d-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="92c4d-175">Jobscience şirket sitesinde tıklatın **güvenlik denetimleri**ve ardından **çoklu oturum açma ayarları**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="92c4d-176">![Güvenlik denetimleri](./media/active-directory-saas-jobscience-tutorial/ic784364.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="92c4d-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="92c4d-177">İçinde **çoklu oturum açma ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4d-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="92c4d-178">![Çoklu oturum açma ayarları](./media/active-directory-saas-jobscience-tutorial/ic781026.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="92c4d-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="92c4d-179">a.</span><span class="sxs-lookup"><span data-stu-id="92c4d-179">a.</span></span> <span data-ttu-id="92c4d-180">Seçin **SAML etkin**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="92c4d-181">b.</span><span class="sxs-lookup"><span data-stu-id="92c4d-181">b.</span></span> <span data-ttu-id="92c4d-182">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-182">Click **New**.</span></span>

13. <span data-ttu-id="92c4d-183">Üzerinde **SAML çoklu oturum açma ayarını Düzenle** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4d-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="92c4d-184">![Oturum açma SAML tek ayar](./media/active-directory-saas-jobscience-tutorial/ic784365.png "oturum açma SAML tek ayar")</span><span class="sxs-lookup"><span data-stu-id="92c4d-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="92c4d-185">a.</span><span class="sxs-lookup"><span data-stu-id="92c4d-185">a.</span></span> <span data-ttu-id="92c4d-186">İçinde **adı** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="92c4d-187">b.</span><span class="sxs-lookup"><span data-stu-id="92c4d-187">b.</span></span> <span data-ttu-id="92c4d-188">İçinde **veren** metin değerini yapıştırın **SAML varlık kimliği**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="92c4d-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="92c4d-189">c.</span><span class="sxs-lookup"><span data-stu-id="92c4d-189">c.</span></span> <span data-ttu-id="92c4d-190">İçinde **varlık kimliği** metin kutusuna, türü`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="92c4d-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="92c4d-191">d.</span><span class="sxs-lookup"><span data-stu-id="92c4d-191">d.</span></span> <span data-ttu-id="92c4d-192">Tıklatın **Gözat** Azure AD sertifikanızı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="92c4d-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="92c4d-193">e.</span><span class="sxs-lookup"><span data-stu-id="92c4d-193">e.</span></span> <span data-ttu-id="92c4d-194">Olarak **SAML kimlik türü**seçin **onaylamayı içeren kullanıcı nesnesinden Federasyon kimliği**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="92c4d-195">f.</span><span class="sxs-lookup"><span data-stu-id="92c4d-195">f.</span></span> <span data-ttu-id="92c4d-196">Olarak **SAML kimlik konumu**seçin **kimliktir konu deyimi NameIdentfier öğesinde**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="92c4d-197">g.</span><span class="sxs-lookup"><span data-stu-id="92c4d-197">g.</span></span> <span data-ttu-id="92c4d-198">İçinde **kimlik sağlayıcısı oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="92c4d-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="92c4d-199">h.</span><span class="sxs-lookup"><span data-stu-id="92c4d-199">h.</span></span> <span data-ttu-id="92c4d-200">İçinde **kimlik sağlayıcısı oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="92c4d-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="92c4d-201">ı.</span><span class="sxs-lookup"><span data-stu-id="92c4d-201">i.</span></span> <span data-ttu-id="92c4d-202">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-202">Click **Save**.</span></span>

14. <span data-ttu-id="92c4d-203">Sol gezinti bölmesinde, içinde **Yönet** 'yi tıklatın **etki alanı yönetimi** ilgili bölümü genişletin ve ardından **My etki alanı** açmak için **My etki alanı** sayfası.</span><span class="sxs-lookup"><span data-stu-id="92c4d-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="92c4d-204">![Etki alanım](./media/active-directory-saas-jobscience-tutorial/ic767825.png "etki alanım")</span><span class="sxs-lookup"><span data-stu-id="92c4d-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="92c4d-205">Üzerinde **My etki alanı** sayfasında **oturum açma sayfası markalama** 'yi tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="92c4d-206">![Oturum açma sayfası markalama](./media/active-directory-saas-jobscience-tutorial/ic767826.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="92c4d-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="92c4d-207">Üzerinde **oturum açma sayfası markalama** sayfasında **kimlik doğrulama hizmeti** bölümünde, adını, **SAML SSO ayarları** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="92c4d-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="92c4d-208">Seçin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="92c4d-209">![Oturum açma sayfası markalama](./media/active-directory-saas-jobscience-tutorial/ic784366.png "oturum açma sayfası markalama")</span><span class="sxs-lookup"><span data-stu-id="92c4d-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="92c4d-210">SP almak için üzerinde oturum açma URL'si tıklatıldığında çoklu oturum açma başlatılan **çoklu oturum açma ayarları** içinde **güvenlik denetimleri** menü bölümü.</span><span class="sxs-lookup"><span data-stu-id="92c4d-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="92c4d-211">![Güvenlik denetimleri](./media/active-directory-saas-jobscience-tutorial/ic784368.png "güvenlik denetimleri")</span><span class="sxs-lookup"><span data-stu-id="92c4d-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="92c4d-212">Yukarıdaki adımda oluşturduğunuz SSO profiline tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="92c4d-213">Bu sayfa çoklu oturum açma URL'SİNDE şirketiniz için gösterir (örneğin, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="92c4d-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="92c4d-214">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="92c4d-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92c4d-215">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="92c4d-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92c4d-216">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92c4d-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92c4d-217">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="92c4d-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="92c4d-218">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="92c4d-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="92c4d-220">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4d-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92c4d-221">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92c4d-223">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92c4d-225">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="92c4d-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92c4d-227">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4d-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92c4d-229">a.</span><span class="sxs-lookup"><span data-stu-id="92c4d-229">a.</span></span> <span data-ttu-id="92c4d-230">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92c4d-231">b.</span><span class="sxs-lookup"><span data-stu-id="92c4d-231">b.</span></span> <span data-ttu-id="92c4d-232">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="92c4d-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92c4d-233">c.</span><span class="sxs-lookup"><span data-stu-id="92c4d-233">c.</span></span> <span data-ttu-id="92c4d-234">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92c4d-235">d.</span><span class="sxs-lookup"><span data-stu-id="92c4d-235">d.</span></span> <span data-ttu-id="92c4d-236">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="92c4d-237">Jobscience test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="92c4d-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="92c4d-238">Azure AD kullanıcıları için Jobscience oturum açmak etkinleştirmek için bunların Jobscience sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="92c4d-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="92c4d-239">Jobscience söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="92c4d-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="92c4d-240">API tarafından Jobscience sağlamak için Azure Active Directory kullanıcı hesapları sağlanan veya herhangi diğer Jobscience kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c4d-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="92c4d-241">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4d-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="92c4d-242">Oturum, **Jobscience** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="92c4d-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="92c4d-243">Kurulum için gidin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-243">Go to Setup.</span></span>
   
   <span data-ttu-id="92c4d-244">![Kurulum](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="92c4d-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="92c4d-245">Git **kullanıcıları yönetme \> kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="92c4d-246">![Kullanıcıların](./media/active-directory-saas-jobscience-tutorial/ic784369.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="92c4d-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="92c4d-247">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-247">Click **New User**.</span></span>
   
   <span data-ttu-id="92c4d-248">![Tüm kullanıcılar](./media/active-directory-saas-jobscience-tutorial/ic784370.png "tüm kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="92c4d-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="92c4d-249">Üzerinde **kullanıcı düzenleme** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="92c4d-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="92c4d-250">![Kullanıcı düzenleme](./media/active-directory-saas-jobscience-tutorial/ic784371.png "kullanıcı düzenleme")</span><span class="sxs-lookup"><span data-stu-id="92c4d-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="92c4d-251">a.</span><span class="sxs-lookup"><span data-stu-id="92c4d-251">a.</span></span> <span data-ttu-id="92c4d-252">İçinde **ad** metin kutusuna, Britta gibi kullanıcının ilk adını yazın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="92c4d-253">b.</span><span class="sxs-lookup"><span data-stu-id="92c4d-253">b.</span></span> <span data-ttu-id="92c4d-254">İçinde **Soyadı** metin kutusuna, Simon gibi kullanıcının soyadını yazın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="92c4d-255">c.</span><span class="sxs-lookup"><span data-stu-id="92c4d-255">c.</span></span> <span data-ttu-id="92c4d-256">İçinde **diğer** metin kutusuna, kullanıcının brittas gibi bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="92c4d-257">d.</span><span class="sxs-lookup"><span data-stu-id="92c4d-257">d.</span></span> <span data-ttu-id="92c4d-258">İçinde **e-posta** metin kutusuna, kullanıcının e-posta adresi türü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="92c4d-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="92c4d-259">e.</span><span class="sxs-lookup"><span data-stu-id="92c4d-259">e.</span></span> <span data-ttu-id="92c4d-260">İçinde **kullanıcı adı** metin kutusuna, türü kullanıcının kullanıcı adını ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="92c4d-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="92c4d-261">f.</span><span class="sxs-lookup"><span data-stu-id="92c4d-261">f.</span></span> <span data-ttu-id="92c4d-262">İçinde **takma ad** metin kutusu, kullanıcı Simon gibi takma adını yazın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="92c4d-263">g.</span><span class="sxs-lookup"><span data-stu-id="92c4d-263">g.</span></span> <span data-ttu-id="92c4d-264">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="92c4d-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="92c4d-265">Azure Active Directory hesap sahibi bir e-posta alır ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izler.</span><span class="sxs-lookup"><span data-stu-id="92c4d-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92c4d-266">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="92c4d-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92c4d-267">Bu bölümde, Britta Jobscience için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="92c4d-269">**Jobscience için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="92c4d-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="92c4d-270">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="92c4d-272">Uygulamalar listesinde **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-272">In the applications list, select **Jobscience**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="92c4d-274">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="92c4d-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="92c4d-276">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="92c4d-276">Click **Add** button.</span></span> <span data-ttu-id="92c4d-277">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4d-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="92c4d-279">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="92c4d-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92c4d-280">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4d-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92c4d-281">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="92c4d-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92c4d-282">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="92c4d-282">Testing single sign-on</span></span>

<span data-ttu-id="92c4d-283">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="92c4d-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92c4d-284">Erişim paneli Jobscience parçasında tıklattığınızda, otomatik olarak Jobscience uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="92c4d-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="92c4d-285">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92c4d-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92c4d-286">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="92c4d-286">Additional resources</span></span>

* [<span data-ttu-id="92c4d-287">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="92c4d-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92c4d-288">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="92c4d-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

