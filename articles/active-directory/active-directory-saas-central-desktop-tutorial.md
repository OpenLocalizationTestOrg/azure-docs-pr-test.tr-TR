---
title: "Öğretici: Azure Active Directory Tümleştirme Merkezi Masaüstü ile | Microsoft Docs"
description: "Merkezi Masaüstü Azure Active Directory ile çoklu oturum açma, otomatik sağlama ve daha fazlasını sağlamak için nasıl kullanılacağını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="2a2c3-103">Öğretici: Azure Active Directory Tümleştirme ile Merkezi Masaüstü</span><span class="sxs-lookup"><span data-stu-id="2a2c3-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="2a2c3-104">Bu öğreticinin amacı, Azure ve Merkezi Masaüstü tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="2a2c3-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="2a2c3-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2a2c3-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="2a2c3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2a2c3-107">Merkezi bir masaüstü çoklu oturum açma etkin Abonelik / Merkezi Masaüstü Kiracı</span><span class="sxs-lookup"><span data-stu-id="2a2c3-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="2a2c3-108">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="2a2c3-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="2a2c3-109">Uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2a2c3-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="2a2c3-110">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2a2c3-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="2a2c3-111">Kullanıcı hazırlama işleminin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="2a2c3-111">Configuring user provisioning</span></span>
* <span data-ttu-id="2a2c3-112">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="2a2c3-112">Assigning users</span></span>

<span data-ttu-id="2a2c3-113">![Senaryo](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="2a2c3-114">Merkezi Masaüstü uygulama tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="2a2c3-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="2a2c3-115">Bu bölümün amacı, uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirmek nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="2a2c3-116">**Uygulama tümleştirmesi Merkezi Masaüstü için etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a2c3-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c3-117">Azure Klasik portalında, sol gezinti bölmesinde tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="2a2c3-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2a2c3-119">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2a2c3-120">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2a2c3-121">![Uygulamaları](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2a2c3-122">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="2a2c3-123">![Uygulama ekleme](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2a2c3-124">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="2a2c3-125">![Galeriden bir uygulama eklemek](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2a2c3-126">İçinde **arama kutusu**, türü **Merkezi Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="2a2c3-127">![Uygulama Galerisi](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="2a2c3-128">Sonuçlar bölmesinde seçin **Merkezi Masaüstü**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2a2c3-129">![Merkezi Masaüstü](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Merkezi Masaüstü")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2a2c3-130">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2a2c3-130">Configure single sign-on</span></span>

<span data-ttu-id="2a2c3-131">Bu bölümün amacı kullanıcıların Merkezi Masaüstü kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="2a2c3-132">Bu yordam bir parçası olarak, bir base-64 kodlanmış sertifika Merkezi Masaüstü kiracınız karşıya yüklemek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="2a2c3-133">Bu yordama bilmiyorsanız bkz [ikili bir sertifika bir metin dosyasına dönüştürmek nasıl](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="2a2c3-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="2a2c3-134">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a2c3-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c3-135">Azure Klasik portalında üzerinde **Merkezi Masaüstü** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için ** tek oturum yapılandırma üzerinde Aktar ** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="2a2c3-136">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="2a2c3-137">Üzerinde **Merkezi Masaüstü oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2a2c3-138">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="2a2c3-139">Üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları uygulayın ve ardından **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="2a2c3-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="2a2c3-140">İçinde **Merkezi Masaüstü Oturum açma URL'si** metin kutusuna, Merkezi Masaüstü Kiracı URL'sini yazın (örneğin: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="2a2c3-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="2a2c3-141">Merkezi Masaüstü yanıt URL'si metin kutusuna Merkezi Masaüstü AssertionConsumerService URL'nizi yazın (örneğin: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="2a2c3-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2a2c3-142">Değer Merkezi Masaüstü meta verileri alabilir (örn: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="2a2c3-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="2a2c3-143">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="2a2c3-144">Üzerinde **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** , sertifika indirmek için sayfasını tıklatın **indirme sertifika**ve ardından sertifika dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="2a2c3-145">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="2a2c3-146">Oturum, **Merkezi Masaüstü** Kiracı.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="2a2c3-147">Git **ayarları**, tıklatın **Gelişmiş**ve ardından **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="2a2c3-148">![Kurulum - Gelişmiş](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Kurulum - Gelişmiş")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="2a2c3-149">Üzerinde **tek oturum açma ayarları** sayfasında, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a2c3-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="2a2c3-150">![Çoklu oturum açma ayarları](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "tek oturum açma ayarları")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="2a2c3-151">Seçin **etkinleştir SAML v2 çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="2a2c3-152">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfasında, kopya **veren URL'si** değer ve ardından yapıştırın **SSO URL** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="2a2c3-153">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfasında, kopya **uzaktan oturum açma URL'si** değer ve ardından yapıştırın **SSO oturum açma URL'si** metin kutusu .</span><span class="sxs-lookup"><span data-stu-id="2a2c3-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="2a2c3-154">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında Merkezi Masaüstü yapılandırma** sayfasında, kopya **tek Sign-Out hizmeti URL'si** değer ve ardından yapıştırın **SSO oturum kapatma URL'si**metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="2a2c3-155">İçinde **ileti imzası doğrulama yöntemi** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="2a2c3-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="2a2c3-156">![İleti imzası doğrulama yöntemi](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "ileti imzası doğrulama yöntemi")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="2a2c3-157">Seçin **sertifika**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="2a2c3-158">Gelen **SSO sertifika** listesinde **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="2a2c3-159">İndirilen sertifika bir metin dosyası oluşturun, metin dosyasının içeriğini kopyalayın ve ardından yapıştırın **SSO sertifika** alan.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="2a2c3-160">Daha fazla ayrıntı için bkz: [ikili bir sertifika bir metin dosyasına dönüştürme](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="2a2c3-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="2a2c3-161">Seçin **SAMLv2 oturum açma sayfanız bir bağlantı görüntüler**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="2a2c3-162">Tıklatın **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-162">Click **Update**.</span></span>
10. <span data-ttu-id="2a2c3-163">Klasik Azure portalı, çoklu oturum açma yapılandırması onay seçin ve ardından **tam** kapatmak için **tek oturum yapılandırma üzerinde aktar** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="2a2c3-164">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="2a2c3-165">Kullanıcı sağlamayı Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2a2c3-165">Configure user provisioning</span></span>

<span data-ttu-id="2a2c3-166">AAD kullanıcıların oturum açabilmesi için bunların Merkezi Masaüstü uygulamaya sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="2a2c3-167">Bu bölümde, AAD kullanıcı hesaplarının Merkezi Masaüstü nasıl oluşturulacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="2a2c3-168">**Merkezi Masaüstü kullanıcı hesaplarına sağlamak için:**</span><span class="sxs-lookup"><span data-stu-id="2a2c3-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="2a2c3-169">Merkezi Masaüstü kiracınız için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="2a2c3-170">Git **kişiler \> iç üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="2a2c3-171">Tıklatın **iç üye eklemek**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="2a2c3-172">![Kişiler](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "kişiler")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="2a2c3-173">İçinde **yeni üyeler e-posta adresi** metin kutusuna, sağlamak istediğiniz ve ardından bir AAD hesabıyla yazın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="2a2c3-174">![E-posta adreslerini yeni üyeler](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "e-posta adreslerini yeni üyeler")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="2a2c3-175">Tıklatın **Ekle iç üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="2a2c3-176">![İç üye ekleme](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "iç üye ekleme")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2a2c3-177">Eklemiş olduğunuz kullanıcı hesabını etkinleştirmek için tıklatın için gereksinim duydukları onay bağlantısı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="2a2c3-178">Tüm diğer Merkezi Masaüstü kullanıcı hesabı oluşturma araçlarını kullanabilir veya API'ler sağlama AAD kullanıcı hesaplarına Merkezi Masaüstü tarafından sağlanan</span><span class="sxs-lookup"><span data-stu-id="2a2c3-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="2a2c3-179">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="2a2c3-179">Assign users</span></span>
<span data-ttu-id="2a2c3-180">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2a2c3-181">**Kullanıcılar için merkezi masaüstü atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="2a2c3-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="2a2c3-182">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2a2c3-183">Üzerinde **Merkezi Masaüstü** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2a2c3-184">![Kullanıcılar atama](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="2a2c3-185">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2a2c3-186">![Evet](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="2a2c3-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2a2c3-187">Çoklu oturum açma ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="2a2c3-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2a2c3-188">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2a2c3-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

