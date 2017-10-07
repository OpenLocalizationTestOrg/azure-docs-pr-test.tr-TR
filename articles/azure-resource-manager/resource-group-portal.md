---
title: "Azure portal toomanage aaaUse Azure kaynaklarını | Microsoft Docs"
description: "Azure portalı ve Azure Resource Manager toomanage kaynaklarınızı kullanın. Gösterir nasıl toowork panolar toomonitor kaynaklara sahip."
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
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="cb6b0-104">Portal üzerinden Azure kaynaklarınızı yönetmek</span><span class="sxs-lookup"><span data-stu-id="cb6b0-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb6b0-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb6b0-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="cb6b0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cb6b0-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="cb6b0-107">Portal</span><span class="sxs-lookup"><span data-stu-id="cb6b0-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="cb6b0-108">REST API</span><span class="sxs-lookup"><span data-stu-id="cb6b0-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="cb6b0-109">Bu konuda gösterilmektedir nasıl toouse hello [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) toomanage Azure kaynaklarınızı.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="cb6b0-110">Merhaba portalı üzerinden kaynaklarına dağıtma hakkında toolearn bkz [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="cb6b0-111">Şu anda, her hizmeti hello portalı veya Kaynak Yöneticisi'ni destekler.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="cb6b0-112">Bu hizmetler için toouse hello gereksinim [Klasik portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="cb6b0-113">Her hizmet Hello durumu için bkz: [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="cb6b0-114">Kaynak gruplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="cb6b0-114">Manage resource groups</span></span>

<span data-ttu-id="cb6b0-115">Bir kaynak grubu Azure çözümünü ilgili kaynaklara tutan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="cb6b0-116">Merhaba kaynak grubu hello çözüm için tüm hello kaynakları veya yalnızca bir grup olarak toomanage istediğiniz kaynakları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="cb6b0-117">Tooallocate kaynakları istediğiniz karar tooresource gruplara göre ne hello en kuruluşunuz için anlamlı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="cb6b0-118">Genellikle, hello paylaşmak kaynakları eklemek, kolayca dağıtın, güncelleştirme ve bir grup olarak silmek için aynı kaynak grubunda aynı yaşam döngüsü toohello.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="cb6b0-119">Merhaba kaynak grubu hello kaynaklarla ilgili meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="cb6b0-120">Bu nedenle, hello kaynak grubu için bir konumu belirttiğinizde, meta verilerin depolandığı belirtiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="cb6b0-121">Uyumluluk nedenleriyle tooensure gerekebilir, verileriniz belirli bir bölgedeki depolanır.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="cb6b0-122">toosee, aboneliğinizdeki tüm hello kaynak grupları Seç **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![Kaynak grupları Gözat](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="cb6b0-124">toocreate boş bir kaynak grubu seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![Kaynak Grubu Ekle](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="cb6b0-126">Bir ad ve konum hello yeni kaynak grubu için sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="cb6b0-127">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-127">Select **Create**.</span></span>
   
    ![kaynak grubu oluştur](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="cb6b0-129">Tooselect gerekebilir **yenileme** toosee kısa süre önce oluşturuldu hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![kaynak grubu Yenile](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="cb6b0-131">Kaynak grupları için görüntülenen toocustomize hello bilgiler seçin **sütunları**.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![sütunları özelleştirme](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="cb6b0-133">Merhaba sütunları tooadd seçin ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![sütunlar ekleme](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="cb6b0-135">kaynakları tooyour yeni kaynak grubu dağıtma hakkında toolearn bkz [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="cb6b0-136">Hızlı erişim tooa kaynak grubu için hello dikey tooyour Pano sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![PIN kaynak grubu](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="cb6b0-138">Merhaba Pano hello kaynak grubu ve kaynaklarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="cb6b0-139">Merhaba kaynak grupları veya kendi kaynaklarını toonavigate toohello öğesi birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![PIN kaynak grubu](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="cb6b0-141">Etiket kaynakları</span><span class="sxs-lookup"><span data-stu-id="cb6b0-141">Tag resources</span></span>
<span data-ttu-id="cb6b0-142">Etiketler tooresource grupları uygulayabilirsiniz ve kaynakları toologically varlıklarınızı düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="cb6b0-143">Etiketleri ile çalışma hakkında daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="cb6b0-144">Kaynakları izleme</span><span class="sxs-lookup"><span data-stu-id="cb6b0-144">Monitor resources</span></span>
<span data-ttu-id="cb6b0-145">Bir kaynak seçtiğinizde hello kaynak dikey varsayılan grafikleri ve izleme bu kaynak türü için tabloları gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="cb6b0-146">Kaynak ve bildirimi hello seçin **izleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="cb6b0-147">İlgili toohello kaynak türü olan grafikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="cb6b0-148">Merhaba aşağıdaki görüntüde hello varsayılan depolama hesabı için veri izleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![İzleme Göster](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="cb6b0-150">Merhaba bölümün yukarısında hello üç nokta (...) seçerek hello dikey tooyour Pano bölümü sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="cb6b0-151">Ayrıca, hello boyutu hello hello dikey bölümde özelleştirebilir veya tamamen kaldırın.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="cb6b0-152">Merhaba aşağıdaki görüntüde nasıl toopin, özelleştirme, veya hello CPU ve bellek bölümü kaldırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![PIN bölümü](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="cb6b0-154">Hello bölüm toohello panoya sabitleme sonra hello Panoda hello Özet görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="cb6b0-155">Ve hemen seçerek hello veri toomore ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![Görünüm Panosu](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="cb6b0-157">toocompletely özelleştirme izleme hello portal aracılığıyla, tooyour varsayılan pano gidin ve seçin hello veri **yeni Pano**.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![pano](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="cb6b0-159">Yeni panonuz bir ad verin ve hello Pano kutucukları sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="cb6b0-160">Merhaba döşeme farklı seçenekler göre filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-160">hello tiles are filtered by different options.</span></span>
   
    ![pano](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="cb6b0-162">panoları ile çalışma hakkında toolearn bkz [oluşturma ve hello Azure portal panolarında paylaşımı](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="cb6b0-163">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="cb6b0-163">Manage resources</span></span>
<span data-ttu-id="cb6b0-164">Bir kaynak için Hello dikey penceresinde hello kaynak yönetmek için hello seçenekler bakın.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="cb6b0-165">Merhaba portalı bu belirli kaynak türü için yönetim seçenekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="cb6b0-166">Merhaba üstte hello kaynak dikey penceresinin ve hello sol tarafında hello yönetimi komutları bakın.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Kaynakları yönetme](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="cb6b0-168">Aşağıdaki seçeneklerden birini başlatılıyor ve bir sanal makineyi durdurmak veya hello hello sanal makinenin özelliklerini yeniden gibi işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="cb6b0-169">Kaynakları taşıma</span><span class="sxs-lookup"><span data-stu-id="cb6b0-169">Move resources</span></span>
<span data-ttu-id="cb6b0-170">Toomove kaynakları tooanother kaynak grubu veya başka bir abonelik gerekirse bkz [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="cb6b0-171">Kaynakları kilitleme</span><span class="sxs-lookup"><span data-stu-id="cb6b0-171">Lock resources</span></span>
<span data-ttu-id="cb6b0-172">Yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzdaki diğer kullanıcılara abonelik, kaynak grubu veya kaynak tooprevent kilitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="cb6b0-173">Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="cb6b0-174">Aboneliğiniz ve maliyetleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="cb6b0-174">View your subscription and costs</span></span>
<span data-ttu-id="cb6b0-175">Tüm kaynaklar için abonelik ve hello aktarılmış maliyetleri hakkındaki bilgileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="cb6b0-176">Seçin **abonelikleri** ve toosee istediğiniz hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="cb6b0-177">Yalnızca bir abonelik tooselect olabilir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-177">You might only have one subscription tooselect.</span></span>

![aboneliği](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="cb6b0-179">Merhaba abonelik dikey penceresinde içinde yazma oranını bakın.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-179">Within hello subscription blade, you see a burn rate.</span></span>

![yazma oranı](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="cb6b0-181">Ayrıca, kaynak türüne göre maliyetlerin dökümünü.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-181">And, a breakdown of costs by resource type.</span></span>

![kaynak maliyeti](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="cb6b0-183">Şablonu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="cb6b0-183">Export template</span></span>
<span data-ttu-id="cb6b0-184">Kaynak grubunuzun ayarladıktan sonra hello kaynak grubu için tooview hello Resource Manager şablonu isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="cb6b0-185">Dışarı aktarma hello şablon iki avantajları sunar:</span><span class="sxs-lookup"><span data-stu-id="cb6b0-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="cb6b0-186">Merhaba şablonu tüm hello eksiksiz altyapı içerdiğinden hello çözümün gelecekteki dağıtımlar kolayca otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="cb6b0-187">Çözümünüzü temsil eden JavaScript nesne gösterimi (JSON) hello bakarak şablon söz dizimi ile tanıdık.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="cb6b0-188">Adım adım yönergeler için bkz: [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="cb6b0-189">Kaynak grubunu veya kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="cb6b0-189">Delete resource group or resources</span></span>
<span data-ttu-id="cb6b0-190">Bir kaynak grubunu silme içerdiği tüm hello kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="cb6b0-191">Kaynakların kaynak grubunda silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="cb6b0-192">Bağlantılı tooit olan diğer kaynak gruplarının kaynakları olabilir çünkü bir kaynak grubu sildiğinizde tooexercise dikkat istiyor.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="cb6b0-193">Resource Manager bağlı kaynaklar silinmez, ancak bunlar beklenen hello kaynakları doğru çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="cb6b0-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![Grup silme](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="cb6b0-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb6b0-195">Next steps</span></span>
* <span data-ttu-id="cb6b0-196">tooview etkinlik günlüklerine bakın [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="cb6b0-197">bir dağıtım tooview ayrıntılarını görmek [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="cb6b0-198">Merhaba portalı üzerinden toodeploy kaynaklarına bakın [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="cb6b0-199">toomanage erişim tooresources bkz [rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="cb6b0-200">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="cb6b0-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

