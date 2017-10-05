---
title: "Bir Azure tüketen yönetilen uygulama | Microsoft Docs"
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
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="c7461-103">Bir iç yönetilen uygulama kullanma</span><span class="sxs-lookup"><span data-stu-id="c7461-103">Consume an internal managed application</span></span>

<span data-ttu-id="c7461-104">Azure tüketebileceği [yönetilen uygulamaları](managed-application-overview.md) kuruluşunuzun üyeleri için yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="c7461-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="c7461-105">Örneğin, kuruluş standartlarıyla uyumluluğu sağlamak BT departmanınızın yönetilen uygulamaları seçin.</span><span class="sxs-lookup"><span data-stu-id="c7461-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="c7461-106">Bu yönetilen uygulamaların Azure Marketi hizmet Kataloğu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7461-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="c7461-107">Bu makale ile devam etmeden önce aboneliğiniz için bir yönetilen uygulamayı hizmet Kataloğu'nda kullanılabilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c7461-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="c7461-108">Birisi, kuruluşunuzdaki yönetilen bir uygulamaya oluşturulmamış olup [dahili tüketim için yönetilen bir uygulama yayımlama](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c7461-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="c7461-109">Şu anda bir yönetilen uygulamayı kullanmak için Azure CLI veya Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7461-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="c7461-110">Portalı kullanarak yönetilen uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7461-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="c7461-111">Portal üzerinden yönetilen bir uygulamayı dağıtmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7461-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="c7461-112">Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="c7461-112">Go to the Azure portal.</span></span> <span data-ttu-id="c7461-113">Arama **hizmet Kataloğu yönetilen uygulama**.</span><span class="sxs-lookup"><span data-stu-id="c7461-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Hizmet Kataloğu yönetilen uygulama](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="c7461-115">Kullanılabilir çözümleri listesinden oluşturmak istediğiniz yönetilen uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="c7461-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="c7461-116">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="c7461-116">Select **Create**.</span></span>

   ![Yönetilen uygulama seçimi](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="c7461-118">Kaynakları sağlamak üzere gerekli parametreler için değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c7461-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="c7461-119">Seçin **Batı Orta ABD** konumu.</span><span class="sxs-lookup"><span data-stu-id="c7461-119">Select **West Central US** for location.</span></span> <span data-ttu-id="c7461-120">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c7461-120">Select **OK**.</span></span>

   ![Yönetilen uygulama parametreleri](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="c7461-122">Şablon, sağlanan değerler doğrular.</span><span class="sxs-lookup"><span data-stu-id="c7461-122">The template validates the values you provided.</span></span> <span data-ttu-id="c7461-123">Doğrulama başarılı olursa seçin **Tamam** dağıtımı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="c7461-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Yönetilen uygulama doğrulama](./media/managed-application-consumption/validation.png)

<span data-ttu-id="c7461-125">Dağıtım tamamlandıktan sonra şablonda tanımlanan uygun kaynaklara sağladığınız yönetilen kaynak grubunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c7461-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="c7461-126">Azure CLI kullanarak yönetilen uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7461-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="c7461-127">Azure CLI kullanarak bir yönetilen uygulamayı oluşturmanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="c7461-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="c7461-128">Komut, yönetilen uygulamaları oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7461-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="c7461-129">Normal şablon dağıtımı komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7461-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="c7461-130">Şablon dağıtımı komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="c7461-130">Use the template deployment command</span></span>

<span data-ttu-id="c7461-131">Satıcı oluşturulan applianceMainTemplate.json dosyasını dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c7461-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="c7461-132">Daha sonra iki kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7461-132">Then create two resource groups.</span></span> <span data-ttu-id="c7461-133">Yönetilen uygulama kaynağı oluşturulduğu ilk kaynak grubu olduğundan: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="c7461-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="c7461-134">İkinci kaynak grubu mainTemplate.json içinde tanımlanan tüm kaynaklar içeriyor.</span><span class="sxs-lookup"><span data-stu-id="c7461-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="c7461-135">Bu kaynak grubu ISV tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="c7461-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="c7461-136">Kullanım `westcentralus` kaynak grubu konumu olarak.</span><span class="sxs-lookup"><span data-stu-id="c7461-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="c7461-137">MainResourceGroup applianceMainTemplate.json dağıtmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="c7461-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="c7461-138">Yukarıdaki şablonu çalıştıktan sonra şablonda tanımlanan parametre değerlerini ister.</span><span class="sxs-lookup"><span data-stu-id="c7461-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="c7461-139">Bir şablona kaynakları sağlamak üzere gerekli parametreleri ek olarak, iki anahtar parametre değerlerini gerekir:</span><span class="sxs-lookup"><span data-stu-id="c7461-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="c7461-140">**managedResourceGroupId**: applianceMainTemplate.json içinde tanımlanan kaynakları içeren kaynak grubunun kimliği.</span><span class="sxs-lookup"><span data-stu-id="c7461-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="c7461-141">Kimliği biçimidir `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="c7461-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="c7461-142">İsteğe bağlı olarak önceki örnekte kimliği olan `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="c7461-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="c7461-143">**applianceDefinitionId**: yönetilen uygulama tanımı kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="c7461-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="c7461-144">Bu değer, ISV tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c7461-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="c7461-145">Yayımcı, yönetilen uygulama tanımını içeren kaynak grubuna erişim vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7461-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="c7461-146">Tanımı kaynak yayımcı abonelikte oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7461-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="c7461-147">Bu nedenle, bir kullanıcı, kullanıcı grubu veya müşteri Kiracı uygulamada bu kaynak için okuma erişimi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7461-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="c7461-148">Dağıtım başarıyla tamamlandıktan sonra yönetilen uygulama mainResourceGroup içinde oluşturulur bakın.</span><span class="sxs-lookup"><span data-stu-id="c7461-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="c7461-149">StorageAccount kaynak managedResourceGroup içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7461-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="c7461-150">Oluştur komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="c7461-150">Use the create command</span></span>

<span data-ttu-id="c7461-151">Kullanabileceğiniz `az managedapp create` yönetilen uygulamayı tanımından yönetilen bir uygulama oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="c7461-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="c7461-152">**Gereci tanımı kimliği**: yönetilen uygulama tanımının önceki adımda oluşturduğunuz kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="c7461-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="c7461-153">Bu kimliği edinmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c7461-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="c7461-154">Bu komut, yönetilen uygulama tanımının döndürür.</span><span class="sxs-lookup"><span data-stu-id="c7461-154">This command returns the managed application definition.</span></span> <span data-ttu-id="c7461-155">ID özelliği değeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7461-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="c7461-156">**Yönetilen-rg-ID**: applianceMainTemplate.json içinde tanımlanan kaynakları içeren kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="c7461-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="c7461-157">Bu kaynak grubu yönetilen kaynak grubudur.</span><span class="sxs-lookup"><span data-stu-id="c7461-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="c7461-158">Yayımcı tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="c7461-158">It's managed by the publisher.</span></span> <span data-ttu-id="c7461-159">Yoksa, sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7461-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="c7461-160">**kaynak grubu**: yönetilen uygulama kaynağı oluşturulduğu kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="c7461-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="c7461-161">Bu kaynak grubunda Microsoft.Solutions/appliance kaynak yaşar.</span><span class="sxs-lookup"><span data-stu-id="c7461-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="c7461-162">**parametreleri**: applianceMainTemplate.json içinde tanımlanan kaynaklar için gerekli olan parametreleri.</span><span class="sxs-lookup"><span data-stu-id="c7461-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c7461-163">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="c7461-163">Known issues</span></span>

<span data-ttu-id="c7461-164">Bu önizleme sürümü, aşağıdaki konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="c7461-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="c7461-165">Yönetilen uygulama oluşturma sırasında 500 İç sunucu hatası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c7461-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="c7461-166">Bu sorunu yaşayıp çalıştırırsanız, aralıklı olması olasıdır.</span><span class="sxs-lookup"><span data-stu-id="c7461-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="c7461-167">İşlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c7461-167">Retry the operation.</span></span>
* <span data-ttu-id="c7461-168">Yeni bir kaynak grubu yönetilen kaynak grubu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c7461-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="c7461-169">Varolan bir kaynak grubu kullanıyorsanız, dağıtım başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c7461-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="c7461-170">Microsoft.Solutions/appliances kaynak içeren kaynak grubunu oluşturulmalıdır **westcentralus** konumu.</span><span class="sxs-lookup"><span data-stu-id="c7461-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7461-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7461-171">Next steps</span></span>

* <span data-ttu-id="c7461-172">Yönetilen uygulamaların giriş için bkz: [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7461-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c7461-173">Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c7461-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="c7461-174">Azure Marketi'nde yayımlama yönetilen uygulamalar hakkında daha fazla bilgi için bkz: [Azure Market uygulamalarda yönetilen](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="c7461-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="c7461-175">Marketten bir yönetilen uygulamayı kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="c7461-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
