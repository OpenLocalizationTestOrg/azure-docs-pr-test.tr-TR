---
title: "Öğretici: Azure Active Directory Tümleştirme ile Panorama9 | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Panorama9 arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="d7203-103">Öğretici: Azure Active Directory Tümleştirme Panorama9 ile</span><span class="sxs-lookup"><span data-stu-id="d7203-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="d7203-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Panorama9 tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d7203-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7203-105">Panorama9 Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d7203-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7203-106">Panorama9 erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7203-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="d7203-107">Otomatik olarak Panorama9 için açan kullanıcılarınıza etkinleştirebilirsiniz (çoklu oturum açma) Azure AD hesaplarına sahip</span><span class="sxs-lookup"><span data-stu-id="d7203-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7203-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d7203-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7203-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7203-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7203-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d7203-110">Prerequisites</span></span>

<span data-ttu-id="d7203-111">Azure AD tümleştirme Panorama9 ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7203-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="d7203-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d7203-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7203-113">Bir Panorama9 çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d7203-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7203-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d7203-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7203-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7203-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7203-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d7203-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7203-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7203-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7203-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d7203-118">Scenario description</span></span>
<span data-ttu-id="d7203-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d7203-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7203-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d7203-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7203-121">Galeriden Panorama9 ekleme</span><span class="sxs-lookup"><span data-stu-id="d7203-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="d7203-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d7203-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="d7203-123">Galeriden Panorama9 ekleme</span><span class="sxs-lookup"><span data-stu-id="d7203-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="d7203-124">Azure AD Panorama9 tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Panorama9 eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7203-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7203-125">**Galeriden Panorama9 eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7203-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7203-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7203-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7203-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d7203-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7203-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7203-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d7203-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7203-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d7203-133">Arama kutusuna **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="d7203-133">In the search box, type **Panorama9**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="d7203-135">Sonuçlar panelinde seçin **Panorama9**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7203-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7203-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d7203-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="d7203-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Panorama9 ile test etme</span><span class="sxs-lookup"><span data-stu-id="d7203-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d7203-139">Tekli çalışmaya oturum için Azure AD Panorama9 karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d7203-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="d7203-140">Diğer bir deyişle, bir Azure AD kullanıcısının Panorama9 ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7203-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="d7203-141">Panorama9 içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d7203-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d7203-142">Yapılandırma ve Azure AD çoklu oturum açma Panorama9 ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7203-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7203-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d7203-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7203-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d7203-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7203-145">**[Panorama9 test kullanıcısı oluşturma](#creating-a-panorama9-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Panorama9 sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d7203-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7203-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d7203-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7203-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d7203-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7203-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d7203-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7203-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Panorama9 uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d7203-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="d7203-150">**Azure AD çoklu oturum açma ile Panorama9 yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7203-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="d7203-151">Azure portalında üzerinde **Panorama9** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d7203-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d7203-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d7203-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="d7203-155">Üzerinde **Panorama9 etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7203-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="d7203-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7203-157">a.</span></span> <span data-ttu-id="d7203-158">İçinde **oturum açma URL'si** metin kutusuna, URL'yi yazın:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="d7203-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="d7203-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7203-159">b.</span></span> <span data-ttu-id="d7203-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="d7203-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7203-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d7203-161">These values are not real.</span></span> <span data-ttu-id="d7203-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7203-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d7203-163">Kişi [Panorama9 istemci destek ekibi](https://support.panorama9.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="d7203-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="d7203-164">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="d7203-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="d7203-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7203-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7203-168">Üzerinde **Panorama9 yapılandırma** 'yi tıklatın **yapılandırma Panorama9** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d7203-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d7203-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="d7203-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="d7203-171">Farklı web tarayıcısı penceresinde Panorama9 şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d7203-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="d7203-172">Üstteki araç çubuğunda tıklatın **Yönet**ve ardından **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="d7203-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="d7203-173">![Uzantıları](./media/active-directory-saas-panorama9-tutorial/ic790023.png "uzantıları")</span><span class="sxs-lookup"><span data-stu-id="d7203-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="d7203-174">Üzerinde **uzantıları** iletişim kutusunda, tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d7203-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="d7203-175">![Çoklu oturum açma](./media/active-directory-saas-panorama9-tutorial/ic790024.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d7203-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="d7203-176">İçinde **ayarları** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7203-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="d7203-177">![Ayarları](./media/active-directory-saas-panorama9-tutorial/ic790025.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="d7203-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="d7203-178">a.</span><span class="sxs-lookup"><span data-stu-id="d7203-178">a.</span></span> <span data-ttu-id="d7203-179">İçinde **kimlik sağlayıcısı URL'si** metin değerini yapıştırın **çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="d7203-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d7203-180">b.</span><span class="sxs-lookup"><span data-stu-id="d7203-180">b.</span></span> <span data-ttu-id="d7203-181">İçinde **sertifika parmak izi** metin kutusuna, Yapıştır **parmak izi** Azure portalından kopyaladığınız sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="d7203-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="d7203-182">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7203-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d7203-183">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d7203-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7203-184">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d7203-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7203-185">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7203-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7203-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7203-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7203-187">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d7203-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d7203-189">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7203-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7203-190">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7203-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7203-192">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d7203-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7203-194">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="d7203-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7203-196">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d7203-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7203-198">a.</span><span class="sxs-lookup"><span data-stu-id="d7203-198">a.</span></span> <span data-ttu-id="d7203-199">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7203-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7203-200">b.</span><span class="sxs-lookup"><span data-stu-id="d7203-200">b.</span></span> <span data-ttu-id="d7203-201">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d7203-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7203-202">c.</span><span class="sxs-lookup"><span data-stu-id="d7203-202">c.</span></span> <span data-ttu-id="d7203-203">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d7203-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7203-204">d.</span><span class="sxs-lookup"><span data-stu-id="d7203-204">d.</span></span> <span data-ttu-id="d7203-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7203-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="d7203-206">Panorama9 test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7203-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="d7203-207">Azure AD kullanıcıların Panorama9 oturum etkinleştirmek için bunların Panorama9 sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d7203-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="d7203-208">Panorama9 söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d7203-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="d7203-209">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7203-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="d7203-210">Oturum, **Panorama9** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="d7203-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="d7203-211">Üstteki menüde tıklatın **Yönet**ve ardından **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d7203-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="d7203-212">![Kullanıcıların](./media/active-directory-saas-panorama9-tutorial/ic790027.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="d7203-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="d7203-213">Kullanıcılar bölümünde tıklatın  **+**  yeni kullanıcı eklemek için.</span><span class="sxs-lookup"><span data-stu-id="d7203-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="d7203-214">![Kullanıcıların](./media/active-directory-saas-panorama9-tutorial/ic790028.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="d7203-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="d7203-215">Kullanıcı verileri bölümüne gidin, istediğiniz içine sağlamak için geçerli bir Azure Active Directory kullanıcı e-posta adresini yazın **e-posta** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d7203-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="d7203-216">Kullanıcılar bölümü tıklatın gelen **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d7203-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="d7203-217">Azure Active Directory hesap sahibi bir e-posta alır ve bunu etkinleştirilmeden önce kendi hesabı onaylamak için bir bağlantı izler.</span><span class="sxs-lookup"><span data-stu-id="d7203-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7203-218">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d7203-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7203-219">Bu bölümde, Britta Panorama9 için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7203-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d7203-221">**Panorama9 için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d7203-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="d7203-222">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7203-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d7203-224">Uygulamalar listesinde **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="d7203-224">In the applications list, select **Panorama9**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="d7203-226">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d7203-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d7203-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d7203-228">Click **Add** button.</span></span> <span data-ttu-id="d7203-229">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7203-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d7203-231">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d7203-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7203-232">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7203-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7203-233">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d7203-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7203-234">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d7203-234">Testing single sign-on</span></span>

<span data-ttu-id="d7203-235">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d7203-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7203-236">Erişim paneli Panorama9 parçasında tıklattığınızda, otomatik olarak Panorama9 uygulamaya açan.</span><span class="sxs-lookup"><span data-stu-id="d7203-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="d7203-237">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7203-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7203-238">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d7203-238">Additional resources</span></span>

* [<span data-ttu-id="d7203-239">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d7203-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7203-240">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d7203-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

