---
title: "aaaMove, Azure kaynaklarını toonew abonelik veya kaynak grubu | Microsoft Docs"
description: "Azure Resource Manager toomove kaynakları tooa yeni kaynak grubu veya abonelik kullanın."
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
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="8cb2f-103">Kaynakları toonew kaynak grubuna veya aboneliğe taşıma</span><span class="sxs-lookup"><span data-stu-id="8cb2f-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="8cb2f-104">Bu konu, nasıl toomove kaynakları tooeither yeni bir abonelik veya yeni bir kaynak grubunda hello gösterir. aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="8cb2f-105">Merhaba portal, PowerShell, Azure CLI veya hello REST API toomove kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="8cb2f-106">Merhaba taşıma bu konudaki tüm Yardım Azure desteği olmadan kullanılabilir tooyou işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="8cb2f-107">Kaynaklar taşınırken hello kaynak grubu ve hello hedef grubu hello işlemi sırasında kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="8cb2f-108">Yazma ve silme işlemleri hello taşıma işlemi tamamlanana kadar hello kaynak gruplarında engellenir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="8cb2f-109">Bu kilit ekleyemez, güncelleştirme veya hello kaynak gruplarındaki kaynakları silin, ancak hello kaynakları dondurulmuş gelmez anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="8cb2f-110">Örneğin, bir SQL Server ve kendi veritabanı tooa yeni kaynak grubu taşırsanız, hello veritabanı kullanan bir uygulama kapalı kalma süresi karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="8cb2f-111">Bunu hala okuyabilir ve toohello veritabanı yazma.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="8cb2f-112">Merhaba kaynak hello konumunu değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="8cb2f-113">Bir kaynak taşıma yalnızca bu tooa yeni kaynak grubu taşınır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="8cb2f-114">Merhaba yeni kaynak grubu farklı bir konum olabilir, ancak hello kaynak hello konumunu değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="8cb2f-115">Bu makalede, mevcut Azure içindeki toomove kaynakların nasıl önerme hesap açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="8cb2f-116">Azure hesabınızda (Kullandıkça Öde toopre-ödeme yükseltme gibi), mevcut kaynaklarla toowork devam ederken sunumu gerçekten toochange istiyorsanız bkz [Azure aboneliği tooanother teklifiniz geçiş](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="8cb2f-117">Kaynakları geçmeden önce denetim listesi</span><span class="sxs-lookup"><span data-stu-id="8cb2f-117">Checklist before moving resources</span></span>
<span data-ttu-id="8cb2f-118">Bir kaynak taşımadan önce bazı önemli adımlar tooperform vardır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="8cb2f-119">Bu koşulları doğrulayarak hataları önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="8cb2f-120">Merhaba kaynak ve hedef abonelikler hello içinde aynı bulunmalıdır [Azure Active Directory Kiracı](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="8cb2f-121">Her iki aboneliğin sahip Merhaba, aynı toocheck Kiracı kimliği, Azure PowerShell veya Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="8cb2f-122">Azure PowerShell için kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="8cb2f-123">Azure CLI 2.0 için kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="8cb2f-124">Merhaba kimlikleri için Kiracı varsa hello kaynak ve hedef abonelikler olmayan aynı hello toochange hello dizin hello abonelik için deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="8cb2f-125">Ancak, bu seçenek yalnızca kullanılabilir tooService bir Microsoft hesabıyla (Kurumsal bir hesap değil) oturum açmış yöneticileri içindir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="8cb2f-126">Başlangıç dizini, toohello günlüğünde değiştirme tooattempt [Klasik portal](https://manage.windowsazure.com/)seçip **ayarları**ve hello abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="8cb2f-127">Merhaba, **dizini Düzenle** simge mevcut ise, toochange seçin hello ilişkili Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![dizini Düzenle](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="8cb2f-129">Bu simge kullanılabilir durumda değilse, desteği toomove hello kaynakları tooa yeni Kiracı başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="8cb2f-130">Merhaba hizmetini hello özelliği toomove kaynakları etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="8cb2f-131">Bu konu, taşıma kaynakları hangi hizmetlerin etkinleştirmek ve hangi hizmetlerin taşıma kaynakları etkinleştirmeyin listeler.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="8cb2f-132">Merhaba hedef abonelik taşınan hello kaynağının hello kaynak sağlayıcısı için kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="8cb2f-133">Bu hello bildiren bir hata alırsanız, **kaynak türü için abonelik kayıtlı değil**.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="8cb2f-134">Kaynak tooa yeni bir abonelik taşırken bu sorunla karşılaşabilir, ancak bu abonelik hiçbir zaman bu kaynak türü ile kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="8cb2f-135">toolearn nasıl toocheck hello kayıt durumunu ve kaynak sağlayıcıları kaydetme bkz [kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="8cb2f-136">Toocall desteği</span><span class="sxs-lookup"><span data-stu-id="8cb2f-136">When toocall support</span></span>
<span data-ttu-id="8cb2f-137">Bu konuda gösterilen hello Self Servis işlemleri üzerinden en fazla kaynak taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="8cb2f-138">Merhaba Self Servis işlemleri için kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="8cb2f-139">Resource Manager kaynaklarını taşıma</span><span class="sxs-lookup"><span data-stu-id="8cb2f-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="8cb2f-140">Toohello göre Klasik kaynakları taşımak [Klasik dağıtım kısıtlamaları](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="8cb2f-141">Gerektiğinde desteğini arayın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-141">Call support when you need to:</span></span>

* <span data-ttu-id="8cb2f-142">Kaynakları tooa yeni Azure hesabı (ve Azure Active Directory kiracısı) taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="8cb2f-143">Klasik kaynakları taşımak ancak hello kısıtlamalarla sorunu yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="8cb2f-144">Taşıma Etkinleştirme Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8cb2f-144">Services that enable move</span></span>
<span data-ttu-id="8cb2f-145">Şimdilik, taşıma tooboth yeni bir kaynak grubu ve abonelik etkinleştirmek hello hizmetler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="8cb2f-146">API Management</span><span class="sxs-lookup"><span data-stu-id="8cb2f-146">API Management</span></span>
* <span data-ttu-id="8cb2f-147">App Service uygulamalarının (web uygulamaları) - bkz [App Service sınırlamalar](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="8cb2f-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="8cb2f-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8cb2f-148">Application Insights</span></span>
* <span data-ttu-id="8cb2f-149">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="8cb2f-149">Automation</span></span>
* <span data-ttu-id="8cb2f-150">Batch</span><span class="sxs-lookup"><span data-stu-id="8cb2f-150">Batch</span></span>
* <span data-ttu-id="8cb2f-151">Bing Haritalar</span><span class="sxs-lookup"><span data-stu-id="8cb2f-151">Bing Maps</span></span>
* <span data-ttu-id="8cb2f-152">CDN</span><span class="sxs-lookup"><span data-stu-id="8cb2f-152">CDN</span></span>
* <span data-ttu-id="8cb2f-153">Bulut Hizmetleri - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8cb2f-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8cb2f-154">Bilişsel hizmetler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-154">Cognitive Services</span></span>
* <span data-ttu-id="8cb2f-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="8cb2f-155">Content Moderator</span></span>
* <span data-ttu-id="8cb2f-156">Veri Kataloğu</span><span class="sxs-lookup"><span data-stu-id="8cb2f-156">Data Catalog</span></span>
* <span data-ttu-id="8cb2f-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="8cb2f-157">Data Factory</span></span>
* <span data-ttu-id="8cb2f-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8cb2f-158">Data Lake Analytics</span></span>
* <span data-ttu-id="8cb2f-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8cb2f-159">Data Lake Store</span></span>
* <span data-ttu-id="8cb2f-160">DNS</span><span class="sxs-lookup"><span data-stu-id="8cb2f-160">DNS</span></span>
* <span data-ttu-id="8cb2f-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8cb2f-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="8cb2f-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8cb2f-162">Event Hubs</span></span>
* <span data-ttu-id="8cb2f-163">Bkz: Hdınsight kümeleri - [Hdınsight sınırlamaları](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="8cb2f-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="8cb2f-164">IOT hub'ları</span><span class="sxs-lookup"><span data-stu-id="8cb2f-164">IoT Hubs</span></span>
* <span data-ttu-id="8cb2f-165">Anahtar Kasası</span><span class="sxs-lookup"><span data-stu-id="8cb2f-165">Key Vault</span></span>
* <span data-ttu-id="8cb2f-166">Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="8cb2f-166">Load Balancers</span></span>
* <span data-ttu-id="8cb2f-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="8cb2f-167">Logic Apps</span></span>
* <span data-ttu-id="8cb2f-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8cb2f-168">Machine Learning</span></span>
* <span data-ttu-id="8cb2f-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="8cb2f-169">Media Services</span></span>
* <span data-ttu-id="8cb2f-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8cb2f-170">Mobile Engagement</span></span>
* <span data-ttu-id="8cb2f-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="8cb2f-171">Notification Hubs</span></span>
* <span data-ttu-id="8cb2f-172">Operasyonel Öngörüler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-172">Operational Insights</span></span>
* <span data-ttu-id="8cb2f-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="8cb2f-173">Operations Management</span></span>
* <span data-ttu-id="8cb2f-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="8cb2f-174">Power BI</span></span>
* <span data-ttu-id="8cb2f-175">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="8cb2f-175">Redis Cache</span></span>
* <span data-ttu-id="8cb2f-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-176">Scheduler</span></span>
* <span data-ttu-id="8cb2f-177">Arama</span><span class="sxs-lookup"><span data-stu-id="8cb2f-177">Search</span></span>
* <span data-ttu-id="8cb2f-178">Sunucu Yönetimi</span><span class="sxs-lookup"><span data-stu-id="8cb2f-178">Server Management</span></span>
* <span data-ttu-id="8cb2f-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="8cb2f-179">Service Bus</span></span>
* <span data-ttu-id="8cb2f-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8cb2f-180">Service Fabric</span></span>
* <span data-ttu-id="8cb2f-181">Depolama</span><span class="sxs-lookup"><span data-stu-id="8cb2f-181">Storage</span></span>
* <span data-ttu-id="8cb2f-182">Depolama (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8cb2f-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8cb2f-183">Akış analizi - Stream Analytics işleri de çalıştırırken taşınamaz durumu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="8cb2f-184">SQL veritabanı sunucusuna - hello veritabanı ve sunucu bulunmalıdır hello aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="8cb2f-185">Bir SQL server taşıdığınızda, tüm veritabanlarını da taşınır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="8cb2f-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8cb2f-186">Traffic Manager</span></span>
* <span data-ttu-id="8cb2f-187">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="8cb2f-187">Virtual Machines</span></span>
* <span data-ttu-id="8cb2f-188">Anahtar kasası - taşıma toonew kaynak grubu aynı abonelik içinde depolanan sertifika sanal makinelerle etkindir, ancak çapraz abonelik taşıma etkin değil.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="8cb2f-189">Sanal makineler (Klasik) - bkz [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8cb2f-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8cb2f-190">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="8cb2f-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="8cb2f-191">VNet eşlemesi devre dışı bırakılmış kadar sanal ağlar - şu anda, eşlenmiş bir sanal ağ taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="8cb2f-192">Bir kez devre dışı, sanal ağ başarıyla taşınabilmesi hello ve hello VNet eşlemesi etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="8cb2f-193">Ayrıca, kaynak Gezinti bağlantıları olan herhangi bir alt ağ Hello sanal ağ içeriyorsa, bir sanal ağ taşınan tooa farklı bir abonelik olamaz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="8cb2f-194">Örneğin, bu alt ağ Microsoft.Cache redis kaynak dağıtıldığında bir sanal ağ alt kaynak Gezinti bağlantısı vardır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="8cb2f-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="8cb2f-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="8cb2f-196">Taşıma etkinleştirmeyin Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8cb2f-196">Services that do not enable move</span></span>
<span data-ttu-id="8cb2f-197">şu anda bir kaynak taşıma etkinleştirmeyin hello hizmetler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="8cb2f-198">AD etki alanı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8cb2f-198">AD Domain Services</span></span>
* <span data-ttu-id="8cb2f-199">AD karma sistem durumu hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cb2f-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="8cb2f-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="8cb2f-200">Application Gateway</span></span>
* <span data-ttu-id="8cb2f-201">Yönetilen bir diske sahip sanal makinelerle kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="8cb2f-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="8cb2f-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="8cb2f-202">BizTalk Services</span></span>
* <span data-ttu-id="8cb2f-203">Kapsayıcı Hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cb2f-203">Container Service</span></span>
* <span data-ttu-id="8cb2f-204">Express Route</span><span class="sxs-lookup"><span data-stu-id="8cb2f-204">Express Route</span></span>
* <span data-ttu-id="8cb2f-205">DevTest Labs - taşıma toonew kaynak grubu aynı abonelikte etkindir, ancak abonelik taşıma etkin değil.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="8cb2f-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="8cb2f-206">Dynamics LCS</span></span>
* <span data-ttu-id="8cb2f-207">Yönetilen disklerden oluşturulan görüntüler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="8cb2f-208">Yönetilen Diskler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-208">Managed Disks</span></span>
* <span data-ttu-id="8cb2f-209">Yönetilen uygulamalar</span><span class="sxs-lookup"><span data-stu-id="8cb2f-209">Managed Applications</span></span>
* <span data-ttu-id="8cb2f-210">Kurtarma Hizmetleri kasası - ile ilişkili değil hello işlem, ağ ve depolama kaynakları taşıma kurtarma hizmetleri de hello yapmak kasa için bkz: [kurtarma Hizmetleri sınırlamaları](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="8cb2f-211">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="8cb2f-211">Security</span></span>
* <span data-ttu-id="8cb2f-212">Yönetilen disklerden oluşturulan anlık görüntüler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="8cb2f-213">StorSimple cihaz Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="8cb2f-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="8cb2f-214">Yönetilen bir diske sahip sanal makineler</span><span class="sxs-lookup"><span data-stu-id="8cb2f-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="8cb2f-215">Bkz: Sanal ağları (Klasik) - [Klasik dağıtım sınırlamaları](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="8cb2f-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="8cb2f-216">Market kaynaklardan - oluşturulan sanal makineleri abonelikler arasında taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="8cb2f-217">Merhaba geçerli abonelikte sağlaması kaldırılıyor. sağlaması ve yeniden hello yeni abonelikte dağıtılmış toobe kaynak gerekiyor</span><span class="sxs-lookup"><span data-stu-id="8cb2f-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="8cb2f-218">App Service sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="8cb2f-218">App Service limitations</span></span>
<span data-ttu-id="8cb2f-219">Uygulama hizmeti uygulamaları ile çalışırken, yalnızca bir uygulama hizmeti planı taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="8cb2f-220">toomove App Service uygulamalarının Seçenekleriniz şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="8cb2f-221">Merhaba uygulama hizmeti planı ve diğer tüm uygulama hizmeti kaynakları App Service kaynakları zaten sahip olmayan bu kaynak grubu tooa yeni kaynak grubu içinde taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="8cb2f-222">Uygulama hizmeti kaynakları bile taşımalısınız anlamına gelir hello bu gereksinim, uygulama hizmeti planı hello ile ilişkili değildir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="8cb2f-223">Hello uygulamaları tooa farklı bir kaynak grubu taşıma, ancak hello özgün kaynak grubundaki tüm uygulama hizmeti planları tutun.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="8cb2f-224">Merhaba uygulama hizmeti planı içinde tooreside gerekmez hello hello app hello uygulama toofunction için aynı kaynak grubunda doğru.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="8cb2f-225">Örneğin, kaynak grubunuz varsa:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="8cb2f-226">**Web-a** ile ilişkili **planı-a**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="8cb2f-227">**Web b** ile ilişkili **planı b**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="8cb2f-228">Seçenekleriniz şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-228">Your options are:</span></span>

* <span data-ttu-id="8cb2f-229">Taşıma **web-a**, **planı-a**, **web-b**, ve **planı b**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="8cb2f-230">Taşıma **web-a** ve **web-b**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="8cb2f-231">Taşıma **web-a**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-231">Move **web-a**</span></span>
* <span data-ttu-id="8cb2f-232">Taşıma **web-b**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-232">Move **web-b**</span></span>

<span data-ttu-id="8cb2f-233">Diğer tüm birleşimler, bir uygulama hizmeti planı (uygulama hizmeti kaynak türlü) taşırken bırakılamaz arkasındaki bir kaynak türü bırakarak içerir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="8cb2f-234">Web uygulamanızın farklı bir kaynak grubu, uygulama hizmeti planı daha bulunur, ancak her iki tooa yeni kaynak grubu toomove istediğiniz iki adımda hello taşıma gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="8cb2f-235">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-235">For example:</span></span>

* <span data-ttu-id="8cb2f-236">**Web-a** bulunan **web grubu**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="8cb2f-237">**planı bir** bulunan **planı Grup**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="8cb2f-238">İstediğiniz **web-a** ve **planı-a** tooreside içinde **birleştirilmiş Grup**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="8cb2f-239">Bu taşıma hello dizisi aşağıdaki iki ayrı taşıma işlemleri tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="8cb2f-240">Merhaba taşıma **web-a** çok**planı Grup**</span><span class="sxs-lookup"><span data-stu-id="8cb2f-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="8cb2f-241">Taşıma **web-a** ve **planı-a** çok**Birleştirilmiş grup**.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="8cb2f-242">Bir uygulama hizmet sertifikası tooa yeni kaynak grubu veya abonelik sorunları olmadan taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="8cb2f-243">Ancak, web uygulamanızı harici olarak satın alınan ve toohello uygulamanın karşıya bir SSL sertifikası içeriyorsa, taşıma hello web uygulaması önce hello sertifika silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="8cb2f-244">Örneğin, aşağıdaki adımları hello gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="8cb2f-245">Merhaba karşıya sertifika hello web uygulamasından silme</span><span class="sxs-lookup"><span data-stu-id="8cb2f-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="8cb2f-246">Taşıma hello web uygulaması</span><span class="sxs-lookup"><span data-stu-id="8cb2f-246">Move hello web app</span></span>
3. <span data-ttu-id="8cb2f-247">Merhaba sertifika toohello web uygulamasını yükleme</span><span class="sxs-lookup"><span data-stu-id="8cb2f-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="8cb2f-248">Kurtarma Hizmetleri kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="8cb2f-248">Recovery Services limitations</span></span>
<span data-ttu-id="8cb2f-249">Taşıma ağ, depolama için etkin değil veya işlem kaynakları Azure Site Recovery ile olağanüstü durum kurtarma yukarı tooset kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="8cb2f-250">Örneğin, şirket içi makineler tooa depolama hesabınız (Storage1) çoğaltmayı ayarlama ayarladığınız düşünün ve sonra Yük devretme tooAzure tooa sanal ağ (Network1) bir sanal makineye (VM1) bağlı olarak yukarı korumalı hello makine toocome istiyor.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="8cb2f-251">Bu Azure kaynakları - Storage1, VM1, hiçbirini taşıyamazsınız ve Network1 - arasında kaynak grupları hello aynı abonelik veya abonelikler arasında.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="8cb2f-252">Hdınsight sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="8cb2f-252">HDInsight limitations</span></span>

<span data-ttu-id="8cb2f-253">Hdınsight kümeleri tooa yeni abonelik veya kaynak grubu taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="8cb2f-254">Ancak, abonelikleri hello kaynakları bağlantılı toohello Hdınsight kümesi (örneğin, hello sanal ağ, NIC veya yük dengeleyici) ağ üzerinden taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="8cb2f-255">Ayrıca, tooa yeni kaynak grubu ekli tooa sanal makine hello küme için bir NIC taşınamıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="8cb2f-256">Bir Hdınsight kümesi tooa yeni abonelik taşırken, diğer kaynakları (gibi hello depolama hesabı) taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="8cb2f-257">Ardından, hello Hdınsight kümesi tek başına taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="8cb2f-258">Klasik dağıtım sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="8cb2f-258">Classic deployment limitations</span></span>
<span data-ttu-id="8cb2f-259">Merhaba hello Klasik modeli aracılığıyla dağıtılan kaynakları taşıma için seçenekler taşıdığınız bir abonelik veya tooa yeni abonelik içindeki hello kaynaklara göre değişir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="8cb2f-260">Aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="8cb2f-260">Same subscription</span></span>
<span data-ttu-id="8cb2f-261">Bir kaynak grubu tooanother kaynak grubundaki aynı abonelik, kısıtlamaları aşağıdaki hello uygulamak hello içindeki kaynaklar taşınırken:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="8cb2f-262">Sanal ağları (Klasik) taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="8cb2f-263">Sanal makineler (Klasik) hello bulut hizmetiyle taşınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="8cb2f-264">Merhaba taşıma tüm sanal makineleri içerdiğinde bulut hizmeti yalnızca taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="8cb2f-265">Aynı anda yalnızca bir bulut hizmeti taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="8cb2f-266">Aynı anda yalnızca bir depolama hesabı (Klasik) taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="8cb2f-267">Depolama hesabı (Klasik) hello taşınamaz bir sanal makine ya da bir bulut hizmeti ile aynı işlemi.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="8cb2f-268">toomove Klasik kaynakları tooa yeni kaynak grubu içinde Merhaba aynı abonelik, hello aracılığıyla hello standart taşıma işlemlerini kullanmak [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), veya [REST API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="8cb2f-269">Kullandığınız hello aynı işlemleri Resource Manager kaynaklarını taşımak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="8cb2f-270">Yeni abonelik</span><span class="sxs-lookup"><span data-stu-id="8cb2f-270">New subscription</span></span>
<span data-ttu-id="8cb2f-271">Kaynakları tooa yeni abonelik taşırken kısıtlamaları aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="8cb2f-272">Hello hello Abonelikteki tüm Klasik kaynaklar taşınmalıdır aynı işlemi.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="8cb2f-273">Merhaba hedef abonelik diğer Klasik kaynakları içermemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="8cb2f-274">Merhaba taşıma yalnızca klasik taşıma için ayrı bir REST API aracılığıyla istenebilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="8cb2f-275">Klasik kaynaklar tooa yeni abonelik taşırken Hello standart Resource Manager taşıma komutlar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="8cb2f-276">toomove Klasik kaynakları tooa yeni abonelik, belirli tooclassic kaynakları hello REST işlemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="8cb2f-277">toouse REST, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="8cb2f-278">Çapraz abonelik hello kaynak abonelik katılabilir onay taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="8cb2f-279">Merhaba aşağıdaki işlemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="8cb2f-280">Merhaba istek gövdesinde şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="8cb2f-281">Merhaba doğrulama işlemi için Hello yanıt biçimi aşağıdaki hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="8cb2f-282">Çapraz abonelik hello hedef abonelik katılabilir onay taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="8cb2f-283">Merhaba aşağıdaki işlemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="8cb2f-284">Merhaba istek gövdesinde şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="8cb2f-285">Merhaba yanıt aynı hello kaynak abonelik doğrulama biçimi hello kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="8cb2f-286">Her iki aboneliğin doğrulama başarılı olursa, tüm Klasik kaynaklar ile aşağıdaki işlemi hello bir abonelik tooanother abonelikten Taşı:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="8cb2f-287">Merhaba istek gövdesinde şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="8cb2f-288">Merhaba işlemi birkaç dakika çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="8cb2f-289">Portal kullanma</span><span class="sxs-lookup"><span data-stu-id="8cb2f-289">Use portal</span></span>
<span data-ttu-id="8cb2f-290">toomove kaynaklar, bu kaynakları içeren hello kaynak grubu seçin ve ardından hello seçin **taşıma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Kaynakları taşıma](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="8cb2f-292">Merhaba kaynakları tooa yeni kaynak grubu veya yeni bir abonelik taşıma olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="8cb2f-293">Merhaba kaynakları toomove ve hello hedef kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="8cb2f-294">Bu kaynaklar ve seçim için tooupdate betikleri gereksinim kabul **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="8cb2f-295">Merhaba önceki adımda hello Düzenle abonelik simgesini seçtiyseniz hello hedef aboneliği seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![hedef seçin](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="8cb2f-297">İçinde **bildirimleri**, taşıma işlemi çalıştıran bu hello bakın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-297">In **Notifications**, you see that hello move operation is running.</span></span>

![taşıma durumunu göster](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="8cb2f-299">Tamamlandığında, hello sonucunu bildirilir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-299">When it has completed, you are notified of hello result.</span></span>

![taşıma sonucu göster](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="8cb2f-301">PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="8cb2f-301">Use PowerShell</span></span>
<span data-ttu-id="8cb2f-302">toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, `Move-AzureRmResource` komutu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="8cb2f-303">ilk örnekteki Hello nasıl toomove bir kaynak tooa yeni kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="8cb2f-304">Merhaba ikinci örnekteki nasıl toomove birden çok kaynak tooa yeni kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="8cb2f-305">toomove tooa yeni abonelik, hello için bir değer dahil `DestinationSubscriptionId` parametresi.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="8cb2f-306">Bunu Sorduğunuza toomove hello istediğiniz tooconfirm belirtilen kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="8cb2f-307">Azure CLI 2.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="8cb2f-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="8cb2f-308">toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, `az resource move` komutu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="8cb2f-309">Merhaba kaynak hello kaynakları toomove kimliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="8cb2f-310">Kaynak kimlikleri komutu aşağıdaki hello ile alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="8cb2f-311">Aşağıdaki örnek hello nasıl toomove bir depolama hesabı tooa yeni kaynak grubu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="8cb2f-312">Merhaba, `--ids` parametresi hello kaynak kimlikleri toomove boşlukla ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="8cb2f-313">toomove tooa yeni abonelik, hello sağlamak `--destination-subscription-id` parametresi.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="8cb2f-314">Azure CLI 1.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="8cb2f-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="8cb2f-315">toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, `azure resource move` komutu.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="8cb2f-316">Merhaba kaynak hello kaynakları toomove kimliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="8cb2f-317">Kaynak kimlikleri komutu aşağıdaki hello ile alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="8cb2f-318">Biçim aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-318">Which returns hello following format:</span></span>

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

<span data-ttu-id="8cb2f-319">Aşağıdaki örnek hello nasıl toomove bir depolama hesabı tooa yeni kaynak grubu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="8cb2f-320">Merhaba, `-i` parametresi hello kaynak kimlikleri toomove virgülle ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="8cb2f-321">Bunu Sorduğunuza toomove hello istediğiniz tooconfirm belirtilen kaynak.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="8cb2f-322">REST API’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="8cb2f-322">Use REST API</span></span>
<span data-ttu-id="8cb2f-323">toomove mevcut kaynakları tooanother kaynak grubuna veya aboneliğe, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8cb2f-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="8cb2f-324">Merhaba istek gövdesinde hello hedef kaynak grubu ve hello kaynakları toomove belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cb2f-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="8cb2f-325">Merhaba taşıma REST işlemi hakkında daha fazla bilgi için bkz: [taşıma kaynakları](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cb2f-326">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cb2f-326">Next steps</span></span>
* <span data-ttu-id="8cb2f-327">Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında toolearn bkz [Resource Manager ile Azure PowerShell'i kullanarak](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="8cb2f-328">Aboneliğinizi yönetmek için Azure CLI komutları hakkında toolearn bkz [kullanma hello Azure CLI Resource Manager ile](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="8cb2f-329">Aboneliğinizi yönetmek için portal özellikleri hakkında toolearn bkz [hello Azure portal toomanage kaynakları kullanarak](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="8cb2f-330">bir mantıksal kuruluş tooyour kaynakları uygulama hakkında toolearn bkz [kullanarak kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="8cb2f-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
