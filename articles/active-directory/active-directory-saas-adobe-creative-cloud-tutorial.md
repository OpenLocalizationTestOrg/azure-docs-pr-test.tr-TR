---
title: "Öğretici: Azure Active Directory Tümleştirme Adobe Creative bulut ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ve Adobe Creative bulut arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="d8d03-103">Öğretici: Adobe Creative bulut Azure Active Directory Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d8d03-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="d8d03-104">Bu öğreticide, Adobe Creative bulut Azure Active Directory (Azure AD) ile tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8d03-105">Adobe Creative bulut Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="d8d03-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d8d03-106">Adobe Creative bulut erişimi olan Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d8d03-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="d8d03-107">Azure AD hesaplarına otomatik olarak Adobe Creative buluta (çoklu oturum açma) açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d8d03-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8d03-108">Hesaplarınızı bir merkezi konumda - Azure Yönetim Portalı'nı yönetme</span><span class="sxs-lookup"><span data-stu-id="d8d03-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="d8d03-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8d03-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8d03-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d8d03-110">Prerequisites</span></span>

<span data-ttu-id="d8d03-111">Azure AD tümleştirme Adobe Creative Bulutla yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8d03-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="d8d03-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="d8d03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8d03-113">Bir Adobe Creative bulut çoklu oturum açma etkin abonelik</span><span class="sxs-lookup"><span data-stu-id="d8d03-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8d03-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d8d03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8d03-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8d03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8d03-116">Bu gerekli olmadığı sürece, üretim ortamınızın kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d8d03-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8d03-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8d03-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="d8d03-118">Scenario description</span></span>
<span data-ttu-id="d8d03-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8d03-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="d8d03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8d03-121">Galeriden Adobe Creative bulut ekleme</span><span class="sxs-lookup"><span data-stu-id="d8d03-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="d8d03-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d8d03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="d8d03-123">Galeriden Adobe Creative bulut ekleme</span><span class="sxs-lookup"><span data-stu-id="d8d03-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="d8d03-124">Azure AD Adobe Creative bulut tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Adobe Creative bulut eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d8d03-125">**Adobe Creative bulut Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8d03-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d03-126">İçinde  **[Azure Yönetim Portalı](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8d03-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d8d03-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="d8d03-131">Tıklatın **Ekle** iletişim kutusunun üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-131">Click **Add** button on the top of the dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="d8d03-133">Arama kutusuna **Adobe Creative bulut**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="d8d03-135">Sonuçlar panelinde seçin **Adobe Creative bulut**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8d03-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="d8d03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8d03-138">Bu bölümde, yapılandırmak ve Adobe Creative bulut "Britta Simon" adlı bir test kullanıcı tabanlı Azure AD çoklu oturum açmayı sınayın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8d03-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Adobe Creative bulutta bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="d8d03-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="d8d03-140">Diğer bir deyişle, bir Azure AD kullanıcısının ve ilgili kullanıcı Adobe Creative bulutta arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="d8d03-141">Bu bağlantı değeri atayarak ilişkisi **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** Adobe Creative bulutta.</span><span class="sxs-lookup"><span data-stu-id="d8d03-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="d8d03-142">Yapılandırma ve Azure AD çoklu oturum açma Adobe Creative bulut ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8d03-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d8d03-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d8d03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d8d03-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="d8d03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8d03-145">**[Adobe Creative bulut test kullanıcısı oluşturma](#creating-an-adobe-creative-cloud-test-user)**  - Britta Simon, karşılık gelen her, Azure AD gösterimine bağlı Adobe Creative bulut sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="d8d03-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d8d03-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d8d03-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8d03-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8d03-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d8d03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8d03-149">Bu bölümde, Azure AD çoklu oturum açma Azure Yönetim Portalı'nda etkinleştirin ve çoklu oturum açma, Adobe Creative bulut uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="d8d03-150">**Azure AD çoklu oturum açma Adobe Creative Bulutla yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8d03-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d03-151">Azure Yönetim Portalı'nda üzerinde **Adobe Creative bulut** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="d8d03-153">Üzerinde **çoklu oturum açma** iletişim kutusunda, olarak **modu** seçin **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="d8d03-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="d8d03-155">Üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="d8d03-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="d8d03-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8d03-157">a.</span></span> <span data-ttu-id="d8d03-158">İçinde **tanımlayıcısı** metin değeri olarak yazın:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="d8d03-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="d8d03-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8d03-159">b.</span></span> <span data-ttu-id="d8d03-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="d8d03-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8d03-161">Lütfen bu gerçek değerlerin olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-161">Please note that these are not the real values.</span></span> <span data-ttu-id="d8d03-162">Bu değerler gerçek tanımlayıcısı ve yanıt URL'si ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d8d03-163">Burada dizesinin benzersiz değeri tanımlayıcıda kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d8d03-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="d8d03-164">Bir kullanıcı el ile oluşturmanız gerekiyorsa, Adobe Creative bulut Destek ekibine başvurun gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="d8d03-165">Üzerinde **Adobe Creative bulut etki alanı ve URL'leri** bölümünde, uygulamada yapılandırmak istiyorsanız aşağıdaki adımları gerçekleştirin **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="d8d03-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="d8d03-167">a.</span><span class="sxs-lookup"><span data-stu-id="d8d03-167">a.</span></span> <span data-ttu-id="d8d03-168">Tıklayın **Göster Gelişmiş URL ayarları** seçeneği</span><span class="sxs-lookup"><span data-stu-id="d8d03-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d8d03-169">b.</span><span class="sxs-lookup"><span data-stu-id="d8d03-169">b.</span></span> <span data-ttu-id="d8d03-170">İçinde **oturum açma URL'si** metin değeri olarak yazın:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="d8d03-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="d8d03-171">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="d8d03-173">Üzerinde **Adobe Creative bulut Yapılandırması** 'yi tıklatın **Adobe Creative bulut yapılandırma** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d8d03-174">Lütfen kopyalayın **SAML varlık kimliği** ve **SAML SSO hizmet URL'si** hızlı başvuru bölümünden.</span><span class="sxs-lookup"><span data-stu-id="d8d03-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="d8d03-176">Farklı web tarayıcısı penceresinde Adobe Creative bulut kiracınız yönetici olarak oturum.</span><span class="sxs-lookup"><span data-stu-id="d8d03-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="d8d03-177">Git **kimlik** sol gezinti bölmesindeki ve etki alanınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="d8d03-178">Üzerinde aşağıdaki adımları gerçekleştirin **tek oturum yapılandırması gerekli** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d8d03-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="d8d03-179">![Ayarları](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="d8d03-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="d8d03-180">Tıklatın **Gözat** için Azure AD'den indirilen sertifikayı karşıya yüklemek için **IDP sertifika**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="d8d03-181">İçinde **IDP veren** metin kutusuna, put değerini **SAML varlık kimliği** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="d8d03-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="d8d03-182">İçinde **IDP oturum açma URL'si** metin kutusuna, put değerini **SAML SSO hizmet URL'si** öğesinden kopyalanan **yapılandırma oturum açma** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="d8d03-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="d8d03-183">Seçin **HTTP - yeniden yönlendirme** olarak **IDP bağlama**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="d8d03-184">Seçin **e-posta adresi** olarak **kullanıcı oturum açma ayarı**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="d8d03-185">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-185">Click **Save** button.</span></span>

15. <span data-ttu-id="d8d03-186">Pano artık XML sunacaktır **"Meta veriler indirme"** dosya.</span><span class="sxs-lookup"><span data-stu-id="d8d03-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="d8d03-187">Adobe EntityDescriptor URL ve AssertionConsumerService URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="d8d03-188">Lütfen dosyayı açın ve Azure AD uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Çoklu oturum açma uygulama tarafında yapılandırma](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="d8d03-191">a.</span><span class="sxs-lookup"><span data-stu-id="d8d03-191">a.</span></span> <span data-ttu-id="d8d03-192">Adobe için sağlanan EntityDescriptor değerini kullanmak **tanımlayıcısı** üzerinde **uygulama ayarlarını yapılandır** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8d03-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="d8d03-193">b.</span><span class="sxs-lookup"><span data-stu-id="d8d03-193">b.</span></span> <span data-ttu-id="d8d03-194">Adobe için sağlanan AssertionConsumerService değerini kullanmak **yanıt URL'si** üzerinde **uygulama ayarlarını yapılandır** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8d03-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8d03-195">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8d03-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8d03-196">Bu bölümün amacı, Britta Simon adlı Azure Yönetim Portalı'nda bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="d8d03-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="d8d03-198">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8d03-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d03-199">İçinde **Azure Yönetim Portalı**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8d03-201">Git **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar** kullanıcıların listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="d8d03-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8d03-203">İletişim kutusunun üstündeki **Ekle** açmak için **kullanıcı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8d03-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8d03-205">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8d03-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8d03-207">a.</span><span class="sxs-lookup"><span data-stu-id="d8d03-207">a.</span></span> <span data-ttu-id="d8d03-208">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8d03-209">b.</span><span class="sxs-lookup"><span data-stu-id="d8d03-209">b.</span></span> <span data-ttu-id="d8d03-210">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="d8d03-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8d03-211">c.</span><span class="sxs-lookup"><span data-stu-id="d8d03-211">c.</span></span> <span data-ttu-id="d8d03-212">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d8d03-213">d.</span><span class="sxs-lookup"><span data-stu-id="d8d03-213">d.</span></span> <span data-ttu-id="d8d03-214">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="d8d03-215">Adobe Creative bulut test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8d03-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="d8d03-216">Azure AD kullanıcıların Adobe Creative bulutunu oturum etkinleştirmek için bunlar Adobe Creative bulutunu sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d8d03-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="d8d03-217">Adobe Creative bulut söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d8d03-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="d8d03-218">**Kullanıcı hesaplarını sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8d03-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d03-219">Adobe Creative bulut şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="d8d03-220">Tıklatın **kişiler**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-220">Click **People**.</span></span>

    <span data-ttu-id="d8d03-221">![Kişiler](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="d8d03-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="d8d03-222">Tıklatın **davet kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-222">Click **Invite User**.</span></span>

    <span data-ttu-id="d8d03-223">![Kullanıcıları davet](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "kullanıcıları davet et")</span><span class="sxs-lookup"><span data-stu-id="d8d03-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="d8d03-224">Üzerinde **kişileri davet** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d8d03-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="d8d03-225">![Kişileri davet edin](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "kişileri davet edin")</span><span class="sxs-lookup"><span data-stu-id="d8d03-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="d8d03-226">a.</span><span class="sxs-lookup"><span data-stu-id="d8d03-226">a.</span></span> <span data-ttu-id="d8d03-227">İçinde **e-posta** metin kutusuna, Britta Simon hesabı e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="d8d03-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="d8d03-228">b.</span><span class="sxs-lookup"><span data-stu-id="d8d03-228">b.</span></span> <span data-ttu-id="d8d03-229">Tıklatın **davet**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8d03-230">Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce kendi hesabı onaylamak için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d8d03-231">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="d8d03-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d8d03-232">Bu bölümde, Adobe Creative buluta kendi erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="d8d03-234">**Britta Simon Adobe Creative buluta atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="d8d03-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d8d03-235">Azure Yönetim Portalı'nda uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="d8d03-237">Uygulamalar listesinde **Adobe Creative bulut**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="d8d03-239">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d8d03-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="d8d03-241">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8d03-241">Click **Add** button.</span></span> <span data-ttu-id="d8d03-242">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8d03-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="d8d03-244">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="d8d03-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d8d03-245">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8d03-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8d03-246">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d8d03-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8d03-247">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="d8d03-247">Testing single sign-on</span></span>

<span data-ttu-id="d8d03-248">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="d8d03-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d8d03-249">Erişim paneli Adobe Creative bulut parçasında tıklattığınızda, otomatik olarak Adobe Creative bulut uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="d8d03-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d8d03-250">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d8d03-250">Additional resources</span></span>

* [<span data-ttu-id="d8d03-251">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="d8d03-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8d03-252">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="d8d03-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png