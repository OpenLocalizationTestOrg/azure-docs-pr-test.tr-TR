---
title: "Öğretici: Azure Active Directory Tümleştirme ile LockPath Keylight | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile LockPath Keylight arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="cff64-103">Öğretici: Azure Active Directory Tümleştirme LockPath Keylight ile</span><span class="sxs-lookup"><span data-stu-id="cff64-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="cff64-104">Bu öğreticide, Azure Active Directory (Azure AD) ile LockPath Keylight tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cff64-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cff64-105">LockPath Keylight Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cff64-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cff64-106">LockPath Keylight erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cff64-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="cff64-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için LockPath Keylight açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cff64-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cff64-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cff64-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cff64-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cff64-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cff64-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cff64-110">Prerequisites</span></span>

<span data-ttu-id="cff64-111">Azure AD tümleştirme LockPath Keylight ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="cff64-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="cff64-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cff64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cff64-113">Bir LockPath Keylight çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="cff64-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cff64-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cff64-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cff64-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cff64-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cff64-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cff64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cff64-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cff64-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cff64-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cff64-118">Scenario description</span></span>
<span data-ttu-id="cff64-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cff64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cff64-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cff64-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cff64-121">Galeriden LockPath Keylight ekleme</span><span class="sxs-lookup"><span data-stu-id="cff64-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="cff64-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cff64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="cff64-123">Galeriden LockPath Keylight ekleme</span><span class="sxs-lookup"><span data-stu-id="cff64-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="cff64-124">Azure AD LockPath Keylight tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden LockPath Keylight eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cff64-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cff64-125">**Galeriden LockPath Keylight eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cff64-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cff64-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cff64-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cff64-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cff64-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cff64-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cff64-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cff64-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cff64-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cff64-133">Arama kutusuna **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="cff64-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="cff64-135">Sonuçlar panelinde seçin **LockPath Keylight**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cff64-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cff64-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cff64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cff64-138">Bu bölümde, yapılandırmanız ve LockPath Keylight ile Azure AD çoklu oturum açmayı test "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı</span><span class="sxs-lookup"><span data-stu-id="cff64-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cff64-139">Tekli çalışmaya oturum için Azure AD LockPath Keylight karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="cff64-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="cff64-140">Diğer bir deyişle, bir Azure AD kullanıcısının LockPath Keylight ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cff64-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="cff64-141">LockPath Keylight içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cff64-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cff64-142">Yapılandırma ve Azure AD çoklu oturum açma LockPath Keylight ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cff64-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cff64-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cff64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cff64-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="cff64-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cff64-145">**[LockPath Keylight test kullanıcısı oluşturma](#creating-a-lockpath-keylight-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı LockPath Keylight sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="cff64-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cff64-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cff64-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cff64-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cff64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cff64-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cff64-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cff64-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma LockPath Keylight uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cff64-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="cff64-150">**Azure AD çoklu oturum açma LockPath Keylight ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cff64-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="cff64-151">Azure portalında üzerinde **LockPath Keylight** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cff64-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cff64-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cff64-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="cff64-155">Üzerinde **LockPath Keylight etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cff64-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="cff64-157">a.</span><span class="sxs-lookup"><span data-stu-id="cff64-157">a.</span></span> <span data-ttu-id="cff64-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="cff64-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="cff64-159">b.</span><span class="sxs-lookup"><span data-stu-id="cff64-159">b.</span></span> <span data-ttu-id="cff64-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="cff64-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="cff64-161">c.</span><span class="sxs-lookup"><span data-stu-id="cff64-161">c.</span></span> <span data-ttu-id="cff64-162">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="cff64-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="cff64-163">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cff64-163">These values are not real.</span></span> <span data-ttu-id="cff64-164">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cff64-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="cff64-165">Kişi [LockPath Keylight istemci destek ekibi](https://www.lockpath.com/contact/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="cff64-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="cff64-166">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Raw)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cff64-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="cff64-168">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cff64-168">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="cff64-170">Üzerinde **LockPath Keylight yapılandırma** 'yi tıklatın **yapılandırma LockPath Keylight** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cff64-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cff64-171">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cff64-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="cff64-173">LockPath Keylight SSO'yu etkinleştirmek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cff64-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="cff64-174">a.</span><span class="sxs-lookup"><span data-stu-id="cff64-174">a.</span></span> <span data-ttu-id="cff64-175">LockPath Keylight hesabınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="cff64-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="cff64-176">b.</span><span class="sxs-lookup"><span data-stu-id="cff64-176">b.</span></span> <span data-ttu-id="cff64-177">Üstteki menüde tıklatın **kişi**seçip **Keylight Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="cff64-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="cff64-179">c.</span><span class="sxs-lookup"><span data-stu-id="cff64-179">c.</span></span> <span data-ttu-id="cff64-180">Sol taraftaki treeview içinde tıklatın **SAML**.</span><span class="sxs-lookup"><span data-stu-id="cff64-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="cff64-182">d.</span><span class="sxs-lookup"><span data-stu-id="cff64-182">d.</span></span> <span data-ttu-id="cff64-183">Üzerinde **SAML ayarları** iletişim kutusunda, tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="cff64-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="cff64-185">Üzerinde **SAML ayarlarını Düzenle** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cff64-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="cff64-187">a.</span><span class="sxs-lookup"><span data-stu-id="cff64-187">a.</span></span> <span data-ttu-id="cff64-188">Ayarlama **SAML kimlik doğrulaması** için **etkin**.</span><span class="sxs-lookup"><span data-stu-id="cff64-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="cff64-189">b.</span><span class="sxs-lookup"><span data-stu-id="cff64-189">b.</span></span> <span data-ttu-id="cff64-190">Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyaladığınız değeri **kimlik sağlayıcısı oturum açma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="cff64-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="cff64-191">c.</span><span class="sxs-lookup"><span data-stu-id="cff64-191">c.</span></span> <span data-ttu-id="cff64-192">Yapıştır **tek Sign-Out hizmeti URL'si** Azure portalından kopyaladığınız değeri **kimlik sağlayıcısı oturum kapatma URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="cff64-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="cff64-193">d.</span><span class="sxs-lookup"><span data-stu-id="cff64-193">d.</span></span> <span data-ttu-id="cff64-194">Tıklatın **Dosya Seç** indirilen LockPath Keylight sertifikanızı seçin ve ardından **açık** sertifikayı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="cff64-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="cff64-195">e.</span><span class="sxs-lookup"><span data-stu-id="cff64-195">e.</span></span> <span data-ttu-id="cff64-196">Ayarlama **SAML kullanıcı kimliği konumu** için **NameIdentifier öğesi konu deyiminin**.</span><span class="sxs-lookup"><span data-stu-id="cff64-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="cff64-197">f.</span><span class="sxs-lookup"><span data-stu-id="cff64-197">f.</span></span> <span data-ttu-id="cff64-198">Sağlamak **Keylight hizmet sağlayıcısı** şu biçimi kullanarak: **https://&lt;ŞirketAdı&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="cff64-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="cff64-199">g.</span><span class="sxs-lookup"><span data-stu-id="cff64-199">g.</span></span> <span data-ttu-id="cff64-200">Ayarlama **otomatik sağlama kullanıcılar** için **etkin**.</span><span class="sxs-lookup"><span data-stu-id="cff64-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="cff64-201">h.</span><span class="sxs-lookup"><span data-stu-id="cff64-201">h.</span></span> <span data-ttu-id="cff64-202">Ayarlama **otomatik sağlama hesap türü** için **tam kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="cff64-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="cff64-203">ı.</span><span class="sxs-lookup"><span data-stu-id="cff64-203">i.</span></span> <span data-ttu-id="cff64-204">Ayarlama **otomatik sağlama güvenlik rolü**seçin **SAML sahip standart kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="cff64-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="cff64-205">j.</span><span class="sxs-lookup"><span data-stu-id="cff64-205">j.</span></span> <span data-ttu-id="cff64-206">Ayarlama **otomatik sağlama güvenlik config**seçin **standart kullanıcı yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="cff64-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="cff64-207">k.</span><span class="sxs-lookup"><span data-stu-id="cff64-207">k.</span></span> <span data-ttu-id="cff64-208">İçinde **e-posta özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="cff64-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="cff64-209">l.</span><span class="sxs-lookup"><span data-stu-id="cff64-209">l.</span></span> <span data-ttu-id="cff64-210">İçinde **ad özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="cff64-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="cff64-211">m.</span><span class="sxs-lookup"><span data-stu-id="cff64-211">m.</span></span> <span data-ttu-id="cff64-212">İçinde **son name özniteliği** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="cff64-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="cff64-213">n.</span><span class="sxs-lookup"><span data-stu-id="cff64-213">n.</span></span> <span data-ttu-id="cff64-214">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cff64-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cff64-215">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cff64-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cff64-216">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="cff64-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cff64-217">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cff64-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cff64-218">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cff64-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="cff64-219">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="cff64-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cff64-221">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cff64-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cff64-222">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cff64-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cff64-224">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cff64-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cff64-226">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="cff64-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cff64-228">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cff64-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cff64-230">a.</span><span class="sxs-lookup"><span data-stu-id="cff64-230">a.</span></span> <span data-ttu-id="cff64-231">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cff64-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cff64-232">b.</span><span class="sxs-lookup"><span data-stu-id="cff64-232">b.</span></span> <span data-ttu-id="cff64-233">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cff64-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cff64-234">c.</span><span class="sxs-lookup"><span data-stu-id="cff64-234">c.</span></span> <span data-ttu-id="cff64-235">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cff64-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cff64-236">d.</span><span class="sxs-lookup"><span data-stu-id="cff64-236">d.</span></span> <span data-ttu-id="cff64-237">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cff64-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="cff64-238">LockPath Keylight test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cff64-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="cff64-239">Bu bölümde, Britta Simon LockPath Keylight adlı bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cff64-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="cff64-240">LockPath Keylight tam zamanı sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="cff64-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="cff64-241">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="cff64-241">There is no action item for you in this section.</span></span> <span data-ttu-id="cff64-242">Yeni bir kullanıcı, kullanıcı henüz yoksa LockPath Keylight erişirken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cff64-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="cff64-243">Bir kullanıcı el ile oluşturmanız gerekiyorsa, başvurmanız gerekir [LockPath Keylight istemci destek ekibi](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cff64-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cff64-244">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cff64-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cff64-245">Bu bölümde, Britta LockPath Keylight erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cff64-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cff64-247">**LockPath Keylight Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cff64-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="cff64-248">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cff64-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cff64-250">Uygulamalar listesinde **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="cff64-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="cff64-252">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cff64-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cff64-254">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cff64-254">Click **Add** button.</span></span> <span data-ttu-id="cff64-255">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cff64-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cff64-257">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cff64-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cff64-258">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cff64-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cff64-259">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cff64-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cff64-260">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cff64-260">Testing single sign-on</span></span>

<span data-ttu-id="cff64-261">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="cff64-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cff64-262">Erişim paneli LockPath Keylight parçasında tıklattığınızda, otomatik olarak LockPath Keylight uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="cff64-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cff64-263">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cff64-263">Additional resources</span></span>

* [<span data-ttu-id="cff64-264">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="cff64-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cff64-265">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cff64-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

