---
title: "Kaynak ilkeleri için Azure portalı | Microsoft Docs"
description: "Azure portal oluşturmak ve Resource Manager ilkelerini yönetmek için nasıl kullanılacağını açıklar. Abonelik veya kaynak gruplarının ilkeleri uygulanabilir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="dae8e-104">Atama ve kaynak ilkelerini yönetmek için Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="dae8e-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="dae8e-105">Azure portalı kaynak grupları ve abonelikler için kaynak ilkeleri atamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="dae8e-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="dae8e-106">Kullanıcı arabirimi atayın ve ilke ayarlarını özelleştirmek bu ilkeye parametre değerlerini belirtin istediğiniz ilkeyi seçin kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="dae8e-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="dae8e-107">Portal üzerinden ilke atamak için ilke tanımı önceden aboneliğinizde var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dae8e-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="dae8e-108">Aboneliğiniz hazır, kaynak grupları veya abonelikleri atamak birkaç yerleşik ilke tanımları sahip.</span><span class="sxs-lookup"><span data-stu-id="dae8e-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="dae8e-109">Bu yerleşik ilkeleri ve ilkeleri atamak için portal kullanırken, tanımladığınız tüm özel ilkeler bakın.</span><span class="sxs-lookup"><span data-stu-id="dae8e-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="dae8e-110">İlkeleri ve özelleştirilmiş ilkesinin nasıl tanımlanacağını bir giriş için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="dae8e-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="dae8e-111">İlkeler tüm alt kaynaklar tarafından devralınır.</span><span class="sxs-lookup"><span data-stu-id="dae8e-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="dae8e-112">Bu nedenle, bir kaynak grubu için bir ilke uygulandığında, bu kaynak grubundaki tüm kaynaklar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="dae8e-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="dae8e-113">Bu makalede, terimi **kapsam** kaynak grubu veya ilke atanan abonelik başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="dae8e-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="dae8e-114">İlkeleri oluşturma ve (PUT ve işlemleri düzeltme eki) kaynakları güncelleştirme değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="dae8e-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="dae8e-115">Bir ilke atama</span><span class="sxs-lookup"><span data-stu-id="dae8e-115">Assign a policy</span></span>

1. <span data-ttu-id="dae8e-116">Kaynak grubu veya abonelik için bir ilke atamak için bu kaynak grubuna veya aboneliğe seçin.</span><span class="sxs-lookup"><span data-stu-id="dae8e-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="dae8e-117">Ayarları'nda seçin **ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="dae8e-117">In the settings, select **Policies**.</span></span>

   ![İlkeleri'ni seçin](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="dae8e-119">Bu kapsam için bir ilke ataması oluşturmak için seçin **atama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dae8e-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![atama Ekle](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="dae8e-121">Atamak istediğiniz ilkeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="dae8e-121">Select the policy you want to assign.</span></span> <span data-ttu-id="dae8e-122">Aboneliğiniz için tüm ilke tanımları eklemediniz olsa bile atama için uygun olan yerleşik ilkelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="dae8e-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="dae8e-123">Bu yerleşik ilkeleri birçok yaygın senaryolar kapsar.</span><span class="sxs-lookup"><span data-stu-id="dae8e-123">These built-in policies cover many common scenarios.</span></span>

   ![tanımı seçin](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="dae8e-125">Bir ilke seçildikten sonra ilke ve bu ilkeye herhangi bir parametre açıklaması görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="dae8e-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="dae8e-126">Örneğin, aşağıdaki gösterir görüntü **konumları izin** kullanılabilir konumlarını kısıtlayan ilkesi için gerekli olan parametre.</span><span class="sxs-lookup"><span data-stu-id="dae8e-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![Parametreleri Göster](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="dae8e-128">Kullanıcı arabirimi aracılığıyla İlkesi parametreler (örneğin, dağıtım için kullanılan konumları) belirtmek için değerleri seçin.</span><span class="sxs-lookup"><span data-stu-id="dae8e-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![parametre değerlerini seçin](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="dae8e-130">Diğer parametreler için değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="dae8e-130">Provide values for the other parameters.</span></span> <span data-ttu-id="dae8e-131">Kapsam ilke ataması başlatırken seçili dikey penceresinde otomatik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="dae8e-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="dae8e-132">Tamamladığınızda **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="dae8e-132">Select **OK** when done.</span></span>

   ![parametrelerini tanımlayın](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="dae8e-134">Belirtilen kapsam için ilke atadınız.</span><span class="sxs-lookup"><span data-stu-id="dae8e-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="dae8e-135">İlke atamalarını görüntülemek</span><span class="sxs-lookup"><span data-stu-id="dae8e-135">View policy assignments</span></span>

<span data-ttu-id="dae8e-136">Bir ilke atadıktan sonra bu kapsama ilkelerin listesini konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="dae8e-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="dae8e-137">**Ayrıntıları** sekmesi ilke ataması özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="dae8e-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![Ayrıntıları Göster](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="dae8e-139">**Atama kuralı** sekmesi ilke tanımı için JSON gösterir.</span><span class="sxs-lookup"><span data-stu-id="dae8e-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![atama kuralı Göster](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="dae8e-141">Var olan bir ilke atamasını değiştirin</span><span class="sxs-lookup"><span data-stu-id="dae8e-141">Change an existing policy assignment</span></span>

<span data-ttu-id="dae8e-142">Bir ilkeyi değiştirmek için seçin **Düzenle atama** veya **Sil**</span><span class="sxs-lookup"><span data-stu-id="dae8e-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![düzenleme veya silme atama](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="dae8e-144">Özel ilkeler atayın</span><span class="sxs-lookup"><span data-stu-id="dae8e-144">Assign custom policies</span></span>

<span data-ttu-id="dae8e-145">Özel ilkeler, aboneliğinizde tanımladıysanız, bu ilkeleri portal aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dae8e-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="dae8e-146">Bu ilkeleri ile başlayan **[özel]**</span><span class="sxs-lookup"><span data-stu-id="dae8e-146">Those policies are prefaced with **[Custom]**</span></span>

![özel ilkeler](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="dae8e-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dae8e-148">Next steps</span></span>
* <span data-ttu-id="dae8e-149">İlkeleri tanımlamak için JSON söz dizimi hakkında bilgi edinmek için [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="dae8e-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="dae8e-150">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="dae8e-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="dae8e-151">İlke şema yayımlanma [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="dae8e-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

