---
title: "Öğretici: Azure Active Directory Tümleştirme ile Netsuite | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Netsuite arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="786f8-103">Öğretici: Azure Active Directory Tümleştirme Netsuite ile</span><span class="sxs-lookup"><span data-stu-id="786f8-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="786f8-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Netsuite tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="786f8-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="786f8-105">Netsuite Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="786f8-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="786f8-106">Netsuite erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="786f8-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="786f8-107">Otomatik olarak için Netsuite (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="786f8-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="786f8-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="786f8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="786f8-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="786f8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="786f8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="786f8-110">Prerequisites</span></span>

<span data-ttu-id="786f8-111">Azure AD tümleştirme Netsuite ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="786f8-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="786f8-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="786f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="786f8-113">Bir Netsuite çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="786f8-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="786f8-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="786f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="786f8-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="786f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="786f8-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="786f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="786f8-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="786f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="786f8-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="786f8-118">Scenario description</span></span>
<span data-ttu-id="786f8-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="786f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="786f8-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="786f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="786f8-121">Galeriden Netsuite ekleme</span><span class="sxs-lookup"><span data-stu-id="786f8-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="786f8-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="786f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="786f8-123">Galeriden Netsuite ekleme</span><span class="sxs-lookup"><span data-stu-id="786f8-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="786f8-124">Azure AD Netsuite tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Netsuite eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="786f8-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="786f8-125">**Galeriden Netsuite eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="786f8-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="786f8-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="786f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="786f8-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="786f8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="786f8-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="786f8-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="786f8-131">Tıklatın **yeni uygulama** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="786f8-131">Click **New application** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="786f8-133">Arama kutusuna **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="786f8-133">In the search box, type **Netsuite**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="786f8-135">Sonuçlar panelinde seçin **Netsuite**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="786f8-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="786f8-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="786f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="786f8-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı Netsuite ile test etme</span><span class="sxs-lookup"><span data-stu-id="786f8-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="786f8-139">Tekli çalışmaya oturum için Azure AD Netsuite karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="786f8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="786f8-140">Diğer bir deyişle, bir Azure AD kullanıcısının Netsuite ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="786f8-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="786f8-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Netsuite içinde.</span><span class="sxs-lookup"><span data-stu-id="786f8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="786f8-142">Yapılandırma ve Azure AD çoklu oturum açma Netsuite ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="786f8-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="786f8-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="786f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="786f8-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="786f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="786f8-145">**[Netsuite test kullanıcısı oluşturma](#creating-a-netsuite-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Netsuite sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="786f8-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="786f8-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="786f8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="786f8-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="786f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="786f8-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="786f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="786f8-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Netsuite uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="786f8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="786f8-150">**Azure AD çoklu oturum açma ile Netsuite yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="786f8-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="786f8-151">Azure portalında üzerinde **Netsuite** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="786f8-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="786f8-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="786f8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="786f8-155">Üzerinde **Netsuite etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="786f8-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="786f8-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="786f8-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="786f8-158">Bu değer gerçek değeri değil.</span><span class="sxs-lookup"><span data-stu-id="786f8-158">This value is not real value.</span></span> <span data-ttu-id="786f8-159">Değerin gerçek yanıt URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="786f8-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="786f8-160">Kişi [Netsuite destek ekibi](http://www.netsuite.com/portal/services/support.shtml) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="786f8-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="786f8-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve XML dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="786f8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="786f8-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="786f8-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="786f8-165">Üzerinde **Netsuite yapılandırma** 'yi tıklatın **yapılandırma Netsuite** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="786f8-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="786f8-166">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="786f8-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="786f8-168">Tarayıcınızda yeni bir sekme açın ve Netsuite şirket sitenizin yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="786f8-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="786f8-169">Sayfanın üstündeki araç çubuğunda **Kurulum**, ardından **Kurulum Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="786f8-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="786f8-171">Gelen **kurulum görevlerini** listesinde **tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="786f8-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="786f8-173">İçinde **yönetmek kimlik doğrulama** 'yi tıklatın **SAML çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="786f8-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="786f8-175">Üzerinde **SAML Kurulumu** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="786f8-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="786f8-176">a.</span><span class="sxs-lookup"><span data-stu-id="786f8-176">a.</span></span> <span data-ttu-id="786f8-177">Kopya **SAML çoklu oturum açma hizmet URL'si** değeri **hızlı başvuru** bölümünü **yapılandırma oturum açma** ve yapıştırın **kimlik sağlayıcısı oturum açma sayfası** Netsuite alanındaki.</span><span class="sxs-lookup"><span data-stu-id="786f8-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="786f8-179">b.</span><span class="sxs-lookup"><span data-stu-id="786f8-179">b.</span></span> <span data-ttu-id="786f8-180">Netsuite içinde seçin **birincil kimlik doğrulama yöntemini**.</span><span class="sxs-lookup"><span data-stu-id="786f8-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="786f8-181">c.</span><span class="sxs-lookup"><span data-stu-id="786f8-181">c.</span></span> <span data-ttu-id="786f8-182">Etiketli alan için **SAMLV2 kimlik sağlayıcısı meta verileri**seçin **IDP meta veri dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="786f8-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="786f8-183">Ardından **Gözat** Azure portalından indirdiğiniz meta veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="786f8-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="786f8-185">d.</span><span class="sxs-lookup"><span data-stu-id="786f8-185">d.</span></span> <span data-ttu-id="786f8-186">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="786f8-186">Click **Submit**.</span></span>

12. <span data-ttu-id="786f8-187">Azure AD'de tıklayın **Görünüm ve diğer tüm kullanıcı özniteliklerini düzenleme** onay kutusunu ve özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="786f8-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="786f8-189">İçin **öznitelik adı** alan, yazın `account`.</span><span class="sxs-lookup"><span data-stu-id="786f8-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="786f8-190">İçin **öznitelik değeri** alanında, Netsuite hesabı kimliğinizi yazın Bu, sabit ve hesap değişiklikle değerdir.</span><span class="sxs-lookup"><span data-stu-id="786f8-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="786f8-191">Hesabı Kimliğiniz bulmak yönergeler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="786f8-191">Instructions on how to find your account ID are included below:</span></span>

      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="786f8-193">a.</span><span class="sxs-lookup"><span data-stu-id="786f8-193">a.</span></span> <span data-ttu-id="786f8-194">Netsuite içinde tıklatın **Kurulum** üst gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="786f8-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="786f8-195">b.</span><span class="sxs-lookup"><span data-stu-id="786f8-195">b.</span></span> <span data-ttu-id="786f8-196">Altında tıklatın **kurulum görevlerini** seçin sol gezinti menüsünün bölümünde **tümleştirme** bölümünde ve tıklatın **Web Hizmetleri tercihleri**.</span><span class="sxs-lookup"><span data-stu-id="786f8-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="786f8-197">c.</span><span class="sxs-lookup"><span data-stu-id="786f8-197">c.</span></span> <span data-ttu-id="786f8-198">Netsuite hesabı Kimliğinizi kopyalayın ve yapıştırın **öznitelik değeri** Azure AD alanındaki.</span><span class="sxs-lookup"><span data-stu-id="786f8-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="786f8-200">Kullanıcıların çoklu oturum açma Netsuite gerçekleştirmeden önce ilk Netsuite için uygun izinler atanmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="786f8-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="786f8-201">Bu izinleri atamak için aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="786f8-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="786f8-202">a.</span><span class="sxs-lookup"><span data-stu-id="786f8-202">a.</span></span> <span data-ttu-id="786f8-203">Üst gezinti menüsünde **Kurulum**, ardından **Kurulum Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="786f8-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="786f8-205">b.</span><span class="sxs-lookup"><span data-stu-id="786f8-205">b.</span></span> <span data-ttu-id="786f8-206">Sol gezinti menüsünde seçin **kullanıcıları/rolleri**, ardından **Rolleri Yönet**.</span><span class="sxs-lookup"><span data-stu-id="786f8-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="786f8-208">c.</span><span class="sxs-lookup"><span data-stu-id="786f8-208">c.</span></span> <span data-ttu-id="786f8-209">Tıklatın **yeni rol**.</span><span class="sxs-lookup"><span data-stu-id="786f8-209">Click **New Role**.</span></span>

    <span data-ttu-id="786f8-210">d.</span><span class="sxs-lookup"><span data-stu-id="786f8-210">d.</span></span> <span data-ttu-id="786f8-211">Yazın bir **adı** yeni rol ve select **tek oturum açma yalnızca** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="786f8-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="786f8-213">e.</span><span class="sxs-lookup"><span data-stu-id="786f8-213">e.</span></span> <span data-ttu-id="786f8-214">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="786f8-214">Click **Save**.</span></span>

    <span data-ttu-id="786f8-215">f.</span><span class="sxs-lookup"><span data-stu-id="786f8-215">f.</span></span> <span data-ttu-id="786f8-216">Üstteki menüde tıklatın **izinleri**.</span><span class="sxs-lookup"><span data-stu-id="786f8-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="786f8-217">Ardından **Kurulum**.</span><span class="sxs-lookup"><span data-stu-id="786f8-217">Then click **Setup**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="786f8-219">g.</span><span class="sxs-lookup"><span data-stu-id="786f8-219">g.</span></span> <span data-ttu-id="786f8-220">Seçin **ayarlamak yukarı SAM çoklu oturum açma**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="786f8-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="786f8-221">h.</span><span class="sxs-lookup"><span data-stu-id="786f8-221">h.</span></span> <span data-ttu-id="786f8-222">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="786f8-222">Click **Save**.</span></span>

    <span data-ttu-id="786f8-223">ı.</span><span class="sxs-lookup"><span data-stu-id="786f8-223">i.</span></span> <span data-ttu-id="786f8-224">Üst gezinti menüsünde **Kurulum**, ardından **Kurulum Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="786f8-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="786f8-226">j.</span><span class="sxs-lookup"><span data-stu-id="786f8-226">j.</span></span> <span data-ttu-id="786f8-227">Sol gezinti menüsünde seçin **kullanıcıları/rolleri**, ardından **kullanıcıları yönetme**.</span><span class="sxs-lookup"><span data-stu-id="786f8-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="786f8-229">k.</span><span class="sxs-lookup"><span data-stu-id="786f8-229">k.</span></span> <span data-ttu-id="786f8-230">Bir test kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="786f8-230">Select a test user.</span></span> <span data-ttu-id="786f8-231">Ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="786f8-231">Then click **Edit**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="786f8-233">l.</span><span class="sxs-lookup"><span data-stu-id="786f8-233">l.</span></span> <span data-ttu-id="786f8-234">Rolleri iletişim kutusunda, oluşturduğunuz ve'ı tıklatın rolü seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="786f8-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="786f8-236">m.</span><span class="sxs-lookup"><span data-stu-id="786f8-236">m.</span></span> <span data-ttu-id="786f8-237">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="786f8-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="786f8-238">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="786f8-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="786f8-239">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="786f8-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="786f8-240">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="786f8-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="786f8-241">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="786f8-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="786f8-242">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="786f8-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="786f8-244">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="786f8-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="786f8-245">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="786f8-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="786f8-247">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="786f8-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="786f8-249">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="786f8-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="786f8-251">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="786f8-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="786f8-253">a.</span><span class="sxs-lookup"><span data-stu-id="786f8-253">a.</span></span> <span data-ttu-id="786f8-254">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="786f8-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="786f8-255">b.</span><span class="sxs-lookup"><span data-stu-id="786f8-255">b.</span></span> <span data-ttu-id="786f8-256">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="786f8-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="786f8-257">c.</span><span class="sxs-lookup"><span data-stu-id="786f8-257">c.</span></span> <span data-ttu-id="786f8-258">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="786f8-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="786f8-259">d.</span><span class="sxs-lookup"><span data-stu-id="786f8-259">d.</span></span> <span data-ttu-id="786f8-260">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="786f8-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="786f8-261">Netsuite test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="786f8-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="786f8-262">Bu bölümde, Britta Simon adlı bir kullanıcı Netsuite içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="786f8-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="786f8-263">Netsuite yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="786f8-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="786f8-264">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="786f8-264">There is no action item for you in this section.</span></span> <span data-ttu-id="786f8-265">Bir kullanıcı Netsuite zaten yoksa, Netsuite erişmeyi denediğinde yeni bir tane oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="786f8-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="786f8-266">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="786f8-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="786f8-267">Bu bölümde, Britta Netsuite için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="786f8-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="786f8-269">**Netsuite için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="786f8-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="786f8-270">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="786f8-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="786f8-272">Uygulamalar listesinde **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="786f8-272">In the applications list, select **Netsuite**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="786f8-274">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="786f8-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="786f8-276">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="786f8-276">Click **Add** button.</span></span> <span data-ttu-id="786f8-277">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="786f8-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="786f8-279">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="786f8-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="786f8-280">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="786f8-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="786f8-281">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="786f8-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="786f8-282">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="786f8-282">Testing single sign-on</span></span>

<span data-ttu-id="786f8-283">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="786f8-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="786f8-284">Çoklu oturum açma ayarlarınızı sınamak için adresinden erişim Paneli'nde açın [https://myapps.microsoft.com](https://myapps.microsoft.com/), oturum test dikkate ve tıklatın **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="786f8-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="786f8-285">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="786f8-285">Additional resources</span></span>

* [<span data-ttu-id="786f8-286">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="786f8-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="786f8-287">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="786f8-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="786f8-288">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="786f8-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

