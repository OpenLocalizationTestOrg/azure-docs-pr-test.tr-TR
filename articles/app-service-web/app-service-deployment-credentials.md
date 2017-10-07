---
title: "Uygulama hizmeti dağıtım kimlik bilgileri aaaAzure | Microsoft Docs"
description: "Nasıl toouse hello Azure uygulama hizmeti dağıtım kimlik bilgileri öğrenin."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="cf830-103">Dağıtım kimlik bilgileri Azure App Service için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cf830-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="cf830-104">[Azure uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) iki tür kimlik bilgilerini destekler [yerel Git dağıtımı](app-service-deploy-local-git.md) ve [FTP/S dağıtım](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="cf830-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="cf830-105">Bunlar olan değil hello Azure Active Directory kimlik bilgileriniz ile aynı.</span><span class="sxs-lookup"><span data-stu-id="cf830-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="cf830-106">**Kullanıcı düzeyinde kimlik**: bir hello tüm Azure hesabı için kimlik bilgileri kümesi.</span><span class="sxs-lookup"><span data-stu-id="cf830-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="cf830-107">Herhangi bir uygulama izni tooaccess Azure hesabı hello herhangi abonelikte için kullanılan toodeploy tooApp hizmet olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf830-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="cf830-108">Yapılandırdığınız hello varsayılan kimlik bilgileri kümesi bunlar **uygulama hizmetleri** > **&lt;app_name >** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="cf830-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="cf830-109">Bu olduğunu da hello hello portal GUI ortaya varsayılan kümesi (Merhaba gibi **genel bakış** ve **özellikleri** , uygulamanızın, [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="cf830-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="cf830-110">Rol tabanlı erişim denetimi (RBAC) veya ortak yönetici izinleri aracılığıyla erişim tooAzure kaynaklara temsilci atarken, erişim tooan uygulama alan her bir Azure kullanıcı erişimi iptal kadar güncelleştirmesini kişisel kullanıcı düzeyinde kimlik bilgilerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="cf830-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="cf830-111">Bu dağıtım kimlik bilgileri Azure diğer kullanıcılarla Paylaşılmaması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cf830-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="cf830-112">**Uygulama düzeyinde kimlik**: bir her uygulama için kimlik bilgileri kümesi.</span><span class="sxs-lookup"><span data-stu-id="cf830-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="cf830-113">Yalnızca kullanılan toodeploy toothat uygulama olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf830-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="cf830-114">her uygulamanın uygulama oluşturma sırasında otomatik olarak oluşturulur ve hello uygulamanın içinde bulunan için yayımlama profili hello kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cf830-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="cf830-115">Merhaba kimlik bilgilerini el ile yapılandıramazsınız, ancak bunları bir uygulama için dilediğiniz zaman sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf830-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cf830-116">Sipariş toogive birisi erişim toothese kimlik bilgilerini aracılığıyla rol tabanlı erişim denetimi (RBAC), toomake gerek bunları katkıda bulunan veya hello Web uygulaması üzerinde daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="cf830-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="cf830-117">Okuyucular toopublish izin verilmiyor ve bu nedenle bu kimlik bilgilerini erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="cf830-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="cf830-118"><a name="userscope"></a>Ayarlama ve kullanıcı düzeyinde kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="cf830-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="cf830-119">Bir uygulamanın ait kullanıcı düzeyinde kimlik bilgilerinizi yapılandırabilirsiniz [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="cf830-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="cf830-120">Ne olursa olsun hangi uygulamanın bu kimlik bilgilerini yapılandırın, Azure içinde tüm abonelikler için hesap ve tooall uygulamaları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cf830-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="cf830-121">tooconfigure kullanıcı düzeyinde kimlik bilgilerinizi:</span><span class="sxs-lookup"><span data-stu-id="cf830-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="cf830-122">Merhaba, [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="cf830-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cf830-123">Merhaba Portalı'nda hello dağıtım kimlik bilgileri dikey penceresini erişebilmeniz için önce en az bir uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf830-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="cf830-124">Bununla birlikte, hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), kullanıcı düzeyinde kimlik bilgileri olan bir uygulama olmadan yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf830-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="cf830-125">Merhaba kullanıcı adını ve parolasını yapılandırın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cf830-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="cf830-126">Dağıtım kimlik bilgilerinizi ayarladıktan sonra hello bulabilirsiniz *Git* dağıtım kullanıcıadı uygulamanızın **genel bakış**,</span><span class="sxs-lookup"><span data-stu-id="cf830-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="cf830-127">ve ve *FTP* dağıtım kullanıcıadı uygulamanızın **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="cf830-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="cf830-128">Azure kullanıcı düzeyinde dağıtım parolanızı göstermez.</span><span class="sxs-lookup"><span data-stu-id="cf830-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="cf830-129">Merhaba parolanızı unutursanız, alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="cf830-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="cf830-130">Ancak, bu bölümdeki hello adımları izleyerek kimlik bilgilerinizi sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf830-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="cf830-131"><a name="appscope"></a>Alma ve uygulama düzeyinde kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="cf830-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="cf830-132">App Service içinde her uygulama için uygulama düzeyinde kimlik bilgilerini hello depolanan XML yayımlama profili.</span><span class="sxs-lookup"><span data-stu-id="cf830-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="cf830-133">tooget hello uygulama düzeyinde kimlik bilgileri:</span><span class="sxs-lookup"><span data-stu-id="cf830-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="cf830-134">Merhaba, [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="cf830-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="cf830-135">Tıklatın **... Daha fazla** > **Get yayımlama profili**, indirme başlatılması için ve bir. PublishSettings dosyası.</span><span class="sxs-lookup"><span data-stu-id="cf830-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="cf830-136">Açık hello. PublishSettings dosyasını açıp hello bulur `<publishProfile>` hello özniteliği etiketiyle `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="cf830-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="cf830-137">Daha sonra kendi `userName` ve `password` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="cf830-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="cf830-138">Bunlar hello uygulama düzeyinde kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="cf830-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="cf830-139">Benzer toohello kullanıcı düzeyinde kimlik bilgileri, hello FTP dağıtım kullanıcı adınızdır hello biçiminde `<app_name>\<username>`, ve hello Git dağıtım kullanıcı adı yalnızca `<username>` hello önceki olmadan `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="cf830-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="cf830-140">tooreset hello uygulama düzeyinde kimlik bilgileri:</span><span class="sxs-lookup"><span data-stu-id="cf830-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="cf830-141">Merhaba, [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="cf830-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="cf830-142">Tıklatın **... Daha fazla** > **sıfırlama yayımlama profili**.</span><span class="sxs-lookup"><span data-stu-id="cf830-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="cf830-143">Tıklatın **Evet** tooconfirm hello sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="cf830-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="cf830-144">Merhaba sıfırlama eylemi herhangi önceden indirilmiş geçersiz kılar. PublishSettings dosyaları.</span><span class="sxs-lookup"><span data-stu-id="cf830-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf830-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf830-145">Next steps</span></span>

<span data-ttu-id="cf830-146">Öğrenin toouse bu kimlik bilgileri toodeploy uygulamanızdan [yerel Git](app-service-deploy-local-git.md) veya kullanarak [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="cf830-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
