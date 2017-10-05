---
title: "Öğretici: Azure Active Directory Tümleştirme ile Expensify | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Expensify arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="9cbe4-103">Öğretici: Azure Active Directory Tümleştirme Expensify ile</span><span class="sxs-lookup"><span data-stu-id="9cbe4-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="9cbe4-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Expensify tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cbe4-105">Expensify Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9cbe4-106">Expensify erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9cbe4-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="9cbe4-107">Otomatik olarak için Expensify (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="9cbe4-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cbe4-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="9cbe4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9cbe4-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cbe4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cbe4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9cbe4-110">Prerequisites</span></span>

<span data-ttu-id="9cbe4-111">Azure AD tümleştirme Expensify ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="9cbe4-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="9cbe4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cbe4-113">Bir Expensify çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="9cbe4-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cbe4-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cbe4-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cbe4-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cbe4-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cbe4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cbe4-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="9cbe4-118">Scenario description</span></span>
<span data-ttu-id="9cbe4-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cbe4-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cbe4-121">Galeriden Expensify ekleme</span><span class="sxs-lookup"><span data-stu-id="9cbe4-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="9cbe4-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9cbe4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="9cbe4-123">Galeriden Expensify ekleme</span><span class="sxs-lookup"><span data-stu-id="9cbe4-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="9cbe4-124">Azure AD Expensify tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Expensify eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9cbe4-125">**Galeriden Expensify eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9cbe4-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9cbe4-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cbe4-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9cbe4-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="9cbe4-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="9cbe4-133">Arama kutusuna **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-133">In the search box, type **Expensify**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="9cbe4-135">Sonuçlar panelinde seçin **Expensify**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cbe4-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="9cbe4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cbe4-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Expensify sınayın.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9cbe4-139">Tekli çalışmaya oturum için Azure AD Expensify karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="9cbe4-140">Diğer bir deyişle, bir Azure AD kullanıcısının Expensify ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="9cbe4-141">Expensify içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9cbe4-142">Yapılandırma ve Azure AD çoklu oturum açma Expensify ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9cbe4-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9cbe4-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cbe4-145">**[Bir Expensify test kullanıcısı oluşturma](#creating-an-expensify-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Expensify sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cbe4-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cbe4-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cbe4-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9cbe4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cbe4-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Expensify uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="9cbe4-150">**Azure AD çoklu oturum açma ile Expensify yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9cbe4-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="9cbe4-151">Azure portalında üzerinde **Expensify** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="9cbe4-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="9cbe4-155">Üzerinde **Expensify etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="9cbe4-157">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-157">a.</span></span> <span data-ttu-id="9cbe4-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="9cbe4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="9cbe4-159">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-159">b.</span></span> <span data-ttu-id="9cbe4-160">İçinde **tanımlayıcı URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="9cbe4-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="9cbe4-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-161">These values are not real.</span></span> <span data-ttu-id="9cbe4-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="9cbe4-163">Kişi [Expensify istemci destek ekibi](mailto:help@expensify.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="9cbe4-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="9cbe4-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cbe4-168">Expensify SSO'yu etkinleştirmek için önce etkinleştirmeniz gerekir **etki alanı denetim** uygulamadaki.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="9cbe4-169">Listelenen adımları üzerinden uygulama içinde etki alanı denetimini etkinleştir [burada](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="9cbe4-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="9cbe4-170">Ek destek için çalışmak [Expensify istemci destek ekibi](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="9cbe4-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="9cbe4-171">Etki alanı etkin denetim olduktan sonra aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="9cbe4-173">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-173">a.</span></span> <span data-ttu-id="9cbe4-174">Expensify uygulamanıza oturum açma.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="9cbe4-175">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-175">b.</span></span> <span data-ttu-id="9cbe4-176">Üstteki araç çubuğunda tıklatın **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="9cbe4-177">c.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-177">c.</span></span> <span data-ttu-id="9cbe4-178">Sol panelinde tıklatın **etki alanı**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="9cbe4-179">d.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-179">d.</span></span> <span data-ttu-id="9cbe4-180">Doğrulanmış etki alanı adınıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="9cbe4-181">e.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-181">e.</span></span> <span data-ttu-id="9cbe4-182">Sol panelinde tıklatın **SAML**ve ardından **etkin**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="9cbe4-183">f.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-183">f.</span></span> <span data-ttu-id="9cbe4-184">İndirilen Federasyon meta verilerini Azure AD'den Not Defteri'nde açın, içeriği Kopyala ve ardından yapıştırın **kimlik sağlayıcısı meta verileri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="9cbe4-185">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="9cbe4-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9cbe4-186">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9cbe4-187">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cbe4-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cbe4-188">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cbe4-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cbe4-189">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="9cbe4-191">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9cbe4-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9cbe4-192">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cbe4-194">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cbe4-196">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cbe4-198">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9cbe4-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cbe4-200">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-200">a.</span></span> <span data-ttu-id="9cbe4-201">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cbe4-202">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-202">b.</span></span> <span data-ttu-id="9cbe4-203">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cbe4-204">c.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-204">c.</span></span> <span data-ttu-id="9cbe4-205">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9cbe4-206">d.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-206">d.</span></span> <span data-ttu-id="9cbe4-207">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="9cbe4-208">Bir Expensify test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cbe4-208">Creating an Expensify test user</span></span>

<span data-ttu-id="9cbe4-209">Bu bölümde, Expensify içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="9cbe4-210">Çalışmak [Expensify istemci destek ekibi](mailto:help@expensify.com) Expensify platform kullanıcıları eklemek için.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9cbe4-211">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="9cbe4-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9cbe4-212">Bu bölümde, Britta Expensify için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="9cbe4-214">**Expensify için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="9cbe4-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="9cbe4-215">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="9cbe4-217">Uygulamalar listesinde **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-217">In the applications list, select **Expensify**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="9cbe4-219">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="9cbe4-221">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-221">Click **Add** button.</span></span> <span data-ttu-id="9cbe4-222">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="9cbe4-224">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9cbe4-225">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cbe4-226">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cbe4-227">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="9cbe4-227">Testing single sign-on</span></span>

<span data-ttu-id="9cbe4-228">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="9cbe4-229">Erişim paneli Expensify parçasında tıklattığınızda, otomatik olarak Expensify uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="9cbe4-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cbe4-230">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="9cbe4-230">Additional resources</span></span>

* [<span data-ttu-id="9cbe4-231">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="9cbe4-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cbe4-232">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="9cbe4-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

