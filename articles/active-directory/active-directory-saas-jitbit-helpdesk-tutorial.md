---
title: "Öğretici: Azure Active Directory Tümleştirme Jitbit Yardım Masası ile | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile Jitbit Yardım Masası arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="cebbf-103">Öğretici: Azure Active Directory Tümleştirme Jitbit Yardım Masası ile</span><span class="sxs-lookup"><span data-stu-id="cebbf-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="cebbf-104">Bu öğreticide, Azure Active Directory (Azure AD) ile Jitbit Yardım Masası tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cebbf-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cebbf-105">Jitbit Yardım Masası Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cebbf-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cebbf-106">Jitbit Yardım Masası erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cebbf-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="cebbf-107">Azure AD hesaplarına otomatik olarak (çoklu oturum açma) için Yardım Masası Jitbit açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cebbf-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cebbf-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cebbf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cebbf-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cebbf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cebbf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cebbf-110">Prerequisites</span></span>

<span data-ttu-id="cebbf-111">Azure AD tümleştirme Jitbit Yardım Masası ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="cebbf-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="cebbf-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cebbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cebbf-113">Bir Jitbit Yardım Masası çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cebbf-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cebbf-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cebbf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cebbf-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cebbf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cebbf-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cebbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cebbf-117">Bir Azure AD deneme ortam yoksa, bir aylık deneme alabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cebbf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cebbf-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cebbf-118">Scenario description</span></span>
<span data-ttu-id="cebbf-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cebbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cebbf-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cebbf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cebbf-121">Galeriden Jitbit Yardım Masası ekleme</span><span class="sxs-lookup"><span data-stu-id="cebbf-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="cebbf-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cebbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="cebbf-123">Galeriden Jitbit Yardım Masası ekleme</span><span class="sxs-lookup"><span data-stu-id="cebbf-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="cebbf-124">Azure AD Jitbit Yardım Masası tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden Jitbit Yardım Masası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cebbf-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cebbf-125">**Galeriden Jitbit Yardım Masası eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cebbf-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cebbf-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cebbf-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cebbf-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-129">Then go to **All applications**.</span></span>

    ![Uygulamalar][2]
    
3. <span data-ttu-id="cebbf-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Uygulamalar][3]

4. <span data-ttu-id="cebbf-133">Arama kutusuna **Jitbit Yardım Masası**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="cebbf-135">Sonuçlar panelinde seçin **Jitbit Yardım Masası**ve ardından **Ekle** uygulama eklemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cebbf-137">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cebbf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cebbf-138">Bu bölümde, yapılandırmanız ve Jitbit Yardım Masası ile Azure AD çoklu oturum açmayı test "Britta Simon" adlı bir test kullanıcı tabanlı.</span><span class="sxs-lookup"><span data-stu-id="cebbf-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cebbf-139">Tekli çalışmaya oturum için Azure AD Jitbit Yardım Masası karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="cebbf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="cebbf-140">Diğer bir deyişle, bir Azure AD kullanıcısının Jitbit Yardım Masası ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cebbf-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="cebbf-141">Değeri Jitbit Yardım Masası Ata **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cebbf-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cebbf-142">Yapılandırma ve Azure AD çoklu oturum açma Jitbit Yardım Masası ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cebbf-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cebbf-143">**[Azure AD çoklu oturum açma yapılandırma](#configuring-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cebbf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cebbf-144">**[Bir Azure AD test kullanıcısı oluşturma](#creating-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="cebbf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cebbf-145">**[Jitbit Yardım Masası test kullanıcısı oluşturma](#creating-a-jitbit-helpdesk-test-user)**  - Britta Simon, karşılık gelen Jitbit kullanıcı Azure AD gösterimini bağlı olan Yardım Masası sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="cebbf-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cebbf-146">**[Azure AD test kullanıcısı atama](#assigning-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cebbf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cebbf-147">**[Çoklu oturum açmayı test](#testing-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cebbf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cebbf-148">Azure AD çoklu oturum açmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cebbf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cebbf-149">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma Jitbit Yardım Masası uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cebbf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="cebbf-150">**Azure AD çoklu oturum açma Jitbit Yardım Masası ile yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cebbf-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="cebbf-151">Azure portalında üzerinde **Jitbit Yardım Masası** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açmayı yapılandırın][4]

2. <span data-ttu-id="cebbf-153">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cebbf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="cebbf-155">Üzerinde **Jitbit Yardım Masası etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cebbf-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="cebbf-157">a.</span><span class="sxs-lookup"><span data-stu-id="cebbf-157">a.</span></span> <span data-ttu-id="cebbf-158">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:</span><span class="sxs-lookup"><span data-stu-id="cebbf-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="cebbf-159">Bu değer gerçek değil.</span><span class="sxs-lookup"><span data-stu-id="cebbf-159">This value is not real.</span></span> <span data-ttu-id="cebbf-160">Bu değer gerçek oturum açma URL'si ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cebbf-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="cebbf-161">Kişi [Jitbit Yardım Masası istemci destek ekibi](https://www.jitbit.com/support/) bu değeri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="cebbf-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="cebbf-162">b.</span><span class="sxs-lookup"><span data-stu-id="cebbf-162">b.</span></span>  <span data-ttu-id="cebbf-163">İçinde **tanımlayıcısı** metin kutusuna, şu URL'yi yazın:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="cebbf-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="cebbf-164">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cebbf-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="cebbf-166">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-166">Click **Save** button.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cebbf-168">Üzerinde **Jitbit Yardım Masası yapılandırma** 'yi tıklatın **yapılandırma Jitbit Yardım Masası** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cebbf-169">Kopya **SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cebbf-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="cebbf-171">Farklı web tarayıcısı penceresinde Jitbit Yardım Masası şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cebbf-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="cebbf-172">Üstteki araç çubuğunda tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="cebbf-173">![Yönetim](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="cebbf-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="cebbf-174">Tıklatın **genel ayarları**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="cebbf-175">![Kullanıcılar, şirketler ve izinleri](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "kullanıcıları, şirketler ve izinleri")</span><span class="sxs-lookup"><span data-stu-id="cebbf-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="cebbf-176">İçinde **kimlik doğrulama ayarlarını** yapılandırma bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cebbf-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="cebbf-177">![Kimlik doğrulama ayarlarını](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "kimlik doğrulama ayarları")</span><span class="sxs-lookup"><span data-stu-id="cebbf-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="cebbf-178">a.</span><span class="sxs-lookup"><span data-stu-id="cebbf-178">a.</span></span> <span data-ttu-id="cebbf-179">Seçin **SAML 2.0 tek etkinleştirmek oturum**, çoklu oturum açma (SSO), kullanarak oturum **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="cebbf-180">b.</span><span class="sxs-lookup"><span data-stu-id="cebbf-180">b.</span></span> <span data-ttu-id="cebbf-181">İçinde **uç nokta URL'si** metin değerini yapıştırın **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cebbf-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cebbf-182">c.</span><span class="sxs-lookup"><span data-stu-id="cebbf-182">c.</span></span> <span data-ttu-id="cebbf-183">Açık, **base-64** kodlanmış sertifika Not Defteri'nde, içeriğini, panoya kopyalayın ve yapıştırın kendisine **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="cebbf-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="cebbf-184">d.</span><span class="sxs-lookup"><span data-stu-id="cebbf-184">d.</span></span> <span data-ttu-id="cebbf-185">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cebbf-186">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cebbf-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cebbf-187">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="cebbf-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cebbf-188">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cebbf-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cebbf-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cebbf-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="cebbf-190">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="cebbf-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD Kullanıcı oluşturma][100]

<span data-ttu-id="cebbf-192">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cebbf-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cebbf-193">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cebbf-195">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cebbf-197">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="cebbf-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cebbf-199">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cebbf-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cebbf-201">a.</span><span class="sxs-lookup"><span data-stu-id="cebbf-201">a.</span></span> <span data-ttu-id="cebbf-202">İçinde **adı** metin kutusuna, tür adı olarak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="cebbf-203">b.</span><span class="sxs-lookup"><span data-stu-id="cebbf-203">b.</span></span> <span data-ttu-id="cebbf-204">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cebbf-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cebbf-205">c.</span><span class="sxs-lookup"><span data-stu-id="cebbf-205">c.</span></span> <span data-ttu-id="cebbf-206">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cebbf-207">d.</span><span class="sxs-lookup"><span data-stu-id="cebbf-207">d.</span></span> <span data-ttu-id="cebbf-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cebbf-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="cebbf-209">Jitbit Yardım Masası test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cebbf-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="cebbf-210">Azure AD kullanıcıların Jitbit Yardım Masası oturum etkinleştirmek için bunların Jitbit Yardım Masası sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cebbf-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="cebbf-211">Jitbit Yardım Masası söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="cebbf-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="cebbf-212">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cebbf-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cebbf-213">Oturum, **Jitbit Yardım Masası** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="cebbf-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="cebbf-214">Üstteki menüde tıklatın **Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="cebbf-215">![Yönetim](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Yönetim")</span><span class="sxs-lookup"><span data-stu-id="cebbf-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="cebbf-216">Tıklatın **kullanıcıları, şirketler ve izinleri**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="cebbf-217">![Kullanıcılar, şirketler ve izinleri](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "kullanıcıları, şirketler ve izinleri")</span><span class="sxs-lookup"><span data-stu-id="cebbf-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="cebbf-218">Tıklatın **Kullanıcı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="cebbf-219">![Kullanıcı Ekle](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Kullanıcı Ekle")</span><span class="sxs-lookup"><span data-stu-id="cebbf-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="cebbf-220">Create bölümünde aşağıdaki gibi sağlamak istediğiniz Azure AD hesabının veri türü:</span><span class="sxs-lookup"><span data-stu-id="cebbf-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="cebbf-221">![Oluşturma](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "oluşturma")</span><span class="sxs-lookup"><span data-stu-id="cebbf-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="cebbf-222">a.</span><span class="sxs-lookup"><span data-stu-id="cebbf-222">a.</span></span> <span data-ttu-id="cebbf-223">İçinde **kullanıcıadı** metin kutusuna, türü **BrittaSimon**, Azure portalında olduğu gibi kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="cebbf-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="cebbf-224">b.</span><span class="sxs-lookup"><span data-stu-id="cebbf-224">b.</span></span> <span data-ttu-id="cebbf-225">İçinde **e-posta** metin kutusuna, kullanıcının e-posta ister  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cebbf-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="cebbf-226">c.</span><span class="sxs-lookup"><span data-stu-id="cebbf-226">c.</span></span> <span data-ttu-id="cebbf-227">İçinde **ad** metin kutusuna, tür ilk gibi kullanıcı adını **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="cebbf-228">d.</span><span class="sxs-lookup"><span data-stu-id="cebbf-228">d.</span></span> <span data-ttu-id="cebbf-229">İçinde **Soyadı** metin kutusuna, türü kullanıcının soyadını gibi **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="cebbf-230">e.</span><span class="sxs-lookup"><span data-stu-id="cebbf-230">e.</span></span> <span data-ttu-id="cebbf-231">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cebbf-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="cebbf-232">Azure AD kullanıcı hesaplarını sağlamak için herhangi bir Jitbit Yardım Masası kullanıcı hesabı oluşturma araçlarını veya Jitbit Yardım Masası tarafından sağlanan API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cebbf-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cebbf-233">Azure AD test kullanıcısı atama</span><span class="sxs-lookup"><span data-stu-id="cebbf-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cebbf-234">Bu bölümde, Britta Jitbit Yardım Masası için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cebbf-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Kullanıcı atama][200] 

<span data-ttu-id="cebbf-236">**Jitbit Yardım Masası için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cebbf-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="cebbf-237">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cebbf-239">Uygulamalar listesinde **Jitbit Yardım Masası**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Çoklu oturum açmayı yapılandırın](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="cebbf-241">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cebbf-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Kullanıcı atama][202] 

4. <span data-ttu-id="cebbf-243">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cebbf-243">Click **Add** button.</span></span> <span data-ttu-id="cebbf-244">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cebbf-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Kullanıcı atama][203]

5. <span data-ttu-id="cebbf-246">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cebbf-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cebbf-247">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cebbf-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cebbf-248">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cebbf-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cebbf-249">Çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cebbf-249">Testing single sign-on</span></span>

<span data-ttu-id="cebbf-250">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="cebbf-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cebbf-251">Erişim paneli Jitbit Yardım Masası parçasında tıkladığınızda, oturum açma sayfasına Jitbit Yardım Masası uygulamasının almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cebbf-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="cebbf-252">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cebbf-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cebbf-253">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cebbf-253">Additional resources</span></span>

* [<span data-ttu-id="cebbf-254">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="cebbf-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cebbf-255">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cebbf-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

