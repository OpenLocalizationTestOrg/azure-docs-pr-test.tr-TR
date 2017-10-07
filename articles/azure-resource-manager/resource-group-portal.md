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
# <a name="manage-azure-resources-through-portal"></a>Portal üzerinden Azure kaynaklarınızı yönetmek
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

Bu konuda gösterilmektedir nasıl toouse hello [Azure portal](https://portal.azure.com) ile [Azure Resource Manager](resource-group-overview.md) toomanage Azure kaynaklarınızı. Merhaba portalı üzerinden kaynaklarına dağıtma hakkında toolearn bkz [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).

Şu anda, her hizmeti hello portalı veya Kaynak Yöneticisi'ni destekler. Bu hizmetler için toouse hello gereksinim [Klasik portal](https://manage.windowsazure.com). Her hizmet Hello durumu için bkz: [Azure portal kullanılabilirlik grafik](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Kaynak gruplarını yönetme

Bir kaynak grubu Azure çözümünü ilgili kaynaklara tutan bir kapsayıcıdır. Merhaba kaynak grubu hello çözüm için tüm hello kaynakları veya yalnızca bir grup olarak toomanage istediğiniz kaynakları içerebilir. Tooallocate kaynakları istediğiniz karar tooresource gruplara göre ne hello en kuruluşunuz için anlamlı üzerinde. Genellikle, hello paylaşmak kaynakları eklemek, kolayca dağıtın, güncelleştirme ve bir grup olarak silmek için aynı kaynak grubunda aynı yaşam döngüsü toohello. 

Merhaba kaynak grubu hello kaynaklarla ilgili meta verileri depolar. Bu nedenle, hello kaynak grubu için bir konumu belirttiğinizde, meta verilerin depolandığı belirtiyorsanız. Uyumluluk nedenleriyle tooensure gerekebilir, verileriniz belirli bir bölgedeki depolanır.

1. toosee, aboneliğinizdeki tüm hello kaynak grupları Seç **kaynak grupları**.
   
    ![Kaynak grupları Gözat](./media/resource-group-portal/browse-groups.png)
2. toocreate boş bir kaynak grubu seçin **Ekle**.
   
    ![Kaynak Grubu Ekle](./media/resource-group-portal/add-resource-group.png)
3. Bir ad ve konum hello yeni kaynak grubu için sağlar. **Oluştur**’u seçin.
   
    ![kaynak grubu oluştur](./media/resource-group-portal/create-empty-group.png)
4. Tooselect gerekebilir **yenileme** toosee kısa süre önce oluşturuldu hello kaynak grubu.
   
    ![kaynak grubu Yenile](./media/resource-group-portal/refresh-resource-groups.png)
5. Kaynak grupları için görüntülenen toocustomize hello bilgiler seçin **sütunları**.
   
    ![sütunları özelleştirme](./media/resource-group-portal/select-columns.png)
6. Merhaba sütunları tooadd seçin ve ardından **güncelleştirme**.
   
    ![sütunlar ekleme](./media/resource-group-portal/add-columns.png)
7. kaynakları tooyour yeni kaynak grubu dağıtma hakkında toolearn bkz [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).
8. Hızlı erişim tooa kaynak grubu için hello dikey tooyour Pano sabitleyebilirsiniz.
   
    ![PIN kaynak grubu](./media/resource-group-portal/pin-group.png)
9. Merhaba Pano hello kaynak grubu ve kaynaklarını görüntüler. Merhaba kaynak grupları veya kendi kaynaklarını toonavigate toohello öğesi birini seçebilirsiniz.
   
    ![PIN kaynak grubu](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Etiket kaynakları
Etiketler tooresource grupları uygulayabilirsiniz ve kaynakları toologically varlıklarınızı düzenleyebilirsiniz. Etiketleri ile çalışma hakkında daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Kaynakları izleme
Bir kaynak seçtiğinizde hello kaynak dikey varsayılan grafikleri ve izleme bu kaynak türü için tabloları gösterir.

1. Kaynak ve bildirimi hello seçin **izleme** bölümü. İlgili toohello kaynak türü olan grafikleri içerir. Merhaba aşağıdaki görüntüde hello varsayılan depolama hesabı için veri izleme gösterir.
   
    ![İzleme Göster](./media/resource-group-portal/show-monitoring.png)
2. Merhaba bölümün yukarısında hello üç nokta (...) seçerek hello dikey tooyour Pano bölümü sabitleyebilirsiniz. Ayrıca, hello boyutu hello hello dikey bölümde özelleştirebilir veya tamamen kaldırın. Merhaba aşağıdaki görüntüde nasıl toopin, özelleştirme, veya hello CPU ve bellek bölümü kaldırmak gösterir.
   
    ![PIN bölümü](./media/resource-group-portal/pin-cpu-section.png)
3. Hello bölüm toohello panoya sabitleme sonra hello Panoda hello Özet görürsünüz. Ve hemen seçerek hello veri toomore ayrıntılarını alır.
   
    ![Görünüm Panosu](./media/resource-group-portal/view-startboard.png)
4. toocompletely özelleştirme izleme hello portal aracılığıyla, tooyour varsayılan pano gidin ve seçin hello veri **yeni Pano**.
   
    ![pano](./media/resource-group-portal/dashboard.png)
5. Yeni panonuz bir ad verin ve hello Pano kutucukları sürükleyin. Merhaba döşeme farklı seçenekler göre filtrelenir.
   
    ![pano](./media/resource-group-portal/create-dashboard.png)
   
     panoları ile çalışma hakkında toolearn bkz [oluşturma ve hello Azure portal panolarında paylaşımı](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Kaynakları yönetme
Bir kaynak için Hello dikey penceresinde hello kaynak yönetmek için hello seçenekler bakın. Merhaba portalı bu belirli kaynak türü için yönetim seçenekleri sunar. Merhaba üstte hello kaynak dikey penceresinin ve hello sol tarafında hello yönetimi komutları bakın.

![Kaynakları yönetme](./media/resource-group-portal/manage-resources.png)

Aşağıdaki seçeneklerden birini başlatılıyor ve bir sanal makineyi durdurmak veya hello hello sanal makinenin özelliklerini yeniden gibi işlemler gerçekleştirebilirsiniz.

## <a name="move-resources"></a>Kaynakları taşıma
Toomove kaynakları tooanother kaynak grubu veya başka bir abonelik gerekirse bkz [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](resource-group-move-resources.md).

## <a name="lock-resources"></a>Kaynakları kilitleme
Yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzdaki diğer kullanıcılara abonelik, kaynak grubu veya kaynak tooprevent kilitleyebilirsiniz. Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Aboneliğiniz ve maliyetleri görüntüleyin
Tüm kaynaklar için abonelik ve hello aktarılmış maliyetleri hakkındaki bilgileri görüntüleyebilirsiniz. Seçin **abonelikleri** ve toosee istediğiniz hello abonelik. Yalnızca bir abonelik tooselect olabilir.

![aboneliği](./media/resource-group-portal/select-subscription.png)

Merhaba abonelik dikey penceresinde içinde yazma oranını bakın.

![yazma oranı](./media/resource-group-portal/burn-rate.png)

Ayrıca, kaynak türüne göre maliyetlerin dökümünü.

![kaynak maliyeti](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Şablonu dışarı aktarma
Kaynak grubunuzun ayarladıktan sonra hello kaynak grubu için tooview hello Resource Manager şablonu isteyebilirsiniz. Dışarı aktarma hello şablon iki avantajları sunar:

1. Merhaba şablonu tüm hello eksiksiz altyapı içerdiğinden hello çözümün gelecekteki dağıtımlar kolayca otomatik hale getirebilirsiniz.
2. Çözümünüzü temsil eden JavaScript nesne gösterimi (JSON) hello bakarak şablon söz dizimi ile tanıdık.

Adım adım yönergeler için bkz: [Azure Resource Manager şablonunu dışarı mevcut kaynaklardan](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Kaynak grubunu veya kaynakları silme
Bir kaynak grubunu silme içerdiği tüm hello kaynakları siler. Kaynakların kaynak grubunda silebilirsiniz. Bağlantılı tooit olan diğer kaynak gruplarının kaynakları olabilir çünkü bir kaynak grubu sildiğinizde tooexercise dikkat istiyor. Resource Manager bağlı kaynaklar silinmez, ancak bunlar beklenen hello kaynakları doğru çalışmayabilir.

![Grup silme](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Sonraki adımlar
* tooview etkinlik günlüklerine bakın [denetim işlemleri Resource Manager ile](resource-group-audit.md).
* bir dağıtım tooview ayrıntılarını görmek [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
* Merhaba portalı üzerinden toodeploy kaynaklarına bakın [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](resource-group-template-deploy-portal.md).
* toomanage erişim tooresources bkz [rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](../active-directory/role-based-access-control-configure.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

