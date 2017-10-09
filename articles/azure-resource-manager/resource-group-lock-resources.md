---
title: "aaaLock Azure kaynaklarını tooprevent değişiklikleri | Microsoft Docs"
description: "Kullanıcının güncelleştirme veya tüm kullanıcılar ve roller için bir kilit uygulayarak kritik Azure kaynakları silmesini engeller."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Kilitleme kaynakları tooprevent beklenmeyen değişiklikleri 
Yönetici olarak, yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzdaki diğer kullanıcıların toolock bir abonelik, kaynak grubu veya kaynak tooprevent gerekebilir. Merhaba kilit düzeyi çok ayarlayabilirsiniz**CanNotDelete** veya **salt okunur**. 

* **CanNotDelete** yetkili kullanıcıların, hala okuyun ve kaynak değiştirebilirsiniz, ancak hello kaynağı silemezsiniz anlamına gelir. 
* **Salt okunur** yetkili kullanıcılar, bir kaynak okuyabilir, ancak delete veya update hello kaynak anlamına gelir. Bu kilit uygulama olan tüm yetkili kullanıcıların toohello hello tarafından izinler benzer toorestricting **okuyucu** rol. 

## <a name="how-locks-are-applied"></a>Kilitleri nasıl uygulanır

Bir üst kapsamda kilit uyguladığınızda, kapsamı içindeki tüm kaynakların hello devral aynı kilitle. Hatta kaynak daha sonra Ekle hello kilit hello üst öğeden devralır. Merhaba en kısıtlayıcı kilit hello Devralmada önceliklidir.

Rol tabanlı erişim denetimi farklı olarak, tüm kullanıcılar ve roller yönetim kilitleri tooapply bir kısıtlama kullanın. Kullanıcılar ve roller için izinleri ayarlama hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

Resource Manager kilitleri uygulamak çok gönderilen işlemden oluşur hello Yönetim düzeyi içinde gerçekleşen toooperations`https://management.azure.com`. Merhaba kilitleri nasıl kaynakları kendi işlevleri gerçekleştirmek kısıtlamaz. Kaynak kısıtlı değişir, ancak kaynak işlemlerinin sınırlı değildir. Örneğin, bir SQL veritabanında salt okunur kilit silmesini engeller veya hello veritabanı, ancak değiştirme, oluşturma, güncelleştirme ya da hello veritabanındaki verileri silme engellemez. Bu işlemler çok gönderilmediği için veri hareketlerini izin verilen`https://management.azure.com`.

Uygulama **ReadOnly** gibi görünen bazı işlemler gerçekten ek eylemleri gerektirir okuma olduğundan toounexpected sonuçları yol açabilir. Örneğin, yerleştirme bir **ReadOnly** bir depolama hesabı üzerinde kilit hello anahtarları listeleme tüm kullanıcıları engeller. yazma işlemlerini hello listesi Hello anahtarların döndürdüğünden anahtarları işlemi bir POST isteği gerçekleştirilir. Başka bir örneğin yerleştirme bir **ReadOnly** kilit bir uygulama hizmeti kaynağına yazma erişimi bu etkileşimi gerektirmesi nedeniyle hello kaynak dosyalarını görüntüleme Visual Studio Sunucu Gezgini engeller.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Kimin oluşturmak veya kuruluşunuzdaki kilitleri silmek mi
Yönetim kilit toocreate ya da delete gerekir erişiminiz çok`Microsoft.Authorization/*` veya `Microsoft.Authorization/locks/*` eylemler. Merhaba yerleşik roller, yalnızca **sahibi** ve **kullanıcı erişimi Yöneticisi** bu eylemleri verilir.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Şablon
Hello aşağıdaki örnekte bir depolama hesabı üzerinde bir kilit oluşturan bir şablonu gösterir. Merhaba depolama hesabı üzerinde hangi tooapply hello kilit parametre olarak sağlanır. Merhaba hello kilit adı hello kaynak adı ile birleştirerek oluşturulan **/Microsoft.Authorization/** ve bu durumda hello hello kilit adı **myLock**.

sağlanan hello türü belirli toohello kaynak türüdür. Depolama alanı için hello türü too"Microsoft.Storage/storageaccounts/providers/locks"ayarlayın.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Kilit hello kullanarak kaynakları Azure PowerShell ile dağıtılan [yeni AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) komutu.

toolock bir kaynak hello kaynağın hello adı, kaynak türü ve kaynak grubu adını sağlayın.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

bir kaynak grubu toolock hello hello kaynak grubunun adını sağlayın.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

kilit, kullanım bilgilerini tooget [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget, aboneliğinizdeki tüm hello kilitleri kullanın:

```powershell
Get-AzureRmResourceLock
```

bir kaynak için tüm kilitleri tooget kullanın:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

bir kaynak grubu için tüm kilitleri tooget kullanın:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell diğer komutları gibi çalışma kilitlerini sağlar [kümesi AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate bir kilit ve [Kaldır AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete kilit.

## <a name="azure-cli"></a>Azure CLI

Kilit hello kullanarak Azure CLI kaynaklarla dağıtılan [az kilit oluşturmak](/cli/azure/lock#create) komutu.

toolock bir kaynak hello kaynağın hello adı, kaynak türü ve kaynak grubu adını sağlayın.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

bir kaynak grubu toolock hello hello kaynak grubunun adını sağlayın.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

kilit, kullanım bilgilerini tooget [az kilit listesi](/cli/azure/lock#list). tooget, aboneliğinizdeki tüm hello kilitleri kullanın:

```azurecli
az lock list
```

bir kaynak için tüm kilitleri tooget kullanın:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

bir kaynak grubu için tüm kilitleri tooget kullanın:

```azurecli
az lock list --resource-group exampleresourcegroup
```

Azure CLI diğer komutları gibi çalışma kilitlerini sağlar [az kilit güncelleştirme](/cli/azure/lock#update) tooupdate bir kilit ve [az kilit silme](/cli/azure/lock#delete) toodelete kilit.

## <a name="rest-api"></a>REST API
Dağıtılan hello kaynaklarla kilitleyebilirsiniz [yönetim kilitleri için REST API](https://docs.microsoft.com/rest/api/resources/managementlocks). Merhaba REST API toocreate sağlar ve kilitleri silin ve varolan kilitler hakkında bilgi alın.

toocreate bir kilit çalıştırın:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir. Merhaba kilit-istediğiniz addır toocall hello kilitle. API sürümü için kullanmak **2015-01-01**.

Merhaba istekte hello kilitleme hello özelliklerini belirten bir JSON nesnesi içerir.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Sonraki adımlar
* Kaynak kilitleri ile çalışma hakkında daha fazla bilgi için bkz: [kilit aşağı bilgisayarınızı Azure kaynakları](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* mantıksal olarak kaynaklarınızı düzenleme hakkında toolearn bakın [kullanarak kaynaklarınızı tooorganize etiketleri](resource-group-using-tags.md)
* hangi kaynak grubu bir kaynak bulunur, toochange bakın [kaynakları toonew kaynak grubu taşıma](resource-group-move-resources.md)
* Özelleştirilmiş ilkeler aboneliğinizle arasında kısıtlamaları ve kuralları uygulayabilirsiniz. Daha fazla bilgi için bkz: [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](resource-manager-policy.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

