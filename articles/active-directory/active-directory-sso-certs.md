---
title: "Azure AD içinde Federasyon sertifikalarını yönetmek | Microsoft Docs"
description: "Federasyon sertifikalarınızı sona erme tarihini özelleştirmeyi ve süresi yakında dolacak sertifikaları yenilemek nasıl öğrenin."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: 1283b570200f05003658824760ecbb6722f241d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a><span data-ttu-id="08d8c-103">Federasyon tek oturum açma için Azure Active Directory'de sertifikaları yönetme</span><span class="sxs-lookup"><span data-stu-id="08d8c-103">Manage certificates for federated single sign-on in Azure Active Directory</span></span>
<span data-ttu-id="08d8c-104">Bu makale ortak sorular ve Federasyon çoklu oturum açma (SSO) SaaS uygulamalarınıza oluşturmak için Azure Active Directory (Azure AD) oluşturur sertifikalar ilgili bilgiler yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="08d8c-104">This article covers common questions and information related to the certificates that Azure Active Directory (Azure AD) creates to establish federated single sign-on (SSO) to your SaaS applications.</span></span> <span data-ttu-id="08d8c-105">Uygulamaları Azure AD uygulama galerisinde veya bir galeri olmayan uygulama şablonu kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08d8c-105">Add applications from the Azure AD app gallery or by using a non-gallery application template.</span></span> <span data-ttu-id="08d8c-106">Uygulama, Federasyon SSO seçeneğini kullanarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="08d8c-106">Configure the application by using the federated SSO option.</span></span>

<span data-ttu-id="08d8c-107">Bu makalede, Azure AD SSO SAML Federasyon aracılığıyla kullanmak için aşağıdaki örnekte gösterildiği gibi yapılandırılan uygulamalar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="08d8c-107">This article is relevant only to apps that are configured to use Azure AD SSO through SAML federation, as shown in the following example:</span></span>

![Azure AD çoklu oturum açma](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a><span data-ttu-id="08d8c-109">Galeri ve galeri olmayan uygulamalar için otomatik olarak oluşturulan sertifika</span><span class="sxs-lookup"><span data-stu-id="08d8c-109">Auto-generated certificate for gallery and non-gallery applications</span></span>
<span data-ttu-id="08d8c-110">Galeriden yeni bir uygulama eklemek ve bir SAML tabanlı oturum açma yapılandırdığınızda Azure AD üç yıl geçerli olan uygulama için bir sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="08d8c-110">When you add a new application from the gallery and configure a SAML-based sign-on, Azure AD generates a certificate for the application that is valid for three years.</span></span> <span data-ttu-id="08d8c-111">Bu sertifikayı indirebilirsiniz **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="08d8c-111">You can download this certificate from the **SAML Signing Certificate** section.</span></span> <span data-ttu-id="08d8c-112">Galeri uygulamalar için bu bölümde sertifika veya meta veri, uygulama gereksinim bağlı olarak indirmek için bir seçenek gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="08d8c-112">For gallery applications, this section might show an option to download the certificate or metadata, depending on the requirement of the application.</span></span>

![Azure AD çoklu oturum açma](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-the-expiration-date-for-your-federation-certificate-and-roll-it-over-to-a-new-certificate"></a><span data-ttu-id="08d8c-114">Federasyon sertifikanızı sona erme tarihini özelleştirebilir ve yeni bir sertifika geçir</span><span class="sxs-lookup"><span data-stu-id="08d8c-114">Customize the expiration date for your federation certificate and roll it over to a new certificate</span></span>
<span data-ttu-id="08d8c-115">Varsayılan olarak, sertifikaları üç yıl sonra süresi dolacak şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="08d8c-115">By default, certificates are set to expire after three years.</span></span> <span data-ttu-id="08d8c-116">Aşağıdaki adımları izleyerek sertifikanızı farklı sona erme tarihini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08d8c-116">You can choose a different expiration date for your certificate by completing the following steps.</span></span>
<span data-ttu-id="08d8c-117">Ekran görüntüleri Salesforce amacıyla örnek kullanın, ancak tüm Federasyon SaaS uygulamaları için bu adımları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08d8c-117">The screenshots use Salesforce for the sake of example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="08d8c-118">İçinde [Azure portal](https://aad.portal.azure.com), tıklatın **Kurumsal uygulama** sol bölmesinde ve ardından **yeni uygulama** üzerinde **genel bakış** sayfa:</span><span class="sxs-lookup"><span data-stu-id="08d8c-118">In the [Azure portal](https://aad.portal.azure.com), click **Enterprise application** in the left pane and then click **New application** on the **Overview** page:</span></span>

   ![SSO Yapılandırma Sihirbazı'nı açın](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. <span data-ttu-id="08d8c-120">İçin Galeri uygulama arayın ve ardından eklemek istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="08d8c-120">Search for the gallery application and then select the application that you want to add.</span></span> <span data-ttu-id="08d8c-121">Gerekli uygulama bulamazsanız, uygulamasını kullanarak eklemek **olmayan galeri uygulama** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="08d8c-121">If you cannot find the required application, add the application by using the **Non-gallery application** option.</span></span> <span data-ttu-id="08d8c-122">Bu özellik yalnızca Azure AD Premium (P1 ve P2) SKU'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08d8c-122">This feature is available only in the Azure AD Premium (P1 and P2) SKU.</span></span>

    ![Azure AD çoklu oturum açma](./media/active-directory-sso-certs/add_gallery_application.png)

3. <span data-ttu-id="08d8c-124">Tıklatın **çoklu oturum açma** değiştirmek ve bağlama sol bölmede **tek oturum açma modu** için **SAML tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="08d8c-124">Click the **Single sign-on** link in the left pane and change **Single Sign-on Mode** to **SAML-based Sign-on**.</span></span> <span data-ttu-id="08d8c-125">Bu adımı uygulamanız için üç yıllık sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="08d8c-125">This step generates a three-year certificate for your application.</span></span>

4. <span data-ttu-id="08d8c-126">Yeni bir sertifika oluşturmak için tıklatın **yeni sertifika oluştur** bağlamak **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="08d8c-126">To create a new certificate, click the **Create new certificate** link in the **SAML Signing Certificate** section.</span></span>

    ![Yeni bir sertifika oluşturma](./media/active-directory-sso-certs/create_new_certficate.png)

5. <span data-ttu-id="08d8c-128">**Yeni bir sertifika oluşturmak** bağlantı Takvim denetimi açar.</span><span class="sxs-lookup"><span data-stu-id="08d8c-128">The **Create a new certificate** link opens the calendar control.</span></span> <span data-ttu-id="08d8c-129">Herhangi bir tarihi ayarlamak ve geçerli tarihten en fazla üç yıl saat.</span><span class="sxs-lookup"><span data-stu-id="08d8c-129">You can set any date and time up to three years from the current date.</span></span> <span data-ttu-id="08d8c-130">Seçilen tarih ve saat olan yeni sona erme tarihi ve yeni sertifikanızın süresi.</span><span class="sxs-lookup"><span data-stu-id="08d8c-130">The selected date and time is the new expiration date and time of your new certificate.</span></span> <span data-ttu-id="08d8c-131">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="08d8c-131">Click **Save**.</span></span>

    ![İndirme sonra sertifikasını karşıya yükle](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. <span data-ttu-id="08d8c-133">Şimdi yeni sertifikayı yüklemek kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08d8c-133">Now the new certificate is available to download.</span></span> <span data-ttu-id="08d8c-134">Tıklatın **sertifika** indirmeleri için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="08d8c-134">Click the **Certificate** link to download it.</span></span> <span data-ttu-id="08d8c-135">Bu noktada, sertifikanızı etkin değil.</span><span class="sxs-lookup"><span data-stu-id="08d8c-135">At this point, your certificate is not active.</span></span> <span data-ttu-id="08d8c-136">Bu sertifika için değil, UTC'ye istediğinizde seçin **yeni sertifika etkin hale getirin** onay kutusunu ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="08d8c-136">When you want to roll over to this certificate, select the **Make new certificate active** check box and click **Save**.</span></span> <span data-ttu-id="08d8c-137">Bu noktadan itibaren Azure AD yanıt imzalama için yeni sertifikayı kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="08d8c-137">From that point, Azure AD starts using the new certificate for signing the response.</span></span>

7.  <span data-ttu-id="08d8c-138">Sertifika belirli SaaS uygulamanızı karşıya yükleme konusunda bilgi almak için Yardım düğmesini tıklatın **görünüm uygulaması yapılandırma Öğreticisi** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="08d8c-138">To learn how to upload the certificate to your particular SaaS application, click the **View application configuration tutorial** link.</span></span>

## <a name="renew-a-certificate-that-will-soon-expire"></a><span data-ttu-id="08d8c-139">Süresi yakında dolacak bir sertifikayı yenileme</span><span class="sxs-lookup"><span data-stu-id="08d8c-139">Renew a certificate that will soon expire</span></span>
<span data-ttu-id="08d8c-140">Aşağıdaki yenileme adımları sonucunda kullanıcılarınız için önemli kapalı kalma süresi.</span><span class="sxs-lookup"><span data-stu-id="08d8c-140">The following renewal steps should result in no significant downtime for your users.</span></span> <span data-ttu-id="08d8c-141">Bu bölümde özelliği Salesforce örneği, ancak bu adımların olarak görüntülerde tüm Federasyon SaaS uygulamaları için geçerli olabilir.</span><span class="sxs-lookup"><span data-stu-id="08d8c-141">The screenshots in this section feature Salesforce as an example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="08d8c-142">Üzerinde **Azure Active Directory** uygulama **çoklu oturum açma** sayfasında, uygulamanız için yeni sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08d8c-142">On the **Azure Active Directory** application **Single sign-on** page, generate the new certificate for your application.</span></span> <span data-ttu-id="08d8c-143">Tıklayarak bunu yapabilirsiniz **yeni sertifika oluştur** bağlamak **SAML imzalama sertifikası** bölümü.</span><span class="sxs-lookup"><span data-stu-id="08d8c-143">You can do this by clicking the **Create new certificate** link in the **SAML Signing Certificate** section.</span></span>

    ![Yeni bir sertifika oluşturma](./media/active-directory-sso-certs/create_new_certficate.png)

2. <span data-ttu-id="08d8c-145">İstenen sona erme tarihi ve saati, yeni sertifika seçin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="08d8c-145">Select the desired expiration date and time for your new certificate and click **Save**.</span></span>

3. <span data-ttu-id="08d8c-146">Sertifikayı indirin **SAML imzalama sertifikası** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="08d8c-146">Download the certificate in the **SAML Signing certificate** option.</span></span> <span data-ttu-id="08d8c-147">Yeni sertifika SaaS uygulamanın tek oturum açma yapılandırma ekranına karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08d8c-147">Upload the new certificate to the SaaS application's single sign-on configuration screen.</span></span> <span data-ttu-id="08d8c-148">Belirli SaaS uygulamanız için bunu öğrenmek için Yardım düğmesini tıklatın **görünüm uygulaması yapılandırma Öğreticisi** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="08d8c-148">To learn how to do this for your particular SaaS application, click the **View application configuration tutorial** link.</span></span>
   
4. <span data-ttu-id="08d8c-149">Azure AD'de yeni sertifikayı etkinleştirmek için seçin **yeni sertifika etkin hale getirin** onay kutusunu ve tıklatın **kaydetmek** sayfanın üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08d8c-149">To activate the new certificate in Azure AD, select the **Make new certificate active** check box and click the **Save** button at the top of the page.</span></span> <span data-ttu-id="08d8c-150">Bu Azure AD tarafında yeni sertifika yapar.</span><span class="sxs-lookup"><span data-stu-id="08d8c-150">This rolls over the new certificate on the Azure AD side.</span></span> <span data-ttu-id="08d8c-151">Sertifikanın durumunu değiştirir **yeni** için **etkin**.</span><span class="sxs-lookup"><span data-stu-id="08d8c-151">The status of the certificate changes from **New** to **Active**.</span></span> <span data-ttu-id="08d8c-152">Bu noktadan itibaren Azure AD yanıt imzalama için yeni sertifikayı kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="08d8c-152">From that point, Azure AD starts using the new certificate for signing the response.</span></span> 
   
    ![Yeni bir sertifika oluşturma](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a><span data-ttu-id="08d8c-154">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="08d8c-154">Related articles</span></span>
* [<span data-ttu-id="08d8c-155">Azure Active Directory ile SaaS uygulamalarını tümleştirme ile nasıl öğreticiler listesi</span><span class="sxs-lookup"><span data-stu-id="08d8c-155">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08d8c-156">Azure Active Directory'de uygulama yönetimi için makale dizini</span><span class="sxs-lookup"><span data-stu-id="08d8c-156">Article index for application management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="08d8c-157">Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="08d8c-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="08d8c-158">Sorun giderme SAML tabanlı çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="08d8c-158">Troubleshooting SAML-based single sign-on</span></span>](active-directory-saml-debugging.md)
