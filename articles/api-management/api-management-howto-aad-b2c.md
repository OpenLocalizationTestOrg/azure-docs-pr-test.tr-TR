---
title: "Azure Active Directory B2C - Azure API Management kullanarak aaaAuthorize Geliştirici hesaplarını | Microsoft Docs"
description: "Bilgi nasıl API Management'te Azure Active Directory B2C kullanarak tooauthorize kullanıcılar."
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="2b4f0-103">Azure API Management'te Azure Active Directory B2C kullanarak tooauthorize Geliştirici nasıl hesapları</span><span class="sxs-lookup"><span data-stu-id="2b4f0-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="2b4f0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2b4f0-104">Overview</span></span>
<span data-ttu-id="2b4f0-105">Azure Active Directory B2C bir tüketiciye yönelik web ve mobil uygulamaları için bulut kimlik yönetimi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="2b4f0-106">Toomanage erişim tooyour Geliştirici Portalı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="2b4f0-107">Bu kılavuz, API Management hizmeti toointegrate Azure Active Directory B2C ile de gerekli yapılandırmayla hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="2b4f0-108">Klasik Azure Active Directory kullanılarak erişim toohello Geliştirici Portalı etkinleştirme hakkında daha fazla bilgi için bkz: [nasıl tooauthorize Geliştirici kullanarak hesapları Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="2b4f0-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="2b4f0-109">Bu kılavuzdaki toocomplete hello adımları, öncelikle bir Azure Active Directory B2C Kiracı toocreate bir uygulama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="2b4f0-110">Ayrıca, toohave kaydolma ve oturum açma ilkeleri hazır gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="2b4f0-111">Daha fazla bilgi için bkz: [Azure Active Directory B2C genel bakış].</span><span class="sxs-lookup"><span data-stu-id="2b4f0-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="2b4f0-112">Azure Active Directory B2C kullanarak Geliştirici hesaplarını yetkilendirmede</span><span class="sxs-lookup"><span data-stu-id="2b4f0-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="2b4f0-113">başlatıldı, tooget tıklatın **yayımcı portalına** hello API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="2b4f0-114">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-114">This takes you toohello API Management publisher portal.</span></span>

   ![Yayımcı portalı][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="2b4f0-116">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management öğreticiileçalışmayabaşlama][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2b4f0-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="2b4f0-117">Merhaba üzerinde **API Management** menüsünde tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="2b4f0-118">Merhaba üzerinde **kimlikleri** sekmesinde, seçin **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Dış kimlikler 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="2b4f0-120">Merhaba Not **tekrar yönlendirme URL'sini** ve hello Azure portal'ın Active Directory B2C tooAzure üzerinden geçin.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Dış kimlikler 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="2b4f0-122">Merhaba tıklatın **uygulamaları** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-122">Click hello **Applications** button.</span></span>

  ![Yeni bir uygulama 1 kaydetme][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="2b4f0-124">Merhaba tıklatın **Ekle** düğmesini toocreate yeni bir Azure Active Directory B2C uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Yeni bir uygulama 2 kaydetme][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="2b4f0-126">Merhaba, **yeni uygulama** dikey penceresinde hello uygulama için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="2b4f0-127">Seçin **Evet** altında **Web uygulaması/Web API**ve seçin **Evet** altında **örtük akışına izin**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="2b4f0-128">Ardından kopya hello **tekrar yönlendirme URL'sini** hello gelen **Azure Active Directory B2C** hello bölümünü **kimlikleri** sekmesinde hello yayımcı Portalı'nda ve helloyapıştırma**Yanıt URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Yeni bir uygulamayı 3 Kaydet][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="2b4f0-130">Merhaba tıklatın **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-130">Click hello **Create** button.</span></span> <span data-ttu-id="2b4f0-131">Merhaba uygulaması oluşturulduğunda hello göründüğü **uygulamaları** dikey.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="2b4f0-132">Merhaba uygulama adı toosee ayrıntılarını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-132">Click hello application name toosee its details.</span></span>

  ![Yeni bir uygulama 4 kaydetme][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="2b4f0-134">Merhaba gelen **özellikleri** dikey penceresinde, kopyalama hello **uygulama kimliği** toohello Pano.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![1 uygulama kimliği][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="2b4f0-136">Geçiş geri toohello yayımcı portalı ve hello kimliği hello yapıştırma **istemci kimliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![Uygulama kimliği 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="2b4f0-138">Anahtarı geri toohello Azure portal, hello tıklatın **anahtarları** düğmesine tıklayın ve ardından **anahtar üret**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="2b4f0-139">Tıklatın **kaydetmek** toosave hello yapılandırması ve görüntü hello **uygulama anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="2b4f0-140">Merhaba anahtar toohello panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-140">Copy hello key toohello clipboard.</span></span>

  ![1 uygulama anahtarı][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="2b4f0-142">Anahtar geri toohello yayımcı portalı ve Yapıştır hello anahtara hello **gizli** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Uygulama anahtarı 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="2b4f0-144">Hello Azure Active Directory B2C kiracınızda Hello etki alanı adını belirtin **izin Kiracı**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![İzin verilen Kiracı][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="2b4f0-146">Merhaba belirtin **kaydolma İlkesi** ve **Signın İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="2b4f0-147">İsteğe bağlı olarak, ayrıca hello sağlayabilir **Profil Düzenleme İlkesi** ve **parola sıfırlama İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![İlkeler][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="2b4f0-149">İlkeler hakkında daha fazla bilgi için bkz: [Azure Active Directory B2C: Genişletilebilir ilke çerçevesini].</span><span class="sxs-lookup"><span data-stu-id="2b4f0-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="2b4f0-150">Merhaba istenen yapılandırma belirttikten sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="2b4f0-151">Hello değişiklikler kaydedildikten sonra geliştiriciler yeni hesapları mümkün toocreate olması ve Azure Active Directory B2C kullanarak toohello Geliştirici Portalı'nda oturum.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="2b4f0-152">Azure Active Directory B2C kullanarak bir geliştirici hesabı için kaydolun</span><span class="sxs-lookup"><span data-stu-id="2b4f0-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="2b4f0-153">toosign Azure Active Directory B2C kullanarak bir geliştirici hesabı için yeni bir tarayıcı penceresi açın ve toohello Geliştirici portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="2b4f0-154">Merhaba tıklatın **kaydolun** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-154">Click hello **Sign up** button.</span></span>

   ![Geliştirici Portalı 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="2b4f0-156">İle toosign seçin **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Geliştirici Portalı 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="2b4f0-158">Merhaba önceki bölümde yapılandırılmış yeniden yönlendirilen toohello kaydolma İlkesi demektir.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="2b4f0-159">Toosign e-posta adresinizi veya var olan sosyal hesaplarınızı birini kullanarak seçin.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b4f0-160">Azure Active Directory B2C hello üzerinde etkin hello tek seçenek ise **kimlikleri** sekmesini hello yayımcı Portalı'nda, yeniden yönlendirilen toohello kaydolma İlkesi doğrudan olması.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![Geliştirici portalı][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="2b4f0-162">Merhaba kaydolma tamamlandığında yeniden yönlendirilen geri toohello Geliştirici Portalı demektir.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="2b4f0-163">API Management hizmet örneği için şimdi toohello Geliştirici Portalı'nda oturum açtınız.</span><span class="sxs-lookup"><span data-stu-id="2b4f0-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Kayıt tamamlandı][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="2b4f0-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b4f0-165">Next steps</span></span>

*  <span data-ttu-id="2b4f0-166">[Azure Active Directory B2C genel bakış]</span><span class="sxs-lookup"><span data-stu-id="2b4f0-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="2b4f0-167">[Azure Active Directory B2C: Genişletilebilir ilke çerçevesini]</span><span class="sxs-lookup"><span data-stu-id="2b4f0-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="2b4f0-168">[Azure Active Directory B2C, kimlik sağlayıcısı bir Microsoft hesabı kullanın]</span><span class="sxs-lookup"><span data-stu-id="2b4f0-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="2b4f0-169">[Azure Active Directory B2C, kimlik sağlayıcısı bir Google hesabı kullan]</span><span class="sxs-lookup"><span data-stu-id="2b4f0-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="2b4f0-170">[Azure Active Directory B2C, kimlik sağlayıcısı LinkedIn hesabını kullan]</span><span class="sxs-lookup"><span data-stu-id="2b4f0-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="2b4f0-171">[Azure Active Directory B2C, kimlik sağlayıcısı Facebook hesabıyla kullanın]</span><span class="sxs-lookup"><span data-stu-id="2b4f0-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Azure Active Directory B2C genel bakış]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[nasıl tooauthorize Geliştirici kullanarak hesapları Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: Genişletilebilir ilke çerçevesini]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Azure Active Directory B2C, kimlik sağlayıcısı bir Microsoft hesabı kullanın]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Azure Active Directory B2C, kimlik sağlayıcısı bir Google hesabı kullan]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Azure Active Directory B2C, kimlik sağlayıcısı Facebook hesabıyla kullanın]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Azure Active Directory B2C, kimlik sağlayıcısı LinkedIn hesabını kullan]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
