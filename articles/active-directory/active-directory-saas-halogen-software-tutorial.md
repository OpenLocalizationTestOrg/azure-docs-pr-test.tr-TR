---
title: "Öğretici: Azure Active Directory Tümleştirme halojensiz yazılımıyla | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve halojensiz yazılımı arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="6f919-103">Öğretici: Azure Active Directory Tümleştirme halojensiz yazılımıyla</span><span class="sxs-lookup"><span data-stu-id="6f919-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="6f919-104">Bu öğreticide, halojensiz yazılım Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6f919-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f919-105">Halojensiz yazılım Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6f919-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6f919-106">Halojensiz yazılım erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6f919-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="6f919-107">Azure AD hesaplarına otomatik olarak halojensiz yazılımı (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6f919-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f919-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6f919-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6f919-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f919-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f919-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6f919-110">Prerequisites</span></span>

<span data-ttu-id="6f919-111">Azure AD tümleştirme halojensiz yazılımıyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f919-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="6f919-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6f919-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f919-113">Bir halojensiz yazılım çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6f919-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f919-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6f919-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f919-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f919-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f919-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6f919-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f919-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f919-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f919-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6f919-118">Scenario description</span></span>

<span data-ttu-id="6f919-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6f919-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f919-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6f919-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f919-121">Galeriden halojensiz yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="6f919-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="6f919-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f919-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="6f919-123">Galeriden halojensiz yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="6f919-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="6f919-124">Azure AD halojensiz yazılım tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden halojensiz yazılım eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f919-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f919-125">**Galeriden halojensiz yazılım eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f919-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f919-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f919-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6f919-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6f919-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f919-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6f919-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6f919-133">Arama kutusuna **halojensiz yazılım**.</span><span class="sxs-lookup"><span data-stu-id="6f919-133">In the search box, type **Halogen Software**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="6f919-135">Sonuçlar panelinde seçin **halojensiz yazılım**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f919-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6f919-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f919-138">Bu bölümde, yapılandırmak ve halojensiz yazılım "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="6f919-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f919-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen halojensiz yazılım bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="6f919-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="6f919-140">Diğer bir deyişle, bir Azure AD kullanıcısının halojensiz yazılım ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f919-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="6f919-141">Değeri halojensiz yazılımda atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6f919-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6f919-142">Yapılandırmak ve Azure AD çoklu oturum açma halojensiz yazılımıyla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6f919-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f919-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6f919-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f919-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="6f919-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f919-145">**[Halojensiz yazılım test kullanıcısı oluşturma](#creating-a-halogen-software-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı halojensiz yazılım sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="6f919-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f919-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6f919-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f919-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6f919-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f919-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6f919-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f919-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma halojensiz yazılım uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6f919-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="6f919-150">**Azure AD çoklu oturum açma halojensiz yazılımıyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f919-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="6f919-151">Azure portalında üzerinde **halojensiz yazılım** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6f919-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6f919-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6f919-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="6f919-155">Üzerinde **halojensiz yazılım etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f919-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="6f919-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f919-157">a.</span></span> <span data-ttu-id="6f919-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="6f919-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="6f919-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f919-159">b.</span></span> <span data-ttu-id="6f919-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="6f919-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f919-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6f919-161">These values are not real.</span></span> <span data-ttu-id="6f919-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f919-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6f919-163">Kişi [halojensiz yazılım istemci destek ekibi](https://support.halogensoftware.com/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="6f919-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="6f919-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6f919-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="6f919-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f919-168">Farklı bir tarayıcı penceresinde için oturum, **halojensiz yazılım** yönetici olarak uygulama.</span><span class="sxs-lookup"><span data-stu-id="6f919-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="6f919-169">Tıklatın **seçenekleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-169">Click the **Options** tab.</span></span> 
   
    ![Azure AD Connect nedir?][12]

8. <span data-ttu-id="6f919-171">Sol gezinti bölmesinde **SAML Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="6f919-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Azure AD Connect nedir?][13]

9. <span data-ttu-id="6f919-173">Üzerinde **SAML Yapılandırması** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f919-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Azure AD Connect nedir?][14]

     <span data-ttu-id="6f919-175">a.</span><span class="sxs-lookup"><span data-stu-id="6f919-175">a.</span></span> <span data-ttu-id="6f919-176">Olarak **benzersiz tanımlayıcı**seçin **NameID**.</span><span class="sxs-lookup"><span data-stu-id="6f919-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="6f919-177">b.</span><span class="sxs-lookup"><span data-stu-id="6f919-177">b.</span></span> <span data-ttu-id="6f919-178">Olarak **benzersiz tanıtıcı eşlemeleri için**seçin **kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="6f919-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="6f919-179">c.</span><span class="sxs-lookup"><span data-stu-id="6f919-179">c.</span></span> <span data-ttu-id="6f919-180">İndirilen meta veri dosyanızı karşıya yüklemek için tıklayın **Gözat** dosyasını seçmek için ve ardından **dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="6f919-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="6f919-181">d.</span><span class="sxs-lookup"><span data-stu-id="6f919-181">d.</span></span> <span data-ttu-id="6f919-182">Yapılandırmanızı sınamak için **testi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="6f919-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="6f919-183">Öğesinin ileti beklemesi gerekir "*SAML test tamamlandıktan. Lütfen bu pencereyi kapatmak*".</span><span class="sxs-lookup"><span data-stu-id="6f919-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="6f919-184">Ardından, açılan tarayıcı penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="6f919-184">Then, close the opened browser window.</span></span> <span data-ttu-id="6f919-185">**Etkinleştirmek SAML** onay kutusunu test olmuşsa yalnızca etkin.</span><span class="sxs-lookup"><span data-stu-id="6f919-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="6f919-186">e.</span><span class="sxs-lookup"><span data-stu-id="6f919-186">e.</span></span> <span data-ttu-id="6f919-187">Seçin **etkinleştirmek SAML**.</span><span class="sxs-lookup"><span data-stu-id="6f919-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="6f919-188">f.</span><span class="sxs-lookup"><span data-stu-id="6f919-188">f.</span></span> <span data-ttu-id="6f919-189">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6f919-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="6f919-190">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6f919-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6f919-191">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="6f919-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6f919-192">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f919-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f919-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f919-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="6f919-194">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6f919-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6f919-196">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f919-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f919-197">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f919-199">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6f919-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f919-201">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="6f919-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f919-203">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f919-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f919-205">a.</span><span class="sxs-lookup"><span data-stu-id="6f919-205">a.</span></span> <span data-ttu-id="6f919-206">İçinde **adı** metin kutusuna, tür adı olarak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f919-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="6f919-207">b.</span><span class="sxs-lookup"><span data-stu-id="6f919-207">b.</span></span> <span data-ttu-id="6f919-208">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6f919-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f919-209">c.</span><span class="sxs-lookup"><span data-stu-id="6f919-209">c.</span></span> <span data-ttu-id="6f919-210">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6f919-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6f919-211">d.</span><span class="sxs-lookup"><span data-stu-id="6f919-211">d.</span></span> <span data-ttu-id="6f919-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f919-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="6f919-213">Halojensiz yazılım test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f919-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="6f919-214">Bu bölümün amacı Britta Simon halojensiz yazılım adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6f919-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="6f919-215">**Britta Simon halojensiz yazılım adlı bir kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f919-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="6f919-216">Oturum, **halojensiz yazılım** yönetici olarak uygulama.</span><span class="sxs-lookup"><span data-stu-id="6f919-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="6f919-217">Tıklatın **kullanıcı Merkezi** sekmesini ve ardından **kullanıcı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="6f919-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Azure AD Connect nedir?][300]  

3. <span data-ttu-id="6f919-219">Üzerinde **yeni kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6f919-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Connect nedir?][301]

    <span data-ttu-id="6f919-221">a.</span><span class="sxs-lookup"><span data-stu-id="6f919-221">a.</span></span> <span data-ttu-id="6f919-222">İçinde **ad** metin kutusuna, tür ilk gibi kullanıcı adını **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6f919-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="6f919-223">b.</span><span class="sxs-lookup"><span data-stu-id="6f919-223">b.</span></span> <span data-ttu-id="6f919-224">İçinde **Soyadı** metin kutusuna, türü kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f919-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="6f919-225">c.</span><span class="sxs-lookup"><span data-stu-id="6f919-225">c.</span></span> <span data-ttu-id="6f919-226">İçinde **kullanıcıadı** metin kutusuna, türü **Britta Simon**, Azure portalında olduğu gibi kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="6f919-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="6f919-227">d.</span><span class="sxs-lookup"><span data-stu-id="6f919-227">d.</span></span> <span data-ttu-id="6f919-228">İçinde **parola** metin kutusuna, Britta parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="6f919-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="6f919-229">e.</span><span class="sxs-lookup"><span data-stu-id="6f919-229">e.</span></span> <span data-ttu-id="6f919-230">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f919-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6f919-231">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6f919-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6f919-232">Bu bölümde, Britta halojensiz yazılıma erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f919-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6f919-234">**Britta Simon halojensiz yazılım atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6f919-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="6f919-235">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6f919-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6f919-237">Uygulamalar listesinde **halojensiz yazılım**.</span><span class="sxs-lookup"><span data-stu-id="6f919-237">In the applications list, select **Halogen Software**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="6f919-239">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6f919-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6f919-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f919-241">Click **Add** button.</span></span> <span data-ttu-id="6f919-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f919-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6f919-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6f919-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6f919-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f919-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f919-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6f919-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f919-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6f919-247">Testing single sign-on</span></span>

<span data-ttu-id="6f919-248">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="6f919-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6f919-249">Erişim paneli halojensiz yazılım parçasında tıklattığınızda, otomatik olarak halojensiz yazılım uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="6f919-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f919-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6f919-250">Additional resources</span></span>

* [<span data-ttu-id="6f919-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="6f919-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f919-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6f919-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
