---
title: "Öğretici: Azure Active Directory Tümleştirme Confluence Kantega SSO | Microsoft Docs"
description: "Çoklu oturum açma Kantega SSO Confluence için Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ec11decbff4cf2f6c39b40228e349312fd86da00
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a><span data-ttu-id="4505a-103">Öğretici: Azure Active Directory Tümleştirme Confluence Kantega SSO</span><span class="sxs-lookup"><span data-stu-id="4505a-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span></span>

<span data-ttu-id="4505a-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Kantega SSO Confluence için tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4505a-104">In this tutorial, you learn how to integrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4505a-105">Kantega SSO Confluence için Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="4505a-105">Integrating Kantega SSO for Confluence with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4505a-106">Confluence Kantega SSO erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4505a-106">You can control in Azure AD who has access to Kantega SSO for Confluence</span></span>
- <span data-ttu-id="4505a-107">Azure AD hesaplarına otomatik olarak Kantega SSO (çoklu oturum açma) Confluence için için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4505a-107">You can enable your users to automatically get signed-on to Kantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4505a-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="4505a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4505a-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4505a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4505a-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4505a-110">Prerequisites</span></span>

<span data-ttu-id="4505a-111">Azure AD tümleştirme Confluence Kantega SSO ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="4505a-111">To configure Azure AD integration with Kantega SSO for Confluence, you need the following items:</span></span>

- <span data-ttu-id="4505a-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="4505a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4505a-113">Abonelik Kantega SSO Confluence çoklu oturum açma için etkin</span><span class="sxs-lookup"><span data-stu-id="4505a-113">A Kantega SSO for Confluence single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4505a-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4505a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4505a-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4505a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4505a-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4505a-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4505a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4505a-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="4505a-118">Scenario description</span></span>
<span data-ttu-id="4505a-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="4505a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4505a-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="4505a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4505a-121">Galeriden Kantega SSO Confluence için ekleme</span><span class="sxs-lookup"><span data-stu-id="4505a-121">Adding Kantega SSO for Confluence from the gallery</span></span>
2. <span data-ttu-id="4505a-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4505a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-confluence-from-the-gallery"></a><span data-ttu-id="4505a-123">Galeriden Kantega SSO Confluence için ekleme</span><span class="sxs-lookup"><span data-stu-id="4505a-123">Adding Kantega SSO for Confluence from the gallery</span></span>
<span data-ttu-id="4505a-124">Azure AD'ye Confluence Kantega SSO tümleştirmesini yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Confluence Kantega SSO eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4505a-124">To configure the integration of Kantega SSO for Confluence into Azure AD, you need to add Kantega SSO for Confluence from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4505a-125">**Galeriden Confluence Kantega SSO eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4505a-125">**To add Kantega SSO for Confluence from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4505a-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4505a-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="4505a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4505a-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4505a-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="4505a-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="4505a-133">Arama kutusuna **Kantega SSO Confluence için**.</span><span class="sxs-lookup"><span data-stu-id="4505a-133">In the search box, type **Kantega SSO for Confluence**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. <span data-ttu-id="4505a-135">Sonuçlar panelinde seçin **Kantega SSO Confluence için**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-135">In the results panel, select **Kantega SSO for Confluence**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4505a-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="4505a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4505a-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Confluence Kantega SSO ile test etme.</span><span class="sxs-lookup"><span data-stu-id="4505a-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4505a-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Kantega SSO Confluence için bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="4505a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Confluence is to a user in Azure AD.</span></span> <span data-ttu-id="4505a-140">Diğer bir deyişle, bir Azure AD kullanıcısının Kantega SSO Confluence için ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4505a-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Confluence needs to be established.</span></span>

<span data-ttu-id="4505a-141">Değeri Confluence için Kantega SSO içinde atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="4505a-141">In Kantega SSO for Confluence, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4505a-142">Yapılandırmak ve Azure AD çoklu oturum açma Confluence Kantega SSO sınamak için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="4505a-142">To configure and test Azure AD single sign-on with Kantega SSO for Confluence, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4505a-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4505a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4505a-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="4505a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4505a-145">**[Kantega SSO Confluence test kullanıcısı için oluşturma](#creating-a-kantega-sso-for-confluence-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Confluence Kantega SSO sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4505a-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Confluence that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4505a-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4505a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4505a-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4505a-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4505a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4505a-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve, Kantega SSO Confluence uygulama için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4505a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span></span>

<span data-ttu-id="4505a-150">**Azure AD çoklu oturum açma Kantega SSO Confluence için yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4505a-150">**To configure Azure AD single sign-on with Kantega SSO for Confluence, perform the following steps:**</span></span>

1. <span data-ttu-id="4505a-151">Azure portalında üzerinde **Kantega SSO Confluence için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="4505a-151">In the Azure portal, on the **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="4505a-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="4505a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. <span data-ttu-id="4505a-155">İçinde **IDP** üzerinde modunda başlatılan **Kantega SSO Confluence etki alanı ve URL'ler için** bölümü aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-155">In **IDP** initiated mode, on the **Kantega SSO for Confluence Domain and URLs** section perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    <span data-ttu-id="4505a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-157">a.</span></span> <span data-ttu-id="4505a-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="4505a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="4505a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-159">b.</span></span> <span data-ttu-id="4505a-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="4505a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="4505a-161">İçinde **SP** başlatılan modu, onay **Göster Gelişmiş URL ayarları** ve aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    <span data-ttu-id="4505a-163">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="4505a-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4505a-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="4505a-164">These values are not real.</span></span> <span data-ttu-id="4505a-165">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4505a-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4505a-166">Öğreticide daha sonra açıklanan Confluence eklentisi yapılandırma sırasında bu değerleri alma.</span><span class="sxs-lookup"><span data-stu-id="4505a-166">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="4505a-167">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4505a-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. <span data-ttu-id="4505a-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4505a-171">Farklı web tarayıcısı penceresinde oturum açın, **Confluence Yönetici portalı** yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="4505a-171">In a different web browser window, log in to your **Confluence admin portal** as an administrator.</span></span>

8. <span data-ttu-id="4505a-172">Dişlisine üzerine gelin ve tıklatın **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="4505a-172">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. <span data-ttu-id="4505a-174">Altında **ATLASSIAN Market** sekmesini tıklatın, **Bul yeni eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="4505a-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. <span data-ttu-id="4505a-176">Arama **Kantega SSO Confluence SAML Kerberos için** tıklatıp **yükleme** yeni SAML eklentisini yüklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="4505a-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. <span data-ttu-id="4505a-178">Eklentisi yüklemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="4505a-178">The plugin installation starts.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. <span data-ttu-id="4505a-180">Yükleme tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="4505a-180">Once the installation is complete.</span></span> <span data-ttu-id="4505a-181">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-181">Click **Close**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. <span data-ttu-id="4505a-183">**Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-183">Click **Manage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. <span data-ttu-id="4505a-185">Tıklatın **yapılandırma** yeni eklenti yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="4505a-185">Click **Configure** to configure the new plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. <span data-ttu-id="4505a-187">Bu yeni eklenti ayrıca altında bulunabilir **kullanıcılar ve güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-187">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. <span data-ttu-id="4505a-189">İçinde **SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4505a-189">In the **SAML** section.</span></span> <span data-ttu-id="4505a-190">Seçin **Azure Active Directory (Azure AD)** gelen **Ekle kimlik sağlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="4505a-190">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. <span data-ttu-id="4505a-192">Abonelik düzeyi olarak **temel**.</span><span class="sxs-lookup"><span data-stu-id="4505a-192">Select subscription level as **Basic**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. <span data-ttu-id="4505a-194">Üzerinde **uygulama özellikleri** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-194">On the **App properties** section, perform following steps:</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    <span data-ttu-id="4505a-196">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-196">a.</span></span> <span data-ttu-id="4505a-197">Kopya **uygulama kimliği URI'si** değer ve olarak kullanmak **tanımlayıcısı, yanıt URL'si ve oturum açma URL'si** üzerinde **Kantega SSO Confluence etki alanı ve URL'ler için** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="4505a-197">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="4505a-198">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-198">b.</span></span> <span data-ttu-id="4505a-199">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-199">Click **Next**.</span></span>

19. <span data-ttu-id="4505a-200">Üzerinde **meta veri içeri aktarma** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-200">On the **Metadata import** section, perform following steps:</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    <span data-ttu-id="4505a-202">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-202">a.</span></span> <span data-ttu-id="4505a-203">Seçin **meta veri dosyası bilgisayarımda**ve Azure portalından karşıdan yükleme meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="4505a-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="4505a-204">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-204">b.</span></span> <span data-ttu-id="4505a-205">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-205">Click **Next**.</span></span>

20. <span data-ttu-id="4505a-206">Üzerinde **adı ve SSO konumunu** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-206">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    <span data-ttu-id="4505a-208">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-208">a.</span></span> <span data-ttu-id="4505a-209">Kimlik sağlayıcı adını eklemek **kimlik sağlayıcı adı** textbox (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4505a-209">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="4505a-210">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-210">b.</span></span> <span data-ttu-id="4505a-211">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-211">Click **Next**.</span></span>

21. <span data-ttu-id="4505a-212">İmzalama sertifikası doğrulayın ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="4505a-212">Verify the Signing certificate and click **Next**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. <span data-ttu-id="4505a-214">Üzerinde **Confluence kullanıcı hesapları** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-214">On the **Confluence user accounts** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    <span data-ttu-id="4505a-216">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-216">a.</span></span> <span data-ttu-id="4505a-217">Seçin **gerekirse Confluence'nın iç dizinde kullanıcılar oluşturma** ve kullanıcılar uygun Grup adını girin (olabilir birden çok yok.</span><span class="sxs-lookup"><span data-stu-id="4505a-217">Select **Create users in Confluence's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="4505a-218">virgülle ayrılmış grupları).</span><span class="sxs-lookup"><span data-stu-id="4505a-218">of groups separated by comma).</span></span>

    <span data-ttu-id="4505a-219">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-219">b.</span></span> <span data-ttu-id="4505a-220">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-220">Click **Next**.</span></span>

23. <span data-ttu-id="4505a-221">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-221">Click **Finish**.</span></span>   

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. <span data-ttu-id="4505a-223">Üzerinde **için Azure AD etki alanları bilinen** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-223">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    <span data-ttu-id="4505a-225">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-225">a.</span></span> <span data-ttu-id="4505a-226">Seçin **etki alanları bilinen** sayfanın sol panelindeki.</span><span class="sxs-lookup"><span data-stu-id="4505a-226">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="4505a-227">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-227">b.</span></span> <span data-ttu-id="4505a-228">Etki alanı adı girin **etki alanları bilinen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="4505a-228">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="4505a-229">c.</span><span class="sxs-lookup"><span data-stu-id="4505a-229">c.</span></span> <span data-ttu-id="4505a-230">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-230">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="4505a-231">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="4505a-231">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4505a-232">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="4505a-232">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4505a-233">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4505a-233">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4505a-234">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4505a-234">Creating an Azure AD test user</span></span>
<span data-ttu-id="4505a-235">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4505a-235">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="4505a-237">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4505a-237">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4505a-238">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-238">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4505a-240">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="4505a-240">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4505a-242">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="4505a-242">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4505a-244">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-244">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4505a-246">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-246">a.</span></span> <span data-ttu-id="4505a-247">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4505a-247">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4505a-248">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-248">b.</span></span> <span data-ttu-id="4505a-249">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="4505a-249">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4505a-250">c.</span><span class="sxs-lookup"><span data-stu-id="4505a-250">c.</span></span> <span data-ttu-id="4505a-251">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="4505a-251">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4505a-252">d.</span><span class="sxs-lookup"><span data-stu-id="4505a-252">d.</span></span> <span data-ttu-id="4505a-253">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4505a-253">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a><span data-ttu-id="4505a-254">Kantega SSO Confluence test kullanıcısı için oluşturma</span><span class="sxs-lookup"><span data-stu-id="4505a-254">Creating a Kantega SSO for Confluence test user</span></span>

<span data-ttu-id="4505a-255">Azure AD kullanıcıları için Confluence oturum açmak etkinleştirmek için bunların Confluence sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4505a-255">To enable Azure AD users to log in to Confluence, they must be provisioned into Confluence.</span></span> <span data-ttu-id="4505a-256">Söz konusu olduğunda Kantega SSO Confluence için sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="4505a-256">In the case of Kantega SSO for Confluence, provisioning is a manual task.</span></span>

<span data-ttu-id="4505a-257">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4505a-257">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4505a-258">Kantega SSO Confluence şirket site için bir yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4505a-258">Log in to your Kantega SSO for Confluence company site as an administrator.</span></span>

2. <span data-ttu-id="4505a-259">Dişlisine üzerine gelin ve tıklatın **kullanıcı yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="4505a-259">Hover on cog and click the **User management**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. <span data-ttu-id="4505a-261">Kullanıcılar bölümü altında tıklatın **Kullanıcı Ekle** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-261">Under Users section, click **Add Users** tab.</span></span> <span data-ttu-id="4505a-262">Üzerinde **"Bir kullanıcı Ekle"** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4505a-262">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    <span data-ttu-id="4505a-264">a.</span><span class="sxs-lookup"><span data-stu-id="4505a-264">a.</span></span> <span data-ttu-id="4505a-265">İçinde **kullanıcıadı** metin kutusu, kullanıcı e-posta türünü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4505a-265">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="4505a-266">b.</span><span class="sxs-lookup"><span data-stu-id="4505a-266">b.</span></span> <span data-ttu-id="4505a-267">İçinde **tam adı** metin kutusuna, Britta Simon gibi kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="4505a-267">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="4505a-268">c.</span><span class="sxs-lookup"><span data-stu-id="4505a-268">c.</span></span> <span data-ttu-id="4505a-269">İçinde **e-posta** metin kutusuna, kullanıcının e-posta adresi türü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4505a-269">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="4505a-270">d.</span><span class="sxs-lookup"><span data-stu-id="4505a-270">d.</span></span> <span data-ttu-id="4505a-271">İçinde **parola** metin kutusu, kullanıcı parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="4505a-271">In the **Password** textbox, type the password for user.</span></span>

    <span data-ttu-id="4505a-272">e.</span><span class="sxs-lookup"><span data-stu-id="4505a-272">e.</span></span> <span data-ttu-id="4505a-273">Tıklatın **parolayı onayla** parolayı yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="4505a-273">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="4505a-274">f.</span><span class="sxs-lookup"><span data-stu-id="4505a-274">f.</span></span> <span data-ttu-id="4505a-275">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-275">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4505a-276">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="4505a-276">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4505a-277">Bu bölümde, Britta Confluence Kantega SSO için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4505a-277">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Confluence.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="4505a-279">**Kantega SSO Confluence için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="4505a-279">**To assign Britta Simon to Kantega SSO for Confluence, perform the following steps:**</span></span>

1. <span data-ttu-id="4505a-280">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="4505a-280">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="4505a-282">Uygulamalar listesinde **Kantega SSO Confluence için**.</span><span class="sxs-lookup"><span data-stu-id="4505a-282">In the applications list, select **Kantega SSO for Confluence**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. <span data-ttu-id="4505a-284">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="4505a-284">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="4505a-286">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4505a-286">Click **Add** button.</span></span> <span data-ttu-id="4505a-287">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4505a-287">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="4505a-289">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="4505a-289">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4505a-290">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4505a-290">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4505a-291">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="4505a-291">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4505a-292">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="4505a-292">Testing single sign-on</span></span>

<span data-ttu-id="4505a-293">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="4505a-293">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4505a-294">Erişim paneli Confluence parçasında Kantega SSO tıklattığınızda, otomatik olarak, Kantega SSO Confluence uygulama için açan.</span><span class="sxs-lookup"><span data-stu-id="4505a-294">When you click the Kantega SSO for Confluence tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Confluence application.</span></span>
<span data-ttu-id="4505a-295">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4505a-295">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4505a-296">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4505a-296">Additional resources</span></span>

* [<span data-ttu-id="4505a-297">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="4505a-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4505a-298">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="4505a-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

