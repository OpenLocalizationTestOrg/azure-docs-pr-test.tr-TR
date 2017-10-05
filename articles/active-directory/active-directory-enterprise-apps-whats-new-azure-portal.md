---
title: "Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikler | Microsoft Docs"
description: "Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikleri öğrenin."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: asteen
ms.reviewer: asteen
ms.openlocfilehash: 0c32a6719292aa903aa32dfdc4a31114e7a28346
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="whats-new-in-enterprise-application-management-in-azure-active-directory"></a><span data-ttu-id="6c55a-103">Azure Active Directory'de Kurumsal Uygulama Yönetimi'nde yenilikler</span><span class="sxs-lookup"><span data-stu-id="6c55a-103">What's new in Enterprise Application management in Azure Active Directory</span></span> 

<span data-ttu-id="6c55a-104">Azure Active Directory (Azure AD) ile yeni özellikler ve yetenekler yöneten uygulamalar daha basit ve verimli hale getirmek için kurumsal uygulama yönetimi araçları Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="6c55a-104">Azure Active Directory (Azure AD) has enhanced enterprise application management tools, with new features and capabilities to make managing apps simpler and efficient.</span></span>

<span data-ttu-id="6c55a-105">Aşağıdaki Azure AD'de için bazı iyileştirmeler olan [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c55a-105">Following are some of the enhancements for Azure AD in the [Azure portal](https://portal.azure.com).</span></span>

- <span data-ttu-id="6c55a-106">Geliştirilmiş uygulama Galerisi, Basitleştirilmiş uygulama oluşturma modeliyle deneyimi ve için kullanılan tüm uygulama türleri için destek.</span><span class="sxs-lookup"><span data-stu-id="6c55a-106">An improved application gallery experience, with a simplified application creation model and support for all the application types that you’re used to.</span></span> 
- <span data-ttu-id="6c55a-107">Yardımcı olabilecek bir yeni hızlı başlangıç deneyimi alma, uygulamanızın bir pilot adımıdır.</span><span class="sxs-lookup"><span data-stu-id="6c55a-107">A brand-new quick start experience that can help you get going with a pilot of your application.</span></span> 
- <span data-ttu-id="6c55a-108">Self Servis ilkeleri yalnızca birkaç tıklama ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6c55a-108">Configure self-service policies with just a few clicks.</span></span> 
- <span data-ttu-id="6c55a-109">Uygulama proxy'si geliştirmeleri tek oturum açma yapılandırması ve yanıtlar daha önce elde size izin vererek, kendi uygulama deneyimleri duruma getirin.</span><span class="sxs-lookup"><span data-stu-id="6c55a-109">Improvements to application proxy, single sign-on configuration, and bring your own application experiences, allowing you to get more done than before.</span></span>

## <a name="improvements-to-the-azure-active-directory-application-gallery"></a><span data-ttu-id="6c55a-110">Azure Active Directory Uygulama galerisinde geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="6c55a-110">Improvements to the Azure Active Directory Application Gallery</span></span>

<span data-ttu-id="6c55a-111">Gelen olup, sık kullanılan uygulamalar eklemek [uygulama Galerisi](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), buluta genişletme özel uygulamalar veya yeni uygulamalar geliştirme.</span><span class="sxs-lookup"><span data-stu-id="6c55a-111">Add your favorite applications whether they are from the [application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), custom applications you’re extending to the cloud, or new applications you’re developing.</span></span>  <span data-ttu-id="6c55a-112">Bu yeni deneyim, başlayabiliriz tıklayarak **Ekle** üzerinde **kurumsal uygulamalar** genel bakış veya **tüm uygulamaları** dikey pencereleri.</span><span class="sxs-lookup"><span data-stu-id="6c55a-112">You can get started with this new experience by clicking **Add** on the **Enterprise Applications** overview or **All applications** blades.</span></span>
 
  ![Bir uygulama ekleme](./media/active-directory-enterprise-apps-whats-new-azure-portal/01.png)

<span data-ttu-id="6c55a-114">Bir kez Galerisi'nde kullanıcı sağlamayı destekleyen tüm bizim öne çıkan uygulamaları Ön Orta görüntülendiğini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-114">Once in the gallery, you’ll see all our featured applications which support user provisioning displayed front-and-center.</span></span>  <span data-ttu-id="6c55a-115">İlgilendiğiniz uygulamaları incelemek için farklı kategoriler her türlü göz atabilir veya hızlı bir şekilde tümleştirmek istediğiniz uygulamaları bulmak için arama deneyimini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-115">You can browse all sorts of different categories to drill into the applications you care about, or you can use the search experience to rapidly find the applications you want to integrate.</span></span>

  ![Uygulama Galerisi](./media/active-directory-enterprise-apps-whats-new-azure-portal/02.png)

## <a name="add-custom-applications-from-one-place"></a><span data-ttu-id="6c55a-117">Tek bir yerden özel uygulamalar ekleme</span><span class="sxs-lookup"><span data-stu-id="6c55a-117">Add custom applications from one place</span></span>

<span data-ttu-id="6c55a-118">Önceden tümleştirilmiş uygulamaların Galeriden ekleme ek olarak, tüm özel uygulama yapılandırması için Klasik Yönetim Portalı'nda kullandığınız karşılaştığında şimdi yeni Portalı'nda mümkündür.</span><span class="sxs-lookup"><span data-stu-id="6c55a-118">In addition to adding pre-integrated applications from the gallery, all the custom application configuration experiences that you were used to in the classic management portal are now possible in the new portal.</span></span> <span data-ttu-id="6c55a-119">Kullanılıp parolanızı veya Federasyon SSO uygulaması tümleştirme uygulaması proxy'si kullanarak şirket içi bir uygulamadan genişletme veya Uygulama Kayıt Defteri'ni kullanarak yeni bir uygulama oluşturma, için tüm bu tek bir yerden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-119">Whether you are extending an application from on-premises using the application proxy, integrating your own password or federated SSO application, or creating a brand-new application using the application registry, you can get to it all from this one single place.</span></span>

  ![Kendi uygulama ekleme](./media/active-directory-enterprise-apps-whats-new-azure-portal/03.png)

 
<span data-ttu-id="6c55a-121">**Kendi uygulamanızı ekleme başlamak için**:</span><span class="sxs-lookup"><span data-stu-id="6c55a-121">**To get started adding your own application**:</span></span>

1. <span data-ttu-id="6c55a-122">Tıklatın **kendi bağlantısı eklemek** üst uygulama Galerisi.</span><span class="sxs-lookup"><span data-stu-id="6c55a-122">Click the **add your own link** at the top of the application gallery.</span></span> 
2. <span data-ttu-id="6c55a-123">Önünde iki seçenek görürsünüz: **var olan bir uygulamayı dağıtmak** veya **yeni bir uygulama geliştirme**.</span><span class="sxs-lookup"><span data-stu-id="6c55a-123">You’ll see two options in front of you: **deploy an existing application** or **develop a new application**.</span></span> <span data-ttu-id="6c55a-124">İçin okumaya iki seçenek ve bunları nasıl kullanacağınızı arasındaki farkı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6c55a-124">Read on to learn the difference between the two options and how to use them.</span></span>

### <a name="deploying-existing-applications"></a><span data-ttu-id="6c55a-125">Var olan uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="6c55a-125">Deploying existing applications</span></span>

1. <span data-ttu-id="6c55a-126">Zaten çalışan bir uygulama aldınız ve yalnızca üzerinde Azure AD çoklu oturum şekilde entegre veya sağlama, seçmek istediğiniz **var olan bir uygulamayı dağıtmak** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6c55a-126">If you’ve got an application running already and just want to integrate it into Azure AD for single-sign on or provisioning, choose the **Deploy an existing application** option.</span></span> <span data-ttu-id="6c55a-127">Uygulamanız için bir ad seçin, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6c55a-127">Pick a name for your application, click **Add**.</span></span>
2. <span data-ttu-id="6c55a-128">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="6c55a-128">That's it!</span></span> <span data-ttu-id="6c55a-129">Uygulamanızı Önden ile ilgili tüm ayrıntıları öğrenmek gereksinimi yerine, yeni uygulamanızı sol menünüzden gezinme ve herhangi bir zamanda, istediğiniz uygulamaya yapılandırarak işleyişi şimdi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-129">Instead of needing to know all the details about your application up front, you can now set up how your new application works by navigating through the left menu and configuring the application to your liking at any time.</span></span>

  ![Tek bir tıklatmayla var olan bir uygulama ekleme](./media/active-directory-enterprise-apps-whats-new-azure-portal/04.png)
 
### <a name="developing-new-applications"></a><span data-ttu-id="6c55a-131">Yeni uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="6c55a-131">Developing new applications</span></span>

1. <span data-ttu-id="6c55a-132">Yeni bir uygulama geliştiriyorsanız, uygulama kayıt defterine Galeriden sağ almanız için kolay bir yol vardır:</span><span class="sxs-lookup"><span data-stu-id="6c55a-132">If you’re developing a new application, there's an easy way for you to get to the Application Registry right from the gallery:</span></span>
2. <span data-ttu-id="6c55a-133">Tıklayın **kendi eklemek** uygulama Galerisi, select seçeneğinden **varolan uygulama geliştirme** seçim ve uygulama Ekle deneyimi sağdan hızlı bir bağlantı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-133">Click on the **add your own** option from the Application Gallery, select the **develop an existing application** choice, and you’ll see a quick link right to the application add experience.</span></span>

  ![Birkaç tıklama ile yeni geliştirilen bir uygulama ekleme](./media/active-directory-enterprise-apps-whats-new-azure-portal/05.png)


>[!NOTE]
><span data-ttu-id="6c55a-135">Uygulama kayıt defterini kullanarak bir uygulama ekledikten sonra bunu burada erişim ilkelerini yeni uygulamanız için çoklu oturum açma yapılandırmanıza ve yönetmenize mümkün olacaktır kurumsal uygulamalar listesinde görünmesi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-135">Once you add an application using the Application Registry, you’ll see it show up in the list of Enterprise Applications where you’ll be able to configure single sign-on and manage access policies for your new application.</span></span>

  ![Kuruluş uygulamaları altında yeni uygulamanıza erişimi yönetme](./media/active-directory-enterprise-apps-whats-new-azure-portal/06.png)


## <a name="quick-start-get-going-with-your-new-application-right-away"></a><span data-ttu-id="6c55a-137">Hızlı Başlangıç: yeni uygulamanızla birlikte hemen kullanmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="6c55a-137">Quick start: Get going with your new application right away</span></span> 

<span data-ttu-id="6c55a-138">Bir uygulama, önceden tümleştirilmiş veya kendi uygulamanızı ekledikten sonra yeni uygulamalar deneyimi hızla topraklanmış almak için özel bir hızlı başlangıç deneyimi oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="6c55a-138">After you’ve added an application, whether it be pre-integrated or your own app, we’ve created a tailored quick-start experience to get you grounded in the new applications experience quickly.</span></span> <span data-ttu-id="6c55a-139">Her seçenek sistematik olarak izlerseniz, biz, kullanıcı Arabirimi aracılığıyla yol ve yeni uygulamanızın bir pilot mümkün olan en kısa sürede yapmalarını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6c55a-139">If you follow each option systematically, we’ll walk you through the UI and show you how to get going with a pilot of your new application as quickly as possible.</span></span> 
 
  ![Deneyimi yeni uygulamalar Hızlı Başlat](./media/active-directory-enterprise-apps-whats-new-azure-portal/07.png)

 <span data-ttu-id="6c55a-141">Tıklayarak herhangi bir zamanda ve herhangi bir uygulama için yeni Bu hızlı başlangıç deneyimi ziyaret edebilirsiniz **Hızlı Başlangıç** uygulama sol gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="6c55a-141">You can visit this new quick start experience at any time, and for any application, by clicking on **Quick start** from the application left navigation menu.</span></span>


## <a name="updated-application-proxy-configuration"></a><span data-ttu-id="6c55a-142">Güncelleştirilmiş uygulama proxy yapılandırması</span><span class="sxs-lookup"><span data-stu-id="6c55a-142">Updated application proxy configuration</span></span>
<span data-ttu-id="6c55a-143">Artık, şirket içi ortamınızda say eklediğiniz yeni uygulamalardan biri şimdi çalışıyor ve Azure AD ile tümleştirmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-143">Now, let’s say one of the new applications you added is running in your on-premises environment and you want to integrate it with Azure AD.</span></span>  <span data-ttu-id="6c55a-144">Yeni uygulama yapılandırma deneyimi hakkında harika yeni özelliklerinden biri yeni Azure AD portalı, uygulamanın oturum açma modundan uygulama proxy yapılandırmasını bölerek, şimdi kolayca parola SSO açmasıdır veya Federasyon şirket ağınızda birden çok uygulama örneğini oluşturmak zorunda kalmadan buluta sağ çalışan uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="6c55a-144">One of the cool new things about the new application configuration experience in the new Azure AD portal is that by splitting the application’s sign-on mode from its application proxy configuration, you can now easily expose password SSO or federated applications that are running in your corporate network right to the cloud, without having to create multiple instances of the application.</span></span>

<span data-ttu-id="6c55a-145">Buna ek olarak, şimdi de, yerel Windows kimlik doğrulama deneyimleri destekleyen uygulamalar da dahil olmak üzere yeni portalı, Azure AD uygulama proxy'si sağa ile kullanılmak üzere eklediğiniz yeni uygulamalardan herhangi biri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-145">In addition to this, you can now also configure any of the new applications you’ve added for use with the Azure AD Application Proxy right from the new portal, including applications which support native Windows authentication experiences.</span></span>

  ![Oturum açma tümleşik Windows kimlik doğrulaması seçeneği kullanmak için uygulamayı yapılandırma](./media/active-directory-enterprise-apps-whats-new-azure-portal/08.png)
 

<span data-ttu-id="6c55a-147">Uygulama Ara sunucusu ile bir yerel Windows kimlik doğrulama uygulaması yapılandırmaya başlamak için:</span><span class="sxs-lookup"><span data-stu-id="6c55a-147">To get started configuring a native Windows authentication application with the Application Proxy:</span></span>
1. <span data-ttu-id="6c55a-148">Üzerinde çoklu oturum açma Gezinti öğesi'ı tıklatın ve seçin **tümleşik Windows kimlik doğrulaması** oturum açma ayarlar dikey penceresinden ve, istediğiniz ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6c55a-148">Click on the Single sign-on navigation item and choose **Integrated Windows Authentication** from the sign-on settings blade and configure the settings to your liking.</span></span>
2. <span data-ttu-id="6c55a-149">Bu yeni kimlik doğrulama modları destekleyen en üstünde, şimdi de güvenli uç noktaları kuruluşunuz içinde çalışan uygulamaları desteklemek için özel etki alanlarını sertifikaları karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-149">On top of supporting these new authentication modes, you can now also upload certificates from custom domains to support applications running on secure endpoints within your organization.</span></span>  
 
   ![Uygulama Ara sunucusu ile kullanılacak bir sertifika karşıya yükleniyor](./media/active-directory-enterprise-apps-whats-new-azure-portal/09.png)

3. <span data-ttu-id="6c55a-151">Sık kullanılan şirket içi uygulamanız için yeni bir sertifika yüklemek için tıklayın **uygulama proxy'si** seçeneği sol gezinti menüsünde, tıklatın **sertifika** Seçici ve şifrelemek için kullanabileceğiniz bir sertifika dosyası istekleri bizim bulut uç noktasından uygulamanızı karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="6c55a-151">To upload a new certificate for your favorite on-premises application, click on the **Application proxy** option from the left navigation menu, click the **Certificate** selector, and upload a certificate file we can use to encrypt requests from our cloud endpoint to your application.</span></span>

## <a name="advanced-federated-single-sign-on-configuration"></a><span data-ttu-id="6c55a-152">Federasyon tek oturum açma Gelişmiş Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c55a-152">Advanced federated single sign-on configuration</span></span>

<span data-ttu-id="6c55a-153">Bu Federasyon uygulamalarına bugün kullananlar vardır birçok yeni özellik SAML tabanlı oturum açma yapılandırma dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="6c55a-153">For those of you using federated applications today, there are many new features in the SAML-based sign-on configuration blade.</span></span> <span data-ttu-id="6c55a-154">İle başlamak artık tam olarak özelleştirmek, eklemek, kaldırmak ve SAML belirteçleri Taleplerde olarak verilen varolan kullanıcı öznitelikleri eşlemek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-154">To start with, now you can fully customize, add, remove, and map the existing user attributes issued as claims in SAML tokens.</span></span>
 
  ![Geçirilen bir federasyon uygulaması SAML belirteci kullanıcı özniteliklerini özelleştirme](./media/active-directory-enterprise-apps-whats-new-azure-portal/10.png)


<span data-ttu-id="6c55a-156">Yeni SSO yapılandırma federe olduğunu denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="6c55a-156">To check that out the new federated SSO configuration:</span></span>
1. <span data-ttu-id="6c55a-157">Bir Federasyon uygulamanın açmak **çoklu oturum açma** emin olun ve sol gezinti menüsü dikey penceresinde '*SAML tabanlı oturum açma** modu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="6c55a-157">Open a federated application’s **single sign-on** blade from the left navigation menu and make sure the ‘*SAML-based Sign-on** mode is selected.</span></span> 
2. <span data-ttu-id="6c55a-158">Kez altındaki onay kutusunu, etkinleştirme **kullanıcı öznitelikleri** başlık tüm SAML belirtecine eklenen özniteliklerini değiştirmek için bu uygulamaya geçirildi.</span><span class="sxs-lookup"><span data-stu-id="6c55a-158">Once there, enable the checkbox under the **User Attributes** heading to modify all of the attributes included in the SAML token passed to that application.</span></span>

<span data-ttu-id="6c55a-159">De oluşturma, aktarma ve Federasyon çoklu oturum açma için kullanılan sertifikaları yönetme yanı Düzenle sertifikanızı dolmak üzere olduğunda kimin bildirim.</span><span class="sxs-lookup"><span data-stu-id="6c55a-159">You can also create, rollover, and manage certificates used for federated single sign-on, as well as edit who gets notified when your certificate is about to expire.</span></span> <span data-ttu-id="6c55a-160">Bu yeni seçenekleri altında görürsünüz **sertifikaları** aynı tek oturum açma dikey penceresinde başlığı.</span><span class="sxs-lookup"><span data-stu-id="6c55a-160">You’ll see these new options under the **Certificates** heading on the same Single sign-on blade.</span></span>
 
  ![Süre sonu bildirim e-posta ve seçenekleri imzalama sertifikası özelleştirme yeni bir sertifika oluşturma](./media/active-directory-enterprise-apps-whats-new-azure-portal/11.png)

### <a name="relay-state-paramenter"></a><span data-ttu-id="6c55a-162">Geçiş durumunu paramenter</span><span class="sxs-lookup"><span data-stu-id="6c55a-162">Relay State paramenter</span></span>
<span data-ttu-id="6c55a-163">Son olarak, biz de dahil etmek için desteklediğimiz SAML URL parametrelerinin Genişletilmiş **geçiş durumunu parametresi**, kullanıcılarınızın güden üzerinde bir federasyon uygulaması içinde oturum açma tamamlandıktan sonra sayfa olduğu.</span><span class="sxs-lookup"><span data-stu-id="6c55a-163">Finally, we’ve also extended the set of SAML URL parameters we support to include the **Relay State parameter**, which is the page your users will land on inside of a federated application once the sign-in is completed.</span></span> <span data-ttu-id="6c55a-164">Kullanıcılarınızın bunları hızlı bir şekilde giderek almak için uygulama içinde belirli bir yere göndermek istiyorsanız yapılandırmak için çok kullanışlı ayar budur.</span><span class="sxs-lookup"><span data-stu-id="6c55a-164">This is very useful setting to configure if you want to send your users to a specific place within the application to get them going quickly.</span></span>

  ![SAML geçiş durumunu parametre ayarı](./media/active-directory-enterprise-apps-whats-new-azure-portal/12.png)
 
<span data-ttu-id="6c55a-166">**Geçiş durumu parametresini ayarlama**:</span><span class="sxs-lookup"><span data-stu-id="6c55a-166">**To set the relay state parameter**:</span></span>

1. <span data-ttu-id="6c55a-167">Etkinleştirme **Göster Gelişmiş URL ayarları** altındaki onay kutusunu **etki alanı ve URL'leri** çoklu oturum açma yapılandırma dikey penceresi başlığı.</span><span class="sxs-lookup"><span data-stu-id="6c55a-167">Enable the **Show advanced URL settings** check-box under the **Domain and URLs** heading on the single-sign on configuration blade.</span></span> 
2. <span data-ttu-id="6c55a-168">Bunu yaptıktan sonra bu ve diğer SAML URL ayarları ayarlamanıza olanak sağlayacak kutuları görüntülenir yeni URL bir dizi giriş görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-168">Once you do this, you’ll see a set of new URL input boxes appear which will allow you to set this, and other, SAML URL settings.</span></span>

## <a name="bring-your-own-password-sso-applications"></a><span data-ttu-id="6c55a-169">SSO uygulamaları kendi parolanızı Getir</span><span class="sxs-lookup"><span data-stu-id="6c55a-169">Bring your own password SSO applications</span></span>

<span data-ttu-id="6c55a-170">Her uygulama kutunun sağ dışında Federasyon desteklediğini biliyoruz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-170">We know that not every application supports federation right out of the box.</span></span> <span data-ttu-id="6c55a-171">Örneğin, belki de eklediğiniz yeni uygulamalardan biri kullanıcılarınız oturum açmak için bir kullanıcı adı ve parola kullanan bir özel oturum açma ekranı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6c55a-171">For example, maybe one of the new applications you added has a custom login screen that your users use a username and password to sign in to.</span></span> <span data-ttu-id="6c55a-172">Azure AD kullanarak, bu tür uygulamalar hala tümleştirebilirsiniz bizim **kendi uygulamalarınızı Getir** yeni Portalı'nda yapılandırmanız için kullanıma sunulmuştur özelliği.</span><span class="sxs-lookup"><span data-stu-id="6c55a-172">You can still integrate these types of applications with Azure AD using our **Bring your own applications** feature, which is now available for you to configure in the new portal.</span></span>
 
  ![Azure AD ile uygulamaları vaulting özel parola tümleştirme](./media/active-directory-enterprise-apps-whats-new-azure-portal/13.png)

<span data-ttu-id="6c55a-174">**'Kendi uygulamalarınızı Yap' özelliği denetlemek için**:</span><span class="sxs-lookup"><span data-stu-id="6c55a-174">**To check out the 'Bring your own applications' feature**:</span></span>

1. <span data-ttu-id="6c55a-175">Yeni özel bir uygulama için tek oturum açma modu ayarlandıktan sonra ekledik **parola tabanlı oturum açma**, uygulamanın, oturum açma ekranı burada işler URL'sini girin ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="6c55a-175">After you set the single sign-on mode for a new custom application that you’ve added to **Password-based Sign-on**, enter the URL where the application renders its login screen and click **Save**.</span></span>  
2. <span data-ttu-id="6c55a-176">Bunu gerçekleştirdikten sonra biz otomatik olarak bir kullanıcı adı için bu URL'yi scrape ve parola giriş kutusu ve Azure AD erişim paneli tarayıcı uzantısı kullanarak bu uygulamaya parolaları güvenli bir şekilde iletmek için kullanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6c55a-176">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="configure-self-service-application-access"></a><span data-ttu-id="6c55a-177">Self Servis uygulama erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c55a-177">Configure self-service application access</span></span>

<span data-ttu-id="6c55a-178">Çok sayıda yeni uygulamaları ekledikten sonra belki de gözatın ve yönetici olarak rahatsız gerek kalmadan bu uygulamaları kendi access Panel eklemek, kullanıcılarınızın izin vermek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-178">After you’ve added lots of new applications, maybe you want to allow your users to browse and add those applications to their own access panels, without needing to bother you as an administrator.</span></span> <span data-ttu-id="6c55a-179">Şimdi, bu en son sürüm ile yapılandırın ve Self Servis uygulamaya erişim hakkı yeni Portalı'ndan yönetin.</span><span class="sxs-lookup"><span data-stu-id="6c55a-179">Now, with this latest release, you can configure and manage self-service application access right from the new portal.</span></span>

  ![Self Servis uygulama erişimi için bir parola SSO uygulama yapılandırma](./media/active-directory-enterprise-apps-whats-new-azure-portal/14.png)
 
<span data-ttu-id="6c55a-181">**Yapılandırma ve Self Servis uygulama erişimi yönetmek için**:</span><span class="sxs-lookup"><span data-stu-id="6c55a-181">**To configure and manage self-service application access**:</span></span>

1. <span data-ttu-id="6c55a-182">Başlamak için seçebileceğiniz **Self Servis** uygulama seçeneğinden sol gezinti menüsünde ve ayarlama **bu uygulamaya erişmek kullanıcıların?** için seçenek '**Evet**'.</span><span class="sxs-lookup"><span data-stu-id="6c55a-182">To get started, you can select the **Self-service** option from the application’s left navigation menu and set the **Allow users to request access to this application?** option to ‘**Yes**’.</span></span> 
2. <span data-ttu-id="6c55a-183">Bu, bu uygulamaya erişim onaylama yetkisi olan kişileri ve hangi grubu Self Servis kullanıcıları eklenecek yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6c55a-183">This will enable you to configure who is allowed to approve access to this application, and which group self-service users will be added.</span></span> <span data-ttu-id="6c55a-184">Ayrıca, uygulama parolası çoklu oturum açma için yapılandırılmışsa, isteğe bağlı olarak uygulamaya atanan parolaları yönetmek bu onaylayanlar olanak sağlayan başka bir seçenek de görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6c55a-184">In addition, if the application is configured for password single-sign on, you’ll also see another option which lets you optionally allow those approvers to manage the passwords assigned to the application.</span></span>

##<a name="feedback"></a><span data-ttu-id="6c55a-185">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="6c55a-185">Feedback</span></span>

<span data-ttu-id="6c55a-186">Geliştirilmiş kullanarak gibi umuyoruz Azure AD deneyimi.</span><span class="sxs-lookup"><span data-stu-id="6c55a-186">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="6c55a-187">Gelen geri bildirim unutmayın!</span><span class="sxs-lookup"><span data-stu-id="6c55a-187">Please keep the feedback coming!</span></span> <span data-ttu-id="6c55a-188">Geri bildirim ve fikir geliştirme için post **Yönetici portalı** bölümünü bizim [geri bildirim Forumunda](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span><span class="sxs-lookup"><span data-stu-id="6c55a-188">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="6c55a-189">Biz, her gün harika yeni hizmetler oluşturma hakkında heyecan ve şekil, kılavuzlar kullanabilir ve sonraki geliştirmemiz ne tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6c55a-189">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c55a-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c55a-190">Next steps</span></span>

<span data-ttu-id="6c55a-191">Daha fazla ayrıntı için bkz: [Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md).</span><span class="sxs-lookup"><span data-stu-id="6c55a-191">For more details, see [Managing Applications with Azure Active Directory](active-directory-enable-sso-scenario.md).</span></span>



