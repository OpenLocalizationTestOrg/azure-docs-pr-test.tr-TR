---
title: "Kaynak ilkeleri için aaaAzure portalı | Microsoft Docs"
description: "Açıklar nasıl toouse Azure portal toocreate Resource Manager ilkeleri ve yönetin. Merhaba abonelik veya kaynak gruplarının ilkeleri uygulanabilir."
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
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="d3693-104">Azure portal tooassign kullanın ve kaynak ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="d3693-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="d3693-105">Hello Azure portal, tooassign kaynak ilkeleri tooresource grupları ve abonelikleri etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d3693-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="d3693-106">Merhaba kullanıcı arabirimi tooassign istediğiniz ve o İlkesi toocustomize hello İlkesi ayarları için parametre değerlerini belirtin kolay tooselect hello İlkesi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d3693-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="d3693-107">tooassign İlkesi hello portal aracılığıyla, hello ilke tanımı önceden aboneliğinizde var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d3693-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="d3693-108">Aboneliğiniz, tooassign tooresource gruplar veya abonelikler için hazır olan birkaç yerleşik ilke tanımları sahip.</span><span class="sxs-lookup"><span data-stu-id="d3693-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="d3693-109">Bu yerleşik ilkeleri ve hello portal tooassign ilkeleri kullanırken tanımladığınız tüm özel ilkeler bakın.</span><span class="sxs-lookup"><span data-stu-id="d3693-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="d3693-110">Bir giriş toopolicies ve nasıl toodefine özelleştirilmiş ilke için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d3693-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="d3693-111">İlkeler tüm alt kaynaklar tarafından devralınır.</span><span class="sxs-lookup"><span data-stu-id="d3693-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="d3693-112">Bu nedenle, bir ilke uygulanmış tooa kaynak grubu ise, uygun tooall hello kaynakların kaynak grubunda olur.</span><span class="sxs-lookup"><span data-stu-id="d3693-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="d3693-113">Bu makalede, hello terim **kapsam** toohello kaynak grubu veya hello İlkesi atanmış abonelik başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="d3693-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="d3693-114">İlkeleri oluşturma ve (PUT ve işlemleri düzeltme eki) kaynakları güncelleştirme değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d3693-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="d3693-115">Bir ilke atama</span><span class="sxs-lookup"><span data-stu-id="d3693-115">Assign a policy</span></span>

1. <span data-ttu-id="d3693-116">tooassign İlkesi tooeither bir kaynak grubu veya abonelik, bu kaynak grubuna veya aboneliğe seçin.</span><span class="sxs-lookup"><span data-stu-id="d3693-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="d3693-117">Hello Ayarları'nda seçin **ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="d3693-117">In hello settings, select **Policies**.</span></span>

   ![İlkeleri'ni seçin](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="d3693-119">toocreate bu kapsam için bir ilke atamasını seçin **atama Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d3693-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![atama Ekle](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="d3693-121">Tooassign hello ilkeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="d3693-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="d3693-122">Herhangi bir ilke tanımları tooyour abonelik eklemediniz olsa bile atama için uygun olan yerleşik ilkeleri hello bakın.</span><span class="sxs-lookup"><span data-stu-id="d3693-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="d3693-123">Bu yerleşik ilkeleri birçok yaygın senaryolar kapsar.</span><span class="sxs-lookup"><span data-stu-id="d3693-123">These built-in policies cover many common scenarios.</span></span>

   ![tanımı seçin](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="d3693-125">Bir ilke seçildikten sonra bu ilkeye herhangi bir parametre ve bir açıklama hello İlkesi bakın.</span><span class="sxs-lookup"><span data-stu-id="d3693-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="d3693-126">Örneğin, hello aşağıdaki görüntüde hello gösterir **konumları izin** hello kullanılabilir konumlarını kısıtlayan hello ilkesi için gerekli olan parametre.</span><span class="sxs-lookup"><span data-stu-id="d3693-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![Parametreleri Göster](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="d3693-128">Merhaba kullanıcı arabirimi aracılığıyla hello değerleri toospecify hello İlkesi parametreler (örneğin, dağıtım için kullanılan hello konumları) için seçin.</span><span class="sxs-lookup"><span data-stu-id="d3693-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![parametre değerlerini seçin](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="d3693-130">Değerleri hello için diğer parametreler girin.</span><span class="sxs-lookup"><span data-stu-id="d3693-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="d3693-131">Merhaba kapsam hello dikey penceresinde hello ilke ataması başlatırken seçili otomatik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="d3693-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="d3693-132">Tamamladığınızda **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d3693-132">Select **OK** when done.</span></span>

   ![parametrelerini tanımlayın](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="d3693-134">Hello İlkesi atadığınız toohello Belirtilen kapsam.</span><span class="sxs-lookup"><span data-stu-id="d3693-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="d3693-135">İlke atamalarını görüntülemek</span><span class="sxs-lookup"><span data-stu-id="d3693-135">View policy assignments</span></span>

<span data-ttu-id="d3693-136">Bir ilke atadıktan sonra bu kapsam için ilke hello listesi konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="d3693-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="d3693-137">Merhaba **ayrıntıları** sekmesi hello ilke ataması özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3693-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![Ayrıntıları Göster](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="d3693-139">Merhaba **atama kuralı** sekmesi hello JSON hello ilke tanımı için gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3693-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![atama kuralı Göster](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="d3693-141">Var olan bir ilke atamasını değiştirin</span><span class="sxs-lookup"><span data-stu-id="d3693-141">Change an existing policy assignment</span></span>

<span data-ttu-id="d3693-142">toochange bir ilke seçin **Düzenle atama** veya **Sil**</span><span class="sxs-lookup"><span data-stu-id="d3693-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![düzenleme veya silme atama](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="d3693-144">Özel ilkeler atayın</span><span class="sxs-lookup"><span data-stu-id="d3693-144">Assign custom policies</span></span>

<span data-ttu-id="d3693-145">Özel ilkeler, aboneliğinizde tanımladıysanız, bu ilkeleri hello portal aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d3693-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="d3693-146">Bu ilkeleri ile başlayan **[özel]**</span><span class="sxs-lookup"><span data-stu-id="d3693-146">Those policies are prefaced with **[Custom]**</span></span>

![özel ilkeler](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="d3693-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3693-148">Next steps</span></span>
* <span data-ttu-id="d3693-149">toolearn ilkelerini tanımlamak için hello JSON söz dizimi hakkında bkz [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d3693-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="d3693-150">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d3693-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="d3693-151">Hello İlkesi Şema konumunda yayımlanır [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="d3693-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

