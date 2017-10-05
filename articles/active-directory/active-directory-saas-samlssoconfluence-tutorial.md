---
title: "Öğretici: Azure Active Directory ile tümleştirme Confluence için SAML SSO GmbH çözünürlüğün | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile SAML SSO Confluence için arasında GmbH çözünürlüğün yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="5a0c9-103">Öğretici: Çözümleme GmbH Confluence için SAML SSO Azure Active Directory Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="5a0c9-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="5a0c9-104">Bu öğreticide, Azure Active Directory (Azure AD) ile GmbH çözünürlüğün SAML SSO Confluence için tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a0c9-105">Azure AD ile GmbH çözünürlüğün SAML SSO Confluence için tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5a0c9-106">SAML SSO Confluence için GmbH çözünürlüğün erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5a0c9-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="5a0c9-107">Otomatik olarak Confluence için SAML SSO için Azure AD hesaplarına sahip (çoklu oturum açma) GmbH çözünürlüğün açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5a0c9-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a0c9-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="5a0c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5a0c9-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a0c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a0c9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5a0c9-110">Prerequisites</span></span>

<span data-ttu-id="5a0c9-111">Çözümleme GmbH tarafından Confluence için SAML SSO ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="5a0c9-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="5a0c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a0c9-113">SAML SSO etkin abonelik GmbH çoklu oturum çözünürlüğün Confluence için</span><span class="sxs-lookup"><span data-stu-id="5a0c9-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a0c9-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a0c9-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a0c9-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a0c9-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a0c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a0c9-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="5a0c9-118">Scenario description</span></span>
<span data-ttu-id="5a0c9-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a0c9-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a0c9-121">SAML SSO Confluence için çözüm GmbH tarafından Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="5a0c9-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="5a0c9-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5a0c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="5a0c9-123">SAML SSO Confluence için çözüm GmbH tarafından Galeriden ekleme</span><span class="sxs-lookup"><span data-stu-id="5a0c9-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>

<span data-ttu-id="5a0c9-124">SAML SSO Confluence için Azure AD'ye tümleştirme GmbH çözünürlüğün yapılandırmak için SAML SSO Confluence için çözüm GmbH tarafından Galeriden yönetilen SaaS uygulamaları listenize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5a0c9-125">**SAML SSO Confluence için çözüm GmbH tarafından Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a0c9-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5a0c9-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a0c9-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5a0c9-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="5a0c9-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="5a0c9-133">Arama kutusuna **SAML SSO GmbH çözünürlüğün Confluence için**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="5a0c9-135">Sonuçlar panelinde seçin **SAML SSO GmbH çözünürlüğün Confluence için**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a0c9-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="5a0c9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5a0c9-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Confluence için SAML SSO GmbH "Britta Simon." olarak adlandırılan bir test kullanıcı tabanlı çözünürlüğün test etme</span><span class="sxs-lookup"><span data-stu-id="5a0c9-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5a0c9-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen kullanıcı Confluence için SAML SSO tarafından çözümleme GmbH Azure AD'de bir kullanıcı için olduğunu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="5a0c9-140">Diğer bir deyişle, bir Azure AD kullanıcısının SAML SSO Confluence için ilgili kullanıcı çözünürlüğün arasında bir bağlantı ilişkisi GmbH kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="5a0c9-141">Değeri GmbH çözünürlüğün Confluence için SAML SSO içinde atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5a0c9-142">Yapılandırmak ve Azure AD çoklu oturum açma Confluence için SAML SSO GmbH çözünürlüğün sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5a0c9-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5a0c9-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a0c9-145">**[SAML SSO çözümleme GmbH test kullanıcı tarafından Confluence için oluşturma](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  - Britta Simon, karşılık gelen SAML SSO Confluence için kullanıcı Azure AD gösterimini bağlı GmbH çözünürlüğün sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a0c9-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a0c9-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a0c9-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5a0c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a0c9-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma, SAML SSO Confluence için çözüm GmbH uygulama tarafından yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="5a0c9-150">**Azure AD çoklu oturum açma Confluence için SAML SSO GmbH çözümleme tarafından yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a0c9-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="5a0c9-151">Azure portalında üzerinde **SAML SSO GmbH çözünürlüğün Confluence için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="5a0c9-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="5a0c9-155">Üzerinde **Confluence GmbH etki alanı çözünürlüğün ve URL'ler için SAML SSO** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="5a0c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-157">a.</span></span> <span data-ttu-id="5a0c9-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="5a0c9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="5a0c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-159">b.</span></span> <span data-ttu-id="5a0c9-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="5a0c9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="5a0c9-161">Denetleme **Göster Gelişmiş URL ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="5a0c9-162">Uygulamada yapılandırmak istiyorsanız **SP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="5a0c9-164">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="5a0c9-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5a0c9-165">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-165">These values are not real.</span></span> <span data-ttu-id="5a0c9-166">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5a0c9-167">Kişi [SAML SSO GmbH istemci çözünürlüğün Confluence için destek ekibi](https://www.resolution.de/go/support) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="5a0c9-168">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="5a0c9-170">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-170">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="5a0c9-172">Farklı web tarayıcısı penceresinde oturum açın, **SAML SSO çözümleme GmbH Yönetici portalı tarafından Confluence için** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="5a0c9-173">Dişlisine üzerine gelin ve tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="5a0c9-175">Yönetici erişimi sayfasına yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="5a0c9-176">Parolayı girin ve tıklayın **Onayla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-176">Enter the password and click **Confirm** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="5a0c9-178">Altında **ATLASSIAN Market** sekmesini tıklatın, **Bul yeni eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="5a0c9-180">Arama **SAML çoklu oturum açma (SSO) Confluence için** tıklatıp **yükleme** yeni SAML eklentisini yüklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="5a0c9-182">Eklenti yükleme başlar.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-182">The plugin installation will start.</span></span> <span data-ttu-id="5a0c9-183">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-183">Click **Close**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="5a0c9-186">**Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-186">Click **Manage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="5a0c9-188">Tıklatın **yapılandırma** yeni eklenti yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-188">Click **Configure** to configure the new plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="5a0c9-190">Bu yeni eklenti ayrıca altında bulunabilir **kullanıcılar ve güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="5a0c9-192">Üzerinde **SAML SingleSignOn eklentisi yapılandırma** sayfasında, **ek kimlik sağlayıcısı ekleyin** düğmesi kimlik sağlayıcısı ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="5a0c9-194">Bu sayfada şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-194">Perform following steps on this page:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="5a0c9-196">a.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-196">a.</span></span> <span data-ttu-id="5a0c9-197">Ekleme **adı** kimlik sağlayıcısı (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a0c9-197">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="5a0c9-198">b.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-198">b.</span></span> <span data-ttu-id="5a0c9-199">Ekleme **açıklama** kimlik sağlayıcısı (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a0c9-199">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="5a0c9-200">c.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-200">c.</span></span> <span data-ttu-id="5a0c9-201">Tıklatın **XML** seçip **meta veri** Azure Portalı'ndan indirilen dosya.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-201">Click **XML** and select the **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="5a0c9-202">d.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-202">d.</span></span> <span data-ttu-id="5a0c9-203">Tıklatın **yük** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-203">Click **Load** button.</span></span>

    <span data-ttu-id="5a0c9-204">e.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-204">e.</span></span> <span data-ttu-id="5a0c9-205">IDP meta verileri okur ve alanları ekran görüntüsünde vurgulanmış şekilde doldurur.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-205">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 
18. <span data-ttu-id="5a0c9-206">' I tıklatın **ayarlarını kaydetmek** düğmesini tıklatarak ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-206">Click **Save settings** button to save the settings.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="5a0c9-208">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="5a0c9-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5a0c9-209">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5a0c9-210">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a0c9-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a0c9-211">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a0c9-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a0c9-212">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="5a0c9-214">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a0c9-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5a0c9-215">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-215">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a0c9-217">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-217">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a0c9-219">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-219">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a0c9-221">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-221">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a0c9-223">a.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-223">a.</span></span> <span data-ttu-id="5a0c9-224">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-224">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a0c9-225">b.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-225">b.</span></span> <span data-ttu-id="5a0c9-226">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-226">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a0c9-227">c.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-227">c.</span></span> <span data-ttu-id="5a0c9-228">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-228">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5a0c9-229">d.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-229">d.</span></span> <span data-ttu-id="5a0c9-230">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="5a0c9-231">SAML SSO çözümleme GmbH test kullanıcı tarafından Confluence için oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a0c9-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="5a0c9-232">SAML SSO Confluence için çözüm GmbH tarafından oturum açmak Azure AD kullanıcıları etkinleştirmek için bunlar Confluence için SAML SSO içine GmbH çözümleme tarafından sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-232">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="5a0c9-233">Confluence GmbH çözünürlüğün için SAML SSO içinde sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="5a0c9-234">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a0c9-234">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5a0c9-235">SAML SSO çözümleme GmbH şirket site tarafından Confluence için yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-235">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="5a0c9-236">Dişlisine üzerine gelin ve tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-236">Hover on cog and click the **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="5a0c9-238">Kullanıcılar bölümü altında tıklatın **kullanıcıları eklemek** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-238">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="5a0c9-239">Üzerinde **"Bir kullanıcı Ekle"** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5a0c9-239">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="5a0c9-241">a.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-241">a.</span></span> <span data-ttu-id="5a0c9-242">İçinde **kullanıcıadı** metin kutusu, kullanıcı Britta Simon gibi e-posta yazın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-242">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="5a0c9-243">b.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-243">b.</span></span> <span data-ttu-id="5a0c9-244">İçinde **tam adı** metin kutusuna, Britta Simon gibi kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-244">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="5a0c9-245">c.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-245">c.</span></span> <span data-ttu-id="5a0c9-246">İçinde **e-posta** metin kutusuna, kullanıcının e-posta adresi türü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-246">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="5a0c9-247">d.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-247">d.</span></span> <span data-ttu-id="5a0c9-248">İçinde **parola** metin kutusuna, Britta Simon için parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-248">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="5a0c9-249">e.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-249">e.</span></span> <span data-ttu-id="5a0c9-250">Tıklatın **parolayı onayla** parolayı yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-250">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="5a0c9-251">f.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-251">f.</span></span> <span data-ttu-id="5a0c9-252">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-252">Click **Add** button.</span></span>    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5a0c9-253">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="5a0c9-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5a0c9-254">Bu bölümde, çözüm GmbH tarafından Confluence için SAML SSO için erişim vererek, Azure çoklu oturum açma kullanılacak Britta Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="5a0c9-256">**Çözümleme GmbH tarafından Confluence için SAML SSO Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="5a0c9-256">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="5a0c9-257">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="5a0c9-259">Uygulamalar listesinde **SAML SSO GmbH çözünürlüğün Confluence için**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-259">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="5a0c9-261">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="5a0c9-263">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-263">Click **Add** button.</span></span> <span data-ttu-id="5a0c9-264">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="5a0c9-266">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5a0c9-267">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a0c9-268">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a0c9-269">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="5a0c9-269">Testing single sign-on</span></span>

<span data-ttu-id="5a0c9-270">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5a0c9-271">Çözümleme GmbH kutucuğu erişim Paneli'nde tarafından Confluence SAML SSO tıklattığınızda, otomatik olarak Confluence, SAML SSO için çözümleme GmbH uygulama tarafından açan.</span><span class="sxs-lookup"><span data-stu-id="5a0c9-271">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="5a0c9-272">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a0c9-272">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5a0c9-273">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="5a0c9-273">Additional resources</span></span>

* [<span data-ttu-id="5a0c9-274">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="5a0c9-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a0c9-275">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5a0c9-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

