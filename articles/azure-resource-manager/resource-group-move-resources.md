---
title: "Azure kaynakları için yeni abonelik veya kaynak grubu taşıma | Microsoft Docs"
description: "Yeni kaynak grubu ya da abonelik kaynaklarını taşımak için Azure Resource Manager kullanın."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="51381-103">Kaynakları yeni kaynak grubuna veya aboneliğe taşıyın.</span><span class="sxs-lookup"><span data-stu-id="51381-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="51381-104">Bu konu, yeni bir abonelik veya yeni bir kaynak grubu aynı abonelikte kaynakları taşımak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="51381-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="51381-105">Kaynak taşıma için portal, PowerShell, Azure CLI veya REST API'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="51381-106">Taşıma işlemleri bu konuda Azure Destek'ten herhangi bir Yardım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="51381-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="51381-107">Kaynaklar taşınırken işlemi sırasında kaynak grubu ve hedef grubu kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="51381-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="51381-108">Yazma ve silme işlemleri taşıma işlemi tamamlanana kadar kaynak gruplarında engellenir.</span><span class="sxs-lookup"><span data-stu-id="51381-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="51381-109">Bu kilit ekleyemez, güncelleştirme veya kaynak gruplarındaki kaynakları silin, ancak kaynaklar dondurulmuş gelmez anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="51381-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="51381-110">Örneğin, bir SQL Server ve veritabanının yeni bir kaynak grubuna taşırsanız, veritabanı kullanan bir uygulama kapalı kalma süresi karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="51381-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="51381-111">Bunu hala okuyabilir ve veritabanına yazma.</span><span class="sxs-lookup"><span data-stu-id="51381-111">It can still read and write to the database.</span></span>

<span data-ttu-id="51381-112">Kaynağın konumu değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="51381-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="51381-113">Bir kaynak taşıma yalnızca bu yeni bir kaynak grubuna taşınır.</span><span class="sxs-lookup"><span data-stu-id="51381-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="51381-114">Yeni kaynak grubu farklı bir konum olabilir, ancak kaynak konumunu değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="51381-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="51381-115">Bu makalede, mevcut Azure içindeki kaynaklara önerme hesap taşımayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="51381-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="51381-116">Gerçekte (önceden ödenecek Kullandıkça Öde yükseltme gibi) sunan Azure hesabınızda değiştirmek mevcut kaynakları ile çalışmak için bkz: devam ederken istiyorsanız [Azure aboneliğinizi başka bir teklife geç](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="51381-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="51381-117">Kaynakları geçmeden önce denetim listesi</span><span class="sxs-lookup"><span data-stu-id="51381-117">Checklist before moving resources</span></span>
<span data-ttu-id="51381-118">Bir kaynağı taşımadan önce gerçekleştirmeniz gereken bazı önemli adımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="51381-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="51381-119">Bu koşulları doğrulayarak hataları önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="51381-120">Kaynak ve hedef abonelikler aynı içinde bulunmalıdır [Azure Active Directory Kiracı](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="51381-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="51381-121">Her iki aboneliğin aynı Kiracı kimliği olduğunu denetlemek için Azure PowerShell veya Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="51381-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="51381-122">Azure PowerShell için kullanın:</span><span class="sxs-lookup"><span data-stu-id="51381-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="51381-123">Azure CLI 2.0 için kullanın:</span><span class="sxs-lookup"><span data-stu-id="51381-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="51381-124">Kaynak ve hedef abonelikler için Kiracı kimlikleri aynı değilse, abonelik için dizini değiştirmek deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="51381-125">Ancak, bu seçenek yalnızca bir Microsoft hesabıyla (Kurumsal bir hesap değil) oturum açmış hizmet yöneticileri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="51381-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="51381-126">Dizini değiştirme girişiminde oturum [Klasik portal](https://manage.windowsazure.com/)seçip **ayarları**ve aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="51381-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="51381-127">Varsa **dizini Düzenle** simgesi kullanılabilir, ilişkili Azure Active Directory değiştirmek için seçin.</span><span class="sxs-lookup"><span data-stu-id="51381-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![dizini Düzenle](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="51381-129">Bu simge kullanılabilir durumda değilse, kaynakları için yeni bir kiracı taşımak için desteğe başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="51381-130">Hizmet, kaynakları taşıma olanağını sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="51381-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="51381-131">Bu konu, taşıma kaynakları hangi hizmetlerin etkinleştirmek ve hangi hizmetlerin taşıma kaynakları etkinleştirmeyin listeler.</span><span class="sxs-lookup"><span data-stu-id="51381-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="51381-132">Hedef abonelik, taşınan kaynağın kaynak sağlayıcısına kayıtlı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51381-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="51381-133">Belirten bir hata alırsanız, **kaynak türü için abonelik kayıtlı değil**.</span><span class="sxs-lookup"><span data-stu-id="51381-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="51381-134">Kaynağı taşıdığınız yeni abonelik, ilgili kaynak türüyle daha önce kullanılmamışsa bu sorunla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="51381-135">Kayıt durumunu denetleme ve kaynak sağlayıcılarını kaydetme hakkında bilgi almak için bkz. [Kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="51381-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="51381-136">Destek çağrısı yapıldığında</span><span class="sxs-lookup"><span data-stu-id="51381-136">When to call support</span></span>
<span data-ttu-id="51381-137">Bu konuda gösterilen Self Servis işlemleri üzerinden en fazla kaynak taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="51381-138">Self Servis işlemleri için kullanın:</span><span class="sxs-lookup"><span data-stu-id="51381-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="51381-139">Resource Manager kaynaklarını taşıma</span><span class="sxs-lookup"><span data-stu-id="51381-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="51381-140">Klasik kaynakları göre taşımak [Klasik dağıtım kısıtlamaları](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="51381-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="51381-141">Gerektiğinde desteğini arayın:</span><span class="sxs-lookup"><span data-stu-id="51381-141">Call support when you need to:</span></span>

* <span data-ttu-id="51381-142">Kaynaklarınızın bir yeni bir Azure hesabı (ve Azure Active Directory kiracısı) taşıyın.</span><span class="sxs-lookup"><span data-stu-id="51381-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="51381-143">Klasik kaynakları taşımak ancak kısıtlamalarla sorunu yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="51381-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="51381-144">Taşıma Etkinleştirme Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="51381-144">Services that enable move</span></span>
<span data-ttu-id="51381-145">Şimdilik, bir yeni kaynak grubu ve abonelik için taşıma etkinleştirmek hizmetler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51381-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="51381-146">API Management</span><span class="sxs-lookup"><span data-stu-id="51381-146">API Management</span></span>
* <span data-ttu-id="51381-147">App Service uygulamalarının (web uygulamaları) - bkz [App Service sınırlamalar](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="51381-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="51381-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="51381-148">Application Insights</span></span>
* <span data-ttu-id="51381-149">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="51381-149">Automation</span></span>
* <span data-ttu-id="51381-150">Batch</span><span class="sxs-lookup"><span data-stu-id="51381-150">Batch</span></span>
* <span data-ttu-id="51381-151">Bing Haritalar</span><span class="sxs-lookup"><span data-stu-id="51381-151">Bing Maps</span></span>
* <span data-ttu-id="51381-152">CDN</span><span class="sxs-lookup"><span data-stu-id="51381-152">CDN</span></span>
* <span data-ttu-id="51381-153">Bulut Hizmetleri - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="51381-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="51381-154">Bilişsel hizmetler</span><span class="sxs-lookup"><span data-stu-id="51381-154">Cognitive Services</span></span>
* <span data-ttu-id="51381-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="51381-155">Content Moderator</span></span>
* <span data-ttu-id="51381-156">Veri Kataloğu</span><span class="sxs-lookup"><span data-stu-id="51381-156">Data Catalog</span></span>
* <span data-ttu-id="51381-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="51381-157">Data Factory</span></span>
* <span data-ttu-id="51381-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="51381-158">Data Lake Analytics</span></span>
* <span data-ttu-id="51381-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="51381-159">Data Lake Store</span></span>
* <span data-ttu-id="51381-160">DNS</span><span class="sxs-lookup"><span data-stu-id="51381-160">DNS</span></span>
* <span data-ttu-id="51381-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="51381-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="51381-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="51381-162">Event Hubs</span></span>
* <span data-ttu-id="51381-163">Bkz: Hdınsight kümeleri - [Hdınsight sınırlamaları](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="51381-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="51381-164">IOT hub'ları</span><span class="sxs-lookup"><span data-stu-id="51381-164">IoT Hubs</span></span>
* <span data-ttu-id="51381-165">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="51381-165">Key Vault</span></span>
* <span data-ttu-id="51381-166">Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="51381-166">Load Balancers</span></span>
* <span data-ttu-id="51381-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="51381-167">Logic Apps</span></span>
* <span data-ttu-id="51381-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="51381-168">Machine Learning</span></span>
* <span data-ttu-id="51381-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="51381-169">Media Services</span></span>
* <span data-ttu-id="51381-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="51381-170">Mobile Engagement</span></span>
* <span data-ttu-id="51381-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="51381-171">Notification Hubs</span></span>
* <span data-ttu-id="51381-172">Operasyonel Öngörüler</span><span class="sxs-lookup"><span data-stu-id="51381-172">Operational Insights</span></span>
* <span data-ttu-id="51381-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="51381-173">Operations Management</span></span>
* <span data-ttu-id="51381-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="51381-174">Power BI</span></span>
* <span data-ttu-id="51381-175">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="51381-175">Redis Cache</span></span>
* <span data-ttu-id="51381-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="51381-176">Scheduler</span></span>
* <span data-ttu-id="51381-177">Arama</span><span class="sxs-lookup"><span data-stu-id="51381-177">Search</span></span>
* <span data-ttu-id="51381-178">Sunucu Yönetimi</span><span class="sxs-lookup"><span data-stu-id="51381-178">Server Management</span></span>
* <span data-ttu-id="51381-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="51381-179">Service Bus</span></span>
* <span data-ttu-id="51381-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="51381-180">Service Fabric</span></span>
* <span data-ttu-id="51381-181">Depolama</span><span class="sxs-lookup"><span data-stu-id="51381-181">Storage</span></span>
* <span data-ttu-id="51381-182">Depolama (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="51381-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="51381-183">Akış analizi - Stream Analytics işleri de çalıştırırken taşınamaz durumu.</span><span class="sxs-lookup"><span data-stu-id="51381-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="51381-184">SQL veritabanı sunucusu - veritabanı ve sunucu, aynı kaynak grubunda bulunmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="51381-185">Bir SQL server taşıdığınızda, tüm veritabanlarını da taşınır.</span><span class="sxs-lookup"><span data-stu-id="51381-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="51381-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="51381-186">Traffic Manager</span></span>
* <span data-ttu-id="51381-187">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="51381-187">Virtual Machines</span></span>
* <span data-ttu-id="51381-188">Sanal makineler sertifikayla anahtar kasasında depolanan - yeni kaynak grubu aynı abonelikte etkindir, ancak çapraz abonelik taşıma etkin değil taşıyın.</span><span class="sxs-lookup"><span data-stu-id="51381-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="51381-189">Sanal makineler (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="51381-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="51381-190">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="51381-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="51381-191">VNet eşlemesi devre dışı bırakılmış kadar sanal ağlar - şu anda, eşlenmiş bir sanal ağ taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="51381-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="51381-192">Sonra devre dışı, sanal ağ başarıyla taşınabilir ve VNet eşlemesi etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="51381-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="51381-193">Ayrıca, sanal ağ kaynak Gezinti bağlantıları olan herhangi bir alt ağ içeriyorsa, bir sanal ağ farklı bir aboneliğe taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="51381-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="51381-194">Örneğin, bu alt ağ Microsoft.Cache redis kaynak dağıtıldığında bir sanal ağ alt kaynak Gezinti bağlantısı vardır.</span><span class="sxs-lookup"><span data-stu-id="51381-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="51381-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="51381-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="51381-196">Taşıma etkinleştirmeyin Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="51381-196">Services that do not enable move</span></span>
<span data-ttu-id="51381-197">Şu anda bir kaynak taşıma etkinleştirmeyin hizmetler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51381-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="51381-198">AD etki alanı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="51381-198">AD Domain Services</span></span>
* <span data-ttu-id="51381-199">AD karma sistem durumu hizmeti</span><span class="sxs-lookup"><span data-stu-id="51381-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="51381-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="51381-200">Application Gateway</span></span>
* <span data-ttu-id="51381-201">Yönetilen bir diske sahip sanal makinelerle kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="51381-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="51381-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="51381-202">BizTalk Services</span></span>
* <span data-ttu-id="51381-203">Kapsayıcı Hizmeti</span><span class="sxs-lookup"><span data-stu-id="51381-203">Container Service</span></span>
* <span data-ttu-id="51381-204">Express Route</span><span class="sxs-lookup"><span data-stu-id="51381-204">Express Route</span></span>
* <span data-ttu-id="51381-205">DevTest Labs - taşıma aynı Abonelikteki yeni kaynak grubu için etkinleştirildi, ancak çapraz abonelik taşıma etkin değil.</span><span class="sxs-lookup"><span data-stu-id="51381-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="51381-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="51381-206">Dynamics LCS</span></span>
* <span data-ttu-id="51381-207">Yönetilen disklerden oluşturulan görüntüler</span><span class="sxs-lookup"><span data-stu-id="51381-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="51381-208">Yönetilen Diskler</span><span class="sxs-lookup"><span data-stu-id="51381-208">Managed Disks</span></span>
* <span data-ttu-id="51381-209">Yönetilen uygulamalar</span><span class="sxs-lookup"><span data-stu-id="51381-209">Managed Applications</span></span>
* <span data-ttu-id="51381-210">Kurtarma Hizmetleri kasası - ayrıca yapın kurtarma Hizmetleri kasası ile ilişkili işlem, ağ ve depolama kaynaklarını taşıyamazsınız bkz [kurtarma Hizmetleri sınırlamaları](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="51381-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="51381-211">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="51381-211">Security</span></span>
* <span data-ttu-id="51381-212">Yönetilen disklerden oluşturulan anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="51381-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="51381-213">StorSimple cihaz Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="51381-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="51381-214">Yönetilen bir diske sahip sanal makineler</span><span class="sxs-lookup"><span data-stu-id="51381-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="51381-215">Bkz: Sanal ağları (Klasik) - [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="51381-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="51381-216">Market kaynaklardan - oluşturulan sanal makineleri abonelikler arasında taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="51381-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="51381-217">Kaynağın geçerli abonelikte sağlaması kaldırılıyor. sağlaması ve yeniden yeni abonelikte dağıtılmış gerekiyor</span><span class="sxs-lookup"><span data-stu-id="51381-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="51381-218">App Service sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="51381-218">App Service limitations</span></span>
<span data-ttu-id="51381-219">Uygulama hizmeti uygulamaları ile çalışırken, yalnızca bir uygulama hizmeti planı taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="51381-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="51381-220">App Service uygulamalarının taşımak için seçenekleriniz şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51381-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="51381-221">Uygulama hizmeti planı ve diğer tüm uygulama hizmeti kaynakları bu kaynak grubunda zaten App Service kaynakları yok yeni bir kaynak grubuna taşıyın.</span><span class="sxs-lookup"><span data-stu-id="51381-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="51381-222">Bu gereksinim, hatta uygulama hizmeti plan ile ilişkili olmayan uygulama hizmeti kaynakları taşımalısınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="51381-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="51381-223">Uygulamalar farklı bir kaynak grubuna taşımak, ancak tüm uygulama hizmeti planları özgün kaynak grubunda tutun.</span><span class="sxs-lookup"><span data-stu-id="51381-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="51381-224">Uygulama hizmeti planı düzgün çalışabilmesi için aynı kaynak grubunda için uygulaması olarak bulunmaları gerekmez.</span><span class="sxs-lookup"><span data-stu-id="51381-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="51381-225">Örneğin, kaynak grubunuz varsa:</span><span class="sxs-lookup"><span data-stu-id="51381-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="51381-226">**Web-a** ile ilişkili **planı-a**</span><span class="sxs-lookup"><span data-stu-id="51381-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="51381-227">**Web b** ile ilişkili **planı b**</span><span class="sxs-lookup"><span data-stu-id="51381-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="51381-228">Seçenekleriniz şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51381-228">Your options are:</span></span>

* <span data-ttu-id="51381-229">Taşıma **web-a**, **planı-a**, **web-b**, ve **planı b**</span><span class="sxs-lookup"><span data-stu-id="51381-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="51381-230">Taşıma **web-a** ve **web-b**</span><span class="sxs-lookup"><span data-stu-id="51381-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="51381-231">Taşıma **web-a**</span><span class="sxs-lookup"><span data-stu-id="51381-231">Move **web-a**</span></span>
* <span data-ttu-id="51381-232">Taşıma **web-b**</span><span class="sxs-lookup"><span data-stu-id="51381-232">Move **web-b**</span></span>

<span data-ttu-id="51381-233">Diğer tüm birleşimler, bir uygulama hizmeti planı (uygulama hizmeti kaynak türlü) taşırken bırakılamaz arkasındaki bir kaynak türü bırakarak içerir.</span><span class="sxs-lookup"><span data-stu-id="51381-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="51381-234">Web uygulamanızın farklı bir kaynak grubu, uygulama hizmeti planı daha bulunur, ancak her ikisi de yeni bir kaynak grubuna taşımak istediğiniz iki adımda taşıma gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="51381-235">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="51381-235">For example:</span></span>

* <span data-ttu-id="51381-236">**Web-a** bulunan **web grubu**</span><span class="sxs-lookup"><span data-stu-id="51381-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="51381-237">**planı bir** bulunan **planı Grup**</span><span class="sxs-lookup"><span data-stu-id="51381-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="51381-238">İstediğiniz **web-a** ve **planı-a** bulunması için **birleştirilmiş Grup**</span><span class="sxs-lookup"><span data-stu-id="51381-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="51381-239">Bu taşıma gerçekleştirmek için iki ayrı taşıma işlemi aşağıdaki sırayla gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="51381-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="51381-240">Taşıma **web-a** için **planı Grup**</span><span class="sxs-lookup"><span data-stu-id="51381-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="51381-241">Taşıma **web-a** ve **planı-a** için **Birleştirilmiş grup**.</span><span class="sxs-lookup"><span data-stu-id="51381-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="51381-242">Yeni kaynak grubu veya abonelik sorunları olmadan, bir uygulama hizmet sertifikası taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="51381-243">Ancak, web uygulamanızı dışarıdan satın ve uygulamaya karşıya bir SSL sertifikası içeriyorsa, web uygulaması taşımadan önce sertifika silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="51381-244">Örneğin, aşağıdaki adımları gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51381-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="51381-245">Karşıya yüklenen sertifikanın web uygulamasından silme</span><span class="sxs-lookup"><span data-stu-id="51381-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="51381-246">Web uygulaması taşıma</span><span class="sxs-lookup"><span data-stu-id="51381-246">Move the web app</span></span>
3. <span data-ttu-id="51381-247">Web uygulaması'na ve sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="51381-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="51381-248">Kurtarma Hizmetleri kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="51381-248">Recovery Services limitations</span></span>
<span data-ttu-id="51381-249">Ağ, depolama için etkin değil taşıyın veya işlem kaynaklarını Azure Site Recovery ile olağanüstü durum kurtarma ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51381-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="51381-250">Örneğin, şirket içi makinelerinizi bir depolama hesabına (Storage1) çoğaltmasını ayarladıktan ve bir sanal ağa (Network1) bağlı sanal makine (VM1) olarak Azure için yük devretme sonrasında gündeme için korumalı makine istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="51381-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="51381-251">Bu Azure kaynakları - Storage1, VM1 ve Network1 - hiçbirini aynı abonelik içindeki kaynak grupları arasında veya abonelikler arasında taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="51381-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="51381-252">Hdınsight sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="51381-252">HDInsight limitations</span></span>

<span data-ttu-id="51381-253">Yeni Abonelik veya kaynak grubu için Hdınsight kümeleri taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51381-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="51381-254">Ancak, ağ kaynaklarını (örneğin, sanal ağ, NIC veya yük dengeleyici) bir Hdınsight kümesine bağlı abonelikler arasında taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="51381-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="51381-255">Ayrıca, küme için bir sanal makineye bağlı bir NIC yeni bir kaynak grubuna taşıyamazsınız.</span><span class="sxs-lookup"><span data-stu-id="51381-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="51381-256">Hdınsight kümesi için yeni bir abonelik taşırken, diğer kaynakları (örneğin, depolama hesabı) taşıyın.</span><span class="sxs-lookup"><span data-stu-id="51381-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="51381-257">Ardından, Hdınsight kümesi tek başına taşıyın.</span><span class="sxs-lookup"><span data-stu-id="51381-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="51381-258">Klasik dağıtım sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="51381-258">Classic deployment limitations</span></span>
<span data-ttu-id="51381-259">Klasik modeli aracılığıyla dağıtılan kaynakları taşıma seçeneklerini taşıdığınız bir abonelik içindeki veya yeni bir abonelik için kaynaklara göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="51381-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="51381-260">Aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="51381-260">Same subscription</span></span>
<span data-ttu-id="51381-261">Kaynaklar aynı abonelik içindeki başka bir kaynak grubu için bir kaynak grubundan taşırken, aşağıdaki kısıtlamalar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="51381-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="51381-262">Sanal ağları (Klasik) taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="51381-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="51381-263">Sanal makineler (Klasik) bulut hizmetiyle taşınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="51381-264">Tüm sanal makineleri taşıma içerdiği durumlarda bulut hizmeti yalnızca taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="51381-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="51381-265">Aynı anda yalnızca bir bulut hizmeti taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="51381-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="51381-266">Aynı anda yalnızca bir depolama hesabı (Klasik) taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="51381-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="51381-267">Depolama hesabı (Klasik), sanal makine ya da bir bulut hizmeti ile aynı işlemde taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="51381-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="51381-268">Klasik kaynaklar aynı abonelik içindeki yeni bir kaynak grubuna taşımak için standart taşıma işlemleri aracılığıyla kullanmak [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), veya [REST API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="51381-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="51381-269">Resource Manager kaynaklarını taşımak için kullandığınız gibi işlemlerin aynısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="51381-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="51381-270">Yeni abonelik</span><span class="sxs-lookup"><span data-stu-id="51381-270">New subscription</span></span>
<span data-ttu-id="51381-271">Kaynaklar için yeni bir abonelik taşırken, aşağıdaki kısıtlamalar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="51381-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="51381-272">Abonelikteki tüm Klasik kaynaklar aynı işlem içinde taşınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="51381-273">Hedef abonelik diğer Klasik kaynakları içermemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="51381-274">Taşıma yalnızca klasik taşıma için ayrı bir REST API aracılığıyla istenebilir.</span><span class="sxs-lookup"><span data-stu-id="51381-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="51381-275">Klasik kaynaklar için yeni bir abonelik taşırken standart Resource Manager taşıma komutlar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="51381-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="51381-276">Klasik kaynaklar için yeni bir aboneliği taşımak için Klasik kaynakları için belirli REST işlemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="51381-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="51381-277">REST kullanmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="51381-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="51381-278">Kaynak abonelik bir çapraz abonelik taşıma katılabilmesi için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="51381-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="51381-279">Aşağıdaki işlemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="51381-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="51381-280">İstek gövdesinde şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="51381-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="51381-281">Yanıt için doğrulama işlemi aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="51381-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="51381-282">Hedef abonelik bir çapraz abonelik taşıma katılabilmesi için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="51381-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="51381-283">Aşağıdaki işlemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="51381-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="51381-284">İstek gövdesinde şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="51381-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="51381-285">Kaynak abonelik doğrulama ile aynı biçimi yanıt kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="51381-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="51381-286">Her iki aboneliğin doğrulama başarılı olursa, tüm Klasik kaynaklar bir abonelikten şu işlemi başka bir aboneliğe taşıyın:</span><span class="sxs-lookup"><span data-stu-id="51381-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="51381-287">İstek gövdesinde şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="51381-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="51381-288">İşlemi birkaç dakika çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="51381-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="51381-289">Portal kullanma</span><span class="sxs-lookup"><span data-stu-id="51381-289">Use portal</span></span>
<span data-ttu-id="51381-290">Kaynakları taşımak için bu kaynakları içeren kaynak grubunu seçin ve ardından **taşıma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="51381-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Kaynakları taşıma](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="51381-292">Yeni bir kaynak grubu veya yeni bir abonelik için kaynakları taşıma olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="51381-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="51381-293">Taşıma için kaynak ve hedef kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="51381-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="51381-294">Bu kaynaklar için komut dosyaları güncelleştirmek ve seçmek gereken kabul **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="51381-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="51381-295">Önceki adımda Düzenle abonelik simgesini seçtiyseniz, hedef abonelik seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51381-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![hedef seçin](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="51381-297">İçinde **bildirimleri**, taşıma işleminin çalıştığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="51381-297">In **Notifications**, you see that the move operation is running.</span></span>

![taşıma durumunu göster](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="51381-299">Tamamlandığında, sonucu bildirilir.</span><span class="sxs-lookup"><span data-stu-id="51381-299">When it has completed, you are notified of the result.</span></span>

![taşıma sonucu göster](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="51381-301">PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="51381-301">Use PowerShell</span></span>
<span data-ttu-id="51381-302">Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için kullanmak `Move-AzureRmResource` komutu.</span><span class="sxs-lookup"><span data-stu-id="51381-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="51381-303">İlk örnek yeni bir kaynak grubu için bir kaynak taşıma gösterir.</span><span class="sxs-lookup"><span data-stu-id="51381-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="51381-304">İkinci örnek, birden çok kaynakları yeni bir kaynak grubuna taşımak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="51381-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="51381-305">Yeni bir aboneliği taşımak için bir değer dahil `DestinationSubscriptionId` parametresi.</span><span class="sxs-lookup"><span data-stu-id="51381-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="51381-306">Belirtilen kaynaklar taşımak istediğiniz onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="51381-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="51381-307">Azure CLI 2.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="51381-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="51381-308">Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için kullanmak `az resource move` komutu.</span><span class="sxs-lookup"><span data-stu-id="51381-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="51381-309">Kaynak taşımak için kimlikleri kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="51381-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="51381-310">Kaynak kimlikleri aşağıdaki komutu kullanarak elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51381-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="51381-311">Aşağıdaki örnek, bir depolama hesabını yeni bir kaynak grubuna taşımak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="51381-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="51381-312">İçinde `--ids` parametresi, kaynak taşımak için kimlikleri boşlukla ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="51381-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="51381-313">Yeni bir abonelik taşımanızı sağlayan `--destination-subscription-id` parametresi.</span><span class="sxs-lookup"><span data-stu-id="51381-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="51381-314">Azure CLI 1.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="51381-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="51381-315">Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için kullanmak `azure resource move` komutu.</span><span class="sxs-lookup"><span data-stu-id="51381-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="51381-316">Kaynak taşımak için kimlikleri kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="51381-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="51381-317">Kaynak kimlikleri aşağıdaki komutu kullanarak elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51381-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="51381-318">Aşağıdaki biçimde döndürür:</span><span class="sxs-lookup"><span data-stu-id="51381-318">Which returns the following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="51381-319">Aşağıdaki örnek, bir depolama hesabını yeni bir kaynak grubuna taşımak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="51381-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="51381-320">İçinde `-i` parametresi, kaynak kimlikleri taşımak için virgülle ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="51381-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="51381-321">Belirtilen kaynak taşımak istediğiniz onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="51381-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="51381-322">REST API’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="51381-322">Use REST API</span></span>
<span data-ttu-id="51381-323">Başka bir kaynak grubuna veya aboneliğe mevcut kaynakları taşımak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="51381-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="51381-324">İstek gövdesinde hedef kaynak grubu ve kaynakları taşımak için belirtin.</span><span class="sxs-lookup"><span data-stu-id="51381-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="51381-325">Taşıma REST işlemi hakkında daha fazla bilgi için bkz: [taşıma kaynakları](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="51381-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51381-326">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51381-326">Next steps</span></span>
* <span data-ttu-id="51381-327">Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında bilgi edinmek için [Resource Manager ile Azure PowerShell'i kullanarak](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="51381-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="51381-328">Aboneliğinizi yönetmek için Azure CLI komutları hakkında bilgi edinmek için [Resource Manager ile Azure CLI kullanarak](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="51381-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="51381-329">Aboneliğinizi yönetmeye yönelik portal özellikleri hakkında bilgi edinmek için [kaynakları yönetmek için Azure portalını kullanarak](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="51381-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="51381-330">Kaynaklarınız için bir mantıksal kuruluş uygulama hakkında bilgi edinmek için [etiketleri kullanarak kaynaklarınızı düzenleme](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="51381-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
