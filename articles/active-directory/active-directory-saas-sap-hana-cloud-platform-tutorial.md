---
title: "Öğretici: SAP HANA bulut platformu Azure Active Directory Tümleştirme | Microsoft Docs"
description: "Azure Active Directory tooenable ile toouse SAP HANA bulut platformu nasıl tek oturum açma, otomatik sağlama ve daha fazlasını öğrenin!"
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
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="49e3a-103">Öğretici: SAP HANA Cloud Platform ile Azure Active Directory tümleştirme</span><span class="sxs-lookup"><span data-stu-id="49e3a-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="49e3a-104">Merhaba amacı Bu öğretici, Azure ve SAP HANA bulut platformu tooshow hello tümleştirme ' dir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="49e3a-105">Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="49e3a-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="49e3a-106">Geçerli bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="49e3a-106">A valid Azure subscription</span></span>
* <span data-ttu-id="49e3a-107">SAP HANA bulut platformu hesabı</span><span class="sxs-lookup"><span data-stu-id="49e3a-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="49e3a-108">Bu öğreticiyi tamamladıktan sonra Azure AD kullanıcılarının atamış HANA bulut platformu olacaktır tooSAP mümkün toosingle oturum hello kullanarak hello uygulamasına hello [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49e3a-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="49e3a-109">Hesap tootest tek oturum açma, SAP HANA bulut platformunda tooan uygulama abone veya toodeploy kendi uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="49e3a-110">Bu öğreticide, bir uygulama hello hesabında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="49e3a-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="49e3a-111">Bu öğreticide gösterilen hello senaryo yapı taşları aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="49e3a-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="49e3a-112">Merhaba uygulama tümleştirmesi SAP HANA bulut platformu için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="49e3a-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="49e3a-113">Çoklu oturum açma (SSO) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49e3a-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="49e3a-114">Bir rol tooa kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="49e3a-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="49e3a-115">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="49e3a-115">Assigning users</span></span>

<span data-ttu-id="49e3a-116">![Senaryo](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "senaryosu")</span><span class="sxs-lookup"><span data-stu-id="49e3a-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="49e3a-117">Merhaba uygulama tümleştirmesi SAP HANA bulut platformu için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="49e3a-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="49e3a-118">Bu bölümde Hello amacı olan toooutline nasıl tooenable hello uygulama tümleştirmesi için SAP HANA bulut platformu.</span><span class="sxs-lookup"><span data-stu-id="49e3a-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="49e3a-119">**SAP HANA bulut platformu için tooenable hello uygulama tümleştirmesi hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="49e3a-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="49e3a-120">Merhaba Sol Gezinti Bölmesi ' hello Azure Yönetim Portalı'ı tıklatın **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="49e3a-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="49e3a-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="49e3a-122">Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="49e3a-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="49e3a-123">Merhaba dizin görünümünde tooopen hello uygulamaları Görüntüle'yi tıklatın **uygulamaları** hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="49e3a-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="49e3a-124">![Uygulamaları](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "uygulamalar")</span><span class="sxs-lookup"><span data-stu-id="49e3a-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="49e3a-125">Tıklatın **Ekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="49e3a-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="49e3a-126">![Uygulama ekleme](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="49e3a-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="49e3a-127">Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **hello Galeriden bir uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="49e3a-128">![Galeriden bir uygulama eklemek](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Galeriden bir uygulama ekleme")</span><span class="sxs-lookup"><span data-stu-id="49e3a-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="49e3a-129">Merhaba, **arama kutusu**, türü **SAP HANA bulut platformu**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="49e3a-130">![Uygulama Galerisi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "uygulama Galerisi")</span><span class="sxs-lookup"><span data-stu-id="49e3a-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="49e3a-131">Merhaba sonuçlar bölmesinde seçin **SAP HANA bulut platformu**ve ardından **tam** tooadd Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="49e3a-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="49e3a-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="49e3a-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="49e3a-133">Çoklu oturum açmayı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="49e3a-133">Configure single sign-on</span></span>

<span data-ttu-id="49e3a-134">Bu bölümde Hello amacı nasıl hello SAML protokolünü kullanarak Federasyon Azure AD'de hesabıyla tooenable kullanıcılar tooauthenticate tooSAP HANA bulut platformu temel toooutline ' dir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="49e3a-135">Bu yordam bir parçası, gerekli tooupload base-64 kodlanmış sertifika tooyour SAP HANA bulut platformu Kiracı olur.</span><span class="sxs-lookup"><span data-stu-id="49e3a-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="49e3a-136">Bu yordama bilmiyorsanız bkz [nasıl tooconvert bir ikili sertifika bir metin dosyasına](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="49e3a-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="49e3a-137">**tooconfigure çoklu oturum açma, hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="49e3a-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="49e3a-138">Merhaba hello üzerinde Klasik Azure Portalı'nda **SAP HANA bulut platformu** uygulama tümleştirme sayfası, tıklatın **çoklu oturum açma özelliğini yapılandırın** tooopen hello **yapılandırma çoklu oturum açma**iletişim.</span><span class="sxs-lookup"><span data-stu-id="49e3a-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="49e3a-139">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="49e3a-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="49e3a-140">Merhaba üzerinde **nasıl kullanıcılar toosign tooSAP HANA bulut platformu üzerinde gibi yaptığınız** sayfasında, **Microsoft Azure AD çoklu oturum açma**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="49e3a-141">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="49e3a-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="49e3a-142">Farklı web tarayıcısı penceresinde toohello SAP HANA bulut platformu Pilot https://account adresindeki oturum. \<yatay konak\>.ondemand.com/cockpit (örn: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="49e3a-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="49e3a-143">Merhaba tıklatın **güven** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="49e3a-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="49e3a-144">![Güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "güven")</span><span class="sxs-lookup"><span data-stu-id="49e3a-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="49e3a-145">Güven Yönetimi bölümünde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="49e3a-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="49e3a-146">![Meta veri alma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "meta verileri alma")</span><span class="sxs-lookup"><span data-stu-id="49e3a-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="49e3a-147">Merhaba tıklatın **yerel hizmet sağlayıcısı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="49e3a-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="49e3a-148">toodownload hello SAP HANA bulut platformu meta veri dosyası, tıklatın **meta verileri alma**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="49e3a-149">Merhaba üzerinde hello Azure Active Klasik Portalı'nda **uygulama URL'sini Yapılandır** sayfasında, aşağıdaki adımları hello gerçekleştirmek ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="49e3a-150">![Uygulama URL'sini Yapılandır](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "uygulama URL'sini yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="49e3a-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="49e3a-151">Merhaba, **oturum üzerinde URL'si** metin kutusuna,, kullanıcıların toosign tarafından kullanılan türü hello URL, **SAP HANA bulut platformu** uygulama.</span><span class="sxs-lookup"><span data-stu-id="49e3a-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="49e3a-152">SAP HANA bulut platformu uygulamanızda korumalı bir kaynağın hello hesaba özel URL budur.</span><span class="sxs-lookup"><span data-stu-id="49e3a-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="49e3a-153">Merhaba URL deseni takip hello üzerinde dayanır: *https://\<applicationName\>\<accountName\>.\< Yatay konak\>.ondemand.com/\<yolu\_için\_korumalı\_kaynak\>*  (örn: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="49e3a-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="49e3a-154">SAP HANA bulut platformu uygulamanızda hello kullanıcı tooauthenticate gerektirir hello URL budur.</span><span class="sxs-lookup"><span data-stu-id="49e3a-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="49e3a-155">İndirilen hello SAP HANA bulut platformu meta veri dosyasını açın ve hello bulun **ns3:AssertionConsumerService** etiketi.</span><span class="sxs-lookup"><span data-stu-id="49e3a-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="49e3a-156">Merhaba Hello değerini kopyalayın **konumu** özniteliği ve hello yapıştırma **SAP HANA bulut platformu yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="49e3a-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="49e3a-157">Merhaba üzerinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırmak** sayfası, toodownload meta verileriniz tıklatın **karşıdan meta veri**ve hello dosyayı bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="49e3a-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="49e3a-158">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="49e3a-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="49e3a-159">SAP HANA bulut platformu Pilot hello hello üzerinde **yerel hizmet sağlayıcısı** bölümünde, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="49e3a-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="49e3a-160">![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "güven Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="49e3a-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="49e3a-161">**Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="49e3a-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="49e3a-162">Olarak **yapılandırma türü**seçin **özel**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="49e3a-163">Olarak **yerel sağlayıcı adı**, hello varsayılan değeri bırakın.</span><span class="sxs-lookup"><span data-stu-id="49e3a-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="49e3a-164">toogenerate bir **imzalama anahtarı** ve **imzalama sertifikası** anahtar çifti, tıklatın **anahtar çifti oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="49e3a-165">Olarak **asıl yayma**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="49e3a-166">Olarak **zorla kimlik doğrulama**seçin **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="49e3a-167">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="49e3a-167">Click **Save**.</span></span>

9. <span data-ttu-id="49e3a-168">Merhaba tıklatın **güvenilen kimlik sağlayıcısı** sekmesini ve ardından **güvenilen kimlik sağlayıcısı ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="49e3a-169">![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "güven Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="49e3a-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="49e3a-170">Güvenilen kimlik sağlayıcıları toomanage hello listesi, hello yerel hizmet sağlayıcısı bölüm hello özel yapılandırma türü seçilen toohave gerekir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="49e3a-171">Varsayılan yapılandırma türü için düzenlenemeyen ve örtük güven toohello SAP ID hizmeti sahip.</span><span class="sxs-lookup"><span data-stu-id="49e3a-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="49e3a-172">Hiçbiri için herhangi bir güven ayarı yok.</span><span class="sxs-lookup"><span data-stu-id="49e3a-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="49e3a-173">Hello tıklatın **genel** sekmesini ve ardından **Gözat** tooupload hello meta veri dosyası indirilir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="49e3a-174">![Yönetim güven](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "güven Yönetimi")</span><span class="sxs-lookup"><span data-stu-id="49e3a-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="49e3a-175">Merhaba değerleri Hello meta veri dosyası karşıya yüklemeden sonra **çoklu oturum açma URL'si**, **çoklu oturum kapatma URL'si** ve **imzalama sertifikası** otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="49e3a-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="49e3a-176">Merhaba tıklatın **öznitelikleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="49e3a-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="49e3a-177">Merhaba üzerinde **öznitelikleri** sekmesinde, adım aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="49e3a-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="49e3a-178">![Öznitelikleri](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "öznitelikleri")</span><span class="sxs-lookup"><span data-stu-id="49e3a-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="49e3a-179">Tıklatın **Add Assertion-Based özniteliği**ve ardından onaylama tabanlı öznitelikler aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="49e3a-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="49e3a-180">Onaylama işlemi özniteliği</span><span class="sxs-lookup"><span data-stu-id="49e3a-180">Assertion Attribute</span></span> | <span data-ttu-id="49e3a-181">Asıl özniteliği</span><span class="sxs-lookup"><span data-stu-id="49e3a-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="49e3a-182">http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/givenName</span><span class="sxs-lookup"><span data-stu-id="49e3a-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="49e3a-183">FirstName</span><span class="sxs-lookup"><span data-stu-id="49e3a-183">firstname</span></span> |
    | <span data-ttu-id="49e3a-184">http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/surname</span><span class="sxs-lookup"><span data-stu-id="49e3a-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="49e3a-185">Soyadı</span><span class="sxs-lookup"><span data-stu-id="49e3a-185">lastname</span></span> |
    | <span data-ttu-id="49e3a-186">http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="49e3a-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="49e3a-187">E-posta</span><span class="sxs-lookup"><span data-stu-id="49e3a-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="49e3a-188">Merhaba öznitelikleri Hello yapılandırmasını nasıl hello uygulamaları HCP üzerinde geliştirilmiş, yani hangi öznitelikleri hello SAML yanıtını bekledikleri ve bu öznitelik hello kodda eriştiklerinde hangi adla (asıl özniteliği) bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="49e3a-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="49e3a-189">Merhaba **varsayılan özniteliği** hello ekran yalnızca gösterim amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="49e3a-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="49e3a-190">Bu gerekli toomake hello senaryosu iş.</span><span class="sxs-lookup"><span data-stu-id="49e3a-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="49e3a-191">Merhaba adlarını ve değerlerini **asıl özniteliği** hello gösterildiği ekran bağımlı nasıl Merhaba uygulaması geliştirmiştir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="49e3a-192">Uygulamanızın farklı eşlemeleri gerektirdiği mümkündür.</span><span class="sxs-lookup"><span data-stu-id="49e3a-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="49e3a-193">Merhaba hello üzerinde Klasik Azure portalı içinde **çoklu oturum açma sırasında SAP HANA bulut platformu yapılandırma** iletişim kutusunda sayfa, hello tek oturum açma yapılandırması onay seçin ve ardından **tam**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="49e3a-194">![Çoklu oturum açma yapılandırma](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "çoklu oturum açmayı yapılandırın")</span><span class="sxs-lookup"><span data-stu-id="49e3a-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="49e3a-195">Onaylama işlemi tabanlı grupları</span><span class="sxs-lookup"><span data-stu-id="49e3a-195">Assertion-based groups</span></span>
<span data-ttu-id="49e3a-196">İsteğe bağlı bir adım, Azure Active Directory kimlik sağlayıcısı için onaylama tabanlı grupları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49e3a-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="49e3a-197">SAP HANA bulut platformunda gruplarını kullanarak toodynamically Ata bir sağlar veya daha fazla kullanıcı tooone ya da daha fazla roller, SAP HANA bulut platformu uygulamalarınızda belirlediği hello SAML özniteliklerinin değerlerini 2.0 onaylama.</span><span class="sxs-lookup"><span data-stu-id="49e3a-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="49e3a-198">Örneğin, hello onaylama hello özniteliği varsa, "*sözleşme geçici =*", tüm etkilenen kullanıcılar toobe eklenen toohello grubu isteyebilirsiniz"*geçici*".</span><span class="sxs-lookup"><span data-stu-id="49e3a-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="49e3a-199">Merhaba grup "*geçici*" SAP HANA bulut platformu hesabınızda dağıtılan bir veya daha fazla uygulamalardan bir veya daha fazla rol içerebilir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="49e3a-200">Toosimultaneously istediğinizde onaylama tabanlı gruplar kullanılması birçok kullanıcılar tooone veya SAP HANA bulut platformu hesabınızı uygulamaların daha fazla rolü atayın.</span><span class="sxs-lookup"><span data-stu-id="49e3a-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="49e3a-201">Tooassign kullanıcılar toospecific rolleri, yalnızca tek veya küçük sayıda istiyorsanız, bunları doğrudan hello atama öneririz "**yetkilerini**" Merhaba SAP HANA bulut platformu Pilot sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="49e3a-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="49e3a-202">Rol tooa kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="49e3a-202">Assign a role tooa user</span></span>
<span data-ttu-id="49e3a-203">SAP HANA bulut platformu içine sipariş tooenable Azure AD kullanıcıların toolog içinde hello SAP HANA bulut platformu toothem rollerinde atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="49e3a-204">**bir rol tooa kullanıcı tooassign hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="49e3a-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="49e3a-205">İçinde tooyour oturum **SAP HANA bulut platformu** Pilot.</span><span class="sxs-lookup"><span data-stu-id="49e3a-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="49e3a-206">Merhaba aşağıdakileri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="49e3a-206">Perform hello following:</span></span>
   
   <span data-ttu-id="49e3a-207">![Yetkilerini](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "yetkileri değiştirme")</span><span class="sxs-lookup"><span data-stu-id="49e3a-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="49e3a-208">Tıklatın **yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="49e3a-209">Merhaba tıklatın **kullanıcılar** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="49e3a-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="49e3a-210">Merhaba, **kullanıcı** metin kutusuna, türü hello kullanıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="49e3a-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="49e3a-211">Tıklatın **atamak** tooassign hello kullanıcı tooa rolü.</span><span class="sxs-lookup"><span data-stu-id="49e3a-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="49e3a-212">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="49e3a-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="49e3a-213">Kullanıcılar atama</span><span class="sxs-lookup"><span data-stu-id="49e3a-213">Assign users</span></span>
<span data-ttu-id="49e3a-214">tootest yapılandırmanıza, uygulama erişim tooit atayarak kullanarak tooallow istediğiniz toogrant hello Azure AD kullanıcıları gerekir.</span><span class="sxs-lookup"><span data-stu-id="49e3a-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="49e3a-215">**tooassign kullanıcılar tooSAP HANA bulut platformu hello aşağıdaki adımları gerçekleştirin:**</span><span class="sxs-lookup"><span data-stu-id="49e3a-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="49e3a-216">Hello Klasik Azure portalı, bir test hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49e3a-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="49e3a-217">Hello üzerinde **SAP HANA bulut platformu** uygulama tümleştirme sayfasını tıklatın **kullanıcı atama**.</span><span class="sxs-lookup"><span data-stu-id="49e3a-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="49e3a-218">![Kullanıcılar atama](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "kullanıcı atama")</span><span class="sxs-lookup"><span data-stu-id="49e3a-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="49e3a-219">Test kullanıcınız seçin, **atamak**ve ardından **Evet** tooconfirm, atama.</span><span class="sxs-lookup"><span data-stu-id="49e3a-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="49e3a-220">![Evet](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Evet")</span><span class="sxs-lookup"><span data-stu-id="49e3a-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="49e3a-221">SSO ayarlarınızı tootest istiyorsanız hello erişim paneli açın.</span><span class="sxs-lookup"><span data-stu-id="49e3a-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="49e3a-222">Merhaba erişim paneli hakkında daha fazla ayrıntı için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49e3a-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

