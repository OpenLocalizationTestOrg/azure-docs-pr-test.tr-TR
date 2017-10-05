---
title: "Azure kaynaklarınızı dağıtmak için Azure portalını kullanma | Microsoft Docs"
description: "Azure portalı ve Azure Resource Manager kaynaklarınızı dağıtmak için kullanın."
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
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

Bu konuda nasıl kullanılacağını gösterir [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) Azure kaynaklarınızı dağıtmak için. Kaynaklarınızın yönetilmesi hakkında bilgi edinmek için [yönetmek Azure kaynakları portal üzerinden](resource-group-portal.md).

Şu anda, her hizmeti Portalı'nı veya Kaynak Yöneticisi'ni destekler. Bu hizmetler için kullanmanız gerekir. [Klasik portal](https://manage.windowsazure.com). Her hizmet durumunu görmek [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Kaynak grubu oluşturma
1. Boş bir kaynak grubu oluşturmak için seçin **yeni** > **Yönetim** > **kaynak grubu**.
   
    ![boş bir kaynak grubu oluştur](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Bir ad ve konum girin ve gerekiyorsa, bir abonelik seçin. Kaynak grubu kaynaklarla ilgili meta verileri depoladığından kaynak grubu için bir konum sağlamanız gerekir. Uyumluluk nedenleriyle meta verilerin nerede depolanacağını belirtmek isteyebilirsiniz. Genel olarak, çoğu kaynaklarınızın bulunacağı bir konum belirtin öneririz. Aynı konuma kullanarak şablonunuzu basitleştirebilirsiniz.
   
    ![kümesi Grup değerleri](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Market kaynaklardan dağıtma
Bir kaynak grubu oluşturduktan sonra kendisine marketten kaynakları dağıtabilirsiniz. Market yaygın senaryoları için önceden tanımlanmış çözümleri sağlar.

1. Bir dağıtımı başlatmak için **yeni** ve dağıtmak istiyor kaynak türü. Ardından, dağıtmak istediğiniz kaynak belirli sürümü için bakın.
   
    ![Kaynak dağıtma](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Dağıtmak istediğiniz belirli çözüm görmüyorsanız, Market arayabilirsiniz.
   
    ![Arama Market](./media/resource-group-template-deploy-portal/search-resource.png)
3. Seçilen kaynak türüne bağlı olarak, dağıtım öncesinde ayarlamak için ilgili özellikleri koleksiyonu vardır. Kaynak türü göre farklılık bu seçenekler Burada, bunlar gösterilmiyor. Tüm türleri için bir hedef kaynak grubu seçmelisiniz. Aşağıdaki resimde, bir web uygulaması oluşturmak ve oluşturduğunuz kaynak grubuna dağıtmak gösterilmiştir.
   
    ![kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Alternatif olarak, kaynaklarınızın dağıtırken bir kaynak grubu oluşturmak için karar verebilirsiniz. Seçin **Yeni Oluştur** ve kaynak grubu bir ad verin.
   
    ![Yeni kaynak grubu oluştur](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Dağıtımınızı başlar. Dağıtımın birkaç dakika sürebilir. Dağıtım tamamlandığında, bir bildirim görür.
   
    ![Görünüm bildirim](./media/resource-group-template-deploy-portal/view-notification.png)
5. Kaynaklarınızı dağıttıktan sonra daha fazla kaynak kaynak grubuna kullanarak ekleyebileceğiniz **Ekle** kaynak grubu dikey komutu.
   
    ![kaynak ekle](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Özel şablon kaynaklardan dağıtma
Bir dağıtım yürütme ancak şablonlardan herhangi birini markette kullanmamak istiyorsanız, çözümünüz için altyapıyı tanımlayan özelleştirilmiş bir şablon oluşturabilirsiniz. Şablonları oluşturma hakkında bilgi edinmek için [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

1. Özelleştirilmiş bir şablon portal üzerinden dağıtmak için seçin **yeni**ve Arama Başlat **şablon dağıtımı** kadar seçenekler arasından seçim yapabilirsiniz.
   
    ![Arama şablon dağıtımı](./media/resource-group-template-deploy-portal/search-template.png)
2. Seçin **şablon dağıtımı** kullanılabilir kaynaklardan.
   
    ![Şablon dağıtımı seçin](./media/resource-group-template-deploy-portal/select-template.png)
3. Şablon dağıtımı başlatılıyor sonra özelleştirmek için kullanılabilir boş şablonu açın.
   
    ![Şablonu oluşturma](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Düzenleyicisi'nde dağıtmak istediğiniz kaynakları tanımlayan JSON söz dizimi ekleyin. Seçin **kaydetmek** bittiğinde. JSON söz dizimi yazma ile ilgili yönergeler için bkz: [Resource Manager şablonu Kılavuzu](resource-manager-template-walkthrough.md).
   
    ![şablonu düzenleme](./media/resource-group-template-deploy-portal/edit-template.png)
4. Veya önceden varolan bir şablondan seçebilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/). Bu şablonlar, topluluk tarafından katkısı. Birçok ortak senaryolarını kapsamak ve birisi ne dağıtmaya çalıştığınız benzer bir şablon eklenmiş. Şablonları senaryonuzla eşleşen bir şey bulmak için arama yapabilirsiniz.
   
    ![Hızlı Başlatma şablonunu seçin](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Seçili şablonu Düzenleyicisi'nde görüntüleyebilirsiniz.
5. Diğer tüm değerleri girdikten sonra seçin **oluşturma** şablonu dağıtmak için. 
   
    ![şablonu dağıtma](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a>Hesabınız için kaydedilen bir şablon kaynaklardan dağıtma
Portal, Azure hesabınızda bir şablonu kaydetmek ve daha sonra yeniden dağıtmak sağlar. Bu şablonlar, kaydedilen çalışma hakkında daha fazla bilgi için [Azure Portal'da özel şablonları kullanmaya başlama](../marketplace-consumer/mytemplates-getstarted.md).

1. Kaydedilen şablonlarınızı bulmak için seçin **Gözat** > **şablonları**.
   
    ![Şablonları Gözat](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Hesabınıza kaydedilebilir şablonları listesinden, üzerinde çalışmak istediğiniz birini seçin.
   
    ![kaydedilen şablonları](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Seçin **dağıtma** kaydedilmiş bu şablonu yeniden dağıtılamadı.
   
    ![Kaydedilmiş şablonu dağıtma](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Sonraki adımlar
* Denetim günlüklerini görüntülemek için bkz: [denetim işlemleri Resource Manager ile](resource-group-audit.md).
* Dağıtım hataları gidermek için bkz: [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
* Bir dağıtım veya kaynak grubunu şablon almak için bkz: [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).
* Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).

