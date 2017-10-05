---
title: "Öğretici: Azure Active Directory Tümleştirme ile TiViTz | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile TiViTz arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: b1b27918bb5fcff1d19f4711ea70fe46a5697933
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="d80b1-103">Öğretici: Azure Active Directory Tümleştirme TiViTz ile</span><span class="sxs-lookup"><span data-stu-id="d80b1-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="d80b1-104">Bu öğreticide, Azure Active Directory (Azure AD) ile TiViTz tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d80b1-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d80b1-105">TiViTz Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d80b1-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d80b1-106">TiViTz erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d80b1-106">You can control in Azure AD who has access to TiViTz</span></span>
- <span data-ttu-id="d80b1-107">Otomatik olarak için TiViTz (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d80b1-107">You can enable your users to automatically get signed-on to TiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d80b1-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="d80b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d80b1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d80b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d80b1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d80b1-110">Prerequisites</span></span>

<span data-ttu-id="d80b1-111">Azure AD tümleştirme TiViTz ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d80b1-111">To configure Azure AD integration with TiViTz, you need the following items:</span></span>

- <span data-ttu-id="d80b1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d80b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d80b1-113">Bir TiViTz çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="d80b1-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d80b1-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d80b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d80b1-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d80b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d80b1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="d80b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d80b1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d80b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d80b1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d80b1-118">Scenario description</span></span>
<span data-ttu-id="d80b1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d80b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d80b1-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d80b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d80b1-121">Galeriden TiViTz ekleme</span><span class="sxs-lookup"><span data-stu-id="d80b1-121">Adding TiViTz from the gallery</span></span>
2. <span data-ttu-id="d80b1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d80b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-the-gallery"></a><span data-ttu-id="d80b1-123">Galeriden TiViTz ekleme</span><span class="sxs-lookup"><span data-stu-id="d80b1-123">Adding TiViTz from the gallery</span></span>
<span data-ttu-id="d80b1-124">Azure AD TiViTz tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden TiViTz eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d80b1-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d80b1-125">**Galeriden TiViTz eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d80b1-125">**To add TiViTz from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d80b1-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d80b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d80b1-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d80b1-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d80b1-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d80b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d80b1-133">Arama kutusuna **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-133">In the search box, type **TiViTz**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_search.png)

5. <span data-ttu-id="d80b1-135">Sonuçlar panelinde seçin **TiViTz**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d80b1-135">In the results panel, select **TiViTz**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d80b1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d80b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d80b1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı TiViTz sınayın.</span><span class="sxs-lookup"><span data-stu-id="d80b1-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d80b1-139">Tekli çalışmaya oturum için Azure AD TiViTz karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d80b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span></span> <span data-ttu-id="d80b1-140">Diğer bir deyişle, bir Azure AD kullanıcısının TiViTz ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d80b1-140">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span></span>

<span data-ttu-id="d80b1-141">TiViTz içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-141">In TiViTz, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d80b1-142">Yapılandırma ve Azure AD çoklu oturum açma TiViTz ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d80b1-142">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d80b1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d80b1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d80b1-145">**[TiViTz test kullanıcısı oluşturma](#creating-a-tivitz-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı TiViTz sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d80b1-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d80b1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d80b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d80b1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d80b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d80b1-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma TiViTz uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d80b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="d80b1-150">**Azure AD çoklu oturum açma ile TiViTz yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d80b1-150">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="d80b1-151">Azure portalında üzerinde **TiViTz** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-151">In the Azure portal, on the **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d80b1-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_samlbase.png)

3. <span data-ttu-id="d80b1-155">Üzerinde **TiViTz etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d80b1-155">On the **TiViTz Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="d80b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="d80b1-157">a.</span></span> <span data-ttu-id="d80b1-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="d80b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="d80b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="d80b1-159">b.</span></span> <span data-ttu-id="d80b1-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="d80b1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d80b1-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="d80b1-161">These values are not real.</span></span> <span data-ttu-id="d80b1-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d80b1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d80b1-163">Kişi [TiViTz istemci destek ekibi](mailto:info@tivitz.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="d80b1-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) to get these values.</span></span> 

4. <span data-ttu-id="d80b1-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d80b1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_certificate.png) 

5. <span data-ttu-id="d80b1-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d80b1-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tivitz-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d80b1-168">Çoklu oturum açma yapılandırmak için **TiViTz** yan, indirilen göndermek için ihtiyacınız **meta veri XML** için [TiViTz destek ekibi](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="d80b1-168">To configure single sign-on on **TiViTz** side, you need to send the downloaded **Metadata XML** to [TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="d80b1-169">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="d80b1-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d80b1-170">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="d80b1-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d80b1-171">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d80b1-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d80b1-172">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d80b1-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="d80b1-173">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d80b1-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d80b1-175">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d80b1-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d80b1-176">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d80b1-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tivitz-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d80b1-178">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tivitz-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d80b1-180">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="d80b1-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d80b1-182">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d80b1-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d80b1-184">a.</span><span class="sxs-lookup"><span data-stu-id="d80b1-184">a.</span></span> <span data-ttu-id="d80b1-185">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d80b1-186">b.</span><span class="sxs-lookup"><span data-stu-id="d80b1-186">b.</span></span> <span data-ttu-id="d80b1-187">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d80b1-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d80b1-188">c.</span><span class="sxs-lookup"><span data-stu-id="d80b1-188">c.</span></span> <span data-ttu-id="d80b1-189">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d80b1-190">d.</span><span class="sxs-lookup"><span data-stu-id="d80b1-190">d.</span></span> <span data-ttu-id="d80b1-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d80b1-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="d80b1-192">TiViTz test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d80b1-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="d80b1-193">Bu bölümün amacı Britta Simon içinde TiViTz adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d80b1-193">The objective of this section is to create a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="d80b1-194">TiViTz yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="d80b1-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d80b1-195">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="d80b1-195">There is no action item for you in this section.</span></span> <span data-ttu-id="d80b1-196">Yeni bir kullanıcı henüz yoksa TiViTz erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d80b1-196">A new user is created during an attempt to access TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d80b1-197">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [TiViTz destek ekibi](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="d80b1-197">If you need to create an user manually, you need to contact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d80b1-198">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d80b1-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d80b1-199">Bu bölümde, Britta TiViTz için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d80b1-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TiViTz.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d80b1-201">**TiViTz için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d80b1-201">**To assign Britta Simon to TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="d80b1-202">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d80b1-204">Uygulamalar listesinde **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-204">In the applications list, select **TiViTz**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_app.png) 

3. <span data-ttu-id="d80b1-206">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d80b1-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d80b1-208">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d80b1-208">Click **Add** button.</span></span> <span data-ttu-id="d80b1-209">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d80b1-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d80b1-211">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d80b1-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d80b1-212">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d80b1-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d80b1-213">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d80b1-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d80b1-214">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d80b1-214">Testing single sign-on</span></span>

<span data-ttu-id="d80b1-215">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d80b1-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d80b1-216">Erişim paneli TiViTz parçasında tıklattığınızda, otomatik olarak TiViTz uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="d80b1-216">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d80b1-217">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d80b1-217">Additional resources</span></span>

* [<span data-ttu-id="d80b1-218">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d80b1-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d80b1-219">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d80b1-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png

