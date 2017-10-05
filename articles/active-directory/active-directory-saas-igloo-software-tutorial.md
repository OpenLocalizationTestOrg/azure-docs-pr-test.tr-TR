---
title: "Öğretici: Azure Active Directory Tümleştirme Igloo yazılımıyla | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Igloo yazılımı arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="41c72-103">Öğretici: Azure Active Directory Tümleştirme Igloo yazılımıyla</span><span class="sxs-lookup"><span data-stu-id="41c72-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="41c72-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Igloo yazılım tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41c72-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41c72-105">Igloo yazılım Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="41c72-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41c72-106">Igloo yazılım erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="41c72-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="41c72-107">Azure AD hesaplarına otomatik olarak Igloo yazılımı (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="41c72-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41c72-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="41c72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="41c72-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41c72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41c72-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41c72-110">Prerequisites</span></span>

<span data-ttu-id="41c72-111">Azure AD tümleştirme Igloo yazılımıyla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="41c72-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="41c72-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="41c72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41c72-113">Bir Igloo yazılım çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="41c72-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41c72-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="41c72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41c72-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="41c72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41c72-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="41c72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41c72-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41c72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41c72-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="41c72-118">Scenario description</span></span>
<span data-ttu-id="41c72-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="41c72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41c72-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="41c72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41c72-121">Galeriden Igloo yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="41c72-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="41c72-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="41c72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="41c72-123">Galeriden Igloo yazılım ekleme</span><span class="sxs-lookup"><span data-stu-id="41c72-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="41c72-124">Azure AD Igloo yazılım tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Igloo yazılım eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="41c72-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41c72-125">**Galeriden Igloo yazılım eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41c72-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41c72-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="41c72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41c72-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="41c72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41c72-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="41c72-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="41c72-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41c72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="41c72-133">Arama kutusuna **Igloo yazılım**.</span><span class="sxs-lookup"><span data-stu-id="41c72-133">In the search box, type **Igloo Software**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="41c72-135">Sonuçlar panelinde seçin **Igloo yazılım**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41c72-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41c72-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="41c72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41c72-138">Bu bölümde, yapılandırmak ve Igloo yazılım "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="41c72-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41c72-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Igloo yazılım bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="41c72-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="41c72-140">Diğer bir deyişle, bir Azure AD kullanıcısının Igloo yazılım ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="41c72-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="41c72-141">Değeri Igloo yazılımda atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="41c72-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="41c72-142">Yapılandırmak ve Azure AD çoklu oturum açma Igloo yazılımıyla sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="41c72-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41c72-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41c72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41c72-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="41c72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41c72-145">**[Bir Igloo yazılım test kullanıcısı oluşturma](#creating-an-igloo-software-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Igloo yazılım sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="41c72-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41c72-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41c72-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41c72-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="41c72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41c72-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41c72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41c72-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Igloo yazılım uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41c72-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="41c72-150">**Azure AD çoklu oturum açma Igloo yazılımıyla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41c72-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="41c72-151">Azure portalında üzerinde **Igloo yazılım** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="41c72-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="41c72-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41c72-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="41c72-155">Üzerinde **Igloo yazılım etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41c72-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="41c72-157">a.</span><span class="sxs-lookup"><span data-stu-id="41c72-157">a.</span></span> <span data-ttu-id="41c72-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="41c72-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="41c72-159">b.</span><span class="sxs-lookup"><span data-stu-id="41c72-159">b.</span></span> <span data-ttu-id="41c72-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="41c72-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="41c72-161">c.</span><span class="sxs-lookup"><span data-stu-id="41c72-161">c.</span></span> <span data-ttu-id="41c72-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="41c72-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41c72-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="41c72-163">These values are not real.</span></span> <span data-ttu-id="41c72-164">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="41c72-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="41c72-165">Kişi [Igloo yazılım istemci destek ekibi](https://www.igloosoftware.com/services/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="41c72-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="41c72-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="41c72-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="41c72-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41c72-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="41c72-170">Üzerinde **Igloo yazılım yapılandırma** 'yi tıklatın **Igloo yazılımı Yapılandır** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="41c72-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="41c72-171">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="41c72-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="41c72-173">Farklı web tarayıcısı penceresinde Igloo yazılım şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="41c72-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="41c72-174">Git **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="41c72-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="41c72-175">![Denetim Masası](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Denetim Masası")</span><span class="sxs-lookup"><span data-stu-id="41c72-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="41c72-176">İçinde **üyelik** sekmesini tıklatın, **ayarları oturum**.</span><span class="sxs-lookup"><span data-stu-id="41c72-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="41c72-177">![Ayarları'nda oturum](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Ayarları'nda oturum açın")</span><span class="sxs-lookup"><span data-stu-id="41c72-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="41c72-178">SAML yapılandırma bölümünde tıklatın **SAML kimlik doğrulaması yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="41c72-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="41c72-179">![SAML Yapılandırması](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="41c72-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="41c72-180">İçinde **genel yapılandırma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41c72-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="41c72-181">![Genel yapılandırma](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "genel yapılandırma")</span><span class="sxs-lookup"><span data-stu-id="41c72-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="41c72-182">a.</span><span class="sxs-lookup"><span data-stu-id="41c72-182">a.</span></span> <span data-ttu-id="41c72-183">İçinde **bağlantı adı** metin kutusuna, yapılandırmanız için özel bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="41c72-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="41c72-184">b.</span><span class="sxs-lookup"><span data-stu-id="41c72-184">b.</span></span> <span data-ttu-id="41c72-185">İçinde **IDP oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="41c72-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="41c72-186">c.</span><span class="sxs-lookup"><span data-stu-id="41c72-186">c.</span></span> <span data-ttu-id="41c72-187">İçinde **IDP oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="41c72-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="41c72-188">d.</span><span class="sxs-lookup"><span data-stu-id="41c72-188">d.</span></span> <span data-ttu-id="41c72-189">Seçin **oturum kapatma yanıt ve İstek HTTP türü** olarak **POST**.</span><span class="sxs-lookup"><span data-stu-id="41c72-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="41c72-190">e.</span><span class="sxs-lookup"><span data-stu-id="41c72-190">e.</span></span> <span data-ttu-id="41c72-191">Açık, **base-64** Not Defteri'nde kodlanmış sertifika Azure Portalı'ndan indirilen, içeriğini, panoya kopyalayın ve yapıştırın kendisine **ortak sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="41c72-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="41c72-192">İçinde **yanıt ve kimlik doğrulama Yapılandırması**, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41c72-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="41c72-193">![Yanıt ve kimlik doğrulama Yapılandırması](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "yanıt ve kimlik doğrulama yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="41c72-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="41c72-194">a.</span><span class="sxs-lookup"><span data-stu-id="41c72-194">a.</span></span> <span data-ttu-id="41c72-195">Olarak **kimlik sağlayıcısı**seçin **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="41c72-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="41c72-196">b.</span><span class="sxs-lookup"><span data-stu-id="41c72-196">b.</span></span> <span data-ttu-id="41c72-197">Olarak **tanımlayıcı türü**seçin **e-posta adresi**.</span><span class="sxs-lookup"><span data-stu-id="41c72-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="41c72-198">c.</span><span class="sxs-lookup"><span data-stu-id="41c72-198">c.</span></span> <span data-ttu-id="41c72-199">İçinde **e-posta özniteliği** metin kutusuna, türü **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="41c72-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="41c72-200">d.</span><span class="sxs-lookup"><span data-stu-id="41c72-200">d.</span></span> <span data-ttu-id="41c72-201">İçinde **ad özniteliği** metin kutusuna, türü **givenname**.</span><span class="sxs-lookup"><span data-stu-id="41c72-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="41c72-202">e.</span><span class="sxs-lookup"><span data-stu-id="41c72-202">e.</span></span> <span data-ttu-id="41c72-203">İçinde **son Name özniteliği** metin kutusuna, türü **Soyadı**.</span><span class="sxs-lookup"><span data-stu-id="41c72-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="41c72-204">Yapılandırmayı tamamlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41c72-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="41c72-205">![Oturum açma kullanıcı oluşturma](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "oturum açma kullanıcı oluşturma")</span><span class="sxs-lookup"><span data-stu-id="41c72-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="41c72-206">a.</span><span class="sxs-lookup"><span data-stu-id="41c72-206">a.</span></span> <span data-ttu-id="41c72-207">Olarak **oturum açma kullanıcı oluşturma**seçin **yeni bir kullanıcı oturum sitenizdeki oluşturduğunuzda**.</span><span class="sxs-lookup"><span data-stu-id="41c72-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="41c72-208">b.</span><span class="sxs-lookup"><span data-stu-id="41c72-208">b.</span></span> <span data-ttu-id="41c72-209">Olarak **ayarlarında oturum**seçin **"Oturum" ekranında kullanım SAML düğmesini**.</span><span class="sxs-lookup"><span data-stu-id="41c72-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="41c72-210">c.</span><span class="sxs-lookup"><span data-stu-id="41c72-210">c.</span></span> <span data-ttu-id="41c72-211">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41c72-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="41c72-212">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="41c72-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41c72-213">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="41c72-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41c72-214">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41c72-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41c72-215">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41c72-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="41c72-216">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="41c72-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="41c72-218">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41c72-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41c72-219">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="41c72-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41c72-221">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="41c72-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41c72-223">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="41c72-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41c72-225">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="41c72-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41c72-227">a.</span><span class="sxs-lookup"><span data-stu-id="41c72-227">a.</span></span> <span data-ttu-id="41c72-228">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41c72-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41c72-229">b.</span><span class="sxs-lookup"><span data-stu-id="41c72-229">b.</span></span> <span data-ttu-id="41c72-230">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="41c72-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41c72-231">c.</span><span class="sxs-lookup"><span data-stu-id="41c72-231">c.</span></span> <span data-ttu-id="41c72-232">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="41c72-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="41c72-233">d.</span><span class="sxs-lookup"><span data-stu-id="41c72-233">d.</span></span> <span data-ttu-id="41c72-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41c72-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="41c72-235">Bir Igloo yazılım test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41c72-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="41c72-236">Kullanıcı için Igloo yazılım sağlama yapılandırmanız için eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="41c72-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="41c72-237">Atanmış bir kullanıcı Igloo erişim paneli kullanarak yazılım için oturum açma girişiminde bulunduğunda, Igloo yazılım kullanıcının var olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="41c72-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="41c72-238">Hiçbir kullanıcı hesabı varsa kullanılabilir henüz, Igloo yazılım tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="41c72-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="41c72-239">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="41c72-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="41c72-240">Bu bölümde, Britta Igloo yazılıma erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="41c72-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="41c72-242">**Britta Simon Igloo yazılım atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="41c72-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="41c72-243">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="41c72-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="41c72-245">Uygulamalar listesinde **Igloo yazılım**.</span><span class="sxs-lookup"><span data-stu-id="41c72-245">In the applications list, select **Igloo Software**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="41c72-247">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="41c72-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="41c72-249">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41c72-249">Click **Add** button.</span></span> <span data-ttu-id="41c72-250">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="41c72-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="41c72-252">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="41c72-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41c72-253">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="41c72-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41c72-254">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="41c72-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41c72-255">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="41c72-255">Testing single sign-on</span></span>

<span data-ttu-id="41c72-256">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="41c72-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="41c72-257">Erişim paneli Igloo yazılım parçasında tıklattığınızda, otomatik olarak Igloo yazılım uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="41c72-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="41c72-258">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="41c72-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="41c72-259">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="41c72-259">Additional resources</span></span>

* [<span data-ttu-id="41c72-260">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="41c72-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41c72-261">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="41c72-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

