---
title: "aaaUnderstand Azure dağıtım hataları | Microsoft Docs"
description: "Açıklar nasıl toolearn Azure dağıtım hataları hakkında."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Dağıtım hatası, azure dağıtım tooazure dağıtma"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Azure dağıtım hataları anlama
Bu konu, dağıtım hatalarını ve hata hakkında daha fazla bilgi nasıl bulabilir açıklar. Çözümleri toocommon dağıtım hataları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>İki tür hataları
İki tür alabileceğiniz hataları vardır:

* Doğrulama hataları
* Dağıtım hataları

Görüntü aşağıdaki hello hello etkinlik günlüğü bir abonelik için gösterir. Bu iki dağıtım temsil eder. Bir dağıtımda hello şablon, doğrulama başarısız oldu (**doğrulama**) ve devam. İçindeki diğer dağıtım Merhaba, hello şablon doğrulamayı geçen ancak hello kaynakları oluşturma başarısız oldu (**yazma dağıtımları**). 

![Hata Kodu Göster](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Dağıtım öncesinde belirlenebilir senaryolardan doğrulama hataları ortaya çıkar. Sözdizimi hataları, şablonu veya abonelik kotalarında aşacak çalışırken toodeploy kaynakları içerirler. Dağıtım hataları hello dağıtım işlemi sırasında ortaya koşullar ortaya çıkabilecek. Paralel olarak dağıtılan bir kaynak tooaccess çalışırken içerirler.

Hataları return tootroubleshoot hello dağıtım kullandığınız bir hata kodu her iki tür. Her iki tür hataları hello görünür [etkinlik günlüğü](resource-group-audit.md). Ancak, doğrulama hataları Hello dağıtım hiçbir zaman başlamadı çünkü dağıtım geçmişiniz görünmez.

## <a name="determine-error-code"></a>Hata kodu belirleme

Merhaba hata iletisi ve hello hata kodu bakarak bir hata hakkında bilgi edinebilirsiniz. Merhaba [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md) makalede hata koduna göre çözümler listelenmektedir. Bu konu, nasıl toouse hello Azure portal toodiscover hello hata kodu gösterir.

### <a name="validation-errors"></a>Doğrulama hataları

Merhaba Portalı aracılığıyla dağıtırken değerlerinizi gönderdikten sonra bir doğrulama hatası bakın.

![Portal doğrulama hatasını göster](./media/resource-manager-troubleshoot-tips/validation-error.png)

Daha fazla ayrıntı için selamlama iletisine seçin. Görüntü aşağıdaki hello gördüğünüz bir **InvalidTemplateDeployment** hata ve bir ilke belirten bir ileti dağıtım engellendi.

![Doğrulama ayrıntıları göster](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Dağıtım hataları

Merhaba işlemi doğrulama başarılı olur, ancak dağıtım sırasında başarısız olduğunda hello Bildirimlerde hello hatasına bakın. Merhaba bildirim seçin.

![bildirim hatası](./media/resource-manager-troubleshoot-tips/notification.png)

Merhaba dağıtımı hakkında daha fazla ayrıntı bakın. Merhaba seçeneği toofind hello hata hakkında daha fazla bilgi seçin.

![dağıtım başarısız oldu](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Merhaba hata iletisi ve hata kodları bakın. İki hata kodları dikkat edin. Merhaba ilk hata kodu (**DeploymentFailed**) hello ayrıntılarını sağlamaz genel bir hata toosolve hello hata gerekiyor. Merhaba ikinci hata kodunu (**StorageAccountNotFound**) ihtiyacınız hello ayrıntıları sağlar. 

![Hata ayrıntıları](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Hata ayıklama günlük kaydını etkinleştir
Bazen, nelerin yanlış gittiğini hello istek ve yanıt toodiscover hakkında daha fazla bilgi gerekir. PowerShell veya Azure CLI kullanarak bir dağıtım sırasında günlüğe ek bilgiler isteyebilir.

- PowerShell

   PowerShell'de hello ayarlamak **DeploymentDebugLogLevel** parametresi tooAll, ResponseContent veya RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Merhaba istek içeriği ile Merhaba cmdlet'i aşağıdaki inceleyin:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   Veya, ile içerik yanıt hello:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Bu bilgiler hello şablonunda bir değer yanlış ayarlanmış olup olmadığını belirlemenize yardımcı olabilir.

- Azure CLI

   Merhaba dağıtım işlemleri ile Merhaba komutu aşağıdaki inceleyin:

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- İç içe geçmiş şablonu

   Kullanım hello iç içe geçmiş bir şablon toolog hata ayıklama bilgileri **debugSetting** öğesi.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Sorun giderme şablonu oluşturma
Bazı durumlarda, en kolay yolu tootroubleshoot hello tootest bölümlerini, şablonudur. Merhaba hataya neden olduğunu düşündüğünüz hello Bölümü'toofocus sağlayan basitleştirilmiş bir şablon oluşturabilirsiniz. Örneğin, bir kaynak başvururken bir hata alıyorsunuz varsayalım. Tüm şablon postalarla yerine, soruna hello parçası döndürür bir şablon oluşturun. Şablon işlevleri doğru kullanarak hello sağ parametrelerinde geçtiğiniz ve beklediğiniz hello kaynak alınıyor belirlemenize yardımcı olabilir.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

Ya da tooincorrectly bağımlılıkları ayarlama ile ilgili olduğunu düşündüğünüz dağıtım hataları karşılaşıyoruz varsayalım. Basitleştirilmiş şablonlara bölerek şablonunuzu test edin. İlk olarak, yalnızca tek bir kaynak (bir SQL sunucu gibi) dağıtan bir şablon oluşturun. Bu kaynağı doğru tanımlı sahip olduğunuzdan emin olduğunuzda (SQL veritabanı gibi) bağımlı bir kaynak ekleyin. Doğru tanımlanmadı iki kaynaklarla varsa, bağımlı diğer kaynaklar (örneğin, denetim ilkeleri) ekleyin. Her sınama dağıtımı Between hello kaynak grubu toomake emin, yeterli sınama hello bağımlılıkları silin. 

## <a name="check-deployment-sequence"></a>Onay dağıtım sırası

Kaynakları içinde beklenmeyen bir sıra dağıtılan birçok dağıtım hata meydana gelir. Bağımlılıklar doğru ayarlanmadı, bu hatalar ortaya çıkar. Gerekli bir bağımlılığı eksik olduğunda, bir kaynak için başka bir kaynak ancak hello başka bir değer henüz yok toouse çalışır. Bir kaynağın bulunamadığını bildiren bir hata alırsınız. Bu tür hatalara zaman zaman karşılaşabilirsiniz hello dağıtım süresini her kaynak için değişebileceğinden. Örneğin, ilk denemesi toodeploy kaynaklarınızı başarılı gerekli bir kaynağa zamanında rastgele tamamladığı için. Ancak, kaynak süre içinde tamamlanmadı Hello gerekli olduğundan girişiminiz başarısız olur. 

Ancak, gerekli olmayan tooavoid ayarı bağımlılıkları istiyor. Gereksiz bağımlılıkları varsa, paralel olarak dağıtılan birbirlerine bağımlı olmayan kaynakları engelleyerek hello hello dağıtım süresini uzatmak. Ayrıca, hello dağıtım engelleme döngüsel bağımlılıklar oluşturabilir. Merhaba [başvuru](resource-group-template-functions-resource.md#reference) işlevi bu kaynak hello dağıtıldığında bu dolaylı bir bağımlılığı hello başvurulan kaynakta oluşturur aynı şablonu. Bu nedenle, hello belirtilen hello bağımlılıkları'den daha fazla bağımlılıkları olabilir **dependsOn** özelliği. Merhaba [ResourceId](resource-group-template-functions-resource.md#resourceid) işlevi oluşturmaz dolaylı bir bağımlılığı veya hello kaynak var olduğunu doğrulayın.

Bağımlılık sorunlarını karşılaştığınızda, kaynak dağıtım hello sırasını toogain fikirler gerekir. Merhaba sırasını dağıtım işlemlerini tooview:

1. Merhaba dağıtım geçmişi kaynak grubunuz için seçin.

   ![Dağıtım geçmişi seçin](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Bir dağıtım hello geçmişinden ve seçin **olayları**.

   ![Dağıtım olaylarını seçin](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Her kaynak için olayların Hello sırası inceleyin. Dikkat toohello her işlemin durumunu ücret ödersiniz. Örneğin, hello aşağıdaki görüntüde dağıtılan üç depolama hesaplarını paralel olarak gösterir. Üç depolama hesapları hello bildirimi sırasında hello başlatıldı aynı anda.

   ![Paralel dağıtım](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   Merhaba sonraki resim paralel olarak değil dağıtılan üç depolama hesaplarını gösterir. Hello ikinci depolama hesabı hello ilk depolama hesabında bağlıdır ve hello üçüncü depolama hesabı hello ikinci depolama hesabına bağlıdır. Bu nedenle, hello ilk depolama hesabı başlatıldı, kabul ve hello bir sonraki başlatılışında önce tamamlandı.

   ![sıralı dağıtım](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Hatta daha karmaşık senaryolar için kullandığınız dağıtım başlatıldığında ve her kaynak için tamamlanan aynı teknik toodiscover hello. Merhaba sırası, beklediğinizden farklı ise, dağıtım olayları toosee arayın. Öyleyse, bu kaynak için hello bağımlılıkları yeniden.

Resource Manager şablonu doğrulama sırasında döngüsel bağımlılıklar tanımlar. Döngüsel bağımlılık özellikle bildiren bir hata iletisi yok değerini döndürür. toosolve döngüsel bağımlılık:

1. Şablonunuzda, hello döngüsel bağımlılık olarak tanımlanan hello kaynak bulunamıyor. 
2. Bu kaynak için hello inceleyin **dependsOn** özellik ve tüm kullanımlarını hello **başvuru** hangi kaynaklara bağımlı toosee işlev. 
3. Hangi kaynaklara bağlı oldukları bu kaynakları toosee inceleyin. Merhaba özgün kaynaklara bağımlı bir kaynak fark kadar hello bağımlılıkları izleyin.
5. Merhaba döngüsel bağımlılık olarak söz konusu Hello kaynaklar için hello tüm kullanımını dikkatlice inceleyin **dependsOn** özelliği tooidentify gerekli olmayan tüm bağımlılıkları. Bu bağımlılıkları kaldırın. Bir bağımlılık gerekli olmadığından emin değilseniz, bu kaldırmayı deneyin. 
6. Merhaba şablonunu yeniden dağıtın.

Merhaba değerleri kaldırılıyor **dependsOn** hello şablonu dağıttığınızda, özellik hataları neden olabilir. Bir hatayla karşılaşırsanız hello bağımlılık hello şablon uygulamasına geri ekleyin. 

Bu yaklaşımı hello döngüsel bağımlılık çözmezse alt kaynakları (örneğin, uzantıları veya yapılandırma ayarları), dağıtım mantığının parçası taşınmasını göz önünde bulundurun. Bu alt kaynakları toodeploy hello kaynakları hello döngüsel bağımlılık olarak söz konusu sonra yapılandırın. Örneğin, iki sanal makine dağıtıyorsanız ancak toohello diğer başvuran her birinin özelliklerini ayarlamalısınız varsayalım. Bunları sırasının hello dağıtabilirsiniz:

1. VM1
2. vm2
3. Vm1 uzantısı vm1 ve vm2 bağlıdır. Merhaba uzantısı vm2 alır vm1 değerlerini ayarlar.
4. Vm2 uzantısı vm1 ve vm2 bağlıdır. Merhaba uzantısı vm1 alır vm2 değerlerini ayarlar.

Merhaba aynı yaklaşımı uygulama hizmeti uygulamalar için çalışır. Yapılandırma değerlerini hello uygulama kaynak bir alt kaynağı taşımayı düşünün. Sırasının hello iki web uygulamaları dağıtabilirsiniz:

1. webapp1
2. webapp2
3. config webapp1 için webapp1 ve webapp2 bağlıdır. Uygulama ayarları webapp2 değerlerle içerir.
4. config webapp2 için webapp1 ve webapp2 bağlıdır. Uygulama ayarları webapp1 değerlerle içerir.


## <a name="next-steps"></a>Sonraki adımlar
* Çözümleri toocommon dağıtım hataları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
* Eylemler, Denetim hakkında toolearn bkz [denetim işlemleri Resource Manager ile](resource-group-audit.md).
* dağıtım sırasında Eylemler toodetermine hello hatalarla ilgili toolearn bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
