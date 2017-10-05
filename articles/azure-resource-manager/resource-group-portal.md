---
title: "Azure kaynaklarınızı yönetmek için Azure portalını kullanma | Microsoft Docs"
description: "Azure portalı ve Azure Resource Manager kaynaklarınızı yönetmek için kullanın. Kaynakları izlemek için Panolar ile çalışmaya nasıl gösterir."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="ee48f-104">Portal üzerinden Azure kaynaklarınızı yönetmek</span><span class="sxs-lookup"><span data-stu-id="ee48f-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee48f-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee48f-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="ee48f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ee48f-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="ee48f-107">Portal</span><span class="sxs-lookup"><span data-stu-id="ee48f-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="ee48f-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ee48f-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="ee48f-109">Bu konuda nasıl kullanılacağını gösterir [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) Azure kaynaklarınızı yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="ee48f-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="ee48f-110">Kaynakları portal üzerinden dağıtma hakkında bilgi edinmek için bkz: [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="ee48f-111">Şu anda, her hizmeti Portalı'nı veya Kaynak Yöneticisi'ni destekler.</span><span class="sxs-lookup"><span data-stu-id="ee48f-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="ee48f-112">Bu hizmetler için kullanmanız gerekir. [Klasik portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ee48f-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ee48f-113">Her hizmet durumunu görmek [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="ee48f-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="ee48f-114">Kaynak gruplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="ee48f-114">Manage resource groups</span></span>

<span data-ttu-id="ee48f-115">Bir kaynak grubu Azure çözümünü ilgili kaynaklara tutan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ee48f-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="ee48f-116">Kaynak grubu bir çözümün tüm kaynaklarını veya yalnızca grup olarak yönetmek istediğiniz kaynakları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="ee48f-117">Kuruluş için önemli olan faktörleri temel alarak kaynakları kaynak gruplarına nasıl ayıracağınıza siz karar verirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="ee48f-118">Genellikle, kolayca dağıtabilir, güncelleştirme ve bir grup olarak silmek için aynı kaynak grubunda aynı yaşam döngüsü paylaşan kaynak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ee48f-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="ee48f-119">Kaynak grubu, kaynaklarla ilgili meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="ee48f-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="ee48f-120">Bu nedenle, kaynak grubu için bir konum belirttiğinizde meta verilerin nereye depolanacağını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="ee48f-121">Uyumluluk nedeniyle verilerinizin belirli bir bölgeye depolandığından emin olmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="ee48f-122">Aboneliğinizdeki tüm kaynak grupları görmek için seçin **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="ee48f-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![Kaynak grupları Gözat](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="ee48f-124">Boş bir kaynak grubu oluşturmak için seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ee48f-124">To create an empty resource group, select **Add**.</span></span>
   
    ![Kaynak Grubu Ekle](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="ee48f-126">Bir ad ve yeni kaynak grubu için konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="ee48f-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="ee48f-127">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="ee48f-127">Select **Create**.</span></span>
   
    ![kaynak grubu oluştur](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="ee48f-129">Seçmek için gerek duyabileceğiniz **yenileme** son oluşturduğunuz kaynak grubunu görmek için.</span><span class="sxs-lookup"><span data-stu-id="ee48f-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![kaynak grubu Yenile](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="ee48f-131">Kaynak grupları için görüntülenen bilgileri özelleştirmek için seçin **sütunları**.</span><span class="sxs-lookup"><span data-stu-id="ee48f-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![sütunları özelleştirme](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="ee48f-133">Sütun ekleyin ve ardından seçin **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="ee48f-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![sütunlar ekleme](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="ee48f-135">Yeni kaynak grubunuz kaynakları dağıtma hakkında bilgi edinmek için bkz: [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="ee48f-136">Bir kaynak grubu için hızlı erişim için dikey panonuza sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![PIN kaynak grubu](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="ee48f-138">Pano, kaynak grubu ve kaynaklarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ee48f-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="ee48f-139">Kaynak grupları veya herhangi birinde kaynaklarını öğesine gitmek üzere seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![PIN kaynak grubu](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="ee48f-141">Etiket kaynakları</span><span class="sxs-lookup"><span data-stu-id="ee48f-141">Tag resources</span></span>
<span data-ttu-id="ee48f-142">Varlıklarınızı mantıksal olarak düzenlemek için kaynak grupları ve kaynaklar için etiketler uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="ee48f-143">Etiketleri ile çalışma hakkında daha fazla bilgi için bkz: [etiketleri kullanarak Azure kaynaklarınızı düzenleme](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="ee48f-144">Kaynakları izleme</span><span class="sxs-lookup"><span data-stu-id="ee48f-144">Monitor resources</span></span>
<span data-ttu-id="ee48f-145">Bir kaynak seçtiğinizde, kaynak dikey penceresini varsayılan grafikleri ve izleme bu kaynak türü için tabloları gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="ee48f-146">Bir kaynak seçip bildirim **izleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ee48f-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="ee48f-147">Kaynak türü için uygun olan grafikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="ee48f-148">Aşağıdaki resimde, varsayılan depolama hesabı için veri izleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![İzleme Göster](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="ee48f-150">Bölümün yukarısında üç nokta (...) seçerek dikey bir bölümünü panonuza sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="ee48f-151">Ayrıca, dikey bölümde boyutunu özelleştirmek veya tamamen kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ee48f-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="ee48f-152">Aşağıdaki resimde, PIN, özelleştirme veya CPU ve bellek bölümü kaldırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![PIN bölümü](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="ee48f-154">Bölüm panoya sabitleme sonra Özet panosunda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="ee48f-155">Ve hemen seçerek, veriler hakkında daha fazla ayrıntı için alır.</span><span class="sxs-lookup"><span data-stu-id="ee48f-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![Görünüm Panosu](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="ee48f-157">Tamamen Portalı aracılığıyla izleme verileri özelleştirmek için varsayılan panonuz gidin ve seçin **yeni Pano**.</span><span class="sxs-lookup"><span data-stu-id="ee48f-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![pano](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="ee48f-159">Yeni panonuz bir ad verin ve Pano kutucukları sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ee48f-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="ee48f-160">Döşeme farklı seçenekler göre filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-160">The tiles are filtered by different options.</span></span>
   
    ![pano](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="ee48f-162">Panoları ile çalışma hakkında bilgi edinmek için [oluşturma ve Azure portalındaki Pano paylaşımı](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="ee48f-163">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="ee48f-163">Manage resources</span></span>
<span data-ttu-id="ee48f-164">Bir kaynak için dikey penceresinde kaynak yönetmek için seçenekler bakın.</span><span class="sxs-lookup"><span data-stu-id="ee48f-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="ee48f-165">Portal bu belirli kaynak türü için yönetim seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="ee48f-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="ee48f-166">Üstte yer alan kaynak dikey penceresinin ve sol tarafındaki yönetimi komutları bakın.</span><span class="sxs-lookup"><span data-stu-id="ee48f-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![Kaynakları yönetme](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="ee48f-168">Aşağıdaki seçeneklerden birini başlatılıyor ve bir sanal makineyi durdurmak veya sanal makinenin özelliklerini yeniden gibi işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="ee48f-169">Kaynakları taşıma</span><span class="sxs-lookup"><span data-stu-id="ee48f-169">Move resources</span></span>
<span data-ttu-id="ee48f-170">Başka bir kaynak grubu veya başka bir abonelik kaynaklarını taşımak gerekirse bkz [yeni kaynak grubu veya abonelik kaynaklarını taşıma](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="ee48f-171">Kaynakları kilitleme</span><span class="sxs-lookup"><span data-stu-id="ee48f-171">Lock resources</span></span>
<span data-ttu-id="ee48f-172">Abonelik, kaynak grubu veya kaynak yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzda bulunan diğer kullanıcıların önlemek için kilitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="ee48f-173">Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="ee48f-174">Aboneliğiniz ve maliyetleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ee48f-174">View your subscription and costs</span></span>
<span data-ttu-id="ee48f-175">Tüm kaynaklar için aboneliğinizi ve aktarılmış maliyetleri hakkında bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="ee48f-176">Seçin **abonelikleri** ve görmek istediğiniz abonelik.</span><span class="sxs-lookup"><span data-stu-id="ee48f-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="ee48f-177">Yalnızca seçmek için bir abonelik olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-177">You might only have one subscription to select.</span></span>

![aboneliği](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="ee48f-179">Abonelik dikey penceresinde içinde yazma oranını bakın.</span><span class="sxs-lookup"><span data-stu-id="ee48f-179">Within the subscription blade, you see a burn rate.</span></span>

![yazma oranı](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="ee48f-181">Ayrıca, kaynak türüne göre maliyetlerin dökümünü.</span><span class="sxs-lookup"><span data-stu-id="ee48f-181">And, a breakdown of costs by resource type.</span></span>

![kaynak maliyeti](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="ee48f-183">Şablonu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="ee48f-183">Export template</span></span>
<span data-ttu-id="ee48f-184">Kaynak grubunuzun ayarladıktan sonra kaynak grubu için Resource Manager şablonu görüntülemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="ee48f-185">Şablonu dışarı aktarma iki avantajları sunar:</span><span class="sxs-lookup"><span data-stu-id="ee48f-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="ee48f-186">Şablondaki tüm eksiksiz altyapı içerdiğinden çözümün gelecekteki dağıtımlar kolayca otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="ee48f-187">JavaScript nesne gösterimi (çözümünüzü temsil eden JSON adresindeki) bakarak şablon söz dizimi ile tanıdık.</span><span class="sxs-lookup"><span data-stu-id="ee48f-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="ee48f-188">Adım adım yönergeler için bkz: [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="ee48f-189">Kaynak grubunu veya kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="ee48f-189">Delete resource group or resources</span></span>
<span data-ttu-id="ee48f-190">Bir kaynak grubunu silme içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="ee48f-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="ee48f-191">Kaynakların kaynak grubunda silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee48f-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="ee48f-192">Olabileceğinden kaynaklara bağlı olan diğer kaynak gruplarının, bir kaynak grubu sildiğinizde dikkatli istiyor.</span><span class="sxs-lookup"><span data-stu-id="ee48f-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="ee48f-193">Resource Manager bağlı kaynaklar silinmez, ancak bunlar beklenen kaynakları doğru çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ee48f-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![Grup silme](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="ee48f-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee48f-195">Next steps</span></span>
* <span data-ttu-id="ee48f-196">Etkinlik günlükleri görüntülemek için bkz: [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="ee48f-197">Bir dağıtımı hakkındaki ayrıntıları görüntülemek için bkz: [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="ee48f-198">Kaynakları portal üzerinden dağıtmak için bkz: [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="ee48f-199">Kaynaklara erişimi yönetmek için bkz: [Azure aboneliği kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="ee48f-200">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ee48f-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

