---
title: "Öğretici: Azure Active Directory Tümleştirme ile PagerDuty | Microsoft Docs"
description: "Çoklu oturum açma Azure Active Directory ile PagerDuty arasında yapılandırmayı öğrenin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="cdf5f-103">Öğretici: Azure Active Directory Tümleştirme PagerDuty ile</span><span class="sxs-lookup"><span data-stu-id="cdf5f-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="cdf5f-104">Bu öğreticide, Azure Active Directory (Azure AD) ile PagerDuty tümleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cdf5f-105">PagerDuty Azure AD ile tümleştirme ile aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cdf5f-106">PagerDuty erişimi, Azure AD'de kontrol edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cdf5f-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="cdf5f-107">Otomatik olarak için PagerDuty (çoklu oturum açma) ile Azure AD hesaplarına açan kullanıcılarınıza etkinleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="cdf5f-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cdf5f-108">Hesaplarınızı bir merkezi konumda - Azure portalında yönetebilir</span><span class="sxs-lookup"><span data-stu-id="cdf5f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cdf5f-109">Azure AD ile SaaS uygulama tümleştirmesi hakkında daha fazla ayrıntı bilmek istiyorsanız, bkz: [uygulama erişimi ve çoklu oturum açma Azure Active Directory ile nedir](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cdf5f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdf5f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cdf5f-110">Prerequisites</span></span>

<span data-ttu-id="cdf5f-111">Azure AD tümleştirme PagerDuty ile yapılandırmak için aşağıdaki öğeleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="cdf5f-112">Bir Azure AD aboneliği</span><span class="sxs-lookup"><span data-stu-id="cdf5f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cdf5f-113">Bir PagerDuty çoklu oturum açma abonelik etkin</span><span class="sxs-lookup"><span data-stu-id="cdf5f-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdf5f-114">Bu öğreticide adımları test etmek için bir üretim ortamı'nı kullanarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cdf5f-115">Bu öğreticide test adımları için bu önerileri uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cdf5f-116">Gerekli olmadığı sürece, üretim ortamınızın kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cdf5f-117">Bir Azure AD deneme ortam yoksa, şunları yapabilirsiniz [bir aylık deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdf5f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cdf5f-118">Senaryo açıklaması</span><span class="sxs-lookup"><span data-stu-id="cdf5f-118">Scenario description</span></span>
<span data-ttu-id="cdf5f-119">Bu öğreticide, Azure AD çoklu oturum açma bir test ortamında test edin.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cdf5f-120">Bu öğreticide gösterilen senaryo iki ana yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdf5f-121">Galeriden PagerDuty ekleme</span><span class="sxs-lookup"><span data-stu-id="cdf5f-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="cdf5f-122">Çoklu oturum açmayı yapılandırma ve Azure AD sınama</span><span class="sxs-lookup"><span data-stu-id="cdf5f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="cdf5f-123">Galeriden PagerDuty ekleme</span><span class="sxs-lookup"><span data-stu-id="cdf5f-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="cdf5f-124">Azure AD PagerDuty tümleştirilmesi yapılandırmak için yönetilen SaaS uygulamaları listenize Galeriden PagerDuty eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cdf5f-125">**Galeriden PagerDuty eklemek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cdf5f-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cdf5f-126">İçinde  **[Azure portal](https://portal.azure.com)**, sol gezinti panosunda, tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory düğmesi][1]

2. <span data-ttu-id="cdf5f-128">Gidin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cdf5f-129">Ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-129">Then go to **All applications**.</span></span>

    ![Kurumsal uygulamalar dikey penceresi][2]
    
3. <span data-ttu-id="cdf5f-131">Yeni uygulama eklemek için tıklatın **yeni uygulama** iletişim üst kısmında düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Yeni Uygulama düğmesi][3]

4. <span data-ttu-id="cdf5f-133">Arama kutusuna **PagerDuty**seçin **PagerDuty** sonuç panelinden ardından **Ekle** uygulama eklemek için düğmeyi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Bir Azure AD test kullanıcısı oluşturma](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cdf5f-135">Yapılandırma ve Azure AD çoklu oturum açmayı test etme</span><span class="sxs-lookup"><span data-stu-id="cdf5f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cdf5f-136">Bu bölümde, yapılandırma ve Azure AD çoklu oturum açma "Britta Simon" adlı bir test kullanıcı tabanlı PagerDuty sınayın.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cdf5f-137">Tekli çalışmaya oturum için Azure AD PagerDuty karşılık gelen kullanıcı için bir kullanıcı Azure AD'de nedir bilmek ister.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="cdf5f-138">Diğer bir deyişle, bir Azure AD kullanıcısının PagerDuty ilgili kullanıcı arasında bir bağlantı ilişkisi kurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="cdf5f-139">PagerDuty içinde değerini atayın **kullanıcı adı** değeri olarak Azure AD'de **kullanıcıadı** bağlantı ilişkisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cdf5f-140">Yapılandırma ve Azure AD çoklu oturum açma PagerDuty ile test etmek için aşağıdaki yapı taşları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cdf5f-141">**[Azure AD çoklu oturum açma yapılandırma](#configure-azure-ad-single-sign-on)**  - bu özelliği kullanmak, kullanıcılarınızın etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cdf5f-142">**[Bir Azure AD test kullanıcısı oluşturma](#create-an-azure-ad-test-user)**  - Azure AD çoklu oturum açma Britta Simon ile test etmek için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdf5f-143">**[PagerDuty test kullanıcısı oluşturma](#create-a-pagerduty-test-user)**  - Britta Simon, karşılık gelen kullanıcı Azure AD gösterimini bağlı PagerDuty sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cdf5f-144">**[Azure AD test kullanıcısı atayın](#assign-the-azure-ad-test-user)**  - Azure AD çoklu oturum açma kullanmak Britta Simon etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdf5f-145">**[Test çoklu oturum açma](#test-single-sign-on)**  - yapılandırma çalışıp çalışmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cdf5f-146">Azure AD çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cdf5f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cdf5f-147">Bu bölümde, Azure AD çoklu oturum açma Azure portalında etkinleştirin ve çoklu oturum açma PagerDuty uygulamanızda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="cdf5f-148">**Azure AD çoklu oturum açma ile PagerDuty yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cdf5f-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="cdf5f-149">Azure portalında üzerinde **PagerDuty** uygulama tümleştirme sayfasını tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Çoklu oturum açma bağlantısı yapılandırma][4]

2. <span data-ttu-id="cdf5f-151">Üzerinde **çoklu oturum açma** iletişim kutusunda **modu** olarak **SAML tabanlı oturum açma** çoklu oturum açmayı etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Çoklu oturum açma iletişim kutusu](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="cdf5f-153">Üzerinde **PagerDuty etki alanı ve URL'leri** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![PagerDuty etki alanı ve URL'leri tek oturum açma bilgileri](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="cdf5f-155">a.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-155">a.</span></span> <span data-ttu-id="cdf5f-156">İçinde **oturum açma URL'si** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="cdf5f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="cdf5f-157">b.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-157">b.</span></span> <span data-ttu-id="cdf5f-158">İçinde **tanımlayıcısı** metin kutusuna, URL şu biçimi kullanarak bir yazın:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="cdf5f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cdf5f-159">Bu değerler gerçek değildir.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-159">These values are not real.</span></span> <span data-ttu-id="cdf5f-160">Bu değerler gerçek oturum açma URL'si ve tanımlayıcı ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cdf5f-161">Kişi [PagerDuty istemci destek ekibi](https://www.pagerduty.com/support/) bu değerleri almak için.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="cdf5f-162">Üzerinde **SAML imzalama sertifikası** 'yi tıklatın **Certificate(Base64)** ve sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Sertifika indirme bağlantısı](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="cdf5f-164">Tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-164">Click **Save** button.</span></span>

    ![Oturum açma tek Kaydet düğmesi yapılandırın](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cdf5f-166">Üzerinde **PagerDuty yapılandırma** 'yi tıklatın **yapılandırma PagerDuty** açmak için **yapılandırma oturum açma** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cdf5f-167">Kopya **Sign-Out URL ve SAML çoklu oturum açma hizmet URL'si** gelen **hızlı başvuru bölümü.**</span><span class="sxs-lookup"><span data-stu-id="cdf5f-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![PagerDuty yapılandırma](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="cdf5f-169">Farklı web tarayıcısı penceresinde Pagerduty şirket sitenize yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="cdf5f-170">Üstteki menüde tıklatın **hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="cdf5f-171">![Hesap ayarları](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "hesap ayarları")</span><span class="sxs-lookup"><span data-stu-id="cdf5f-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="cdf5f-172">Tıklatın **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="cdf5f-173">![Çoklu oturum açma](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "çoklu oturum açma")</span><span class="sxs-lookup"><span data-stu-id="cdf5f-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="cdf5f-174">Üzerinde **etkinleştirmek çoklu oturum açma (SSO)** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="cdf5f-175">![Çoklu oturum açmayı etkinleştir](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "çoklu oturum açmayı etkinleştir")</span><span class="sxs-lookup"><span data-stu-id="cdf5f-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="cdf5f-176">a.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-176">a.</span></span> <span data-ttu-id="cdf5f-177">Not Defteri'nde Azure portalından indirdiğiniz, base-64 kodlanmış sertifika açın, içeriğini, panoya kopyalayın ve yapıştırın kendisine **X.509 sertifikası** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="cdf5f-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="cdf5f-178">b.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-178">b.</span></span> <span data-ttu-id="cdf5f-179">İçinde **oturum açma URL'si** metin kutusuna, Yapıştır **SAML çoklu oturum açma hizmet URL'si** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="cdf5f-180">c.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-180">c.</span></span> <span data-ttu-id="cdf5f-181">İçinde **oturum kapatma URL'si** metin kutusuna, Yapıştır **Sign-Out URL** Azure portalından kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="cdf5f-182">d.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-182">d.</span></span> <span data-ttu-id="cdf5f-183">Seçin **tek oturum açma kapatma**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="cdf5f-184">e.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-184">e.</span></span> <span data-ttu-id="cdf5f-185">Tıklatın **değişiklikleri kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cdf5f-186">Şimdi bu yönergeleri içinde kısa bir sürümünü okuyabilirsiniz [Azure portal](https://portal.azure.com)uygulaması kuruluyor yaparken!</span><span class="sxs-lookup"><span data-stu-id="cdf5f-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cdf5f-187">Bu uygulamadan ekledikten sonra **Active Directory > Kurumsal uygulamalar** bölümünde, tıklamanız yeterlidir **çoklu oturum açma** sekmesinde ve aracılığıyla katıştırılmış belgelere erişebilir **yapılandırma** alt bölüm.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cdf5f-188">Daha fazla bilgiyi burada embedded belgeler özelliği hakkında: [Azure AD embedded belgeler]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cdf5f-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cdf5f-189">Bir Azure AD test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cdf5f-189">Create an Azure AD test user</span></span>

<span data-ttu-id="cdf5f-190">Bu bölümün amacı, Britta Simon adlı Azure portalında bir test kullanıcı oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Bir Azure AD test kullanıcısı oluşturma][100]

<span data-ttu-id="cdf5f-192">**Azure AD'de bir test kullanıcı oluşturmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cdf5f-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cdf5f-193">İçinde **Azure portal**, sol gezinti bölmesinde tıklatın **Azure Active Directory** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory düğmesi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cdf5f-195">Kullanıcıların listesini görüntülemek için şu adrese gidin **kullanıcılar ve gruplar** tıklatıp **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Kullanıcılar ve Gruplar" ve "Tüm kullanıcılar" bağlantılar](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cdf5f-197">Açmak için **kullanıcı** iletişim kutusunda, tıklatın **Ekle** iletişim kutusunun üst kısmında.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ekle düğmesi](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cdf5f-199">Üzerinde **kullanıcı** iletişim sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Kullanıcı iletişim kutusu](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cdf5f-201">a.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-201">a.</span></span> <span data-ttu-id="cdf5f-202">İçinde **adı** metin kutusuna, türü **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cdf5f-203">b.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-203">b.</span></span> <span data-ttu-id="cdf5f-204">İçinde **kullanıcı adı** metin kutusuna, türü **e-posta adresi** BrittaSimon biri.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cdf5f-205">c.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-205">c.</span></span> <span data-ttu-id="cdf5f-206">Seçin **Göster parola** ve değerini yazma **parola**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cdf5f-207">d.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-207">d.</span></span> <span data-ttu-id="cdf5f-208">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="cdf5f-209">PagerDuty test kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cdf5f-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="cdf5f-210">Azure AD kullanıcıları için PagerDuty oturum açmak etkinleştirmek için bunların PagerDuty sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="cdf5f-211">PagerDuty söz konusu olduğunda, sağlama bir el ile bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="cdf5f-212">API tarafından Pagerduty sağlamak için Azure Active Directory kullanıcı hesapları sağlanan veya herhangi diğer Pagerduty kullanıcı hesabı oluşturma araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="cdf5f-213">**Bir kullanıcı hesabı sağlamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cdf5f-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cdf5f-214">Oturum, **Pagerduty** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="cdf5f-215">Üstteki menüde tıklatın **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="cdf5f-216">Tıklatın **kullanıcıları eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="cdf5f-217">![Kullanıcıları ekleme](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "kullanıcı ekleme")</span><span class="sxs-lookup"><span data-stu-id="cdf5f-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="cdf5f-218">Üzerinde **ekibinizin davet** iletişim kutusunda, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cdf5f-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="cdf5f-219">![Davet Et ekibinizin](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "ekibinizin davet et")</span><span class="sxs-lookup"><span data-stu-id="cdf5f-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="cdf5f-220">a.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-220">a.</span></span> <span data-ttu-id="cdf5f-221">Tür **ilk ve son adı** gibi kullanıcının **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="cdf5f-222">b.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-222">b.</span></span> <span data-ttu-id="cdf5f-223">Girin **e-posta** kullanıcının adresi ister  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="cdf5f-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="cdf5f-224">c.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-224">c.</span></span> <span data-ttu-id="cdf5f-225">Tıklatın **Ekle**ve ardından **Gönder başvurulmasını**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="cdf5f-226">Tüm eklenen kullanıcıların PagerDuty hesabı oluşturmak için bir davet alır.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cdf5f-227">Azure AD test kullanıcısı atayın</span><span class="sxs-lookup"><span data-stu-id="cdf5f-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="cdf5f-228">Bu bölümde, Britta PagerDuty için erişim vererek, Azure çoklu oturum açma kullanılacak Simon etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Kullanıcı rolü atayın][200]

<span data-ttu-id="cdf5f-230">**PagerDuty için Britta Simon atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="cdf5f-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="cdf5f-231">Azure portalında uygulamaları görünümünü açın ve ardından dizin görünümüne gidin ve Git **kurumsal uygulamalar** ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Kullanıcı atama][201] 

2. <span data-ttu-id="cdf5f-233">Uygulamalar listesinde **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-233">In the applications list, select **PagerDuty**.</span></span>

    ![Uygulamalar listesinde PagerDuty bağlantı](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="cdf5f-235">Soldaki menüde tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-235">In the menu on the left, click **Users and groups**.</span></span>

    !["Kullanıcılar ve Gruplar" bağlantı][202]

4. <span data-ttu-id="cdf5f-237">Tıklatın **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-237">Click **Add** button.</span></span> <span data-ttu-id="cdf5f-238">Ardından **kullanıcılar ve gruplar** üzerinde **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Ekleme atama bölmesi][203]

5. <span data-ttu-id="cdf5f-240">Üzerinde **kullanıcılar ve gruplar** iletişim kutusunda **Britta Simon** kullanıcıları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cdf5f-241">Tıklatın **seçin** düğmesini **kullanıcılar ve gruplar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cdf5f-242">Tıklatın **atamak** düğmesini **eklemek atama** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cdf5f-243">Çoklu oturum açmayı test edin</span><span class="sxs-lookup"><span data-stu-id="cdf5f-243">Test single sign-on</span></span>

<span data-ttu-id="cdf5f-244">Bu bölümde, erişim paneli kullanarak Azure AD çoklu oturum açma yapılandırmanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cdf5f-245">Tıkladığınızda erişim Panelyou PagerDuty döşemede otomatik olarak PagerDuty uygulamanıza açan.</span><span class="sxs-lookup"><span data-stu-id="cdf5f-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="cdf5f-246">Erişim paneli hakkında daha fazla bilgi için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cdf5f-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdf5f-247">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cdf5f-247">Additional resources</span></span>

* [<span data-ttu-id="cdf5f-248">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="cdf5f-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdf5f-249">Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="cdf5f-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

