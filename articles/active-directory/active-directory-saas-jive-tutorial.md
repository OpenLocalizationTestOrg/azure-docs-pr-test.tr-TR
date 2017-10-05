---
title: "Öğretici: Azure Active Directory Tümleştirme ile Jive | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Jive arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="1f351-103">Öğretici: Azure Active Directory Tümleştirme Jive ile</span><span class="sxs-lookup"><span data-stu-id="1f351-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="1f351-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Jive tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1f351-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f351-105">Jive Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="1f351-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f351-106">Jive erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1f351-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="1f351-107">Otomatik olarak için Jive (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1f351-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f351-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="1f351-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f351-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla bilgi bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f351-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f351-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1f351-110">Prerequisites</span></span>

<span data-ttu-id="1f351-111">Azure AD tümleştirme Jive ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="1f351-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="1f351-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="1f351-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f351-113">Bir Jive çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="1f351-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f351-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1f351-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f351-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1f351-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f351-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1f351-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f351-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f351-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f351-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="1f351-118">Scenario description</span></span>
<span data-ttu-id="1f351-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="1f351-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f351-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="1f351-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f351-121">Galeriden Jive ekleme</span><span class="sxs-lookup"><span data-stu-id="1f351-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="1f351-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1f351-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="1f351-123">Galeriden Jive ekleme</span><span class="sxs-lookup"><span data-stu-id="1f351-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="1f351-124">Azure AD'ye Jive tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Jive eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f351-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f351-125">**Galeriden Jive eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1f351-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f351-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f351-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1f351-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f351-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1f351-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="1f351-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="1f351-133">Arama kutusuna **Jive**.</span><span class="sxs-lookup"><span data-stu-id="1f351-133">In the search box, type **Jive**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="1f351-135">Sonuçlar panelinde seçin **Jive**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f351-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="1f351-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f351-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Jive ile test etme</span><span class="sxs-lookup"><span data-stu-id="1f351-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f351-139">Tekli çalışmaya oturum için Azure AD Jive karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="1f351-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="1f351-140">Diğer bir deyişle, bir Azure AD kullanıcısının Jive ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f351-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="1f351-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Jive içinde.</span><span class="sxs-lookup"><span data-stu-id="1f351-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="1f351-142">Yapılandırma ve Azure AD çoklu oturum açma Jive ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1f351-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f351-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1f351-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f351-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="1f351-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f351-145">**[Jive test kullanıcısı oluşturma](#creating-a-jive-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Jive sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="1f351-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f351-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1f351-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f351-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1f351-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f351-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1f351-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f351-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Jive uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1f351-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="1f351-150">**Azure AD çoklu oturum açma ile Jive yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1f351-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="1f351-151">Azure portalında üzerinde **Jive** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="1f351-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="1f351-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1f351-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="1f351-155">Üzerinde **Jive etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1f351-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="1f351-157">a.</span><span class="sxs-lookup"><span data-stu-id="1f351-157">a.</span></span> <span data-ttu-id="1f351-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="1f351-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="1f351-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f351-159">b.</span></span> <span data-ttu-id="1f351-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="1f351-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f351-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="1f351-161">These values are not the real.</span></span> <span data-ttu-id="1f351-162">Bu değerleri tanımlayıcısı ve gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1f351-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="1f351-163">Kişi [Jive istemci destek ekibi](https://www.jivesoftware.com/services-support/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="1f351-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="1f351-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1f351-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="1f351-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f351-168">Çoklu oturum açma yapılandırmak için **Jive** tarafında, oturum açma Jive Kiracı yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="1f351-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="1f351-169">Üstteki menüde tıklayın "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="1f351-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="1f351-171">a.</span><span class="sxs-lookup"><span data-stu-id="1f351-171">a.</span></span> <span data-ttu-id="1f351-172">Seçin **etkin** altında **genel** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="1f351-173">b.</span><span class="sxs-lookup"><span data-stu-id="1f351-173">b.</span></span> <span data-ttu-id="1f351-174">Tıklayın "**tüm saml Ayarları Kaydet**" düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="1f351-175">Gidin "**IDP meta veri**" sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="1f351-177">a.</span><span class="sxs-lookup"><span data-stu-id="1f351-177">a.</span></span> <span data-ttu-id="1f351-178">İndirilen meta veri XML dosyasının içeriğini kopyalayın ve ardından yapıştırın **kimlik sağlayıcısı (IDP) meta veri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="1f351-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="1f351-179">b.</span><span class="sxs-lookup"><span data-stu-id="1f351-179">b.</span></span> <span data-ttu-id="1f351-180">Tıklayın "**tüm saml Ayarları Kaydet**" düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="1f351-181">Git "**kullanıcı özniteliği eşleme**" sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="1f351-183">a.</span><span class="sxs-lookup"><span data-stu-id="1f351-183">a.</span></span> <span data-ttu-id="1f351-184">İçinde **e-posta** metin kutusuna, öznitelik adı kopyalayıp **posta** değeri.</span><span class="sxs-lookup"><span data-stu-id="1f351-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="1f351-185">b.</span><span class="sxs-lookup"><span data-stu-id="1f351-185">b.</span></span> <span data-ttu-id="1f351-186">İçinde **ad** metin kutusuna, öznitelik adı kopyalayıp **givenname** değeri.</span><span class="sxs-lookup"><span data-stu-id="1f351-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="1f351-187">c.</span><span class="sxs-lookup"><span data-stu-id="1f351-187">c.</span></span> <span data-ttu-id="1f351-188">İçinde **Soyadı** metin kutusuna, öznitelik adı kopyalayıp **Soyadı** değeri.</span><span class="sxs-lookup"><span data-stu-id="1f351-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="1f351-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="1f351-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f351-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="1f351-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f351-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f351-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f351-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f351-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f351-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="1f351-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="1f351-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1f351-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f351-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f351-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="1f351-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f351-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="1f351-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f351-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1f351-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f351-204">a.</span><span class="sxs-lookup"><span data-stu-id="1f351-204">a.</span></span> <span data-ttu-id="1f351-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f351-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f351-206">b.</span><span class="sxs-lookup"><span data-stu-id="1f351-206">b.</span></span> <span data-ttu-id="1f351-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="1f351-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f351-208">c.</span><span class="sxs-lookup"><span data-stu-id="1f351-208">c.</span></span> <span data-ttu-id="1f351-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="1f351-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f351-210">d.</span><span class="sxs-lookup"><span data-stu-id="1f351-210">d.</span></span> <span data-ttu-id="1f351-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1f351-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="1f351-212">Jive test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f351-212">Creating a Jive test user</span></span>

<span data-ttu-id="1f351-213">Çalışmak [Jive istemci destek ekibi](https://www.jivesoftware.com/services-support/) Jive platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="1f351-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f351-214">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="1f351-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f351-215">Bu bölümde, Britta Jive için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1f351-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="1f351-217">**Jive için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="1f351-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="1f351-218">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="1f351-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="1f351-220">Uygulamalar listesinde **Jive**.</span><span class="sxs-lookup"><span data-stu-id="1f351-220">In the applications list, select **Jive**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="1f351-222">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="1f351-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="1f351-224">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f351-224">Click **Add** button.</span></span> <span data-ttu-id="1f351-225">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1f351-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="1f351-227">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="1f351-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f351-228">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1f351-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f351-229">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="1f351-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f351-230">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="1f351-230">Testing single sign-on</span></span>

<span data-ttu-id="1f351-231">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="1f351-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f351-232">Erişim paneli Jive parçasında tıklattığınızda, otomatik olarak Jive uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="1f351-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f351-233">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1f351-233">Additional resources</span></span>

* [<span data-ttu-id="1f351-234">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="1f351-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f351-235">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="1f351-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1f351-236">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="1f351-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

