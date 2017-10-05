---
title: "Öğretici: Azure Active Directory Tümleştirme ile Kintone | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Kintone arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="6c023-103">Öğretici: Azure Active Directory Tümleştirme Kintone ile</span><span class="sxs-lookup"><span data-stu-id="6c023-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="6c023-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Kintone tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6c023-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c023-105">Kintone Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="6c023-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c023-106">Kintone erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6c023-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="6c023-107">Otomatik olarak için Kintone (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6c023-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c023-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="6c023-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6c023-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c023-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c023-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6c023-110">Prerequisites</span></span>

<span data-ttu-id="6c023-111">Azure AD tümleştirme Kintone ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c023-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="6c023-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="6c023-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c023-113">Bir Kintone çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="6c023-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c023-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6c023-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c023-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c023-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c023-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6c023-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c023-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c023-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c023-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="6c023-118">Scenario description</span></span>
<span data-ttu-id="6c023-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="6c023-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c023-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="6c023-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c023-121">Galeriden Kintone ekleme</span><span class="sxs-lookup"><span data-stu-id="6c023-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="6c023-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6c023-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="6c023-123">Galeriden Kintone ekleme</span><span class="sxs-lookup"><span data-stu-id="6c023-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="6c023-124">Azure AD Kintone tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Kintone eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c023-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c023-125">**Galeriden Kintone eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c023-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c023-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6c023-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c023-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="6c023-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c023-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6c023-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="6c023-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c023-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="6c023-133">Arama kutusuna **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="6c023-133">In the search box, type **Kintone**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="6c023-135">Sonuçlar panelinde seçin **Kintone**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c023-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c023-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="6c023-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c023-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Kintone sınayın.</span><span class="sxs-lookup"><span data-stu-id="6c023-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c023-139">Tekli çalışmaya oturum için Azure AD Kintone karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="6c023-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="6c023-140">Diğer bir deyişle, bir Azure AD kullanıcısının Kintone ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c023-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="6c023-141">Kintone içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6c023-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6c023-142">Yapılandırma ve Azure AD çoklu oturum açma Kintone ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c023-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c023-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6c023-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c023-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="6c023-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c023-145">**[Kintone test kullanıcısı oluşturma](#creating-a-kintone-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Kintone sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="6c023-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c023-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6c023-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c023-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6c023-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c023-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c023-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c023-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Kintone uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6c023-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="6c023-150">**Azure AD çoklu oturum açma ile Kintone yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c023-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="6c023-151">Azure portalında üzerinde **Kintone** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6c023-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="6c023-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="6c023-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="6c023-155">Üzerinde **Kintone etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c023-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="6c023-157">a.</span><span class="sxs-lookup"><span data-stu-id="6c023-157">a.</span></span> <span data-ttu-id="6c023-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="6c023-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="6c023-159">b.</span><span class="sxs-lookup"><span data-stu-id="6c023-159">b.</span></span> <span data-ttu-id="6c023-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="6c023-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="6c023-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="6c023-161">These values are not real.</span></span> <span data-ttu-id="6c023-162">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c023-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6c023-163">Kişi [Kintone istemci destek ekibi](https://www.kintone.com/contact/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="6c023-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="6c023-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **sertifika (Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6c023-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="6c023-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c023-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c023-168">Üzerinde **Kintone yapılandırma** 'yi tıklatın **yapılandırma Kintone** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="6c023-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6c023-169">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="6c023-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="6c023-171">Farklı web tarayıcısı penceresinde oturum açın, **Kintone** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="6c023-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="6c023-172">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="6c023-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="6c023-173">![Ayarları](./media/active-directory-saas-kintone-tutorial/ic785879.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="6c023-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="6c023-174">Tıklatın **kullanıcılar ve sistem yönetimini**.</span><span class="sxs-lookup"><span data-stu-id="6c023-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="6c023-175">![Kullanıcılar ve sistem yönetimini](./media/active-directory-saas-kintone-tutorial/ic785880.png "kullanıcılar ve Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="6c023-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="6c023-176">Altında **Sistem Yönetimi \> güvenlik** tıklatın **oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="6c023-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="6c023-177">![Oturum açma](./media/active-directory-saas-kintone-tutorial/ic785881.png "oturum açma")</span><span class="sxs-lookup"><span data-stu-id="6c023-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="6c023-178">Tıklatın **etkinleştirmek SAML kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="6c023-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="6c023-179">![SAML kimlik doğrulaması](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="6c023-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="6c023-180">SAML kimlik doğrulaması bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c023-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="6c023-181">![SAML kimlik doğrulaması](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML kimlik doğrulaması")</span><span class="sxs-lookup"><span data-stu-id="6c023-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="6c023-182">a.</span><span class="sxs-lookup"><span data-stu-id="6c023-182">a.</span></span> <span data-ttu-id="6c023-183">İçinde **oturum açma URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6c023-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="6c023-184">b.</span><span class="sxs-lookup"><span data-stu-id="6c023-184">b.</span></span> <span data-ttu-id="6c023-185">İçinde **oturum kapatma URL'si** metin değerini yapıştırın **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="6c023-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6c023-186">c.</span><span class="sxs-lookup"><span data-stu-id="6c023-186">c.</span></span> <span data-ttu-id="6c023-187">Tıklatın **Gözat** indirilen sertifikanızı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="6c023-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="6c023-188">d.</span><span class="sxs-lookup"><span data-stu-id="6c023-188">d.</span></span> <span data-ttu-id="6c023-189">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c023-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6c023-190">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="6c023-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6c023-191">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="6c023-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6c023-192">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c023-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c023-193">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c023-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c023-194">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6c023-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="6c023-196">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c023-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c023-197">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="6c023-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c023-199">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="6c023-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c023-201">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="6c023-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c023-203">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c023-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c023-205">a.</span><span class="sxs-lookup"><span data-stu-id="6c023-205">a.</span></span> <span data-ttu-id="6c023-206">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c023-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c023-207">b.</span><span class="sxs-lookup"><span data-stu-id="6c023-207">b.</span></span> <span data-ttu-id="6c023-208">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="6c023-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c023-209">c.</span><span class="sxs-lookup"><span data-stu-id="6c023-209">c.</span></span> <span data-ttu-id="6c023-210">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="6c023-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6c023-211">d.</span><span class="sxs-lookup"><span data-stu-id="6c023-211">d.</span></span> <span data-ttu-id="6c023-212">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c023-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="6c023-213">Kintone test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c023-213">Creating a Kintone test user</span></span>

<span data-ttu-id="6c023-214">Azure AD kullanıcıları için Kintone oturum açmak etkinleştirmek için bunların Kintone sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6c023-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="6c023-215">Kintone söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6c023-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="6c023-216">Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c023-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="6c023-217">Oturum, **Kintone** yönetici olarak şirket site.</span><span class="sxs-lookup"><span data-stu-id="6c023-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="6c023-218">Tıklatın **ayarı**.</span><span class="sxs-lookup"><span data-stu-id="6c023-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="6c023-219">![Ayarları](./media/active-directory-saas-kintone-tutorial/ic785879.png "ayarları")</span><span class="sxs-lookup"><span data-stu-id="6c023-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="6c023-220">Tıklatın **kullanıcılar ve sistem yönetimini**.</span><span class="sxs-lookup"><span data-stu-id="6c023-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="6c023-221">![Kullanıcı & Sistem Yönetimi](./media/active-directory-saas-kintone-tutorial/ic785880.png "kullanıcı & Sistem Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="6c023-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="6c023-222">Altında **kullanıcı yönetimi**, tıklatın **Departmanlar k & ullanıcıların**.</span><span class="sxs-lookup"><span data-stu-id="6c023-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="6c023-223">![K & ullanıcıların departmanı](./media/active-directory-saas-kintone-tutorial/ic785888.png "departmanı ve kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="6c023-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="6c023-224">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="6c023-224">Click **New User**.</span></span>
   
    <span data-ttu-id="6c023-225">![Yeni kullanıcılar](./media/active-directory-saas-kintone-tutorial/ic785889.png "yeni kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="6c023-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="6c023-226">İçinde **yeni kullanıcı** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6c023-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6c023-227">![Yeni kullanıcılar](./media/active-directory-saas-kintone-tutorial/ic785890.png "yeni kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="6c023-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="6c023-228">a.</span><span class="sxs-lookup"><span data-stu-id="6c023-228">a.</span></span> <span data-ttu-id="6c023-229">Tür a **görünen adı**, **oturum açma adı**, **yeni parola**, **parolayı onaylayın**, **e-posta adresi**, ve diğer ayrıntılarını geçerli bir AAD hesabıyla ilgili metin kutularına sağlamayı istiyor.</span><span class="sxs-lookup"><span data-stu-id="6c023-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="6c023-230">b.</span><span class="sxs-lookup"><span data-stu-id="6c023-230">b.</span></span> <span data-ttu-id="6c023-231">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c023-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c023-232">API sağlama AAD kullanıcı hesaplarına Kintone tarafından sağlanan veya herhangi diğer Kintone kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c023-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6c023-233">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="6c023-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6c023-234">Bu bölümde, Britta Kintone için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c023-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="6c023-236">**Kintone için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="6c023-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="6c023-237">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="6c023-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="6c023-239">Uygulamalar listesinde **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="6c023-239">In the applications list, select **Kintone**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="6c023-241">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="6c023-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="6c023-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6c023-243">Click **Add** button.</span></span> <span data-ttu-id="6c023-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6c023-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="6c023-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="6c023-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6c023-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6c023-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c023-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6c023-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c023-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="6c023-249">Testing single sign-on</span></span>

<span data-ttu-id="6c023-250">Bu bölümün amacı erişim paneli kullanılarak Azure AD çoklu oturum açma yapılandırmanızı test etmektir.</span><span class="sxs-lookup"><span data-stu-id="6c023-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6c023-251">Erişim paneli Kintone parçasında tıklattığınızda, otomatik olarak Kintone uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="6c023-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c023-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="6c023-252">Additional resources</span></span>

* [<span data-ttu-id="6c023-253">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="6c023-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c023-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="6c023-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

