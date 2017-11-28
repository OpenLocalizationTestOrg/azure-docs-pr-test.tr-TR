---
title: "bir Azure aaaConsume yönetilen uygulama | Microsoft Docs"
description: "Bir müşteri Azure nasıl oluşturduğunu açıklar yayımlanan dosyalarından yönetilen uygulama."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="21627-103">Bir iç yönetilen uygulama kullanma</span><span class="sxs-lookup"><span data-stu-id="21627-103">Consume an internal managed application</span></span>

<span data-ttu-id="21627-104">Azure tüketebileceği [yönetilen uygulamaları](managed-application-overview.md) kuruluşunuzun üyeleri için yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="21627-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="21627-105">Örneğin, kuruluş standartlarıyla uyumluluğu sağlamak BT departmanınızın yönetilen uygulamaları seçin.</span><span class="sxs-lookup"><span data-stu-id="21627-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="21627-106">Bu yönetilen uygulamaların hello hizmet Kataloğu, hello Azure Market kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21627-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="21627-107">Bu makale ile devam etmeden önce aboneliğiniz için bir yönetilen uygulamayı hello hizmet Kataloğu'nda kullanılabilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="21627-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="21627-108">Birisi, kuruluşunuzdaki yönetilen bir uygulamaya oluşturulmamış olup [dahili tüketim için yönetilen bir uygulama yayımlama](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="21627-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="21627-109">Şu anda, Azure CLI veya hello Azure portal tooconsume yönetilen bir uygulama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21627-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="21627-110">Merhaba portalını kullanarak yönetilen Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="21627-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="21627-111">toodeploy hello portal aracılığıyla bir yönetilen uygulamayı aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="21627-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="21627-112">Toohello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="21627-112">Go toohello Azure portal.</span></span> <span data-ttu-id="21627-113">Arama **hizmet Kataloğu yönetilen uygulama**.</span><span class="sxs-lookup"><span data-stu-id="21627-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Hizmet Kataloğu yönetilen uygulama](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="21627-115">Select hello toocreate kullanılabilir çözümler hello listesinden istediğiniz uygulama yönetiliyor.</span><span class="sxs-lookup"><span data-stu-id="21627-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="21627-116">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="21627-116">Select **Create**.</span></span>

   ![Yönetilen uygulama seçimi](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="21627-118">Gerekli tooprovision hello kaynakları hello parametreleri için değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="21627-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="21627-119">Seçin **Batı Orta ABD** konumu.</span><span class="sxs-lookup"><span data-stu-id="21627-119">Select **West Central US** for location.</span></span> <span data-ttu-id="21627-120">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21627-120">Select **OK**.</span></span>

   ![Yönetilen uygulama parametreleri](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="21627-122">Merhaba şablon sağladığınız hello değerleri doğrular.</span><span class="sxs-lookup"><span data-stu-id="21627-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="21627-123">Doğrulama başarılı olursa seçin **Tamam** toostart hello dağıtım.</span><span class="sxs-lookup"><span data-stu-id="21627-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Yönetilen uygulama doğrulama](./media/managed-application-consumption/validation.png)

<span data-ttu-id="21627-125">Merhaba dağıtım tamamlandıktan sonra hello uygun kaynaklara hello şablonda tanımlanan sağladığınız hello yönetilen kaynak grubunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21627-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="21627-126">Azure CLI kullanarak yönetilen Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="21627-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="21627-127">Vardır iki yolu toocreate yönetilen bir uygulamaya Azure CLI kullanarak:</span><span class="sxs-lookup"><span data-stu-id="21627-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="21627-128">Yönetilen uygulamalar oluşturmak için Hello komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21627-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="21627-129">Merhaba Normal şablon dağıtımı komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21627-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="21627-130">Merhaba şablon dağıtımı komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="21627-130">Use hello template deployment command</span></span>

<span data-ttu-id="21627-131">Oluşturulan satıcı hello hello applianceMainTemplate.json dosyasını dağıtın.</span><span class="sxs-lookup"><span data-stu-id="21627-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="21627-132">Daha sonra iki kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21627-132">Then create two resource groups.</span></span> <span data-ttu-id="21627-133">Merhaba ilk kaynak grubu burada hello yönetilen uygulama kaynağı oluşturulur: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="21627-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="21627-134">Merhaba ikinci kaynak grubu mainTemplate.json içinde tanımlanan tüm hello kaynaklar içeriyor.</span><span class="sxs-lookup"><span data-stu-id="21627-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="21627-135">Bu kaynak grubu hello ISV tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="21627-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="21627-136">Kullanım `westcentralus` hello kaynak grubunun hello konumu olarak.</span><span class="sxs-lookup"><span data-stu-id="21627-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="21627-137">toodeploy applianceMainTemplate.json mainResourceGroup, komutu aşağıdaki kullanım hello içinde:</span><span class="sxs-lookup"><span data-stu-id="21627-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="21627-138">Şablon çalıştırır önceki hello sonra onu hello hello şablonunda tanımlanan hello parametrelerinin değerlerini ister.</span><span class="sxs-lookup"><span data-stu-id="21627-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="21627-139">Ayrıca bir şablon tooprovision kaynaklarında toohello Parametreler gerekli, iki anahtar parametre değerlerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="21627-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="21627-140">**managedResourceGroupId**: applianceMainTemplate.json içinde tanımlanan hello kaynak grubu içeren hello kaynaklara Kimliğini hello.</span><span class="sxs-lookup"><span data-stu-id="21627-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="21627-141">Merhaba kimliğidir hello biçiminde `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="21627-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="21627-142">Örnek önceki hello hello Kimliğini kullanıcının `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="21627-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="21627-143">**applianceDefinitionId**: hello hello Kimliğini yönetilen uygulama tanımı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="21627-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="21627-144">Bu değer hello ISV tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21627-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="21627-145">Merhaba yayımcı hello yönetilen uygulama tanımını içeren toohello kaynak grubu erişim vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21627-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="21627-146">Merhaba tanımı kaynak hello yayımcı abonelikte oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21627-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="21627-147">Bu nedenle, bir kullanıcı, kullanıcı grubu veya hello müşteri Kiracı uygulamada okuma erişimi toothis kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="21627-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="21627-148">Merhaba dağıtım başarıyla tamamlandıktan sonra yönetilen hello bkz uygulama mainResourceGroup içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21627-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="21627-149">Merhaba storageAccount kaynak managedResourceGroup içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21627-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="21627-150">Kullanım hello Oluştur komutu</span><span class="sxs-lookup"><span data-stu-id="21627-150">Use hello create command</span></span>

<span data-ttu-id="21627-151">Merhaba kullanabilirsiniz `az managedapp create` komutu toocreate hello yönetilen bir uygulamadan yönetilen uygulama tanımı.</span><span class="sxs-lookup"><span data-stu-id="21627-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="21627-152">**Gereci tanımı kimliği**: hello hello kaynak kimliği yönetilen adım önceki hello oluşturulan uygulama tanımı.</span><span class="sxs-lookup"><span data-stu-id="21627-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="21627-153">tooobtain hello aşağıdaki komutu çalıştırın, bu kimliği:</span><span class="sxs-lookup"><span data-stu-id="21627-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="21627-154">Bu komut, yönetilen hello uygulama tanımı döndürür.</span><span class="sxs-lookup"><span data-stu-id="21627-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="21627-155">Merhaba kimliği özelliğinin hello değeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="21627-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="21627-156">**Yönetilen-rg-ID**: applianceMainTemplate.json içinde tanımlanan hello kaynak grubu içeren hello kaynaklara hello adı.</span><span class="sxs-lookup"><span data-stu-id="21627-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="21627-157">Bu kaynak grubu hello yönetilen kaynak grubudur.</span><span class="sxs-lookup"><span data-stu-id="21627-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="21627-158">Merhaba yayımcı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="21627-158">It's managed by hello publisher.</span></span> <span data-ttu-id="21627-159">Yoksa, sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21627-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="21627-160">**kaynak grubu**: hello Uygulama kaynağı yönetildiği hello kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21627-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="21627-161">Bu kaynak grubunda Hello Microsoft.Solutions/appliance kaynak yaşar.</span><span class="sxs-lookup"><span data-stu-id="21627-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="21627-162">**parametreleri**: Merhaba applianceMainTemplate.json içinde tanımlanan hello kaynaklar için gerekli olan parametreleri.</span><span class="sxs-lookup"><span data-stu-id="21627-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="21627-163">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="21627-163">Known issues</span></span>

<span data-ttu-id="21627-164">Bu önizleme sürümü sorunları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="21627-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="21627-165">Yönetilen Merhaba uygulaması hello oluşturma sırasında 500 İç sunucu hatası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="21627-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="21627-166">Bu sorunu yaşayıp çalıştırmak, büyük olasılıkla toobe aralıklı olur.</span><span class="sxs-lookup"><span data-stu-id="21627-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="21627-167">Merhaba işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="21627-167">Retry hello operation.</span></span>
* <span data-ttu-id="21627-168">Yeni bir kaynak grubu hello yönetilen kaynak grubu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21627-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="21627-169">Varolan bir kaynak grubu kullanıyorsanız, hello dağıtımı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="21627-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="21627-170">Merhaba hello Microsoft.Solutions/appliances kaynak içeren kaynak grubunu hello oluşturulmalıdır **westcentralus** konumu.</span><span class="sxs-lookup"><span data-stu-id="21627-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21627-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21627-171">Next steps</span></span>

* <span data-ttu-id="21627-172">Bir giriş toomanaged uygulamalar için bkz [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="21627-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="21627-173">Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="21627-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="21627-174">Yönetilen uygulamaların toohello Azure Marketi'nde yayımlama hakkında daha fazla bilgi için bkz: [Azure hello Market uygulamalarda yönetilen](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="21627-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="21627-175">Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="21627-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
