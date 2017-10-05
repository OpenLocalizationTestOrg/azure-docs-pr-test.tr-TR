---
title: "Öğretici: Azure Active Directory Tümleştirme ile UserVoice | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile UserVoice arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="36002-103">Öğretici: Azure Active Directory Tümleştirme UserVoice ile</span><span class="sxs-lookup"><span data-stu-id="36002-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="36002-104">Bu öğreticide, Azure Active Directory (Azure AD) ile UserVoice tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="36002-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36002-105">UserVoice Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="36002-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36002-106">UserVoice erişimi, Azure AD'de kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36002-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="36002-107">Otomatik olarak için UserVoice (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36002-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="36002-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="36002-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="36002-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36002-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36002-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="36002-110">Prerequisites</span></span>

<span data-ttu-id="36002-111">Azure AD tümleştirme UserVoice ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="36002-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="36002-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="36002-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36002-113">Bir UserVoice çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="36002-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36002-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="36002-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36002-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="36002-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36002-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="36002-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36002-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36002-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36002-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="36002-118">Scenario description</span></span>
<span data-ttu-id="36002-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="36002-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36002-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="36002-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36002-121">Galeriden UserVoice ekleme</span><span class="sxs-lookup"><span data-stu-id="36002-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="36002-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="36002-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="36002-123">Galeriden UserVoice ekleme</span><span class="sxs-lookup"><span data-stu-id="36002-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="36002-124">Azure AD UserVoice tümleştirilmesi yapılandırmak için UserVoice Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36002-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36002-125">**Galeriden UserVoice eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36002-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36002-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="36002-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="36002-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="36002-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36002-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="36002-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="36002-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36002-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="36002-133">Arama kutusuna **UserVoice**seçin **UserVoice** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="36002-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![Sonuçlar listesinde UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="36002-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="36002-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="36002-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı UserVoice sınayın.</span><span class="sxs-lookup"><span data-stu-id="36002-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36002-137">Tekli çalışmaya oturum için Azure AD UserVoice karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="36002-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="36002-138">Diğer bir deyişle, bir Azure AD kullanıcısının UserVoice ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36002-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="36002-139">UserVoice içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="36002-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="36002-140">Yapılandırma ve Azure AD çoklu oturum açma UserVoice ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="36002-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36002-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="36002-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36002-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="36002-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36002-143">**[UserVoice test kullanıcısı oluşturma](#create-a-uservoice-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı UserVoice sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="36002-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="36002-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="36002-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36002-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="36002-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="36002-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="36002-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="36002-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma UserVoice uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="36002-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="36002-148">**Azure AD çoklu oturum açma ile UserVoice yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36002-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="36002-149">Azure portalında üzerinde **UserVoice** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="36002-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="36002-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="36002-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="36002-153">Üzerinde **UserVoice etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36002-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![UserVoice etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="36002-155">a.</span><span class="sxs-lookup"><span data-stu-id="36002-155">a.</span></span> <span data-ttu-id="36002-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="36002-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="36002-157">b.</span><span class="sxs-lookup"><span data-stu-id="36002-157">b.</span></span> <span data-ttu-id="36002-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="36002-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36002-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="36002-159">These values are not real.</span></span> <span data-ttu-id="36002-160">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="36002-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="36002-161">Kişi [UserVoice istemci destek ekibi](https://www.uservoice.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="36002-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="36002-162">Üzerinde **SAML imzalama sertifikası** bölümünde, kopyalama **parmak İZİ** sertifika değeri.</span><span class="sxs-lookup"><span data-stu-id="36002-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="36002-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36002-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36002-166">Üzerinde **UserVoice yapılandırma** 'yi tıklatın **yapılandırma UserVoice** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="36002-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="36002-167">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="36002-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![UserVoice yapılandırma](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="36002-169">Farklı web tarayıcısı penceresinde UserVoice şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="36002-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="36002-170">Üstteki araç çubuğunda tıklatın **ayarları**ve ardından **Web portalı** menüsünde.</span><span class="sxs-lookup"><span data-stu-id="36002-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="36002-171">![Uygulama tarafında ayarları bölümünde](./media/active-directory-saas-uservoice-tutorial/ic777519.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="36002-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="36002-172">Üzerinde **Web portalı** sekmesinde **kullanıcı kimlik doğrulaması** 'yi tıklatın **Düzenle** açmak için **kullanıcı kimlik doğrulamasını Düzenle** iletişim sayfası.</span><span class="sxs-lookup"><span data-stu-id="36002-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="36002-173">![Web portalı sekmesini](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portalı")</span><span class="sxs-lookup"><span data-stu-id="36002-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="36002-174">Üzerinde **kullanıcı kimlik doğrulamasını Düzenle** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36002-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="36002-175">![Kullanıcı kimlik doğrulamasını Düzenle](./media/active-directory-saas-uservoice-tutorial/ic777521.png "düzenleme kullanıcı kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="36002-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="36002-176">a.</span><span class="sxs-lookup"><span data-stu-id="36002-176">a.</span></span> <span data-ttu-id="36002-177">Tıklatın **çoklu oturum açma (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="36002-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="36002-178">b.</span><span class="sxs-lookup"><span data-stu-id="36002-178">b.</span></span> <span data-ttu-id="36002-179">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **SSO uzaktan oturum açma** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="36002-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="36002-180">c.</span><span class="sxs-lookup"><span data-stu-id="36002-180">c.</span></span> <span data-ttu-id="36002-181">Yapıştır **Sign-Out URL** Azure portalından kopyaladığınız değeri **SSO uzak Sign-Out textbox**.</span><span class="sxs-lookup"><span data-stu-id="36002-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="36002-182">d.</span><span class="sxs-lookup"><span data-stu-id="36002-182">d.</span></span> <span data-ttu-id="36002-183">Yapıştır **parmak izi** Azure portalından kopyaladığınız değeri **geçerli SHA1 sertifika parmak izi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="36002-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="36002-184">e.</span><span class="sxs-lookup"><span data-stu-id="36002-184">e.</span></span> <span data-ttu-id="36002-185">Tıklatın **kimlik doğrulama ayarlarını Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="36002-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="36002-186">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="36002-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36002-187">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="36002-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36002-188">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36002-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="36002-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="36002-189">Create an Azure AD test user</span></span>

<span data-ttu-id="36002-190">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="36002-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="36002-192">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36002-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36002-193">Sol bölmede, Azure portal'ı tıklatın **Azure Active Directory** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36002-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="36002-195">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar**ve ardından **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="36002-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="36002-197">Açmak için **kullanıcı** iletişim kutusu, tıklatın **Ekle** en üstündeki **tüm kullanıcılar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="36002-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Ekle düğmesi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="36002-199">İçinde **kullanıcı** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36002-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="36002-201">a.</span><span class="sxs-lookup"><span data-stu-id="36002-201">a.</span></span> <span data-ttu-id="36002-202">İçinde **adı** kutusuna **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36002-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36002-203">b.</span><span class="sxs-lookup"><span data-stu-id="36002-203">b.</span></span> <span data-ttu-id="36002-204">İçinde **kullanıcı adı** kullanıcı Britta Simon e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="36002-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="36002-205">c.</span><span class="sxs-lookup"><span data-stu-id="36002-205">c.</span></span> <span data-ttu-id="36002-206">Seçin **Göster parola** onay kutusunu işaretleyin ve ardından görüntülenen değer aşağı yazma **parola** kutusu.</span><span class="sxs-lookup"><span data-stu-id="36002-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="36002-207">d.</span><span class="sxs-lookup"><span data-stu-id="36002-207">d.</span></span> <span data-ttu-id="36002-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="36002-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="36002-209">UserVoice test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="36002-209">Create a UserVoice test user</span></span>

<span data-ttu-id="36002-210">Azure AD kullanıcıları için UserVoice oturum açmayı etkinleştirmek için bunların UserVoice sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="36002-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="36002-211">UserVoice söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="36002-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="36002-212">Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36002-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="36002-213">Oturum, **UserVoice** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="36002-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="36002-214">Git **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="36002-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="36002-215">![Ayarları](./media/active-directory-saas-uservoice-tutorial/ic777811.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="36002-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="36002-216">Tıklatın **genel**.</span><span class="sxs-lookup"><span data-stu-id="36002-216">Click **General**.</span></span>

4. <span data-ttu-id="36002-217">Tıklatın **aracıları ve izinleri**.</span><span class="sxs-lookup"><span data-stu-id="36002-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="36002-218">![Aracılar ve izinleri](./media/active-directory-saas-uservoice-tutorial/ic777812.png "aracıları ve izinleri")</span><span class="sxs-lookup"><span data-stu-id="36002-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="36002-219">Tıklatın **yöneticileri ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="36002-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="36002-220">![Yöneticileri ekleyin](./media/active-directory-saas-uservoice-tutorial/ic777813.png "yöneticileri ekleyin")</span><span class="sxs-lookup"><span data-stu-id="36002-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="36002-221">Üzerinde **davet admins** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36002-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="36002-222">![Yöneticileri davet](./media/active-directory-saas-uservoice-tutorial/ic777814.png "davet yöneticileri")</span><span class="sxs-lookup"><span data-stu-id="36002-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="36002-223">a.</span><span class="sxs-lookup"><span data-stu-id="36002-223">a.</span></span> <span data-ttu-id="36002-224">E-postaları metin kutusuna sağlamak istediğiniz ve ardından hesabın e-posta adresini yazın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="36002-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="36002-225">b.</span><span class="sxs-lookup"><span data-stu-id="36002-225">b.</span></span> <span data-ttu-id="36002-226">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="36002-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="36002-227">API sağlama AAD kullanıcı hesaplarına UserVoice tarafından sağlanan veya herhangi diğer UserVoice kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36002-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="36002-228">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="36002-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="36002-229">Bu bölümde, Britta UserVoice için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="36002-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![Kullanıcı rolü atayın][200] 

<span data-ttu-id="36002-231">**UserVoice için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="36002-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="36002-232">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="36002-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="36002-234">Uygulamalar listesinde **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="36002-234">In the applications list, select **UserVoice**.</span></span>

    ![Uygulamalar listesinde UserVoice bağlantı](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="36002-236">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="36002-236">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="36002-238">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="36002-238">Click **Add** button.</span></span> <span data-ttu-id="36002-239">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36002-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="36002-241">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="36002-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="36002-242">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36002-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36002-243">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="36002-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="36002-244">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="36002-244">Test single sign-on</span></span>

<span data-ttu-id="36002-245">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="36002-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36002-246">Erişim paneli UserVoice parçasında tıklattığınızda, otomatik olarak UserVoice uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="36002-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="36002-247">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36002-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="36002-248">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="36002-248">Additional resources</span></span>

* [<span data-ttu-id="36002-249">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="36002-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36002-250">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="36002-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

