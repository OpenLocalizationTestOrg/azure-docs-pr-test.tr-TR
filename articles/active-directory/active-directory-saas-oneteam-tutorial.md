---
title: "Öğretici: Azure Active Directory Tümleştirme ile Oneteam | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Oneteam arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c4381ca3166bd75bda1179b9a67b2224ba58ae68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="951a1-103">Öğretici: Azure Active Directory Tümleştirme Oneteam ile</span><span class="sxs-lookup"><span data-stu-id="951a1-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="951a1-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Oneteam tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="951a1-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="951a1-105">Oneteam Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="951a1-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="951a1-106">Oneteam erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="951a1-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="951a1-107">Otomatik olarak için Oneteam (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="951a1-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="951a1-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="951a1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="951a1-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="951a1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="951a1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="951a1-110">Prerequisites</span></span>

<span data-ttu-id="951a1-111">Azure AD tümleştirme Oneteam ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="951a1-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="951a1-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="951a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="951a1-113">Bir Oneteam çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="951a1-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="951a1-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="951a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="951a1-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="951a1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="951a1-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="951a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="951a1-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="951a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="951a1-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="951a1-118">Scenario description</span></span>
<span data-ttu-id="951a1-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="951a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="951a1-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="951a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="951a1-121">Galeriden Oneteam ekleme</span><span class="sxs-lookup"><span data-stu-id="951a1-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="951a1-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="951a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="951a1-123">Galeriden Oneteam ekleme</span><span class="sxs-lookup"><span data-stu-id="951a1-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="951a1-124">Azure AD Oneteam tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Oneteam eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="951a1-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="951a1-125">**Galeriden Oneteam eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="951a1-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="951a1-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="951a1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="951a1-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="951a1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="951a1-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="951a1-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="951a1-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="951a1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="951a1-133">Arama kutusuna **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="951a1-133">In the search box, type **Oneteam**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="951a1-135">Sonuçlar panelinde seçin **Oneteam**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="951a1-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="951a1-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="951a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="951a1-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Oneteam sınayın.</span><span class="sxs-lookup"><span data-stu-id="951a1-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="951a1-139">Tekli çalışmaya oturum için Azure AD Oneteam karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="951a1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="951a1-140">Diğer bir deyişle, bir Azure AD kullanıcısının Oneteam ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="951a1-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="951a1-141">Oneteam içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="951a1-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="951a1-142">Yapılandırma ve Azure AD çoklu oturum açma Oneteam ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="951a1-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="951a1-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="951a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="951a1-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="951a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="951a1-145">**[Oneteam test kullanıcısı oluşturma](#creating-a-oneteam-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Oneteam sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="951a1-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="951a1-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="951a1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="951a1-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="951a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="951a1-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="951a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="951a1-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Oneteam uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="951a1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="951a1-150">**Azure AD çoklu oturum açma ile Oneteam yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="951a1-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="951a1-151">Azure portalında üzerinde **Oneteam** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="951a1-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="951a1-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="951a1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="951a1-155">Üzerinde **Oneteam etki alanı ve URL'leri** uygulamada yapılandırmak istiyorsanız, bölüm **IDP** modu tarafından başlatılan:</span><span class="sxs-lookup"><span data-stu-id="951a1-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="951a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="951a1-157">a.</span></span> <span data-ttu-id="951a1-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="951a1-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="951a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="951a1-159">b.</span></span> <span data-ttu-id="951a1-160">İçinde **yanıt URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="951a1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="951a1-161">Denetleme **Göster Gelişmiş URL ayarları**, uygulamada yapılandırmak istiyorsanız **SP** modunda başlatılan:</span><span class="sxs-lookup"><span data-stu-id="951a1-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="951a1-163">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="951a1-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="951a1-164">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="951a1-164">These values are not real.</span></span> <span data-ttu-id="951a1-165">Bu değerler, gerçek tanımlayıcı, yanıt URL'si ve oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="951a1-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="951a1-166">Kişi [Oneteam istemci destek ekibi](https://support.one-team.com/hc/requests/new) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="951a1-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



5. <span data-ttu-id="951a1-167">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **meta veri XML** ve meta veri dosyası, bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="951a1-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="951a1-169">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="951a1-169">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="951a1-171">Uygulamanız için yapılandırılmış SSO almak için destek bileti ile yükseltebilirsiniz [Oneteam destek ekibi](https://support.one-team.com/hc/requests/new) ve indirilen verin **meta verileri**.</span><span class="sxs-lookup"><span data-stu-id="951a1-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="951a1-172">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="951a1-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="951a1-173">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="951a1-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="951a1-174">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="951a1-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="951a1-175">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="951a1-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="951a1-176">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="951a1-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="951a1-178">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="951a1-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="951a1-179">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="951a1-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="951a1-181">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="951a1-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="951a1-183">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="951a1-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="951a1-185">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="951a1-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="951a1-187">a.</span><span class="sxs-lookup"><span data-stu-id="951a1-187">a.</span></span> <span data-ttu-id="951a1-188">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="951a1-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="951a1-189">b.</span><span class="sxs-lookup"><span data-stu-id="951a1-189">b.</span></span> <span data-ttu-id="951a1-190">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="951a1-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="951a1-191">c.</span><span class="sxs-lookup"><span data-stu-id="951a1-191">c.</span></span> <span data-ttu-id="951a1-192">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="951a1-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="951a1-193">d.</span><span class="sxs-lookup"><span data-stu-id="951a1-193">d.</span></span> <span data-ttu-id="951a1-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="951a1-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="951a1-195">Oneteam test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="951a1-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="951a1-196">Bu bölümün amacı Britta Simon içinde Oneteam adlı bir kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="951a1-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="951a1-197">Oneteam yalnızca zaman sağlama, varsayılan olarak etkin olduğu destekler.</span><span class="sxs-lookup"><span data-stu-id="951a1-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="951a1-198">Bu bölümde, eylem öğe yok.</span><span class="sxs-lookup"><span data-stu-id="951a1-198">There is no action item for you in this section.</span></span> <span data-ttu-id="951a1-199">Henüz yoksa yeni bir kullanıcı Oneteam, erişme denemesi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="951a1-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="951a1-200">Bir kullanıcı el ile oluşturmanız gerekiyorsa, destek bileti ile yükseltebilirsiniz [Oneteam destek ekibi](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="951a1-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="951a1-201">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="951a1-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="951a1-202">Bu bölümde, Britta Oneteam için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="951a1-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="951a1-204">**Oneteam için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="951a1-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="951a1-205">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="951a1-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="951a1-207">Uygulamalar listesinde **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="951a1-207">In the applications list, select **Oneteam**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="951a1-209">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="951a1-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="951a1-211">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="951a1-211">Click **Add** button.</span></span> <span data-ttu-id="951a1-212">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="951a1-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="951a1-214">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="951a1-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="951a1-215">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="951a1-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="951a1-216">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="951a1-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="951a1-217">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="951a1-217">Testing single sign-on</span></span>

<span data-ttu-id="951a1-218">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="951a1-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="951a1-219">Erişim paneli Oneteam parçasında tıklattığınızda, otomatik olarak Oneteam uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="951a1-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="951a1-220">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="951a1-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="951a1-221">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="951a1-221">Additional resources</span></span>

* [<span data-ttu-id="951a1-222">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="951a1-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="951a1-223">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="951a1-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

