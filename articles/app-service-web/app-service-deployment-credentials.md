---
title: "Azure uygulama hizmeti dağıtım kimlik bilgileri | Microsoft Docs"
description: "Azure uygulama hizmeti dağıtım kimlik bilgilerini kullanmayı öğrenin."
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
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="3ac98-103">Dağıtım kimlik bilgileri Azure App Service için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3ac98-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="3ac98-104">[Azure uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) iki tür kimlik bilgilerini destekler [yerel Git dağıtımı](app-service-deploy-local-git.md) ve [FTP/S dağıtım](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="3ac98-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="3ac98-105">Bu, Azure Active Directory kimlik bilgileri ile aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="3ac98-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="3ac98-106">**Kullanıcı düzeyinde kimlik**: bir tüm Azure hesabı için kimlik bilgileri kümesi.</span><span class="sxs-lookup"><span data-stu-id="3ac98-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="3ac98-107">Azure hesabı erişim iznine sahip herhangi bir abonelikte, herhangi bir uygulama için uygulama hizmeti dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac98-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="3ac98-108">Yapılandırdığınız varsayılan kimlik bilgileri kümesi bunlar **uygulama hizmetleri** > **&lt;app_name >** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="3ac98-109">Bu aynı zamanda varsayılandır GUI portalında ortaya kümesi (gibi **genel bakış** ve **özellikleri** , uygulamanızın, [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="3ac98-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ac98-110">Rol tabanlı erişim denetimi (RBAC) veya ortak yönetici izinleri üzerinden Azure kaynaklarına erişimi temsilci atarken, bir uygulamaya erişim alan her bir Azure kullanıcı erişimi iptal kadar güncelleştirmesini kişisel kullanıcı düzeyinde kimlik bilgilerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac98-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="3ac98-111">Bu dağıtım kimlik bilgileri Azure diğer kullanıcılarla Paylaşılmaması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3ac98-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="3ac98-112">**Uygulama düzeyinde kimlik**: bir her uygulama için kimlik bilgileri kümesi.</span><span class="sxs-lookup"><span data-stu-id="3ac98-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="3ac98-113">Yalnızca bu uygulama dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac98-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="3ac98-114">Her uygulamanın uygulama oluşturma sırasında otomatik olarak oluşturulur ve uygulamanın içinde bulunan için yayımlama profili kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3ac98-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="3ac98-115">Kimlik bilgilerini el ile yapılandıramazsınız, ancak bunları bir uygulama için dilediğiniz zaman sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac98-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ac98-116">Sunmak için birisi erişim bu kimlik bilgileri aracılığıyla rol tabanlı erişim denetimi (RBAC), bunları Katılımcısı olmanız gerekir veya Web uygulaması üzerinde daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="3ac98-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="3ac98-117">Okuyucular yayımlama izin verilmez ve bu nedenle bu kimlik bilgilerini erişemez.</span><span class="sxs-lookup"><span data-stu-id="3ac98-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="3ac98-118"><a name="userscope"></a>Ayarlama ve kullanıcı düzeyinde kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="3ac98-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="3ac98-119">Bir uygulamanın ait kullanıcı düzeyinde kimlik bilgilerinizi yapılandırabilirsiniz [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="3ac98-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="3ac98-120">Ne olursa olsun hangi uygulamanın bu kimlik bilgilerini yapılandırın, bu tüm uygulamalar ve Azure hesabınızda tüm abonelikler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3ac98-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="3ac98-121">Kullanıcı düzeyinde kimlik bilgilerinizi yapılandırmak için:</span><span class="sxs-lookup"><span data-stu-id="3ac98-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="3ac98-122">İçinde [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ac98-123">Portalda dağıtım kimlik bilgileri dikey penceresini erişebilmeniz için önce en az bir uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3ac98-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="3ac98-124">Bununla birlikte, [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), kullanıcı düzeyinde kimlik bilgileri olan bir uygulama olmadan yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac98-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="3ac98-125">Kullanıcı adını ve parolasını yapılandırın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="3ac98-126">Dağıtım kimlik bilgilerinizi ayarladıktan sonra bulabileceğiniz *Git* dağıtım kullanıcıadı uygulamanızın **genel bakış**,</span><span class="sxs-lookup"><span data-stu-id="3ac98-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="3ac98-127">ve ve *FTP* dağıtım kullanıcıadı uygulamanızın **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="3ac98-128">Azure kullanıcı düzeyinde dağıtım parolanızı göstermez.</span><span class="sxs-lookup"><span data-stu-id="3ac98-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="3ac98-129">Parolanızı unutursanız, alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="3ac98-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="3ac98-130">Ancak, bu bölümdeki adımları izleyerek kimlik bilgilerinizi sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac98-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="3ac98-131"><a name="appscope"></a>Alma ve uygulama düzeyinde kimlik bilgilerini sıfırlama</span><span class="sxs-lookup"><span data-stu-id="3ac98-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="3ac98-132">XML dosyasında depolanan App Service'te her uygulama için uygulama düzeyinde kimlik bilgileri yayımlama profili.</span><span class="sxs-lookup"><span data-stu-id="3ac98-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="3ac98-133">Uygulama düzeyinde kimlik bilgilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="3ac98-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="3ac98-134">İçinde [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="3ac98-135">Tıklatın **... Daha fazla** > **Get yayımlama profili**, indirme başlatılması için ve bir. PublishSettings dosyası.</span><span class="sxs-lookup"><span data-stu-id="3ac98-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="3ac98-136">Açık. PublishSettings dosyasını ve Bul `<publishProfile>` öznitelik etiketiyle `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="3ac98-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="3ac98-137">Daha sonra kendi `userName` ve `password` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="3ac98-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="3ac98-138">Bu, uygulama düzeyinde kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="3ac98-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="3ac98-139">Kullanıcı düzeyinde kimlik bilgileri, FTP dağıtım kullanıcı adı biçiminde benzer `<app_name>\<username>`, ve Git dağıtım kullanıcı adı yalnızca `<username>` önceki olmadan `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="3ac98-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="3ac98-140">Uygulama düzeyinde kimlik bilgilerini sıfırlamak için:</span><span class="sxs-lookup"><span data-stu-id="3ac98-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="3ac98-141">İçinde [Azure portal](https://portal.azure.com), uygulama hizmeti tıklayın >  **&lt;any_app >** > **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="3ac98-142">Tıklatın **... Daha fazla** > **sıfırlama yayımlama profili**.</span><span class="sxs-lookup"><span data-stu-id="3ac98-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="3ac98-143">Tıklatın **Evet** sıfırlama onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="3ac98-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="3ac98-144">Sıfırlama eylemi herhangi önceden indirilmiş geçersiz kılar. PublishSettings dosyaları.</span><span class="sxs-lookup"><span data-stu-id="3ac98-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac98-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ac98-145">Next steps</span></span>

<span data-ttu-id="3ac98-146">Bu kimlik bilgileri, uygulamanızdan dağıtmak için nasıl kullanılacağını öğrenin [yerel Git](app-service-deploy-local-git.md) veya kullanarak [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="3ac98-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
