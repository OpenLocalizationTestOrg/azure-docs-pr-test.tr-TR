---
title: "Azure portal toodeploy aaaUse Azure kaynaklarını | Microsoft Docs"
description: "Azure portalı ve Azure Resource Manager toodeploy kaynaklarınızı kullanın."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="47475-103">Kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="47475-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47475-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47475-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="47475-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="47475-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="47475-106">Portal</span><span class="sxs-lookup"><span data-stu-id="47475-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="47475-107">REST API</span><span class="sxs-lookup"><span data-stu-id="47475-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="47475-108">Bu konuda gösterilmektedir nasıl toouse hello [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) toodeploy Azure kaynaklarınızı.</span><span class="sxs-lookup"><span data-stu-id="47475-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="47475-109">toolearn kaynaklarınızı yönetme hakkında bkz [yönetmek Azure kaynakları portal üzerinden](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47475-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="47475-110">Şu anda, her hizmeti hello portalı veya Kaynak Yöneticisi'ni destekler.</span><span class="sxs-lookup"><span data-stu-id="47475-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="47475-111">Bu hizmetler için toouse hello gereksinim [Klasik portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="47475-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="47475-112">Her hizmet Hello durumu için bkz: [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="47475-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="47475-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="47475-113">Create resource group</span></span>
1. <span data-ttu-id="47475-114">toocreate boş bir kaynak grubu seçin **yeni** > **Yönetim** > **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="47475-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![boş bir kaynak grubu oluştur](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="47475-116">Bir ad ve konum girin ve gerekiyorsa, bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="47475-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="47475-117">Hello kaynak grubu hello kaynaklarla ilgili meta verileri depoladığından hello kaynak grubu için bir konum tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="47475-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="47475-118">Uyumluluk nedenleriyle meta verilerin depolandığı toospecify isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="47475-119">Genel olarak, çoğu kaynaklarınızın bulunacağı bir konum belirtin öneririz.</span><span class="sxs-lookup"><span data-stu-id="47475-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="47475-120">Kullanarak, hello aynı konumu şablonunuzu basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="47475-120">Using hello same location can simplify your template.</span></span>
   
    ![kümesi Grup değerleri](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="47475-122">Market kaynaklardan dağıtma</span><span class="sxs-lookup"><span data-stu-id="47475-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="47475-123">Bir kaynak grubu oluşturduktan sonra kaynakları tooit hello Market gelen dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="47475-124">Merhaba Market yaygın senaryoları için önceden tanımlanmış çözümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="47475-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="47475-125">toostart bir dağıtım seçin **yeni** ve hello türü kaynak toodeploy istersiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="47475-126">Sonra Ara hello belirli sürümü hello kaynak için toodeploy istersiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![Kaynak dağıtma](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="47475-128">Hello belirli çözüm toodeploy ister misiniz yoksa hello Market için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![Arama Market](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="47475-130">Seçilen kaynak Hello türüne bağlı olarak, ilgili özellikleri tooset dağıtmadan önce oluşan bir koleksiyona sahip.</span><span class="sxs-lookup"><span data-stu-id="47475-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="47475-131">Kaynak türü göre farklılık bu seçenekler Burada, bunlar gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="47475-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="47475-132">Tüm türleri için bir hedef kaynak grubu seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="47475-133">Merhaba aşağıdaki görüntü gösterir nasıl toocreate bir web uygulaması ve oluşturduğunuz toohello kaynak grubu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="47475-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="47475-135">Alternatif olarak, bir kaynak grubu toocreate kaynaklarınızı dağıtırken karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="47475-136">Seçin **Yeni Oluştur** ve hello kaynak grubuna bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="47475-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![Yeni kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="47475-138">Dağıtımınızı başlar.</span><span class="sxs-lookup"><span data-stu-id="47475-138">Your deployment begins.</span></span> <span data-ttu-id="47475-139">Merhaba dağıtımın birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="47475-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="47475-140">Merhaba dağıtım tamamlandığında, bir bildirim görür.</span><span class="sxs-lookup"><span data-stu-id="47475-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![Görünüm bildirim](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="47475-142">Kaynaklarınızı dağıttıktan sonra daha fazla kaynakları toohello kaynak grubu hello kullanarak ekleyebileceğiniz **Ekle** hello kaynak grubu dikey komutu.</span><span class="sxs-lookup"><span data-stu-id="47475-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![kaynak ekle](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="47475-144">Özel şablon kaynaklardan dağıtma</span><span class="sxs-lookup"><span data-stu-id="47475-144">Deploy resources from custom template</span></span>
<span data-ttu-id="47475-145">Bir dağıtım tooexecute istiyor, ancak hello şablonlardan hello Market kullanmamanız hello çözümünüz için altyapıyı tanımlayan özelleştirilmiş bir şablon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="47475-146">şablonları oluşturma hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="47475-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="47475-147">toodeploy hello Portalı aracılığıyla özelleştirilmiş bir şablon seçin **yeni**ve Arama Başlat **şablon dağıtımı** kadar hello seçenekler arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![Arama şablon dağıtımı](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="47475-149">Seçin **şablon dağıtımı** hello kullanılabilir kaynaklardan.</span><span class="sxs-lookup"><span data-stu-id="47475-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![Şablon dağıtımı seçin](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="47475-151">Merhaba şablon dağıtımı başlatılıyor sonra özelleştirmek için kullanılabilir olan hello boş şablonu açın.</span><span class="sxs-lookup"><span data-stu-id="47475-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![Şablonu oluşturma](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="47475-153">Merhaba Düzenleyicisi'nde toodeploy hello kaynakları tanımlayan hello JSON söz dizimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="47475-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="47475-154">Seçin **kaydetmek** bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="47475-154">Select **Save** when done.</span></span> <span data-ttu-id="47475-155">Merhaba JSON söz dizimi yazma ile ilgili yönergeler için bkz: [Resource Manager şablonu Kılavuzu](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="47475-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![şablonu düzenleme](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="47475-157">Veya hello önceden var olan bir şablonu seçebilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="47475-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="47475-158">Bu şablonlar hello topluluk tarafından katkısı.</span><span class="sxs-lookup"><span data-stu-id="47475-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="47475-159">Birçok ortak senaryolarını kapsamak ve birisi toodeploy çalıştığınız benzer toowhat olan bir şablon eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="47475-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="47475-160">Merhaba şablonları toofind senaryonuzla eşleşen bir şey arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![Hızlı Başlatma şablonunu seçin](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="47475-162">Merhaba Düzenleyicisi'nde hello Seçili şablon görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47475-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="47475-163">Tüm hello diğer değerleri girdikten sonra Seç **oluşturma** toodeploy hello şablonu.</span><span class="sxs-lookup"><span data-stu-id="47475-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![şablonu dağıtma](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="47475-165">Tooyour hesabı kaydedilmiş bir şablon kaynaklardan dağıtma</span><span class="sxs-lookup"><span data-stu-id="47475-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="47475-166">Merhaba portal şablonu tooyour Azure hesabı toosave sağlar ve daha sonra yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="47475-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="47475-167">Bu şablonlar, kaydedilen çalışma hakkında daha fazla bilgi için [hello Azure portalı özel şablonları kullanmaya başlama](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="47475-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="47475-168">kaydedilen şablonlarınızı toofind seçin **Gözat** > **şablonları**.</span><span class="sxs-lookup"><span data-stu-id="47475-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![Şablonları Gözat](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="47475-170">Tooyour hesabı kaydedilmiş şablon Hello listeden bir istediğiniz toowork üzerinde hello seçin.</span><span class="sxs-lookup"><span data-stu-id="47475-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![kaydedilen şablonları](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="47475-172">Seçin **dağıtma** tooredeploy bu kaydedilmiş şablonu.</span><span class="sxs-lookup"><span data-stu-id="47475-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![Kaydedilmiş şablonu dağıtma](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="47475-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47475-174">Next steps</span></span>
* <span data-ttu-id="47475-175">tooview denetim günlüklerine bakın [denetim işlemleri Resource Manager ile](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="47475-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="47475-176">tootroubleshoot dağıtım hataları, bkz: [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="47475-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="47475-177">tooretrieve dağıtım veya kaynak grubu, bir şablondan bkz [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="47475-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="47475-178">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="47475-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

