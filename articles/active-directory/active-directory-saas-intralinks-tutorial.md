---
title: "Öğretici: Azure Active Directory Tümleştirme ile Intralinks | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Intralinks arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="caa8a-103">Öğretici: Azure Active Directory Tümleştirme Intralinks ile</span><span class="sxs-lookup"><span data-stu-id="caa8a-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="caa8a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Intralinks tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="caa8a-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="caa8a-105">Intralinks Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="caa8a-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="caa8a-106">Intralinks erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="caa8a-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="caa8a-107">Otomatik olarak için Intralinks (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="caa8a-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="caa8a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="caa8a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="caa8a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="caa8a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caa8a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="caa8a-110">Prerequisites</span></span>

<span data-ttu-id="caa8a-111">Azure AD tümleştirme Intralinks ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="caa8a-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="caa8a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="caa8a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="caa8a-113">Bir Intralinks çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="caa8a-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="caa8a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="caa8a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="caa8a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="caa8a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="caa8a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="caa8a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="caa8a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="caa8a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="caa8a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="caa8a-118">Scenario description</span></span>
<span data-ttu-id="caa8a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="caa8a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="caa8a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="caa8a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="caa8a-121">Galeriden Intralinks ekleme</span><span class="sxs-lookup"><span data-stu-id="caa8a-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="caa8a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="caa8a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="caa8a-123">Galeriden Intralinks ekleme</span><span class="sxs-lookup"><span data-stu-id="caa8a-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="caa8a-124">Azure AD Intralinks tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Intralinks eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="caa8a-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="caa8a-125">**Galeriden Intralinks eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="caa8a-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="caa8a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="caa8a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="caa8a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="caa8a-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="caa8a-133">Arama kutusuna **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-133">In the search box, type **Intralinks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="caa8a-135">Sonuçlar panelinde seçin **Intralinks**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="caa8a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="caa8a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="caa8a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Intralinks sınayın.</span><span class="sxs-lookup"><span data-stu-id="caa8a-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="caa8a-139">Tekli çalışmaya oturum için Azure AD Intralinks karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="caa8a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="caa8a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Intralinks ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="caa8a-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="caa8a-141">Intralinks içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="caa8a-142">Yapılandırma ve Azure AD çoklu oturum açma Intralinks ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="caa8a-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="caa8a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="caa8a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="caa8a-145">**[Bir Intralinks test kullanıcısı oluşturma](#creating-an-intralinks-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Intralinks sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="caa8a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="caa8a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="caa8a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="caa8a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="caa8a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="caa8a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Intralinks uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="caa8a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="caa8a-150">**Azure AD çoklu oturum açma ile Intralinks yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="caa8a-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="caa8a-151">Azure portalında üzerinde **Intralinks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="caa8a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="caa8a-155">Üzerinde **Intralinks etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="caa8a-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="caa8a-157">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="caa8a-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="caa8a-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="caa8a-158">This value is not real.</span></span> <span data-ttu-id="caa8a-159">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="caa8a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="caa8a-160">Kişi [Intralinks istemci destek ekibi](https://www.intralinks.com/contact-1) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="caa8a-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="caa8a-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="caa8a-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="caa8a-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="caa8a-165">Çoklu oturum açma yapılandırmak için **Intralinks** yan, indirilen göndermek için ihtiyacınız **meta veri XML** [Intralinks destek ekibi](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="caa8a-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="caa8a-166">Bunlar, her iki tarafta da ayarlamanızı SAML SSO bağlantı sağlamak için bu ayarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="caa8a-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="caa8a-167">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="caa8a-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="caa8a-168">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="caa8a-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="caa8a-169">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="caa8a-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="caa8a-170">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa8a-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="caa8a-171">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="caa8a-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="caa8a-173">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="caa8a-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="caa8a-174">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="caa8a-176">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="caa8a-178">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="caa8a-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="caa8a-180">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="caa8a-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="caa8a-182">a.</span><span class="sxs-lookup"><span data-stu-id="caa8a-182">a.</span></span> <span data-ttu-id="caa8a-183">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="caa8a-184">b.</span><span class="sxs-lookup"><span data-stu-id="caa8a-184">b.</span></span> <span data-ttu-id="caa8a-185">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="caa8a-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="caa8a-186">c.</span><span class="sxs-lookup"><span data-stu-id="caa8a-186">c.</span></span> <span data-ttu-id="caa8a-187">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="caa8a-188">d.</span><span class="sxs-lookup"><span data-stu-id="caa8a-188">d.</span></span> <span data-ttu-id="caa8a-189">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="caa8a-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="caa8a-190">Bir Intralinks test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa8a-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="caa8a-191">Bu bölümde, Intralinks içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="caa8a-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="caa8a-192">Lütfen çalışmak [Intralinks destek ekibi](https://www.intralinks.com/contact-1) Intralinks platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="caa8a-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="caa8a-193">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="caa8a-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="caa8a-194">Bu bölümde, Britta Intralinks için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="caa8a-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="caa8a-196">**Intralinks için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="caa8a-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="caa8a-197">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="caa8a-199">Uygulamalar listesinde **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-199">In the applications list, select **Intralinks**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="caa8a-201">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="caa8a-203">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-203">Click **Add** button.</span></span> <span data-ttu-id="caa8a-204">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="caa8a-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="caa8a-206">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="caa8a-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="caa8a-207">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="caa8a-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="caa8a-208">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="caa8a-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="caa8a-209">Intralinks aracılığıyla veya Elite uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="caa8a-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="caa8a-210">Intralinks aynı SSO kimlik platformu anlaşma Nexus uygulama hariç olmak üzere diğer tüm Intralinks uygulamalar için kullanır.</span><span class="sxs-lookup"><span data-stu-id="caa8a-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="caa8a-211">Başka bir Intralinks uygulama kullanmayı planlıyorsanız, bu nedenle daha sonra ilk, SSO yukarıda açıklanan yordamı kullanarak birincil Intralinks uygulama için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="caa8a-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="caa8a-212">Bundan sonra takip ettiğiniz başka bir Intralinks uygulamaya SSO için birincil bu uygulama yararlanabilirsiniz, Kiracı eklemek için yordam aşağıda.</span><span class="sxs-lookup"><span data-stu-id="caa8a-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="caa8a-213">Bu özellik yalnızca Azure AD Premium SKU müşteriler için kullanılabilir ve ücretsiz veya temel SKU müşteriler için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="caa8a-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="caa8a-214">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="caa8a-216">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="caa8a-217">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-217">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="caa8a-219">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="caa8a-221">Arama kutusuna **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-221">In the search box, type **Intralinks**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="caa8a-223">Üzerinde **uygulama Intralinks Ekle** aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="caa8a-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Intralinks aracılığıyla veya Elite uygulama ekleme](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="caa8a-225">a.</span><span class="sxs-lookup"><span data-stu-id="caa8a-225">a.</span></span> <span data-ttu-id="caa8a-226">İçinde **adı** metin kutusuna, uygun uygulama örneğin adını **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="caa8a-227">b.</span><span class="sxs-lookup"><span data-stu-id="caa8a-227">b.</span></span> <span data-ttu-id="caa8a-228">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="caa8a-229">Azure portalında üzerinde **Intralinks** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

7. <span data-ttu-id="caa8a-231">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **bağlantılı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="caa8a-233">Alma SP tarafından başlatılan SSO'yu URL'den [Intralinks takım](https://www.intralinks.com/contact-1) diğer Intralinks uygulama için ve içinde girin **yapılandırma oturum açma URL'si** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="caa8a-235">Oturum üzerinde URL'si metin kutusuna, kullanıcılarınıza oturum açma şu biçimi kullanarak Intralinks uygulamanız tarafından kullanılan URL'yi yazın:</span><span class="sxs-lookup"><span data-stu-id="caa8a-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="caa8a-236">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="caa8a-236">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="caa8a-238">Kullanıcı veya gruplara uygulama bölümünde gösterildiği gibi atama  **[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="caa8a-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="caa8a-239">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="caa8a-239">Testing single sign-on</span></span>

<span data-ttu-id="caa8a-240">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="caa8a-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="caa8a-241">Erişim paneli Intralinks parçasında tıklattığınızda, otomatik olarak Intralinks uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="caa8a-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="caa8a-242">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="caa8a-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="caa8a-243">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="caa8a-243">Additional resources</span></span>

* [<span data-ttu-id="caa8a-244">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="caa8a-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="caa8a-245">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="caa8a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

