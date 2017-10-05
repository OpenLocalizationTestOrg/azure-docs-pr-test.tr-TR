---
title: "Öğretici: Azure Active Directory Tümleştirme küçük geliştirmelerle | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve küçük geliştirmeler arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 49a8cd3acfc6df15ef6a51171c8421162bc94efc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="cb599-103">Öğretici: Azure Active Directory Tümleştirme küçük geliştirmelerle</span><span class="sxs-lookup"><span data-stu-id="cb599-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="cb599-104">Bu öğreticide, küçük geliştirmeler Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cb599-104">In this tutorial, you learn how to integrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb599-105">Küçük geliştirmeler Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cb599-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb599-106">Küçük geliştirmeleri erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cb599-106">You can control in Azure AD who has access to Small Improvements</span></span>
- <span data-ttu-id="cb599-107">Azure AD hesaplarına otomatik olarak küçük geliştirmeleri (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cb599-107">You can enable your users to automatically get signed-on to Small Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb599-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cb599-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cb599-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb599-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb599-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cb599-110">Prerequisites</span></span>

<span data-ttu-id="cb599-111">Azure AD tümleştirme küçük geliştirmelerle yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="cb599-111">To configure Azure AD integration with Small Improvements, you need the following items:</span></span>

- <span data-ttu-id="cb599-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cb599-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb599-113">Bir küçük geliştirmeleri çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cb599-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb599-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cb599-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb599-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cb599-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb599-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cb599-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb599-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme alabilirsiniz [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb599-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb599-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cb599-118">Scenario description</span></span>
<span data-ttu-id="cb599-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cb599-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb599-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cb599-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb599-121">Galeriden küçük geliştirmeler ekleme</span><span class="sxs-lookup"><span data-stu-id="cb599-121">Adding Small Improvements from the gallery</span></span>
2. <span data-ttu-id="cb599-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cb599-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-the-gallery"></a><span data-ttu-id="cb599-123">Galeriden küçük geliştirmeler ekleme</span><span class="sxs-lookup"><span data-stu-id="cb599-123">Adding Small Improvements from the gallery</span></span>
<span data-ttu-id="cb599-124">Azure AD Küçük geliştirmeleri tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden küçük geliştirmeleri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb599-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb599-125">**Galeriden küçük geliştirmeleri eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cb599-125">**To add Small Improvements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb599-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb599-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cb599-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb599-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cb599-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cb599-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cb599-133">Arama kutusuna **küçük geliştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="cb599-133">In the search box, type **Small Improvements**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="cb599-135">Sonuçlar panelinde seçin **küçük geliştirmeleri**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-135">In the results panel, select **Small Improvements**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb599-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cb599-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb599-138">Bu bölümde, yapılandırmak ve küçük "Britta Simon" adlı bir test kullanıcı doğrultusunda geliştirmeler Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="cb599-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb599-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen küçük geliştirmeleri bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="cb599-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Small Improvements is to a user in Azure AD.</span></span> <span data-ttu-id="cb599-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı küçük geliştirmeleri arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb599-140">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span></span>

<span data-ttu-id="cb599-141">Küçük yenilikleri değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cb599-141">In Small Improvements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb599-142">Yapılandırmak ve Azure AD çoklu oturum açma küçük geliştirmelerle sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cb599-142">To configure and test Azure AD single sign-on with Small Improvements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb599-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cb599-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb599-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="cb599-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb599-145">**[Küçük geliştirmeleri test kullanıcısı oluşturma](#creating-a-small-improvements-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı küçük geliştirmeleri sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="cb599-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb599-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cb599-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb599-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cb599-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb599-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cb599-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb599-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma küçük geliştirmeleri uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cb599-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="cb599-150">**Azure AD çoklu oturum açma küçük geliştirmelerle yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cb599-150">**To configure Azure AD single sign-on with Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="cb599-151">Azure portalında üzerinde **küçük geliştirmeleri** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cb599-151">In the Azure portal, on the **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cb599-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cb599-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="cb599-155">Üzerinde **küçük geliştirmeler etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cb599-155">On the **Small Improvements Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="cb599-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb599-157">a.</span></span> <span data-ttu-id="cb599-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="cb599-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="cb599-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb599-159">b.</span></span> <span data-ttu-id="cb599-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="cb599-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb599-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cb599-161">These values are not real.</span></span> <span data-ttu-id="cb599-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cb599-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cb599-163">Kişi [küçük geliştirmeleri istemci destek ekibi](mailto:support@small-improvements.com) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="cb599-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) to get these values.</span></span> 
 
4. <span data-ttu-id="cb599-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cb599-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="cb599-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb599-168">Üzerinde **küçük geliştirmeleri yapılandırma** 'yi tıklatın **yapılandırma küçük geliştirmeleri** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cb599-168">On the **Small Improvements Configuration** section, click **Configure Small Improvements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cb599-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cb599-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="cb599-171">Başka bir tarayıcı penceresinde küçük geliştirmeleri şirket sitenize yönetici olarak oturum açma.</span><span class="sxs-lookup"><span data-stu-id="cb599-171">In another browser window, sign on to your Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="cb599-172">Ana Panodaki sayfasından tıklatın **Yönetim** sol düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-172">From the main dashboard page, click **Administration** button on the left.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="cb599-174">Tıklatın **SAML SSO** gelen düğmesini **tümleştirmeler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="cb599-174">Click the **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="cb599-176">SSO Kurulumu sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cb599-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="cb599-178">a.</span><span class="sxs-lookup"><span data-stu-id="cb599-178">a.</span></span> <span data-ttu-id="cb599-179">İçinde **HTTP uç noktası** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cb599-179">In the **HTTP Endpoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb599-180">b.</span><span class="sxs-lookup"><span data-stu-id="cb599-180">b.</span></span> <span data-ttu-id="cb599-181">İndirilen sertifikanızı Not Defteri'nde açın, içeriği Kopyala ve ardından yapıştırın **x509 sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="cb599-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="cb599-182">c.</span><span class="sxs-lookup"><span data-stu-id="cb599-182">c.</span></span> <span data-ttu-id="cb599-183">SSO ve oturum açma form kimlik doğrulaması seçeneği kullanıcılar için kullanılabilir olmasını istiyorsanız, ardından denetleyin **oturum açma/parola ile çok erişmesini** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cb599-183">If you wish to have SSO and Login form authentication option available for users, then check the **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="cb599-184">d.</span><span class="sxs-lookup"><span data-stu-id="cb599-184">d.</span></span> <span data-ttu-id="cb599-185">SSO oturum açma düğmesini adlandırmak için uygun değeri girin **SAML komut istemi** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="cb599-185">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="cb599-186">e.</span><span class="sxs-lookup"><span data-stu-id="cb599-186">e.</span></span> <span data-ttu-id="cb599-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb599-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cb599-188">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cb599-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb599-189">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="cb599-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb599-190">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb599-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb599-191">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb599-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb599-192">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="cb599-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cb599-194">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cb599-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb599-195">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb599-197">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cb599-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb599-199">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="cb599-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb599-201">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cb599-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb599-203">a.</span><span class="sxs-lookup"><span data-stu-id="cb599-203">a.</span></span> <span data-ttu-id="cb599-204">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb599-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb599-205">b.</span><span class="sxs-lookup"><span data-stu-id="cb599-205">b.</span></span> <span data-ttu-id="cb599-206">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cb599-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb599-207">c.</span><span class="sxs-lookup"><span data-stu-id="cb599-207">c.</span></span> <span data-ttu-id="cb599-208">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cb599-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb599-209">d.</span><span class="sxs-lookup"><span data-stu-id="cb599-209">d.</span></span> <span data-ttu-id="cb599-210">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cb599-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="cb599-211">Küçük geliştirmeleri test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb599-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="cb599-212">Küçük geliştirmeleri oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar küçük artışlarını sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cb599-212">To enable Azure AD users to log in to Small Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="cb599-213">Küçük geliştirmeleri söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="cb599-213">In the case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="cb599-214">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cb599-214">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cb599-215">Küçük geliştirmeleri şirket sitenize yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="cb599-215">Sign-on to your Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="cb599-216">Giriş sayfasından sol,'ı tıklatın menüsüne gidin **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="cb599-216">From the Home page, go to the menu on the left, click **Administration**.</span></span>

3. <span data-ttu-id="cb599-217">Tıklatın **kullanıcı dizini** kullanıcı yönetimi bölümünden düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-217">Click the **User Directory** button from User Management section.</span></span> 
   
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="cb599-219">Tıklatın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cb599-219">Click **Add users**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="cb599-221">Üzerinde **Kullanıcı Ekle** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cb599-221">On the **Add Users** dialog, perform the following steps:</span></span> 

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="cb599-223">a.</span><span class="sxs-lookup"><span data-stu-id="cb599-223">a.</span></span> <span data-ttu-id="cb599-224">Girin **ad** gibi kullanıcının **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cb599-224">Enter the **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="cb599-225">b.</span><span class="sxs-lookup"><span data-stu-id="cb599-225">b.</span></span> <span data-ttu-id="cb599-226">Girin **Soyadı** gibi kullanıcının **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cb599-226">Enter the **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="cb599-227">c.</span><span class="sxs-lookup"><span data-stu-id="cb599-227">c.</span></span> <span data-ttu-id="cb599-228">Girin **e-posta** gibi kullanıcının  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cb599-228">Enter the **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="cb599-229">d.</span><span class="sxs-lookup"><span data-stu-id="cb599-229">d.</span></span> <span data-ttu-id="cb599-230">Ayrıca kişisel iletisinde girmeyi seçebilirsiniz **bildirim e-posta Gönder** kutusu.</span><span class="sxs-lookup"><span data-stu-id="cb599-230">You can also choose to enter the personal message in the **Send notification email** box.</span></span> <span data-ttu-id="cb599-231">Bildirim göndermek istemiyorsanız bu onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="cb599-231">If you do not wish to send the notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="cb599-232">e.</span><span class="sxs-lookup"><span data-stu-id="cb599-232">e.</span></span> <span data-ttu-id="cb599-233">Tıklatın **kullanıcılar oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cb599-233">Click **Create Users**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb599-234">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cb599-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb599-235">Bu bölümde, Britta küçük geliştirmeleri erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cb599-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Small Improvements.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cb599-237">**Küçük geliştirmeleri Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cb599-237">**To assign Britta Simon to Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="cb599-238">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cb599-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cb599-240">Uygulamalar listesinde **küçük geliştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="cb599-240">In the applications list, select **Small Improvements**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="cb599-242">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cb599-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cb599-244">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cb599-244">Click **Add** button.</span></span> <span data-ttu-id="cb599-245">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cb599-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cb599-247">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cb599-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb599-248">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cb599-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb599-249">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cb599-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb599-250">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cb599-250">Testing single sign-on</span></span>

<span data-ttu-id="cb599-251">Bu bölümün amacı erişim paneli kullanılarak Azure AD SSO yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="cb599-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="cb599-252">Erişim paneli küçük geliştirmeleri parçasında tıklattığınızda, otomatik olarak küçük geliştirmeleri uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="cb599-252">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb599-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cb599-253">Additional resources</span></span>

* [<span data-ttu-id="cb599-254">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="cb599-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb599-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cb599-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

