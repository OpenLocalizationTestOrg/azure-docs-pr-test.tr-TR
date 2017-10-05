---
title: "Öğretici: SAP HANA bulut platformu Azure Active Directory Tümleştirme | Microsoft Docs"
description: "SAP HANA bulut platformu Azure Active Directory ile çoklu oturum açma, otomatik sağlama ve daha fazlasını sağlamak için nasıl kullanılacağını öğrenin!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="221b3-103">Öğretici: SAP HANA Cloud Platform ile Azure Active Directory tümleştirme</span><span class="sxs-lookup"><span data-stu-id="221b3-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="221b3-104">Bu öğreticinin amacı, Azure ve SAP HANA bulut platformu tümleştirmesini göstermektir.</span><span class="sxs-lookup"><span data-stu-id="221b3-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="221b3-105">Bu öğreticide gösterilen senaryo, aşağıdaki öğeleri zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="221b3-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="221b3-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="221b3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="221b3-107">SAP HANA bulut platformu hesabı</span><span class="sxs-lookup"><span data-stu-id="221b3-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="221b3-108">Bu öğreticiyi tamamladıktan sonra SAP HANA bulut platformu için atanmış Azure AD kullanıcılarının uygulama kullanarak çoklu oturum açabilirsiniz [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="221b3-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="221b3-109">Kendi uygulamanızı dağıtmak veya çoklu oturum açma üzerinde test etmek için bir uygulama SAP HANA bulut platformu hesabınızda abone olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="221b3-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="221b3-110">Bu öğreticide, bir uygulama hesabında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="221b3-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="221b3-111">Bu öğreticide gösterilen senaryo, aşağıdaki yapı taşlarını oluşur:</span><span class="sxs-lookup"><span data-stu-id="221b3-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="221b3-112">SAP HANA bulut platformu için uygulama tümleştirmesini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="221b3-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="221b3-113">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="221b3-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="221b3-114">Bir kullanıcıya rol atama</span><span class="sxs-lookup"><span data-stu-id="221b3-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="221b3-115">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="221b3-115">Assigning users</span></span>

<span data-ttu-id="221b3-116">![Senaryo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="221b3-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="221b3-117">SAP HANA bulut platformu için uygulama tümleştirmesini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="221b3-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="221b3-118">Bu bölümün amacı, SAP HANA bulut platformu için uygulama tümleştirme sağlamak üzere nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="221b3-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="221b3-119">**SAP HANA bulut platformu için uygulama tümleştirmesini etkinleştirmek için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="221b3-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="221b3-120">Azure yönetim portalında sol gezinti bölmesinde, tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="221b3-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="221b3-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="221b3-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="221b3-122">Gelen **Directory** listesinde, directory tümleştirmesini etkinleştirmek istediğiniz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="221b3-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="221b3-123">Dizin görünümünde uygulamaları görünümü açmak için **uygulamaları** üst menüde.</span><span class="sxs-lookup"><span data-stu-id="221b3-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="221b3-124">![Uygulamaları](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="221b3-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="221b3-125">Tıklatın **Ekle** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="221b3-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="221b3-126">![Uygulama ekleme](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="221b3-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="221b3-127">Üzerinde **ne yapmak istiyorsunuz** iletişim kutusunda, tıklatın **Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="221b3-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="221b3-128">![Galeriden bir uygulama eklemek](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="221b3-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="221b3-129">İçinde **arama kutusu**, türü **SAP HANA bulut platformu**.</span><span class="sxs-lookup"><span data-stu-id="221b3-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="221b3-130">![Uygulama Galerisi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="221b3-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="221b3-131">Sonuçlar bölmesinde seçin **SAP HANA bulut platformu**ve ardından **tam** uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="221b3-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="221b3-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="221b3-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="221b3-133">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="221b3-133">Configure single sign-on</span></span>

<span data-ttu-id="221b3-134">Bu bölümün amacı kullanıcıların SAP HANA bulut platformu için kendi hesabıyla SAML protokolünü temel Federasyon kullanarak Azure AD kimlik doğrulaması sağlamak nasıl anahat sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="221b3-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="221b3-135">Bu yordam bir parçası olarak, SAP HANA bulut platformu kiracınız base-64 kodlanmış sertifika yüklemek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="221b3-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="221b3-136">Bu yordama bilmiyorsanız bkz [ikili bir sertifika bir metin dosyasına dönüştürme](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="221b3-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="221b3-137">**Çoklu oturum açma yapılandırmak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="221b3-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="221b3-138">Azure Klasik portalında üzerinde **SAP HANA bulut platformu** uygulama tümleştirmesi sayfasında, tıklatın **çoklu oturum açma özelliğini yapılandırın** açmak için **tek oturum yapılandırma üzerinde aktar** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="221b3-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="221b3-139">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="221b3-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="221b3-140">Üzerinde **SAP HANA bulut platformu için oturum açmasını nasıl istiyorsunuz** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="221b3-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="221b3-141">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="221b3-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="221b3-142">Farklı web tarayıcısı penceresinde https://account SAP HANA bulut platformu Pilot için oturum açma. \<yatay konak\>.ondemand.com/cockpit (örn: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="221b3-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="221b3-143">Tıklatın **güven** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="221b3-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="221b3-144">![Güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "güven")</span><span class="sxs-lookup"><span data-stu-id="221b3-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="221b3-145">Güven Yönetimi bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="221b3-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="221b3-146">![Meta veri alma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "meta verileri alma")</span><span class="sxs-lookup"><span data-stu-id="221b3-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="221b3-147">Tıklatın **yerel hizmet sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="221b3-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="221b3-148">SAP HANA bulut platformu meta veri dosyası indirmek için tıklayın **meta verileri alma**.</span><span class="sxs-lookup"><span data-stu-id="221b3-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="221b3-149">Azure Active Klasik Portalı'nda üzerinde **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları uygulayın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="221b3-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="221b3-150">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="221b3-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="221b3-151">İçinde **oturum üzerinde URL'si** metin kutusuna, türü URL kullanılan kullanıcılarınız tarafından oturumu açmak için **SAP HANA bulut platformu** uygulama.</span><span class="sxs-lookup"><span data-stu-id="221b3-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="221b3-152">SAP HANA bulut platformu uygulamanızda korumalı bir kaynağın hesap özgü URL'sidir.</span><span class="sxs-lookup"><span data-stu-id="221b3-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="221b3-153">URL aşağıdaki desenine dayanır: *https://\<applicationName\>\<accountName\>.\< Yatay konak\>.ondemand.com/\<yolu\_için\_korumalı\_kaynak\>*  (örn: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="221b3-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="221b3-154">Bu kullanıcının kimlik doğrulamasını gerektirir, SAP HANA bulut platformu uygulamanızda URL'dir.</span><span class="sxs-lookup"><span data-stu-id="221b3-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="221b3-155">İndirilen SAP HANA bulut platformu meta veri dosyasını açın ve ardından bulun **ns3:AssertionConsumerService** etiketi.</span><span class="sxs-lookup"><span data-stu-id="221b3-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="221b3-156">Değerini kopyalayın **konumu** özniteliği ve ardından yapıştırın **SAP HANA bulut platformu yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="221b3-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="221b3-157">Üzerinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırmak** meta verileriniz, indirme sayfasında, tıklatın **karşıdan meta veri**ve ardından dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="221b3-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="221b3-158">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="221b3-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="221b3-159">SAP HANA bulut platformu Pilot üzerinde içinde **yerel hizmet sağlayıcısı** bölümünde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="221b3-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="221b3-160">![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "güven Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="221b3-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="221b3-161">**Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="221b3-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="221b3-162">Olarak **yapılandırma türü**seçin **özel**.</span><span class="sxs-lookup"><span data-stu-id="221b3-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="221b3-163">Olarak **yerel sağlayıcı adı**, varsayılan değeri bırakın.</span><span class="sxs-lookup"><span data-stu-id="221b3-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="221b3-164">Oluşturmak için bir **imzalama anahtarı** ve **imzalama sertifikası** anahtar çifti, tıklatın **anahtar çifti oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="221b3-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="221b3-165">Olarak **asıl yayma**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="221b3-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="221b3-166">Olarak **zorla kimlik doğrulama**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="221b3-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="221b3-167">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="221b3-167">Click **Save**.</span></span>

9. <span data-ttu-id="221b3-168">Tıklatın **güvenilen kimlik sağlayıcısı** sekmesini ve ardından **güvenilen kimlik sağlayıcısı ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="221b3-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="221b3-169">![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "güven Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="221b3-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="221b3-170">Güvenilen kimlik sağlayıcıları listesini yönetmek için özel yapılandırma türü yerel hizmet sağlayıcısı bölümünde seçmiş olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="221b3-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="221b3-171">Varsayılan yapılandırma türü için düzenlenemeyen ve örtük güven SAP kimliği hizmetine sahip.</span><span class="sxs-lookup"><span data-stu-id="221b3-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="221b3-172">Hiçbiri için herhangi bir güven ayarı yok.</span><span class="sxs-lookup"><span data-stu-id="221b3-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="221b3-173">Tıklatın **genel** sekmesini ve ardından **Gözat** indirilen meta veri dosyasını karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="221b3-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="221b3-174">![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "güven Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="221b3-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="221b3-175">Meta veri dosyası, değerlerini karşıya sonra **çoklu oturum açma URL'si**, **çoklu oturum kapatma URL'si** ve **imzalama sertifikası** otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="221b3-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="221b3-176">**Öznitelikler** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="221b3-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="221b3-177">Üzerinde **öznitelikleri** sekmesinde, aşağıdaki adımı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="221b3-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="221b3-178">![Öznitelikleri](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="221b3-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="221b3-179">Tıklatın **Add Assertion-Based özniteliği**ve ardından aşağıdaki onaylama tabanlı öznitelikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="221b3-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="221b3-180">Onaylama işlemi özniteliği</span><span class="sxs-lookup"><span data-stu-id="221b3-180">Assertion Attribute</span></span> | <span data-ttu-id="221b3-181">Asıl özniteliği</span><span class="sxs-lookup"><span data-stu-id="221b3-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="221b3-182">http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/givenName</span><span class="sxs-lookup"><span data-stu-id="221b3-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="221b3-183">FirstName</span><span class="sxs-lookup"><span data-stu-id="221b3-183">firstname</span></span> |
    | <span data-ttu-id="221b3-184">http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/surname</span><span class="sxs-lookup"><span data-stu-id="221b3-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="221b3-185">Soyadı</span><span class="sxs-lookup"><span data-stu-id="221b3-185">lastname</span></span> |
    | <span data-ttu-id="221b3-186">http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="221b3-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="221b3-187">E-posta</span><span class="sxs-lookup"><span data-stu-id="221b3-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="221b3-188">Öznitelikleri yapılandırma nasıl HCP üzerinde uygulamaları geliştirilmiş, yani hangi öznitelikleri SAML yanıtta bekledikleri ve kod bu öznitelikte eriştiklerinde hangi adla (asıl özniteliği) bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="221b3-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="221b3-189">**Varsayılan özniteliği** ekran görüntüsünde yalnızca gösterim amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="221b3-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="221b3-190">İş senaryosu yapmak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="221b3-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="221b3-191">Adları ve değerleri için **asıl özniteliği** ekran görüntüsünde gösterilen uygulama nasıl geliştirilen bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="221b3-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="221b3-192">Uygulamanızın farklı eşlemeleri gerektirdiği mümkündür.</span><span class="sxs-lookup"><span data-stu-id="221b3-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="221b3-193">Azure Klasik portalında üzerinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırma** iletişim kutusunda sayfa, tek oturum açma yapılandırması onay seçin ve ardından **tam**.</span><span class="sxs-lookup"><span data-stu-id="221b3-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="221b3-194">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="221b3-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="221b3-195">Onaylama işlemi tabanlı grupları</span><span class="sxs-lookup"><span data-stu-id="221b3-195">Assertion-based groups</span></span>
<span data-ttu-id="221b3-196">İsteğe bağlı bir adım, Azure Active Directory kimlik sağlayıcısı için onaylama tabanlı grupları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="221b3-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="221b3-197">SAP HANA bulut platformunda gruplarını kullanarak dinamik olarak bir veya daha fazla kullanıcı, SAP HANA bulut platformu uygulamalarınızda SAML 2.0 onaylama özniteliklerinin değerlerini tarafından belirlenen bir veya daha fazla rol atamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="221b3-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="221b3-198">Onaylama işlemi öznitelik içeriyorsa, örneğin, "*sözleşme geçici =*", etkilenen tüm kullanıcılar grubuna eklenecek isteyebilirler"*geçici*".</span><span class="sxs-lookup"><span data-stu-id="221b3-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="221b3-199">Grup "*geçici*" SAP HANA bulut platformu hesabınızda dağıtılan bir veya daha fazla uygulamalardan bir veya daha fazla rol içerebilir.</span><span class="sxs-lookup"><span data-stu-id="221b3-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="221b3-200">Aynı anda çok sayıda kullanıcı uygulamalarının SAP HANA bulut platformu hesabınızda bir veya daha fazla rol atamak istiyorsanız onaylama tabanlı grupları kullanın.</span><span class="sxs-lookup"><span data-stu-id="221b3-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="221b3-201">Yalnızca tek veya küçük kullanıcı sayısı çok belirli rollere atamak istiyorsanız, bunları doğrudan atama öneririz "**yetkilerini**" SAP HANA bulut platformu Pilot sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="221b3-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="221b3-202">Bir kullanıcıya rol atama</span><span class="sxs-lookup"><span data-stu-id="221b3-202">Assign a role to a user</span></span>
<span data-ttu-id="221b3-203">SAP HANA bulut platformuna oturum Azure AD kullanıcıları etkinleştirmek için SAP HANA bulut platformu rollerinde onlara atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="221b3-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="221b3-204">**Bir kullanıcıya rol atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="221b3-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="221b3-205">Oturum, **SAP HANA bulut platformu** Pilot.</span><span class="sxs-lookup"><span data-stu-id="221b3-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="221b3-206">Aşağıdakileri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="221b3-206">Perform the following:</span></span>
   
   <span data-ttu-id="221b3-207">![Yetkilerini](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "yetkileri değiştirme")</span><span class="sxs-lookup"><span data-stu-id="221b3-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="221b3-208">Tıklatın **yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="221b3-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="221b3-209">Tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="221b3-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="221b3-210">İçinde **kullanıcı** metin kutusuna, kullanıcının e-posta adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="221b3-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="221b3-211">Tıklatın **atamak** kullanıcı role atamak için.</span><span class="sxs-lookup"><span data-stu-id="221b3-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="221b3-212">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="221b3-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="221b3-213">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="221b3-213">Assign users</span></span>
<span data-ttu-id="221b3-214">Yapılandırmanızı test etmek için uygulama erişimi atayarak kullanarak izin vermek istediğiniz Azure AD kullanıcılarının vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="221b3-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="221b3-215">**SAP HANA bulut platformu için kullanıcılara atamak için aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="221b3-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="221b3-216">Klasik Azure portalında bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="221b3-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="221b3-217">Üzerinde **SAP HANA bulut platformu** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="221b3-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="221b3-218">![Kullanıcılar atama](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="221b3-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="221b3-219">Test kullanıcınız seçin, **atamak**ve ardından **Evet** , atama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="221b3-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="221b3-220">![Evet](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="221b3-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="221b3-221">SSO ayarlarınızı test etmek isterseniz, erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="221b3-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="221b3-222">Erişim paneli hakkında daha fazla ayrıntı için bkz: [erişim Paneli'ne giriş](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="221b3-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

