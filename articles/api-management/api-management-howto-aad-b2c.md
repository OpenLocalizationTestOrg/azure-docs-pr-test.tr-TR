---
title: "Azure Active Directory B2C - Azure API Management kullanarak Geliştirici hesaplarını yetkilendirmede | Microsoft Docs"
description: "API Management'te Azure Active Directory B2C kullanarak kullanıcıları yetkilendirmek öğrenin."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="66d8b-103">Azure API Management'te Azure Active Directory B2C kullanarak Geliştirici hesaplarını yetkilendirmede nasıl</span><span class="sxs-lookup"><span data-stu-id="66d8b-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="66d8b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="66d8b-104">Overview</span></span>
<span data-ttu-id="66d8b-105">Azure Active Directory B2C bir tüketiciye yönelik web ve mobil uygulamaları için bulut kimlik yönetimi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="66d8b-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="66d8b-106">Geliştirici portalınızın erişimi yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d8b-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="66d8b-107">Bu kılavuz, Azure Active Directory B2C ile tümleştirmek için API Management hizmetiniz gerekli yapılandırmayla gösterir.</span><span class="sxs-lookup"><span data-stu-id="66d8b-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="66d8b-108">Klasik Azure Active Directory'yi kullanarak Geliştirici portalına erişim etkinleştirme hakkında daha fazla bilgi için bkz: [Azure Active Directory'yi kullanarak Geliştirici hesaplarını yetkilendirmede nasıl].</span><span class="sxs-lookup"><span data-stu-id="66d8b-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="66d8b-109">Bu kılavuzdaki adımları tamamlamak için ilk bir uygulama oluşturmak için bir Azure Active Directory B2C kiracısına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66d8b-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="66d8b-110">Ayrıca, kaydolma ve oturum açma ilkeleri hazır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66d8b-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="66d8b-111">Daha fazla bilgi için bkz: [Azure Active Directory B2C genel bakış].</span><span class="sxs-lookup"><span data-stu-id="66d8b-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="66d8b-112">Azure Active Directory B2C kullanarak Geliştirici hesaplarını yetkilendirmede</span><span class="sxs-lookup"><span data-stu-id="66d8b-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="66d8b-113">Kullanmaya başlamak için tıklayın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="66d8b-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="66d8b-114">Bu sizi API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="66d8b-114">This takes you to the API Management publisher portal.</span></span>

   ![Yayımcı portalı][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="66d8b-116">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] içinde [Azure API Management öğretici ile çalışmaya başlama][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="66d8b-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="66d8b-117">Üzerinde **API Management** menüsünde tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="66d8b-118">Üzerinde **kimlikleri** sekmesinde, seçin **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Dış kimlikler 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="66d8b-120">Not **tekrar yönlendirme URL'sini** ve anahtar Azure Active Directory B2C Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="66d8b-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Dış kimlikler 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="66d8b-122">Tıklatın **uygulamaları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66d8b-122">Click the **Applications** button.</span></span>

  ![Yeni bir uygulama 1 kaydetme][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="66d8b-124">Tıklatın **Ekle** düğmesi yeni bir Azure Active Directory B2C uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66d8b-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Yeni bir uygulama 2 kaydetme][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="66d8b-126">İçinde **yeni uygulama** dikey penceresinde, uygulama için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="66d8b-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="66d8b-127">Seçin **Evet** altında **Web uygulaması/Web API**ve seçin **Evet** altında **örtük akışına izin**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="66d8b-128">Ardından kopyalama **tekrar yönlendirme URL'sini** gelen **Azure Active Directory B2C** bölümünü **kimlikleri** sekmesinde yayımcı portalında ve yapıştırın **yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="66d8b-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Yeni bir uygulamayı 3 Kaydet][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="66d8b-130">**Oluştur** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66d8b-130">Click the **Create** button.</span></span> <span data-ttu-id="66d8b-131">Uygulama oluşturulduğunda görünür **uygulamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="66d8b-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="66d8b-132">Ayrıntılarını görmek için uygulama adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66d8b-132">Click the application name to see its details.</span></span>

  ![Yeni bir uygulama 4 kaydetme][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="66d8b-134">Gelen **özellikleri** dikey penceresinde, kopya **uygulama kimliği** panoya.</span><span class="sxs-lookup"><span data-stu-id="66d8b-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![1 uygulama kimliği][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="66d8b-136">Geçiş yayımcı portalına dönün ve kimliği içine yapıştırma **istemci kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="66d8b-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![Uygulama kimliği 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="66d8b-138">Azure portalına anahtarı, tıklatın **anahtarları** düğmesine tıklayın ve ardından **anahtar üret**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="66d8b-139">Tıklatın **kaydetmek** yapılandırmasını kaydetmek ve görüntülemek için **uygulama anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="66d8b-140">Anahtarı panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="66d8b-140">Copy the key to the clipboard.</span></span>

  ![1 uygulama anahtarı][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="66d8b-142">Geçiş yayımcı portalına dönün ve içine anahtarını yapıştırın **gizli** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="66d8b-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Uygulama anahtarı 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="66d8b-144">Azure Active Directory B2C kiracısı'nda etki alanı adını belirtin **izin Kiracı**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![İzin verilen Kiracı][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="66d8b-146">Belirtin **kaydolma İlkesi** ve **Signın İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="66d8b-147">İsteğe bağlı olarak, ayrıca sağlayabilirsiniz **Profil Düzenleme İlkesi** ve **parola sıfırlama İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![İlkeler][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="66d8b-149">İlkeler hakkında daha fazla bilgi için bkz: [Azure Active Directory B2C: Genişletilebilir ilke çerçevesini].</span><span class="sxs-lookup"><span data-stu-id="66d8b-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="66d8b-150">İstenen yapılandırma belirttikten sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="66d8b-151">Değişiklikler kaydedildikten sonra geliştiricilerin yeni hesapları oluşturabilir ve Azure Active Directory B2C kullanarak oturum açın Geliştirici portalına olacaktır.</span><span class="sxs-lookup"><span data-stu-id="66d8b-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="66d8b-152">Azure Active Directory B2C kullanarak bir geliştirici hesabı için kaydolun</span><span class="sxs-lookup"><span data-stu-id="66d8b-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="66d8b-153">Azure Active Directory B2C kullanarak bir geliştirici hesabı için kaydolmak için yeni bir tarayıcı penceresi açın ve geliştirici portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="66d8b-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="66d8b-154">Tıklatın **kaydolun** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="66d8b-154">Click the **Sign up** button.</span></span>

   ![Geliştirici Portalı 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="66d8b-156">İle kaydolmak isterseniz **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="66d8b-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Geliştirici Portalı 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="66d8b-158">Önceki bölümde yapılandırılmış kaydolma İlkesi yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d8b-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="66d8b-159">E-posta adresinizi veya var olan sosyal hesaplarınızı birini kullanarak kaydolmak seçin.</span><span class="sxs-lookup"><span data-stu-id="66d8b-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="66d8b-160">Azure Active Directory B2C etkin tek seçenek ise **kimlikleri** sekmesini yayımcı Portalı'nda, kaydolma ilkeye doğrudan yönlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="66d8b-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Geliştirici portalı][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="66d8b-162">Kayıt işlemi tamamlandıktan sonra Geliştirici portalına yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d8b-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="66d8b-163">Artık Geliştirici portalına API Management hizmet örneği için oturum açtınız.</span><span class="sxs-lookup"><span data-stu-id="66d8b-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Kayıt tamamlandı][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="66d8b-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66d8b-165">Next steps</span></span>

*  <span data-ttu-id="66d8b-166">[Azure Active Directory B2C genel bakış]</span><span class="sxs-lookup"><span data-stu-id="66d8b-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="66d8b-167">[Azure Active Directory B2C: Genişletilebilir ilke çerçevesini]</span><span class="sxs-lookup"><span data-stu-id="66d8b-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="66d8b-168">[Azure Active Directory B2C, kimlik sağlayıcısı bir Microsoft hesabı kullanın]</span><span class="sxs-lookup"><span data-stu-id="66d8b-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="66d8b-169">[Azure Active Directory B2C, kimlik sağlayıcısı bir Google hesabı kullan]</span><span class="sxs-lookup"><span data-stu-id="66d8b-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="66d8b-170">[Azure Active Directory B2C, kimlik sağlayıcısı LinkedIn hesabını kullan]</span><span class="sxs-lookup"><span data-stu-id="66d8b-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="66d8b-171">[Azure Active Directory B2C, kimlik sağlayıcısı Facebook hesabıyla kullanın]</span><span class="sxs-lookup"><span data-stu-id="66d8b-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="66d8b-172">[Azure Active Directory B2C genel bakış]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="66d8b-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="66d8b-173">[Azure Active Directory'yi kullanarak Geliştirici hesaplarını yetkilendirmede nasıl]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="66d8b-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="66d8b-174">[Azure Active Directory B2C: Genişletilebilir ilke çerçevesini]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="66d8b-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="66d8b-175">[Azure Active Directory B2C, kimlik sağlayıcısı bir Microsoft hesabı kullanın]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="66d8b-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="66d8b-176">[Azure Active Directory B2C, kimlik sağlayıcısı bir Google hesabı kullan]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="66d8b-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="66d8b-177">[Azure Active Directory B2C, kimlik sağlayıcısı Facebook hesabıyla kullanın]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="66d8b-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="66d8b-178">[Azure Active Directory B2C, kimlik sağlayıcısı LinkedIn hesabını kullan]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="66d8b-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
