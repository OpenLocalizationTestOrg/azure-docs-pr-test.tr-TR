---
title: "Öğretici: Azure Active Directory Tümleştirme tanı ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve tanı arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="c66f5-103">Öğretici: Tanı Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="c66f5-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="c66f5-104">Bu öğreticide, Azure Active Directory (Azure AD) ile tanı tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c66f5-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c66f5-105">Tanı Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="c66f5-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c66f5-106">Tanı erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c66f5-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="c66f5-107">Otomatik olarak için tanı (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c66f5-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c66f5-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="c66f5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c66f5-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c66f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c66f5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c66f5-110">Prerequisites</span></span>

<span data-ttu-id="c66f5-111">Azure AD tümleştirme tanı ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="c66f5-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="c66f5-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="c66f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c66f5-113">Bir tanı çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="c66f5-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c66f5-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c66f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c66f5-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c66f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c66f5-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c66f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c66f5-117">Bir Azure AD deneme ortam yoksa, burada bir aylık deneme elde edebilirsiniz: [deneme teklifi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c66f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c66f5-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="c66f5-118">Scenario description</span></span>
<span data-ttu-id="c66f5-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="c66f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c66f5-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="c66f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c66f5-121">Galeriden tanı ekleme</span><span class="sxs-lookup"><span data-stu-id="c66f5-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="c66f5-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c66f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="c66f5-123">Galeriden tanı ekleme</span><span class="sxs-lookup"><span data-stu-id="c66f5-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="c66f5-124">Azure AD tanı tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden tanı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c66f5-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c66f5-125">**Tanı Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c66f5-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c66f5-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c66f5-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c66f5-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="c66f5-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="c66f5-133">Arama kutusuna **tanı**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-133">In the search box, type **Recognize**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="c66f5-135">Sonuçlar panelinde seçin **tanı**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c66f5-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="c66f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c66f5-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı tanı sınayın.</span><span class="sxs-lookup"><span data-stu-id="c66f5-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c66f5-139">Tekli çalışmaya oturum için Azure AD tanı karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="c66f5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="c66f5-140">Diğer bir deyişle, bir Azure AD kullanıcısının tanı ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c66f5-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="c66f5-141">Tanı içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c66f5-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c66f5-142">Yapılandırma ve Azure AD çoklu oturum açma tanı ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c66f5-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c66f5-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c66f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c66f5-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="c66f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c66f5-145">**[Tanı test kullanıcısı oluşturma](#creating-a-recognize-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı tanı sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c66f5-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c66f5-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c66f5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c66f5-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c66f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c66f5-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c66f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c66f5-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma tanı uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c66f5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="c66f5-150">**Azure AD çoklu oturum açma ile tanı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c66f5-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="c66f5-151">Azure portalında üzerinde **tanı** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="c66f5-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c66f5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="c66f5-155">Üzerinde **etki alanı tanıması ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c66f5-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="c66f5-157">a.</span><span class="sxs-lookup"><span data-stu-id="c66f5-157">a.</span></span> <span data-ttu-id="c66f5-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="c66f5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="c66f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="c66f5-159">b.</span></span> <span data-ttu-id="c66f5-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="c66f5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c66f5-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="c66f5-161">These values are not real.</span></span> <span data-ttu-id="c66f5-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c66f5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c66f5-163">Kişi [tanıması istemci destek ekibi](mailto:support@recognizeapp.com) oturum açma URL'si almak için tanımlayıcı değeri öğreticide daha sonra açıklanan SSO ayarları bölümünden servis sağlayıcı meta verileri URL'sini açarak alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c66f5-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="c66f5-164">.</span><span class="sxs-lookup"><span data-stu-id="c66f5-164">.</span></span> 
 
4. <span data-ttu-id="c66f5-165">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c66f5-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="c66f5-167">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-167">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c66f5-169">Üzerinde **Tanı Yapılandırması** 'yi tıklatın **Yapılandırma tanı** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c66f5-170">Kopya **Sign-Out URL, SAML varlık kimliği ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="c66f5-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="c66f5-172">Farklı web tarayıcısı penceresinde tanı kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="c66f5-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="c66f5-173">Bölmenin sağ üst köşesinde tıklatın **menü**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="c66f5-174">Git **şirket yönetici**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-174">Go to **Company Admin**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="c66f5-176">Sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="c66f5-178">Aşağıdaki adımları gerçekleştirin **SSO ayarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c66f5-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="c66f5-180">a.</span><span class="sxs-lookup"><span data-stu-id="c66f5-180">a.</span></span> <span data-ttu-id="c66f5-181">Olarak **etkinleştirmek SSO**seçin **ON**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="c66f5-182">b.</span><span class="sxs-lookup"><span data-stu-id="c66f5-182">b.</span></span> <span data-ttu-id="c66f5-183">İçinde **IDP varlık kimliği** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c66f5-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c66f5-184">c.</span><span class="sxs-lookup"><span data-stu-id="c66f5-184">c.</span></span> <span data-ttu-id="c66f5-185">İçinde **Sso hedef url** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c66f5-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c66f5-186">d.</span><span class="sxs-lookup"><span data-stu-id="c66f5-186">d.</span></span> <span data-ttu-id="c66f5-187">İçinde **Slo hedef url** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="c66f5-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="c66f5-188">e.</span><span class="sxs-lookup"><span data-stu-id="c66f5-188">e.</span></span> <span data-ttu-id="c66f5-189">İndirilen açmak **sertifika (Base64)** dosyasını Not Defteri'nde, içeriğini, panoya kopyalayın ve yapıştırın kendisine **sertifika** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="c66f5-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="c66f5-190">f.</span><span class="sxs-lookup"><span data-stu-id="c66f5-190">f.</span></span> <span data-ttu-id="c66f5-191">Tıklatın **Ayarları Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="c66f5-192">Yanında **SSO ayarları** bölümünde, altında URL'yi kopyalayın **hizmet sağlayıcısı meta veri URL'sini**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="c66f5-194">Açık **meta veri URL'sini bağlantı** meta veri belgesi indirmek için boş bir tarayıcı altında.</span><span class="sxs-lookup"><span data-stu-id="c66f5-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="c66f5-195">Sonra EntityDescriptor value(entityID) dosyasından kopyalayın ve yapıştırın **tanımlayıcısı** metin kutusuna **etki alanı tanıması ve URL'leri bölümüne** Azure Portal'daki.</span><span class="sxs-lookup"><span data-stu-id="c66f5-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Çoklu oturum açma üzerinde uygulama tarafı yapılandırma](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="c66f5-197">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="c66f5-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c66f5-198">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="c66f5-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c66f5-199">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c66f5-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c66f5-200">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c66f5-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c66f5-201">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c66f5-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="c66f5-203">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c66f5-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c66f5-204">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c66f5-206">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c66f5-208">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="c66f5-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c66f5-210">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c66f5-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c66f5-212">a.</span><span class="sxs-lookup"><span data-stu-id="c66f5-212">a.</span></span> <span data-ttu-id="c66f5-213">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c66f5-214">b.</span><span class="sxs-lookup"><span data-stu-id="c66f5-214">b.</span></span> <span data-ttu-id="c66f5-215">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="c66f5-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c66f5-216">c.</span><span class="sxs-lookup"><span data-stu-id="c66f5-216">c.</span></span> <span data-ttu-id="c66f5-217">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c66f5-218">d.</span><span class="sxs-lookup"><span data-stu-id="c66f5-218">d.</span></span> <span data-ttu-id="c66f5-219">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c66f5-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="c66f5-220">Tanı test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c66f5-220">Creating a Recognize test user</span></span>

<span data-ttu-id="c66f5-221">Azure AD kullanıcıların tanı oturum etkinleştirmek için bunların tanı sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c66f5-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="c66f5-222">Tanı söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c66f5-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="c66f5-223">Bu uygulama SCIM'yi sağlama desteklemiyor, ancak kullanıcılar sağlayan bir alternatif kullanıcı eşitleme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c66f5-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="c66f5-224">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c66f5-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c66f5-225">Tanı şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c66f5-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="c66f5-226">Bölmenin sağ üst köşesinde tıklatın **menü**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="c66f5-227">Git **şirket yönetici**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="c66f5-228">Sol gezinti bölmesinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="c66f5-229">Aşağıdaki adımları gerçekleştirin **kullanıcı eşitleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c66f5-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="c66f5-230">![Yeni kullanıcı](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="c66f5-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="c66f5-231">a.</span><span class="sxs-lookup"><span data-stu-id="c66f5-231">a.</span></span> <span data-ttu-id="c66f5-232">Olarak **eşitlemenin etkin**seçin **ON**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="c66f5-233">b.</span><span class="sxs-lookup"><span data-stu-id="c66f5-233">b.</span></span> <span data-ttu-id="c66f5-234">Olarak **Seç eşitleme sağlayıcısı**seçin **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="c66f5-235">c.</span><span class="sxs-lookup"><span data-stu-id="c66f5-235">c.</span></span> <span data-ttu-id="c66f5-236">Tıklatın **kullanıcı eşitleme çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c66f5-237">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="c66f5-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c66f5-238">Bu bölümde, Britta tanı için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c66f5-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="c66f5-240">**Tanı için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="c66f5-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="c66f5-241">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="c66f5-243">Uygulamalar listesinde **tanı**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-243">In the applications list, select **Recognize**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="c66f5-245">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="c66f5-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="c66f5-247">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c66f5-247">Click **Add** button.</span></span> <span data-ttu-id="c66f5-248">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c66f5-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="c66f5-250">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="c66f5-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c66f5-251">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c66f5-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c66f5-252">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c66f5-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c66f5-253">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="c66f5-253">Testing single sign-on</span></span>

<span data-ttu-id="c66f5-254">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="c66f5-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c66f5-255">Erişim paneli tanı parçasında tıklattığınızda, otomatik olarak tanı uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="c66f5-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="c66f5-256">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c66f5-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c66f5-257">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c66f5-257">Additional resources</span></span>

* [<span data-ttu-id="c66f5-258">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="c66f5-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c66f5-259">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="c66f5-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

