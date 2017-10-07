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
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

Bu konuda gösterilmektedir nasıl toouse hello [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) toodeploy Azure kaynaklarınızı. toolearn kaynaklarınızı yönetme hakkında bkz [yönetmek Azure kaynakları portal üzerinden](resource-group-portal.md).

Şu anda, her hizmeti hello portalı veya Kaynak Yöneticisi'ni destekler. Bu hizmetler için toouse hello gereksinim [Klasik portal](https://manage.windowsazure.com). Her hizmet Hello durumu için bkz: [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Kaynak grubu oluşturma
1. toocreate boş bir kaynak grubu seçin **yeni** > **Yönetim** > **kaynak grubu**.
   
    ![boş bir kaynak grubu oluştur](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Bir ad ve konum girin ve gerekiyorsa, bir abonelik seçin. Hello kaynak grubu hello kaynaklarla ilgili meta verileri depoladığından hello kaynak grubu için bir konum tooprovide gerekir. Uyumluluk nedenleriyle meta verilerin depolandığı toospecify isteyebilirsiniz. Genel olarak, çoğu kaynaklarınızın bulunacağı bir konum belirtin öneririz. Kullanarak, hello aynı konumu şablonunuzu basitleştirin.
   
    ![kümesi Grup değerleri](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Market kaynaklardan dağıtma
Bir kaynak grubu oluşturduktan sonra kaynakları tooit hello Market gelen dağıtabilirsiniz. Merhaba Market yaygın senaryoları için önceden tanımlanmış çözümleri sağlar.

1. toostart bir dağıtım seçin **yeni** ve hello türü kaynak toodeploy istersiniz. Sonra Ara hello belirli sürümü hello kaynak için toodeploy istersiniz.
   
    ![Kaynak dağıtma](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Hello belirli çözüm toodeploy ister misiniz yoksa hello Market için arama yapabilirsiniz.
   
    ![Arama Market](./media/resource-group-template-deploy-portal/search-resource.png)
3. Seçilen kaynak Hello türüne bağlı olarak, ilgili özellikleri tooset dağıtmadan önce oluşan bir koleksiyona sahip. Kaynak türü göre farklılık bu seçenekler Burada, bunlar gösterilmiyor. Tüm türleri için bir hedef kaynak grubu seçmelisiniz. Merhaba aşağıdaki görüntü gösterir nasıl toocreate bir web uygulaması ve oluşturduğunuz toohello kaynak grubu dağıtın.
   
    ![kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Alternatif olarak, bir kaynak grubu toocreate kaynaklarınızı dağıtırken karar verebilirsiniz. Seçin **Yeni Oluştur** ve hello kaynak grubuna bir ad verin.
   
    ![Yeni kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Dağıtımınızı başlar. Merhaba dağıtımın birkaç dakika sürebilir. Merhaba dağıtım tamamlandığında, bir bildirim görür.
   
    ![Görünüm bildirim](./media/resource-group-template-deploy-portal/view-notification.png)
5. Kaynaklarınızı dağıttıktan sonra daha fazla kaynakları toohello kaynak grubu hello kullanarak ekleyebileceğiniz **Ekle** hello kaynak grubu dikey komutu.
   
    ![kaynak ekle](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Özel şablon kaynaklardan dağıtma
Bir dağıtım tooexecute istiyor, ancak hello şablonlardan hello Market kullanmamanız hello çözümünüz için altyapıyı tanımlayan özelleştirilmiş bir şablon oluşturabilirsiniz. şablonları oluşturma hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

1. toodeploy hello Portalı aracılığıyla özelleştirilmiş bir şablon seçin **yeni**ve Arama Başlat **şablon dağıtımı** kadar hello seçenekler arasından seçim yapabilirsiniz.
   
    ![Arama şablon dağıtımı](./media/resource-group-template-deploy-portal/search-template.png)
2. Seçin **şablon dağıtımı** hello kullanılabilir kaynaklardan.
   
    ![Şablon dağıtımı seçin](./media/resource-group-template-deploy-portal/select-template.png)
3. Merhaba şablon dağıtımı başlatılıyor sonra özelleştirmek için kullanılabilir olan hello boş şablonu açın.
   
    ![Şablonu oluşturma](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Merhaba Düzenleyicisi'nde toodeploy hello kaynakları tanımlayan hello JSON söz dizimi ekleyin. Seçin **kaydetmek** bittiğinde. Merhaba JSON söz dizimi yazma ile ilgili yönergeler için bkz: [Resource Manager şablonu Kılavuzu](resource-manager-template-walkthrough.md).
   
    ![şablonu düzenleme](./media/resource-group-template-deploy-portal/edit-template.png)
4. Veya hello önceden var olan bir şablonu seçebilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/). Bu şablonlar hello topluluk tarafından katkısı. Birçok ortak senaryolarını kapsamak ve birisi toodeploy çalıştığınız benzer toowhat olan bir şablon eklenmiş. Merhaba şablonları toofind senaryonuzla eşleşen bir şey arayabilirsiniz.
   
    ![Hızlı Başlatma şablonunu seçin](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Merhaba Düzenleyicisi'nde hello Seçili şablon görüntüleyebilirsiniz.
5. Tüm hello diğer değerleri girdikten sonra Seç **oluşturma** toodeploy hello şablonu. 
   
    ![şablonu dağıtma](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Tooyour hesabı kaydedilmiş bir şablon kaynaklardan dağıtma
Merhaba portal şablonu tooyour Azure hesabı toosave sağlar ve daha sonra yeniden dağıtın. Bu şablonlar, kaydedilen çalışma hakkında daha fazla bilgi için [hello Azure portalı özel şablonları kullanmaya başlama](../marketplace-consumer/mytemplates-getstarted.md).

1. kaydedilen şablonlarınızı toofind seçin **Gözat** > **şablonları**.
   
    ![Şablonları Gözat](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Tooyour hesabı kaydedilmiş şablon Hello listeden bir istediğiniz toowork üzerinde hello seçin.
   
    ![kaydedilen şablonları](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Seçin **dağıtma** tooredeploy bu kaydedilmiş şablonu.
   
    ![Kaydedilmiş şablonu dağıtma](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Sonraki adımlar
* tooview denetim günlüklerine bakın [denetim işlemleri Resource Manager ile](resource-group-audit.md).
* tootroubleshoot dağıtım hataları, bkz: [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
* tooretrieve dağıtım veya kaynak grubu, bir şablondan bkz [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

