---
title: "Öğretici: Azure Active Directory Tümleştirme ile InsideView | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile InsideView arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: f2b0a1d4bc44f8d0cd57c61e2d78950cb6a99854
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="70911-103">Öğretici: Azure Active Directory Tümleştirme InsideView ile</span><span class="sxs-lookup"><span data-stu-id="70911-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="70911-104">Bu öğreticide, Azure Active Directory (Azure AD) ile InsideView tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="70911-104">In this tutorial, you learn how to integrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70911-105">InsideView Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="70911-105">Integrating InsideView with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="70911-106">InsideView erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="70911-106">You can control in Azure AD who has access to InsideView</span></span>
- <span data-ttu-id="70911-107">Otomatik olarak için InsideView (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="70911-107">You can enable your users to automatically get signed-on to InsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70911-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="70911-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="70911-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70911-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70911-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="70911-110">Prerequisites</span></span>

<span data-ttu-id="70911-111">Azure AD tümleştirme InsideView ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="70911-111">To configure Azure AD integration with InsideView, you need the following items:</span></span>

- <span data-ttu-id="70911-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="70911-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70911-113">Bir InsideView çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="70911-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70911-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="70911-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70911-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="70911-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70911-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="70911-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70911-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70911-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70911-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="70911-118">Scenario description</span></span>
<span data-ttu-id="70911-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="70911-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70911-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="70911-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70911-121">Galeriden InsideView ekleme</span><span class="sxs-lookup"><span data-stu-id="70911-121">Adding InsideView from the gallery</span></span>
2. <span data-ttu-id="70911-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="70911-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-the-gallery"></a><span data-ttu-id="70911-123">Galeriden InsideView ekleme</span><span class="sxs-lookup"><span data-stu-id="70911-123">Adding InsideView from the gallery</span></span>
<span data-ttu-id="70911-124">Azure ad içinde InsideView tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden InsideView eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="70911-124">To configure the integration of InsideView in to Azure AD, you need to add InsideView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="70911-125">**Galeriden InsideView eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70911-125">**To add InsideView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="70911-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="70911-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70911-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="70911-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="70911-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="70911-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="70911-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70911-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="70911-133">Arama kutusuna **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="70911-133">In the search box, type **InsideView**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="70911-135">Sonuçlar panelinde seçin **InsideView**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70911-135">In the results panel, select **InsideView**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70911-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="70911-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70911-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı InsideView ile test etme</span><span class="sxs-lookup"><span data-stu-id="70911-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70911-139">Tekli çalışmaya oturum için Azure AD InsideView karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="70911-139">For single sign-on to work, Azure AD needs to know what the counterpart user in InsideView is to a user in Azure AD.</span></span> <span data-ttu-id="70911-140">Diğer bir deyişle, bir Azure AD kullanıcısının InsideView ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70911-140">In other words, a link relationship between an Azure AD user and the related user in InsideView needs to be established.</span></span>

<span data-ttu-id="70911-141">InsideView içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="70911-141">In InsideView, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="70911-142">Yapılandırma ve Azure AD çoklu oturum açma InsideView ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="70911-142">To configure and test Azure AD single sign-on with InsideView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="70911-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70911-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="70911-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="70911-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70911-145">**[InsideView test kullanıcısı oluşturma](#creating-a-insideview-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı InsideView sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="70911-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - to have a counterpart of Britta Simon in InsideView that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="70911-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70911-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70911-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="70911-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70911-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70911-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70911-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma InsideView uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70911-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="70911-150">**Azure AD çoklu oturum açma ile InsideView yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70911-150">**To configure Azure AD single sign-on with InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="70911-151">Azure portalında üzerinde **InsideView** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="70911-151">In the Azure portal, on the **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="70911-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="70911-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="70911-155">Üzerinde **InsideView etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="70911-155">On the **InsideView Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="70911-157">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="70911-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70911-158">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="70911-158">This value is not real.</span></span> <span data-ttu-id="70911-159">Bu değer ile gerçek yanıt URL'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="70911-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="70911-160">Kişi [InsideView destek ekibi ](mailto:support@insideview.com) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="70911-160">Contact [InsideView support team ](mailto:support@insideview.com) to get this value.</span></span>
 
4. <span data-ttu-id="70911-161">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (ham)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="70911-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="70911-163">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70911-163">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70911-165">Üzerinde **InsideView yapılandırma** 'yi tıklatın **yapılandırma InsideView** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="70911-165">On the **InsideView Configuration** section, click **Configure InsideView** to open **Configure sign-on** window.</span></span> <span data-ttu-id="70911-166">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="70911-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="70911-168">Farklı web tarayıcısı penceresinde InsideView şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="70911-168">In a different web browser window, log in to your InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="70911-169">Üstteki araç çubuğunda tıklatın **yönetici**, **SingleSignOn ayarları**ve ardından **eklemek SAML**.</span><span class="sxs-lookup"><span data-stu-id="70911-169">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="70911-170">![SAML çoklu oturum açma ayarları](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML çoklu oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="70911-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="70911-171">İçinde **yeni bir SAML eklemek** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="70911-171">In the **Add a New SAML** section, perform the following steps:</span></span>

    <span data-ttu-id="70911-172">![Yeni bir SAML eklemek](./media/active-directory-saas-insideview-tutorial/ic794136.png "yeni bir SAML ekleme")</span><span class="sxs-lookup"><span data-stu-id="70911-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="70911-173">a.</span><span class="sxs-lookup"><span data-stu-id="70911-173">a.</span></span> <span data-ttu-id="70911-174">İçinde **STS adını** metin kutusuna, yapılandırmanız için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="70911-174">In the **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="70911-175">b.</span><span class="sxs-lookup"><span data-stu-id="70911-175">b.</span></span> <span data-ttu-id="70911-176">İçinde **SamlP/WS-Fed istenmeyen EndPoint** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si**, Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="70911-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="70911-177">c.</span><span class="sxs-lookup"><span data-stu-id="70911-177">c.</span></span> <span data-ttu-id="70911-178">Azure portalından indirmiş, base-64 kodlanmış sertifika açmak içeriğini, panoya kopyalayın ve yapıştırın kendisine **STS sertifikası** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="70911-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox.</span></span>

    <span data-ttu-id="70911-179">d.</span><span class="sxs-lookup"><span data-stu-id="70911-179">d.</span></span> <span data-ttu-id="70911-180">İçinde **Crm kullanıcı kimliği eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="70911-180">In the **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="70911-181">e.</span><span class="sxs-lookup"><span data-stu-id="70911-181">e.</span></span> <span data-ttu-id="70911-182">İçinde **Crm e-posta eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="70911-182">In the **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="70911-183">f.</span><span class="sxs-lookup"><span data-stu-id="70911-183">f.</span></span> <span data-ttu-id="70911-184">İçinde **ilk adı Crm eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="70911-184">In the **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="70911-185">g.</span><span class="sxs-lookup"><span data-stu-id="70911-185">g.</span></span> <span data-ttu-id="70911-186">İçinde **Crm lastName eşleme** metin kutusuna, türü `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="70911-186">In the **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="70911-187">h.</span><span class="sxs-lookup"><span data-stu-id="70911-187">h.</span></span> <span data-ttu-id="70911-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="70911-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="70911-189">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="70911-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="70911-190">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="70911-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="70911-191">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70911-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70911-192">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70911-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="70911-193">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="70911-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="70911-195">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70911-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="70911-196">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="70911-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70911-198">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="70911-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70911-200">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="70911-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70911-202">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="70911-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70911-204">a.</span><span class="sxs-lookup"><span data-stu-id="70911-204">a.</span></span> <span data-ttu-id="70911-205">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70911-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70911-206">b.</span><span class="sxs-lookup"><span data-stu-id="70911-206">b.</span></span> <span data-ttu-id="70911-207">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="70911-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70911-208">c.</span><span class="sxs-lookup"><span data-stu-id="70911-208">c.</span></span> <span data-ttu-id="70911-209">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="70911-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="70911-210">d.</span><span class="sxs-lookup"><span data-stu-id="70911-210">d.</span></span> <span data-ttu-id="70911-211">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="70911-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="70911-212">InsideView test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="70911-212">Creating a InsideView test user</span></span>

<span data-ttu-id="70911-213">InsideView için oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar içinde InsideView için hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70911-213">To enable Azure AD users to log in to InsideView, they must be provisioned in to InsideView.</span></span> <span data-ttu-id="70911-214">InsideView söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="70911-214">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="70911-215">Kullanıcılar veya InsideView içinde oluşturulan kişileri almak için başvurun [InsideView destek ekibi](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="70911-215">To get users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="70911-216">API Azure AD kullanıcı hesaplarını sağlamak için InsideView tarafından sağlanan veya herhangi diğer InsideView kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70911-216">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="70911-217">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="70911-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="70911-218">Bu bölümde, Britta InsideView için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="70911-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InsideView.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="70911-220">**InsideView için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="70911-220">**To assign Britta Simon to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="70911-221">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="70911-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="70911-223">Uygulamalar listesinde **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="70911-223">In the applications list, select **InsideView**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="70911-225">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="70911-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="70911-227">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="70911-227">Click **Add** button.</span></span> <span data-ttu-id="70911-228">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="70911-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="70911-230">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="70911-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="70911-231">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="70911-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70911-232">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="70911-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70911-233">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="70911-233">Testing single sign-on</span></span>

<span data-ttu-id="70911-234">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="70911-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="70911-235">Erişim paneli InsideView parçasında tıklattığınızda, otomatik olarak InsideView uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="70911-235">When you click the InsideView tile in the Access Panel, you should get automatically signed-on to your InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70911-236">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="70911-236">Additional resources</span></span>

* [<span data-ttu-id="70911-237">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="70911-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70911-238">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="70911-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

