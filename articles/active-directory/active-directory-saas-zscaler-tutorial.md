---
title: "Öğretici: Azure Active Directory Tümleştirme ile Zscaler | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Zscaler arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="2ee79-103">Öğretici: Azure Active Directory Tümleştirme Zscaler ile</span><span class="sxs-lookup"><span data-stu-id="2ee79-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="2ee79-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Zscaler tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2ee79-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ee79-105">Zscaler Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="2ee79-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2ee79-106">Zscaler erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2ee79-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="2ee79-107">Otomatik olarak için Zscaler (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2ee79-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ee79-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="2ee79-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2ee79-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ee79-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ee79-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ee79-110">Prerequisites</span></span>

<span data-ttu-id="2ee79-111">Azure AD tümleştirme Zscaler ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ee79-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="2ee79-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="2ee79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ee79-113">Bir Zscaler çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="2ee79-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ee79-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2ee79-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ee79-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ee79-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ee79-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ee79-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ee79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ee79-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="2ee79-118">Scenario description</span></span>
<span data-ttu-id="2ee79-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="2ee79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ee79-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2ee79-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ee79-121">Galeriden Zscaler ekleme</span><span class="sxs-lookup"><span data-stu-id="2ee79-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="2ee79-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2ee79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="2ee79-123">Galeriden Zscaler ekleme</span><span class="sxs-lookup"><span data-stu-id="2ee79-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="2ee79-124">Azure AD Zscaler tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Zscaler eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee79-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2ee79-125">**Galeriden Zscaler eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee79-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee79-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ee79-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2ee79-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="2ee79-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="2ee79-133">Arama kutusuna **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-133">In the search box, type **Zscaler**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="2ee79-135">Sonuçlar panelinde seçin **Zscaler**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ee79-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="2ee79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ee79-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Zscaler sınayın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ee79-139">Tekli çalışmaya oturum için Azure AD Zscaler karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="2ee79-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="2ee79-140">Diğer bir deyişle, bir Azure AD kullanıcısının Zscaler ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee79-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="2ee79-141">Zscaler içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2ee79-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2ee79-142">Yapılandırma ve Azure AD çoklu oturum açma Zscaler ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ee79-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2ee79-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2ee79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2ee79-144">**[Proxy ayarlarını yapılandırma](#configuring-proxy-settings)**  - Internet Explorer proxy ayarlarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="2ee79-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="2ee79-145">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="2ee79-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2ee79-146">**[Zscaler test kullanıcısı oluşturma](#creating-a-zscaler-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Zscaler sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="2ee79-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="2ee79-147">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2ee79-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="2ee79-148">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ee79-149">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2ee79-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ee79-150">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Zscaler uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="2ee79-151">**Azure AD çoklu oturum açma ile Zscaler yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee79-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee79-152">Azure portalında üzerinde **Zscaler** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="2ee79-154">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2ee79-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="2ee79-156">Üzerinde **Zscaler etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="2ee79-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="2ee79-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ee79-159">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="2ee79-159">This value is not real.</span></span> <span data-ttu-id="2ee79-160">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ee79-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2ee79-161">Kişi [Zscaler istemci destek ekibi](https://www.zscaler.com/company/contact) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="2ee79-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="2ee79-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2ee79-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="2ee79-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-164">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2ee79-166">Üzerinde **Zscaler yapılandırma** 'yi tıklatın **yapılandırma Zscaler** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2ee79-167">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="2ee79-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="2ee79-169">Farklı web tarayıcısı penceresinde ZScaler şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="2ee79-170">Üstteki menüde tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="2ee79-171">![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="2ee79-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="2ee79-172">Altında **yönetmesine & rolleri**, tıklatın **kullanıcıları yönetme & kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="2ee79-173">![Kullanıcıların & kimlik doğrulaması Yönet](./media/active-directory-saas-zscaler-tutorial/ic800207.png "kullanıcılar & kimlik doğrulaması Yönet")</span><span class="sxs-lookup"><span data-stu-id="2ee79-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="2ee79-174">İçinde **, kuruluşunuz için kimlik doğrulama seçeneklerini seçin** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="2ee79-175">![Kimlik doğrulama](./media/active-directory-saas-zscaler-tutorial/ic800208.png "kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="2ee79-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="2ee79-176">a.</span><span class="sxs-lookup"><span data-stu-id="2ee79-176">a.</span></span> <span data-ttu-id="2ee79-177">Seçin **SAML çoklu oturum açma kullanarak kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="2ee79-178">b.</span><span class="sxs-lookup"><span data-stu-id="2ee79-178">b.</span></span> <span data-ttu-id="2ee79-179">Tıklatın **SAML çoklu oturum açma parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="2ee79-180">Üzerinde **yapılandırma SAML çoklu oturum açma parametreleri** iletişim sayfasında, aşağıdaki adımları uygulayın ve ardından **bitti**</span><span class="sxs-lookup"><span data-stu-id="2ee79-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="2ee79-181">![Çoklu oturum açma](./media/active-directory-saas-zscaler-tutorial/ic800209.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="2ee79-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="2ee79-182">a.</span><span class="sxs-lookup"><span data-stu-id="2ee79-182">a.</span></span> <span data-ttu-id="2ee79-183">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **için kullanıcıların kimlik doğrulaması için gönderilir SAML portalın URL'sini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2ee79-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="2ee79-184">b.</span><span class="sxs-lookup"><span data-stu-id="2ee79-184">b.</span></span> <span data-ttu-id="2ee79-185">İçinde **özniteliği oturum açma adını içeren** metin kutusuna, türü **NameID**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="2ee79-186">c.</span><span class="sxs-lookup"><span data-stu-id="2ee79-186">c.</span></span> <span data-ttu-id="2ee79-187">İndirilen sertifikanızı karşıya yüklemek için tıklayın **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="2ee79-188">d.</span><span class="sxs-lookup"><span data-stu-id="2ee79-188">d.</span></span> <span data-ttu-id="2ee79-189">Seçin **SAML otomatik sağlamayı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="2ee79-190">Üzerinde **kullanıcı kimlik doğrulaması yapılandırma** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="2ee79-191">![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="2ee79-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="2ee79-192">a.</span><span class="sxs-lookup"><span data-stu-id="2ee79-192">a.</span></span> <span data-ttu-id="2ee79-193">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-193">Click **Save**.</span></span>

    <span data-ttu-id="2ee79-194">b.</span><span class="sxs-lookup"><span data-stu-id="2ee79-194">b.</span></span> <span data-ttu-id="2ee79-195">Tıklatın **şimdi etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="2ee79-196">Proxy ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2ee79-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="2ee79-197">Internet Explorer proxy ayarlarını yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="2ee79-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="2ee79-198">Başlat **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="2ee79-199">Seçin **Internet Seçenekleri** gelen **Araçları** açılan menü **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="2ee79-200">![Internet Seçenekleri](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Seçenekleri")</span><span class="sxs-lookup"><span data-stu-id="2ee79-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="2ee79-201">Tıklatın **bağlantıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="2ee79-202">![Bağlantıları](./media/active-directory-saas-zscaler-tutorial/ic769493.png "bağlantıları")</span><span class="sxs-lookup"><span data-stu-id="2ee79-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="2ee79-203">Tıklatın **LAN Ayarları** açmak için **LAN Ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="2ee79-204">Proxy sunucu bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="2ee79-205">![Proxy sunucusu](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy sunucusu")</span><span class="sxs-lookup"><span data-stu-id="2ee79-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="2ee79-206">a.</span><span class="sxs-lookup"><span data-stu-id="2ee79-206">a.</span></span> <span data-ttu-id="2ee79-207">Seçin **AĞINIZ için bir proxy sunucusu kullan**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="2ee79-208">b.</span><span class="sxs-lookup"><span data-stu-id="2ee79-208">b.</span></span> <span data-ttu-id="2ee79-209">Adresi metin kutusuna yazın **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="2ee79-210">c.</span><span class="sxs-lookup"><span data-stu-id="2ee79-210">c.</span></span> <span data-ttu-id="2ee79-211">Bağlantı noktası metin kutusuna yazın **80**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="2ee79-212">d.</span><span class="sxs-lookup"><span data-stu-id="2ee79-212">d.</span></span> <span data-ttu-id="2ee79-213">Seçin **yerel adresler için proxy sunucuyu atla**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="2ee79-214">e.</span><span class="sxs-lookup"><span data-stu-id="2ee79-214">e.</span></span> <span data-ttu-id="2ee79-215">Tıklatın **Tamam** kapatmak için **yerel ağ (LAN) ayarları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="2ee79-216">Tıklatın **Tamam** kapatmak için **Internet Seçenekleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="2ee79-217">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="2ee79-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2ee79-218">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="2ee79-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2ee79-219">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ee79-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ee79-220">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee79-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ee79-221">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="2ee79-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="2ee79-223">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee79-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee79-224">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ee79-226">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ee79-228">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="2ee79-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ee79-230">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ee79-232">a.</span><span class="sxs-lookup"><span data-stu-id="2ee79-232">a.</span></span> <span data-ttu-id="2ee79-233">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ee79-234">b.</span><span class="sxs-lookup"><span data-stu-id="2ee79-234">b.</span></span> <span data-ttu-id="2ee79-235">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="2ee79-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ee79-236">c.</span><span class="sxs-lookup"><span data-stu-id="2ee79-236">c.</span></span> <span data-ttu-id="2ee79-237">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2ee79-238">d.</span><span class="sxs-lookup"><span data-stu-id="2ee79-238">d.</span></span> <span data-ttu-id="2ee79-239">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="2ee79-240">Zscaler test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee79-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="2ee79-241">Azure AD kullanıcıları için ZScaler oturum açmak etkinleştirmek için bunlar için ZScaler sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2ee79-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="2ee79-242">ZScaler söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="2ee79-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="2ee79-243">Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="2ee79-244">Oturum, **Zscaler** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="2ee79-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="2ee79-245">Tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="2ee79-246">![Yönetim](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="2ee79-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="2ee79-247">Tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="2ee79-248">![Ekleme](./media/active-directory-saas-zscaler-tutorial/ic781036.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="2ee79-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="2ee79-249">İçinde **kullanıcılar** sekmesini tıklatın, **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="2ee79-250">![Ekleme](./media/active-directory-saas-zscaler-tutorial/ic781037.png "ekleme")</span><span class="sxs-lookup"><span data-stu-id="2ee79-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="2ee79-251">Kullanıcı Ekle bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2ee79-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="2ee79-252">![Kullanıcı ekleme](./media/active-directory-saas-zscaler-tutorial/ic781038.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="2ee79-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="2ee79-253">a.</span><span class="sxs-lookup"><span data-stu-id="2ee79-253">a.</span></span> <span data-ttu-id="2ee79-254">Tür **UserID**, **kullanıcı görünen adı**, **parola**, **parolayı onayla**ve ardından **grupları** ve **departmanı** sağlamak istediğiniz geçerli bir AAD hesabının.</span><span class="sxs-lookup"><span data-stu-id="2ee79-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="2ee79-255">b.</span><span class="sxs-lookup"><span data-stu-id="2ee79-255">b.</span></span> <span data-ttu-id="2ee79-256">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ee79-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="2ee79-257">API sağlama AAD kullanıcı hesaplarına ZScaler tarafından sağlanan veya herhangi diğer ZScaler kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ee79-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2ee79-258">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="2ee79-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2ee79-259">Bu bölümde, Britta Zscaler için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ee79-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="2ee79-261">**Zscaler için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2ee79-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="2ee79-262">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="2ee79-264">Uygulamalar listesinde **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-264">In the applications list, select **Zscaler**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="2ee79-266">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="2ee79-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="2ee79-268">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2ee79-268">Click **Add** button.</span></span> <span data-ttu-id="2ee79-269">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="2ee79-271">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="2ee79-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2ee79-272">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ee79-273">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2ee79-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ee79-274">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="2ee79-274">Testing single sign-on</span></span>

<span data-ttu-id="2ee79-275">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="2ee79-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2ee79-276">Erişim paneli Zscaler parçasında tıklattığınızda, otomatik olarak Zscaler uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="2ee79-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="2ee79-277">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ee79-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2ee79-278">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2ee79-278">Additional resources</span></span>

* [<span data-ttu-id="2ee79-279">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="2ee79-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ee79-280">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="2ee79-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

