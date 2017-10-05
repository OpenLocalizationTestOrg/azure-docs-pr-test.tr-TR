---
title: "Öğretici: Azure Active Directory Tümleştirme ile AppDynamics | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile AppDynamics arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="6df03-103">Öğretici: Azure Active Directory Tümleştirme AppDynamics ile</span><span class="sxs-lookup"><span data-stu-id="6df03-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="6df03-104">Bu öğreticide, Azure Active Directory (Azure AD) ile AppDynamics tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6df03-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6df03-105">AppDynamics Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6df03-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6df03-106">AppDynamics erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6df03-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="6df03-107">Otomatik olarak için AppDynamics (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6df03-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6df03-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6df03-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6df03-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6df03-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6df03-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6df03-110">Prerequisites</span></span>

<span data-ttu-id="6df03-111">Azure AD tümleştirme AppDynamics ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="6df03-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="6df03-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6df03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6df03-113">Bir AppDynamics çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6df03-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6df03-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6df03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6df03-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6df03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6df03-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6df03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6df03-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6df03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6df03-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6df03-118">Scenario description</span></span>
<span data-ttu-id="6df03-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6df03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6df03-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6df03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6df03-121">Galeriden AppDynamics ekleme</span><span class="sxs-lookup"><span data-stu-id="6df03-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="6df03-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6df03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="6df03-123">Galeriden AppDynamics ekleme</span><span class="sxs-lookup"><span data-stu-id="6df03-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="6df03-124">Azure AD AppDynamics tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden AppDynamics eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6df03-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6df03-125">**Galeriden AppDynamics eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6df03-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6df03-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6df03-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6df03-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6df03-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6df03-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6df03-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6df03-133">Arama kutusuna **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="6df03-133">In the search box, type **AppDynamics**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="6df03-135">Sonuçlar panelinde seçin **AppDynamics**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6df03-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6df03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6df03-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı AppDynamics ile test etme</span><span class="sxs-lookup"><span data-stu-id="6df03-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6df03-139">Tekli çalışmaya oturum için Azure AD AppDynamics karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="6df03-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="6df03-140">Diğer bir deyişle, bir Azure AD kullanıcısının AppDynamics ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6df03-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="6df03-141">AppDynamics içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6df03-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6df03-142">Yapılandırma ve Azure AD çoklu oturum açma AppDynamics ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6df03-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6df03-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6df03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6df03-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="6df03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6df03-145">**[Bir AppDynamics test kullanıcısı oluşturma](#creating-an-appdynamics-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı AppDynamics sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="6df03-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6df03-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6df03-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6df03-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6df03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6df03-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6df03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6df03-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma AppDynamics uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6df03-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="6df03-150">**Azure AD çoklu oturum açma ile AppDynamics yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6df03-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="6df03-151">Azure portalında üzerinde **AppDynamics** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6df03-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6df03-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6df03-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="6df03-155">Üzerinde **AppDynamics etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6df03-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="6df03-157">a.</span><span class="sxs-lookup"><span data-stu-id="6df03-157">a.</span></span> <span data-ttu-id="6df03-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="6df03-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="6df03-159">b.</span><span class="sxs-lookup"><span data-stu-id="6df03-159">b.</span></span> <span data-ttu-id="6df03-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="6df03-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6df03-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6df03-161">These values are not real.</span></span> <span data-ttu-id="6df03-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6df03-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6df03-163">Kişi [AppDynamics istemci destek ekibi](https://www.appdynamics.com/support/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="6df03-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="6df03-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6df03-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="6df03-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6df03-168">Üzerinde **AppDynamics yapılandırma** 'yi tıklatın **yapılandırma AppDynamics** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6df03-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6df03-169">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6df03-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="6df03-171">Farklı web tarayıcısı penceresinde AppDynamics şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6df03-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="6df03-172">Üstteki araç çubuğunda tıklatın **ayarları**ve ardından **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="6df03-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="6df03-173">![Yönetim](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="6df03-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="6df03-174">Tıklatın **kimlik doğrulama sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="6df03-175">![Kimlik doğrulama sağlayıcısı](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "kimlik doğrulama sağlayıcısı")</span><span class="sxs-lookup"><span data-stu-id="6df03-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="6df03-176">İçinde **kimlik doğrulama sağlayıcısı** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6df03-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6df03-177">![SAML Yapılandırması](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML yapılandırması")</span><span class="sxs-lookup"><span data-stu-id="6df03-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="6df03-178">a.</span><span class="sxs-lookup"><span data-stu-id="6df03-178">a.</span></span> <span data-ttu-id="6df03-179">Olarak **kimlik doğrulama sağlayıcısı**seçin **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6df03-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="6df03-180">b.</span><span class="sxs-lookup"><span data-stu-id="6df03-180">b.</span></span> <span data-ttu-id="6df03-181">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6df03-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6df03-182">c.</span><span class="sxs-lookup"><span data-stu-id="6df03-182">c.</span></span> <span data-ttu-id="6df03-183">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6df03-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="6df03-184">d.</span><span class="sxs-lookup"><span data-stu-id="6df03-184">d.</span></span> <span data-ttu-id="6df03-185">Base-64 kodlanmış sertifikanızı Not Defteri'nde açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **sertifika** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="6df03-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="6df03-186">e.</span><span class="sxs-lookup"><span data-stu-id="6df03-186">e.</span></span> <span data-ttu-id="6df03-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6df03-187">Click **Save**.</span></span>

     <span data-ttu-id="6df03-188">![Kaydet](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Kaydet")</span><span class="sxs-lookup"><span data-stu-id="6df03-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="6df03-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6df03-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6df03-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="6df03-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6df03-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6df03-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6df03-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6df03-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="6df03-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6df03-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6df03-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6df03-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6df03-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6df03-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6df03-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6df03-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="6df03-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6df03-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6df03-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6df03-204">a.</span><span class="sxs-lookup"><span data-stu-id="6df03-204">a.</span></span> <span data-ttu-id="6df03-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6df03-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6df03-206">b.</span><span class="sxs-lookup"><span data-stu-id="6df03-206">b.</span></span> <span data-ttu-id="6df03-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6df03-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6df03-208">c.</span><span class="sxs-lookup"><span data-stu-id="6df03-208">c.</span></span> <span data-ttu-id="6df03-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6df03-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6df03-210">d.</span><span class="sxs-lookup"><span data-stu-id="6df03-210">d.</span></span> <span data-ttu-id="6df03-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6df03-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="6df03-212">Bir AppDynamics test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6df03-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="6df03-213">Azure AD kullanıcıları için AppDynamics oturum açmak etkinleştirmek için bunların AppDynamics sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6df03-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="6df03-214">AppDynamics söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6df03-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="6df03-215">**Kullanıcı sağlamayı yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6df03-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6df03-216">AppDynamics şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6df03-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="6df03-217">Git **kullanıcılar**ve ardından  **+**  açmak için **kullanıcı oluştur** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6df03-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="6df03-218">![Kullanıcıların](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="6df03-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="6df03-219">İçinde **kullanıcı oluştur** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6df03-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6df03-220">![Kullanıcı oluşturma](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="6df03-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="6df03-221">a.</span><span class="sxs-lookup"><span data-stu-id="6df03-221">a.</span></span> <span data-ttu-id="6df03-222">Türü **kullanıcıadı**, **adı**, **e-posta**, **yeni parola**, **yineleyin yeni parola** geçerli bir AAD, Hesap ilgili metin kutularına içine sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="6df03-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="6df03-223">b.</span><span class="sxs-lookup"><span data-stu-id="6df03-223">b.</span></span> <span data-ttu-id="6df03-224">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6df03-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6df03-225">API Azure AD kullanıcı hesaplarını sağlamak için AppDynamics tarafından sağlanan veya herhangi diğer AppDynamics kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6df03-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6df03-226">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6df03-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6df03-227">Bu bölümde, Britta AppDynamics için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6df03-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6df03-229">**AppDynamics için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6df03-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="6df03-230">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6df03-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6df03-232">Uygulamalar listesinde **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="6df03-232">In the applications list, select **AppDynamics**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="6df03-234">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6df03-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6df03-236">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6df03-236">Click **Add** button.</span></span> <span data-ttu-id="6df03-237">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6df03-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6df03-239">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6df03-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6df03-240">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6df03-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6df03-241">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6df03-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6df03-242">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6df03-242">Testing single sign-on</span></span>

<span data-ttu-id="6df03-243">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="6df03-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6df03-244">Erişim paneli AppDynamics parçasında tıklattığınızda, otomatik olarak AppDynamics uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="6df03-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6df03-245">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6df03-245">Additional resources</span></span>

* [<span data-ttu-id="6df03-246">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="6df03-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6df03-247">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6df03-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

