---
title: "Öğretici: Azure Active Directory Tümleştirme ile Samanage | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Samanage arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="f7e72-103">Öğretici: Azure Active Directory Tümleştirme Samanage ile</span><span class="sxs-lookup"><span data-stu-id="f7e72-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="f7e72-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Samanage tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7e72-105">Samanage Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="f7e72-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7e72-106">Samanage erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f7e72-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="f7e72-107">Otomatik olarak için Samanage (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f7e72-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7e72-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="f7e72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f7e72-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7e72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7e72-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f7e72-110">Prerequisites</span></span>

<span data-ttu-id="f7e72-111">Azure AD tümleştirme Samanage ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7e72-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="f7e72-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="f7e72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7e72-113">Bir Samanage çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="f7e72-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7e72-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7e72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7e72-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7e72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7e72-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7e72-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7e72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7e72-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="f7e72-118">Scenario description</span></span>
<span data-ttu-id="f7e72-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7e72-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="f7e72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7e72-121">Galeriden Samanage ekleme</span><span class="sxs-lookup"><span data-stu-id="f7e72-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="f7e72-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f7e72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="f7e72-123">Galeriden Samanage ekleme</span><span class="sxs-lookup"><span data-stu-id="f7e72-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="f7e72-124">Azure AD Samanage tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Samanage eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7e72-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7e72-125">**Galeriden Samanage eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7e72-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e72-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f7e72-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7e72-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="f7e72-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="f7e72-133">Arama kutusuna **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-133">In the search box, type **Samanage**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="f7e72-135">Sonuçlar panelinde seçin **Samanage**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7e72-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="f7e72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7e72-138">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı Samanage sınayın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7e72-139">Tekli çalışmaya oturum için Azure AD Samanage karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="f7e72-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="f7e72-140">Diğer bir deyişle, bir Azure AD kullanıcısının Samanage ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7e72-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="f7e72-141">Samanage içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f7e72-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7e72-142">Yapılandırma ve Azure AD çoklu oturum açma Samanage ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f7e72-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7e72-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f7e72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7e72-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="f7e72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7e72-145">**[Samanage test kullanıcısı oluşturma](#creating-a-samanage-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı Samanage sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="f7e72-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7e72-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f7e72-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7e72-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7e72-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f7e72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7e72-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Samanage uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="f7e72-150">**Azure AD çoklu oturum açma ile Samanage yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7e72-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e72-151">Azure portalında üzerinde **Samanage** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="f7e72-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="f7e72-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="f7e72-155">Üzerinde **Samanage etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f7e72-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="f7e72-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7e72-157">a.</span></span> <span data-ttu-id="f7e72-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="f7e72-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="f7e72-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7e72-159">b.</span></span> <span data-ttu-id="f7e72-160">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="f7e72-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7e72-161">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="f7e72-161">These values are not real.</span></span> <span data-ttu-id="f7e72-162">Öğreticide daha sonra açıklanan tanımlayıcısı ve gerçek oturum açma URL'si ile bu değerleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="f7e72-163">Daha fazla ayrıntı başvurun [Samanage istemci destek ekibi](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="f7e72-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="f7e72-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="f7e72-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f7e72-168">Üzerinde **Samanage yapılandırma** 'yi tıklatın **yapılandırma Samanage** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7e72-169">Kopya **Sign-Out URL ve SAML varlık kimliği** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="f7e72-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="f7e72-171">Farklı web tarayıcısı penceresinde Samanage şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="f7e72-172">Tıklatın **Pano** seçip **Kurulum** sol gezinti bölmesindeki.</span><span class="sxs-lookup"><span data-stu-id="f7e72-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="f7e72-173">![Pano](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Panosu")</span><span class="sxs-lookup"><span data-stu-id="f7e72-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="f7e72-174">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="f7e72-175">![Çoklu oturum açma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="f7e72-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="f7e72-176">Gidin **SAML kullanarak oturum açma** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f7e72-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f7e72-177">![SAML kullanarak oturum açma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "SAML ile oturum açın")</span><span class="sxs-lookup"><span data-stu-id="f7e72-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="f7e72-178">a.</span><span class="sxs-lookup"><span data-stu-id="f7e72-178">a.</span></span> <span data-ttu-id="f7e72-179">Tıklatın **çoklu oturum açmayı etkinleştir SAML ile**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="f7e72-180">b.</span><span class="sxs-lookup"><span data-stu-id="f7e72-180">b.</span></span> <span data-ttu-id="f7e72-181">İçinde **kimlik sağlayıcısı URL'si** metin değerini yapıştırın **SAML varlık kimliği** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="f7e72-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="f7e72-182">c.</span><span class="sxs-lookup"><span data-stu-id="f7e72-182">c.</span></span> <span data-ttu-id="f7e72-183">Onayla **oturum açma URL'si** eşleşen **oturum üzerinde URL'si** , **Samanage etki alanı ve URL'leri** Azure portalı bölümünde.</span><span class="sxs-lookup"><span data-stu-id="f7e72-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="f7e72-184">d.</span><span class="sxs-lookup"><span data-stu-id="f7e72-184">d.</span></span> <span data-ttu-id="f7e72-185">İçinde **oturum kapatma URL'si** metin değeri girin **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="f7e72-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="f7e72-186">e.</span><span class="sxs-lookup"><span data-stu-id="f7e72-186">e.</span></span> <span data-ttu-id="f7e72-187">İçinde **SAML veren** uygulama kimliği URI metin kutusuna, türü, kimlik sağlayıcısı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="f7e72-188">f.</span><span class="sxs-lookup"><span data-stu-id="f7e72-188">f.</span></span> <span data-ttu-id="f7e72-189">Not Defteri'nde Azure portalından indirdiğiniz, base-64 kodlanmış sertifika açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **, kimlik sağlayıcısı x.509 sertifika aşağıdaki Yapıştır** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f7e72-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="f7e72-190">g.</span><span class="sxs-lookup"><span data-stu-id="f7e72-190">g.</span></span> <span data-ttu-id="f7e72-191">Tıklatın **Samanage içinde yoksa, kullanıcılar oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="f7e72-192">h.</span><span class="sxs-lookup"><span data-stu-id="f7e72-192">h.</span></span> <span data-ttu-id="f7e72-193">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="f7e72-194">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="f7e72-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7e72-195">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="f7e72-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7e72-196">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7e72-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7e72-197">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7e72-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7e72-198">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="f7e72-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="f7e72-200">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7e72-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e72-201">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7e72-203">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7e72-205">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="f7e72-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7e72-207">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f7e72-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7e72-209">a.</span><span class="sxs-lookup"><span data-stu-id="f7e72-209">a.</span></span> <span data-ttu-id="f7e72-210">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7e72-211">b.</span><span class="sxs-lookup"><span data-stu-id="f7e72-211">b.</span></span> <span data-ttu-id="f7e72-212">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="f7e72-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7e72-213">c.</span><span class="sxs-lookup"><span data-stu-id="f7e72-213">c.</span></span> <span data-ttu-id="f7e72-214">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f7e72-215">d.</span><span class="sxs-lookup"><span data-stu-id="f7e72-215">d.</span></span> <span data-ttu-id="f7e72-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="f7e72-217">Samanage test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7e72-217">Creating a Samanage test user</span></span>

<span data-ttu-id="f7e72-218">Azure AD kullanıcıları için Samanage oturum açmak etkinleştirmek için bunların Samanage sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f7e72-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="f7e72-219">Samanage söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f7e72-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="f7e72-220">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7e72-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e72-221">Samanage şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f7e72-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="f7e72-222">Tıklatın **Pano** seçip **Kurulum** sol gezinti bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="f7e72-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="f7e72-223">![Kurulum](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Kurulumu")</span><span class="sxs-lookup"><span data-stu-id="f7e72-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="f7e72-224">Tıklatın **kullanıcılar** sekmesi</span><span class="sxs-lookup"><span data-stu-id="f7e72-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="f7e72-225">![Kullanıcıların](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "kullanıcılar")</span><span class="sxs-lookup"><span data-stu-id="f7e72-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="f7e72-226">Tıklatın **yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-226">Click **New User**.</span></span>
   
    <span data-ttu-id="f7e72-227">![Yeni kullanıcı](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "yeni kullanıcı")</span><span class="sxs-lookup"><span data-stu-id="f7e72-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="f7e72-228">Tür **adı** ve **e-posta adresi** , önce sağlamak istediğiniz bir Azure Active Directory hesabının **kullanıcı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="f7e72-229">![Kullanıcı oluşturma](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "kullanıcı oluştur")</span><span class="sxs-lookup"><span data-stu-id="f7e72-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f7e72-230">Azure Active Directory hesap sahibi bir e-posta alır ve onu etkinleştirilmeden önce kendi hesabı onaylamak için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="f7e72-231">API tarafından Samanage sağlamak için Azure Active Directory kullanıcı hesapları sağlanan veya herhangi diğer Samanage kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7e72-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7e72-232">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="f7e72-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f7e72-233">Bu bölümde, Britta Samanage için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="f7e72-235">**Samanage için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f7e72-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e72-236">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="f7e72-238">Uygulamalar listesinde **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-238">In the applications list, select **Samanage**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="f7e72-240">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="f7e72-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="f7e72-242">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f7e72-242">Click **Add** button.</span></span> <span data-ttu-id="f7e72-243">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7e72-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="f7e72-245">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="f7e72-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7e72-246">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7e72-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7e72-247">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="f7e72-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7e72-248">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="f7e72-248">Testing single sign-on</span></span>

<span data-ttu-id="f7e72-249">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="f7e72-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f7e72-250">Erişim paneli Samanage parçasında tıklattığınızda, otomatik olarak Samanage uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="f7e72-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="f7e72-251">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f7e72-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7e72-252">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f7e72-252">Additional resources</span></span>

* [<span data-ttu-id="f7e72-253">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="f7e72-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7e72-254">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="f7e72-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

