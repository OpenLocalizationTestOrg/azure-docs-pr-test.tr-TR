---
title: "Öğretici: Azure Active Directory Tümleştirme ile Heroku | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Heroku arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="e1488-103">Öğretici: Azure Active Directory Tümleştirme Heroku ile</span><span class="sxs-lookup"><span data-stu-id="e1488-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="e1488-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Heroku tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e1488-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1488-105">Heroku Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1488-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1488-106">Heroku erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1488-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="e1488-107">Otomatik olarak için Heroku (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e1488-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1488-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="e1488-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1488-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1488-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1488-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1488-110">Prerequisites</span></span>

<span data-ttu-id="e1488-111">Azure AD tümleştirme Heroku ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1488-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="e1488-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="e1488-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1488-113">Bir Heroku çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="e1488-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1488-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e1488-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1488-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1488-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1488-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e1488-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1488-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1488-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1488-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1488-118">Scenario description</span></span>
<span data-ttu-id="e1488-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="e1488-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1488-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="e1488-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1488-121">Galeriden Heroku ekleme</span><span class="sxs-lookup"><span data-stu-id="e1488-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="e1488-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1488-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="e1488-123">Galeriden Heroku ekleme</span><span class="sxs-lookup"><span data-stu-id="e1488-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="e1488-124">Azure AD Heroku tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Heroku eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1488-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1488-125">**Galeriden Heroku eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1488-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1488-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1488-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1488-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e1488-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1488-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1488-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="e1488-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1488-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="e1488-133">Arama kutusuna **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="e1488-133">In the search box, type **Heroku**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="e1488-135">Sonuçlar panelinde seçin **Heroku**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1488-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1488-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="e1488-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="e1488-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Heroku ile test etme</span><span class="sxs-lookup"><span data-stu-id="e1488-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e1488-139">Tekli çalışmaya oturum için Azure AD Heroku karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="e1488-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="e1488-140">Diğer bir deyişle, bir Azure AD kullanıcısının Heroku ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1488-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="e1488-141">Heroku içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e1488-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1488-142">Yapılandırma ve Azure AD çoklu oturum açma Heroku ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1488-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1488-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1488-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e1488-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="e1488-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1488-145">**[Heroku test kullanıcısı oluşturma](#creating-a-heroku-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Heroku sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="e1488-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1488-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1488-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1488-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1488-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1488-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1488-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1488-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Heroku uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e1488-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="e1488-150">**Azure AD çoklu oturum açma ile Heroku yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1488-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="e1488-151">Azure portalında üzerinde **Heroku** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="e1488-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="e1488-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e1488-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="e1488-155">Üzerinde **Heroku etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1488-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="e1488-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1488-157">a.</span></span> <span data-ttu-id="e1488-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="e1488-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="e1488-159">b.</span><span class="sxs-lookup"><span data-stu-id="e1488-159">b.</span></span> <span data-ttu-id="e1488-160">İçinde **tanımlayıcı URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="e1488-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="e1488-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="e1488-161">These values are not real.</span></span> <span data-ttu-id="e1488-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1488-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1488-163">Bu makalenin sonraki bölümlerinde açıklanan Heroku ekibinden bu değerleri alır.</span><span class="sxs-lookup"><span data-stu-id="e1488-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="e1488-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1488-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="e1488-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1488-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1488-168">Heroku SSO'yu etkinleştirmek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1488-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="e1488-169">a.</span><span class="sxs-lookup"><span data-stu-id="e1488-169">a.</span></span> <span data-ttu-id="e1488-170">Heroku hesabı yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1488-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="e1488-171">b.</span><span class="sxs-lookup"><span data-stu-id="e1488-171">b.</span></span> <span data-ttu-id="e1488-172">**Ayarlar** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1488-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="e1488-173">c.</span><span class="sxs-lookup"><span data-stu-id="e1488-173">c.</span></span> <span data-ttu-id="e1488-174">Üzerinde **tek oturum açma sayfasına**, tıklatın **meta veriler karşıya**.</span><span class="sxs-lookup"><span data-stu-id="e1488-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="e1488-175">d.</span><span class="sxs-lookup"><span data-stu-id="e1488-175">d.</span></span> <span data-ttu-id="e1488-176">Azure Portalı'ndan indirilen meta veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1488-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="e1488-177">e.</span><span class="sxs-lookup"><span data-stu-id="e1488-177">e.</span></span> <span data-ttu-id="e1488-178">Kurulum başarılı olduğunda, Yöneticiler bir onay iletişim kutusu bakın ve son kullanıcılar için SSO oturum açma URL'sini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e1488-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="e1488-179">f.</span><span class="sxs-lookup"><span data-stu-id="e1488-179">f.</span></span> <span data-ttu-id="e1488-180">Kopya **Heroku oturum açma URL'si** ve **Heroku varlık kimliği** değerleri ve geri dönüp **Heroku etki alanı ve URL'leri** bölümünde Azure portalında ve bu değerleri içine yapıştırma  **Oturum açma URL'si** ve **tanımlayıcısı** kutularındaki sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="e1488-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="e1488-182">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1488-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="e1488-183">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="e1488-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1488-184">Bu uygulamadan ekledikten sonra **Active Directory kuruluş uygulamaları** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir  **Yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="e1488-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1488-185">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1488-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1488-186">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1488-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="e1488-187">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e1488-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="e1488-189">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1488-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1488-190">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="e1488-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1488-192">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="e1488-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1488-194">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="e1488-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1488-196">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e1488-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1488-198">a.</span><span class="sxs-lookup"><span data-stu-id="e1488-198">a.</span></span> <span data-ttu-id="e1488-199">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1488-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1488-200">b.</span><span class="sxs-lookup"><span data-stu-id="e1488-200">b.</span></span> <span data-ttu-id="e1488-201">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="e1488-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1488-202">c.</span><span class="sxs-lookup"><span data-stu-id="e1488-202">c.</span></span> <span data-ttu-id="e1488-203">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="e1488-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1488-204">d.</span><span class="sxs-lookup"><span data-stu-id="e1488-204">d.</span></span> <span data-ttu-id="e1488-205">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1488-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="e1488-206">Heroku test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1488-206">Creating a Heroku test user</span></span>

<span data-ttu-id="e1488-207">Bu bölümde, Heroku içinde Britta Simon adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1488-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="e1488-208">Heroku yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="e1488-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="e1488-209">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="e1488-209">There is no action item for you in this section.</span></span> <span data-ttu-id="e1488-210">Yeni bir kullanıcı, kullanıcı henüz yoksa Heroku erişirken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1488-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="e1488-211">Hesabı sağlandıktan sonra son kullanıcı bir doğrulama e-posta alır ve bildirim bağlantısına tıklayın gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e1488-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="e1488-212">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [Heroku istemci destek ekibi](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="e1488-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e1488-213">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="e1488-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e1488-214">Bu bölümde, Britta Heroku için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1488-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="e1488-216">**Heroku için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="e1488-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="e1488-217">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e1488-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="e1488-219">Uygulamalar listesinde **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="e1488-219">In the applications list, select **Heroku**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="e1488-221">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e1488-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="e1488-223">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1488-223">Click **Add** button.</span></span> <span data-ttu-id="e1488-224">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1488-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="e1488-226">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="e1488-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e1488-227">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1488-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1488-228">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e1488-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1488-229">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="e1488-229">Testing single sign-on</span></span>

<span data-ttu-id="e1488-230">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="e1488-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1488-231">Erişim paneli Heroku parçasında tıklattığınızda, otomatik olarak Heroku uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="e1488-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1488-232">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1488-232">Additional resources</span></span>

* [<span data-ttu-id="e1488-233">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="e1488-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1488-234">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="e1488-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
