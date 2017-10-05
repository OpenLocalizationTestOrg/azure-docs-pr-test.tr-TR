---
title: "Öğretici: Azure Active Directory Tümleştirme Bitbucket için Kantega SSO | Microsoft Docs"
description: "Çoklu oturum açma Kantega SSO Bitbucket için Azure Active Directory arasındaki yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 6656c9abf8483ee98c0cb1a16c06d078e32240f2
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a><span data-ttu-id="79b73-103">Öğretici: Azure Active Directory Tümleştirme Kantega SSO Bitbucket için</span><span class="sxs-lookup"><span data-stu-id="79b73-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span></span>

<span data-ttu-id="79b73-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Kantega SSO Bitbucket için tümleştirme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="79b73-104">In this tutorial, you learn how to integrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79b73-105">Kantega SSO Bitbucket için Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="79b73-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79b73-106">Bitbucket Kantega SSO erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79b73-106">You can control in Azure AD who has access to Kantega SSO for Bitbucket</span></span>
- <span data-ttu-id="79b73-107">Azure AD hesaplarına otomatik olarak Kantega SSO (çoklu oturum açma) Bitbucket için için açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="79b73-107">You can enable your users to automatically get signed-on to Kantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79b73-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="79b73-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79b73-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79b73-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79b73-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79b73-110">Prerequisites</span></span>

<span data-ttu-id="79b73-111">Bitbucket için Kantega SSO ile Azure AD tümleştirme yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="79b73-111">To configure Azure AD integration with Kantega SSO for Bitbucket, you need the following items:</span></span>

- <span data-ttu-id="79b73-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="79b73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79b73-113">Abonelik Kantega SSO Bitbucket çoklu oturum açma için etkin</span><span class="sxs-lookup"><span data-stu-id="79b73-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79b73-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="79b73-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79b73-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="79b73-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79b73-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79b73-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79b73-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79b73-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="79b73-118">Scenario description</span></span>
<span data-ttu-id="79b73-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="79b73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79b73-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="79b73-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79b73-121">Galeriden Kantega SSO Bitbucket için ekleme</span><span class="sxs-lookup"><span data-stu-id="79b73-121">Adding Kantega SSO for Bitbucket from the gallery</span></span>
2. <span data-ttu-id="79b73-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79b73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bitbucket-from-the-gallery"></a><span data-ttu-id="79b73-123">Galeriden Kantega SSO Bitbucket için ekleme</span><span class="sxs-lookup"><span data-stu-id="79b73-123">Adding Kantega SSO for Bitbucket from the gallery</span></span>
<span data-ttu-id="79b73-124">Azure AD Kantega SSO Bitbucket için tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Kantega SSO Bitbucket için eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b73-124">To configure the integration of Kantega SSO for Bitbucket into Azure AD, you need to add Kantega SSO for Bitbucket from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79b73-125">**Bitbucket için Kantega SSO Galeriden eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b73-125">**To add Kantega SSO for Bitbucket from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79b73-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79b73-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79b73-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="79b73-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79b73-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79b73-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="79b73-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b73-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="79b73-133">Arama kutusuna **Kantega SSO Bitbucket için**.</span><span class="sxs-lookup"><span data-stu-id="79b73-133">In the search box, type **Kantega SSO for Bitbucket**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. <span data-ttu-id="79b73-135">Sonuçlar panelinde seçin **Kantega SSO Bitbucket için**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b73-135">In the results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79b73-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="79b73-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79b73-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma Kantega SSO "Britta Simon" adlı bir test kullanıcı tabanlı Bitbucket için test etme.</span><span class="sxs-lookup"><span data-stu-id="79b73-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79b73-139">Tekli çalışmaya oturum için Azure AD ne karşılık gelen Kantega SSO Bitbucket için bir kullanıcı için Azure AD içinde olduğu bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="79b73-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bitbucket is to a user in Azure AD.</span></span> <span data-ttu-id="79b73-140">Diğer bir deyişle, bir Azure AD kullanıcısının Kantega SSO Bitbucket için ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b73-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bitbucket needs to be established.</span></span>

<span data-ttu-id="79b73-141">Bitbucket için Kantega SSO içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="79b73-141">In Kantega SSO for Bitbucket, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79b73-142">Yapılandırma ve Azure AD çoklu oturum açma Kantega SSO Bitbucket için test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="79b73-142">To configure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79b73-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="79b73-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79b73-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="79b73-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79b73-145">**[Bitbucket test kullanıcısı için Kantega SSO oluşturma](#creating-a-kantega-sso-for-bitbucket-test-user)**  - Kantega SSO kullanıcı Azure AD gösterimini bağlı Bitbucket için Britta Simon, karşılık gelen sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="79b73-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79b73-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="79b73-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79b73-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79b73-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79b73-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79b73-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve, Kantega SSO Bitbucket uygulama için çoklu oturum açmayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="79b73-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span></span>

<span data-ttu-id="79b73-150">**Azure AD çoklu oturum açma Kantega SSO Bitbucket için yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b73-150">**To configure Azure AD single sign-on with Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="79b73-151">Azure portalında üzerinde **Kantega SSO Bitbucket için** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="79b73-151">In the Azure portal, on the **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="79b73-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="79b73-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. <span data-ttu-id="79b73-155">İçinde **IDP** üzerinde modunda başlatılan **Kantega SSO Bitbucket etki alanı ve URL'ler için** bölümü aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-155">In **IDP** initiated mode, on the **Kantega SSO for Bitbucket Domain and URLs** section perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    <span data-ttu-id="79b73-157">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-157">a.</span></span> <span data-ttu-id="79b73-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="79b73-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="79b73-159">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-159">b.</span></span> <span data-ttu-id="79b73-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="79b73-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="79b73-161">İçinde **SP** başlatılan modu, onay **Göster Gelişmiş URL ayarları** ve aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    <span data-ttu-id="79b73-163">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="79b73-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79b73-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="79b73-164">These values are not real.</span></span> <span data-ttu-id="79b73-165">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="79b73-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="79b73-166">Öğreticide daha sonra açıklanan Bitbucket eklentisi yapılandırma sırasında bu değerleri alma.</span><span class="sxs-lookup"><span data-stu-id="79b73-166">These values are recieved during the configuration of Bitbucket plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="79b73-167">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="79b73-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. <span data-ttu-id="79b73-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b73-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="79b73-171">Farklı web tarayıcısı penceresinde Bitbucket yönetim portalınızdaki yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="79b73-171">In a different web browser window, log in to your Bitbucket admin portal as an administrator.</span></span>

8. <span data-ttu-id="79b73-172">Dişlisine ve tıklatın **Bul yeni eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="79b73-172">Click cog and click the **Find new add-ons**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. <span data-ttu-id="79b73-174">Arama **Kantega SSO Bitbucket SAML & Kerberos için** tıklatıp **yükleme** yeni SAML eklentisini yüklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="79b73-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. <span data-ttu-id="79b73-176">Eklentisi yüklemeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="79b73-176">The plugin installation starts.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. <span data-ttu-id="79b73-178">Yükleme tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="79b73-178">Once the installation is complete.</span></span> <span data-ttu-id="79b73-179">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-179">Click **Close**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. <span data-ttu-id="79b73-181">**Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-181">Click **Manage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. <span data-ttu-id="79b73-183">Tıklatın **yapılandırma** yeni eklenti yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="79b73-183">Click **Configure** to configure the new plugin.</span></span>    

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. <span data-ttu-id="79b73-185">İçinde **SAML** bölümü.</span><span class="sxs-lookup"><span data-stu-id="79b73-185">In the **SAML** section.</span></span> <span data-ttu-id="79b73-186">Seçin **Azure Active Directory (Azure AD)** gelen **Ekle kimlik sağlayıcısı** açılır.</span><span class="sxs-lookup"><span data-stu-id="79b73-186">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. <span data-ttu-id="79b73-188">Abonelik düzeyi olarak **temel**.</span><span class="sxs-lookup"><span data-stu-id="79b73-188">Select subscription level as **Basic**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. <span data-ttu-id="79b73-190">Üzerinde **uygulama özellikleri** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-190">On the **App properties** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    <span data-ttu-id="79b73-192">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-192">a.</span></span> <span data-ttu-id="79b73-193">Kopya **uygulama kimliği URI'si** değer ve olarak kullanmak **tanımlayıcısı, yanıt URL'si ve oturum açma URL'si** üzerinde **Kantega SSO Bitbucket etki alanı ve URL'ler için** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="79b73-193">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="79b73-194">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-194">b.</span></span> <span data-ttu-id="79b73-195">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-195">Click **Next**.</span></span>

17. <span data-ttu-id="79b73-196">Üzerinde **meta veri içeri aktarma** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-196">On the **Metadata import** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    <span data-ttu-id="79b73-198">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-198">a.</span></span> <span data-ttu-id="79b73-199">Seçin **meta veri dosyası bilgisayarımda**ve Azure portalından karşıdan yükleme meta veri dosyası.</span><span class="sxs-lookup"><span data-stu-id="79b73-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="79b73-200">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-200">b.</span></span> <span data-ttu-id="79b73-201">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-201">Click **Next**.</span></span>

18. <span data-ttu-id="79b73-202">Üzerinde **adı ve SSO konumunu** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-202">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    <span data-ttu-id="79b73-204">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-204">a.</span></span> <span data-ttu-id="79b73-205">Kimlik sağlayıcı adını eklemek **kimlik sağlayıcı adı** textbox (örneğin Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79b73-205">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="79b73-206">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-206">b.</span></span> <span data-ttu-id="79b73-207">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-207">Click **Next**.</span></span>

19. <span data-ttu-id="79b73-208">İmzalama sertifikası doğrulayın ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="79b73-208">Verify the Signing certificate and click **Next**.</span></span>  

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. <span data-ttu-id="79b73-210">Üzerinde **Bitbucket kullanıcı hesapları** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-210">On the **Bitbucket user accounts** section, perform following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    <span data-ttu-id="79b73-212">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-212">a.</span></span> <span data-ttu-id="79b73-213">Seçin **gerekirse Bitbucket'ınızın iç dizinde kullanıcılar oluşturma** ve kullanıcılar uygun Grup adını girin (olabilir birden çok yok.</span><span class="sxs-lookup"><span data-stu-id="79b73-213">Select **Create users in Bitbucket's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="79b73-214">virgülle ayrılmış grupları).</span><span class="sxs-lookup"><span data-stu-id="79b73-214">of groups separated by comma).</span></span>

    <span data-ttu-id="79b73-215">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-215">b.</span></span> <span data-ttu-id="79b73-216">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-216">Click **Next**.</span></span>

21. <span data-ttu-id="79b73-217">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-217">Click **Finish**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. <span data-ttu-id="79b73-219">Üzerinde **için Azure AD etki alanları bilinen** bölümünde, şu adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-219">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    <span data-ttu-id="79b73-221">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-221">a.</span></span> <span data-ttu-id="79b73-222">Seçin **etki alanları bilinen** sayfanın sol panelindeki.</span><span class="sxs-lookup"><span data-stu-id="79b73-222">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="79b73-223">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-223">b.</span></span> <span data-ttu-id="79b73-224">Etki alanı adı girin **etki alanları bilinen** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="79b73-224">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="79b73-225">c.</span><span class="sxs-lookup"><span data-stu-id="79b73-225">c.</span></span> <span data-ttu-id="79b73-226">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-226">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="79b73-227">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="79b73-227">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79b73-228">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="79b73-228">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79b73-229">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79b73-229">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79b73-230">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b73-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="79b73-231">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="79b73-231">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="79b73-233">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b73-233">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79b73-234">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="79b73-234">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79b73-236">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="79b73-236">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79b73-238">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="79b73-238">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79b73-240">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-240">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79b73-242">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-242">a.</span></span> <span data-ttu-id="79b73-243">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79b73-243">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79b73-244">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-244">b.</span></span> <span data-ttu-id="79b73-245">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="79b73-245">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79b73-246">c.</span><span class="sxs-lookup"><span data-stu-id="79b73-246">c.</span></span> <span data-ttu-id="79b73-247">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="79b73-247">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79b73-248">d.</span><span class="sxs-lookup"><span data-stu-id="79b73-248">d.</span></span> <span data-ttu-id="79b73-249">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-249">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a><span data-ttu-id="79b73-250">Kantega SSO Bitbucket test kullanıcısı için oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b73-250">Creating a Kantega SSO for Bitbucket test user</span></span>

<span data-ttu-id="79b73-251">Bitbucket için oturum açmak Azure AD kullanıcıları etkinleştirmek için bunların Bitbucket sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="79b73-251">To enable Azure AD users to log in to Bitbucket, they must be provisioned into Bitbucket.</span></span> <span data-ttu-id="79b73-252">Bitbucket için Kantega SSO içinde sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="79b73-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span></span>

<span data-ttu-id="79b73-253">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b73-253">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="79b73-254">Bitbucket şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="79b73-254">Log in to your Bitbucket company site as an administrator.</span></span>

2. <span data-ttu-id="79b73-255">Ayarlar simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b73-255">Click on settings icon.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. <span data-ttu-id="79b73-257">Altında **Yönetim** bölüm sekmesini tıklatın, **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="79b73-257">Under **Administration** tab section, click **Users**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. <span data-ttu-id="79b73-259">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="79b73-259">Click **Create user**.</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. <span data-ttu-id="79b73-261">Üzerinde **kullanıcı oluştur** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79b73-261">On the **Create User** dialog page, perform the following steps:</span></span>

    ![Çalışanı ekleyin](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    <span data-ttu-id="79b73-263">a.</span><span class="sxs-lookup"><span data-stu-id="79b73-263">a.</span></span> <span data-ttu-id="79b73-264">İçinde **kullanıcıadı** metin kutusu, kullanıcı e-posta türünü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="79b73-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="79b73-265">b.</span><span class="sxs-lookup"><span data-stu-id="79b73-265">b.</span></span> <span data-ttu-id="79b73-266">İçinde **tam adı** metin kutusuna, Britta Simon gibi kullanıcının tam adını yazın.</span><span class="sxs-lookup"><span data-stu-id="79b73-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="79b73-267">c.</span><span class="sxs-lookup"><span data-stu-id="79b73-267">c.</span></span> <span data-ttu-id="79b73-268">İçinde **e-posta adresi** metin kutusuna, kullanıcının e-posta adresi türü ister Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="79b73-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="79b73-269">d.</span><span class="sxs-lookup"><span data-stu-id="79b73-269">d.</span></span> <span data-ttu-id="79b73-270">İçinde **parola** metin kutusuna, kullanıcının parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="79b73-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="79b73-271">e.</span><span class="sxs-lookup"><span data-stu-id="79b73-271">e.</span></span> <span data-ttu-id="79b73-272">İçinde **parolayı onayla** metin kutusu, kullanıcı parolasını yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="79b73-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="79b73-273">f.</span><span class="sxs-lookup"><span data-stu-id="79b73-273">f.</span></span> <span data-ttu-id="79b73-274">Tıklatın **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="79b73-274">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79b73-275">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="79b73-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79b73-276">Bu bölümde, Britta Bitbucket Kantega SSO için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="79b73-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bitbucket.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="79b73-278">**Bitbucket için Kantega SSO Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="79b73-278">**To assign Britta Simon to Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="79b73-279">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="79b73-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="79b73-281">Uygulamalar listesinde **Kantega SSO Bitbucket için**.</span><span class="sxs-lookup"><span data-stu-id="79b73-281">In the applications list, select **Kantega SSO for Bitbucket**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. <span data-ttu-id="79b73-283">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="79b73-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="79b73-285">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="79b73-285">Click **Add** button.</span></span> <span data-ttu-id="79b73-286">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b73-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="79b73-288">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="79b73-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79b73-289">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b73-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79b73-290">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="79b73-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79b73-291">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="79b73-291">Testing single sign-on</span></span>

<span data-ttu-id="79b73-292">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="79b73-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79b73-293">Erişim paneli Bitbucket parçasında Kantega SSO tıklattığınızda, otomatik olarak, Kantega SSO Bitbucket uygulama için açan.</span><span class="sxs-lookup"><span data-stu-id="79b73-293">When you click the Kantega SSO for Bitbucket tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bitbucket application.</span></span>
<span data-ttu-id="79b73-294">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79b73-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="79b73-295">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="79b73-295">Additional resources</span></span>

* [<span data-ttu-id="79b73-296">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="79b73-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79b73-297">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="79b73-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

