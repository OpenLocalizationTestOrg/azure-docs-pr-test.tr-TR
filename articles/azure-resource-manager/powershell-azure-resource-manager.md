---
title: "aaaManage Azure PowerShell ile çözümleri | Microsoft Docs"
description: "Azure PowerShell ve Resource Manager toomanage kaynaklarınızı kullanın."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Azure PowerShell ve Resource Manager ile kaynakları yönetme
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
>
>

Bu makalede, bilgi nasıl toomanage, Azure PowerShell ve Azure Resource Manager çözümlerinizi. Resource Manager ile bilmiyorsanız bkz [Resource Manager'a genel bakış](resource-group-overview.md). Bu konu, yönetim görevlerine odaklanır. Yapacaklarınız:

1. Kaynak grubu oluşturma
2. Bir kaynak toohello kaynak grubu Ekle
3. Bir etiketi toohello kaynak ekleyin
4. Adlarını veya etiket değerlerine göre kaynaklarını sorgulama
5. Uygulama ve hello kaynak üzerinde bir kilit kaldırın
6. Bir kaynak grubu Sil

Bu makalede gösterme nasıl toodeploy bir Resource Manager şablonu tooyour abonelik. Bu bilgi için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Azure PowerShell ile çalışmaya başlama

Azure PowerShell yüklü değilse bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

Azure PowerShell hello geçmiş yüklü, ancak bu kısa süre önce güncelleştirdiniz değil, hello en son sürümünü yüklemeyi göz önünde bulundurun. Merhaba sürüm hello aracılığıyla güncelleştirebilirsiniz tooinstall kullanılan aynı yöntemi. Örneğin, Web Platformu yükleyicisi hello kullandıysanız, yeniden başlatın ve bir güncelleştirme için bakın.

hello Azure kaynakları modülü sürümünüz toocheck kullanmak hello aşağıdaki cmdlet'i:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Bu konuda 3.3.0 sürümü için güncelleştirildi. Önceki bir sürümü varsa, deneyiminiz Bu konu başlığı altında gösterilen hello adımlar eşleşmeyebilir. Bu sürümde hello cmdlet'ler hakkında daha fazla belgeler için bkz: [AzureRM.Resources Modülü](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Azure hesabı tooyour içinde oturum
Çözümünüzü üzerinde çalışmaya başlamadan önce tooyour hesabında oturum açmanız gerekir.

Azure hesabı tooyour toolog kullanmak hello **Login-AzureRmAccount** cmdlet'i.

```powershell
Login-AzureRmAccount
```

Merhaba cmdlet hello Azure hesabınızda oturum açma kimlik bilgilerini ister. Kullanılabilir tooAzure PowerShell şekilde oturum açtıktan sonra hesap ayarlarınızı indirir.

Merhaba cmdlet, hesap ve hello abonelik toouse hello görevler hakkında bilgi döndürür.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Birden fazla aboneliğiniz varsa, tooa farklı aboneliğe geçebilirsiniz. İlk olarak, hesabınız için tüm hello abonelikleri görelim.

```powershell
Get-AzureRmSubscription
```

Etkin ve devre dışı abonelikler döndürür.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa farklı abonelik ile Merhaba hello abonelik adını sağlayın **Set-AzureRmContext** cmdlet'i.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Tüm kaynaklar tooyour abonelik dağıtmadan önce hello kaynakları içeren bir kaynak grubu oluşturmanız gerekir.

toocreate bir kaynak grubu kullanmak hello **New-AzureRmResourceGroup** cmdlet'i. Merhaba komutunu kullanan hello **adı** parametresi toospecify hello kaynak grubu ve hello için bir ad **konumu** parametresi toospecify konumu.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

Hello çıktı hello biçimi aşağıdaki gibidir:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Tooretrieve hello kaynak grubu daha sonra gerekirse hello aşağıdaki cmdlet'i kullanın:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget tüm kaynak grupları aboneliğinizde Merhaba, bir ad belirtmezseniz:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Kaynakları tooa kaynak grubu Ekle
tooadd kaynak toohello kaynak grubu, kullanabileceğiniz hello **yeni AzureRmResource** cmdlet veya kaynak belirli toohello türünde bir cmdlet oluşturmakta (gibi **New-AzureRmStorageAccount**). Daha kolay toouse hello yeni kaynağı için gerekli hello özellikleri için parametreler içerdiğinden, belirli tooa kaynak türü olan bir cmdlet bulabilirsiniz. toouse **yeni AzureRmResource**, bunlar için istenmeden tüm hello özellikleri tooset bilmeniz gerekir.

Ancak, Hello yeni kaynak bir Resource Manager şablonu mevcut olmadığından kaynak cmdlet'leri aracılığıyla ekleme gelecekteki karışıklığa neden olabilir. Microsoft Azure, çözümünüz için altyapıyı hello Resource Manager şablonunda tanımlama önerir. Şablonları tooreliably etkinleştirin ve tekrar tekrar çözümünüzü dağıtın. Bu konu, bir PowerShell cmdlet'i ile depolama hesabı oluşturma, ancak daha sonra kaynak grubundan bir şablon oluştur.

cmdlet aşağıdaki hello bir depolama hesabı oluşturur. Merhaba örnekte gösterilen hello adını kullanmak yerine, hello depolama hesabı için benzersiz bir ad sağlayın. Merhaba adı uzunluğu 3 ile 24 karakter arasında olmalı ve yalnızca rakamlar ve küçük harfler kullanın. Merhaba örnekte gösterilen hello adı kullanırsanız, bu ad zaten kullanımda olduğundan, bir hata alırsınız.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Bu kaynak daha sonra tooretrieve gerekirse cmdlet'i aşağıdaki hello kullanın:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Etiket ekleme

Etiketler toodifferent özellikleri göre kaynaklarınızı tooorganize etkinleştirin. Örneğin, bazı kaynaklar toohello ait farklı kaynak gruplarında olabilir aynı bölüm. Bir bölüm etiketi ve değer toothose kaynakları toomark uygulayabilirsiniz ait toohello olarak bunları aynı kategori. Veya, bir kaynak bir üretim veya test ortamında kullanılıp kullanılmadığını işaretleyebilirsiniz. Bu konuda etiketleri tooonly bir kaynak geçerli, ancak ortamınızda büyük olasılıkla tooapply tooall kaynaklarınıza etiketler mantıklıdır.

cmdlet aşağıdaki hello iki etiketleri tooyour depolama hesabı geçerlidir:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Etiketler tek bir nesne olarak güncelleştirilir. tooadd zaten etiketlerini içeren bir etiket tooa kaynak ilk hello varolan etiketleri alın. Merhaba varolan etiketleri içeren hello yeni etiket toohello nesne ekleyin ve tüm hello etiketleri toohello kaynak yeniden uygulayın.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Kaynakları Ara

Kullanım hello **Bul AzureRmResource** farklı arama koşulu için cmdlet tooretrieve kaynaklar.

* tooget adıyla bir kaynak sağlayın hello **ResourceNameContains** parametre:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget bir kaynak grubundaki tüm hello kaynaklar sağlar hello **ResourceGroupNameContains** parametre:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget bir etiket adı ve değeri, tüm hello kaynaklarla sağlamak hello **TagName** ve **TagValue** Parametreler:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* belirli bir kaynak türü, tooall hello kaynaklarla sağlamak hello **ResourceType** parametre:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Bir kaynak Kilitle

Kritik bir kaynak yanlışlıkla silinmiş veya değiştirilmiş emin toomake gerektiğinde, bir kilit toohello kaynak uygulayın. Ya da belirtebilirsiniz bir **CanNotDelete** veya **salt okunur**.

Yönetim kilit toocreate ya da delete gerekir erişiminiz çok`Microsoft.Authorization/*` veya `Microsoft.Authorization/locks/*` eylemler. Merhaba yerleşik rolleri, bu eylemleri yalnızca sahip ve kullanıcı erişimi Yöneticisi verilir.

tooapply bir kilit hello aşağıdaki cmdlet'i kullanın:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Merhaba kilit kaldırılana kadar hello örnek önceki hello kilitli kaynak silinemiyor. tooremove bir kilit kullanın:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Ayar kilitleri hakkında daha fazla bilgi için bkz: [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Kaynakları veya kaynak grubunu Kaldır
Bir kaynak veya kaynak grubu kaldırabilirsiniz. Bir kaynak grubu kaldırdığınızda, bu kaynak grubu içindeki tüm hello kaynaklar da kaldırın.

* toodelete hello kaynak grubu, kullanım hello kaynaktan **Kaldır AzureRmResource** cmdlet'i. Bu cmdlet hello kaynak siler, ancak hello kaynak grubu silmez.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete bir kaynak grubu ve kendi kaynaklarını kullanmak hello **Remove-AzureRmResourceGroup** cmdlet'i.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Her iki cmdlet'leri için tooconfirm sorulur tooremove hello kaynağı veya kaynak grubunu istiyor. Merhaba işlemi başarılı bir şekilde hello kaynağı veya kaynak grubunu silip silmediğini, döndürür **doğru**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Azure Automation ile Kaynak Yöneticisi komut dosyalarını çalıştır

Bu konu, nasıl gösterir tooperform temel işlemleri kaynaklarınız Azure PowerShell ile. Daha gelişmiş yönetim senaryoları için genellikle toocreate bir komut dosyası istediğiniz ve komut dosyaları gerektiğinde veya bir zamanlamaya göre yeniden kullanabilirsiniz. [Azure Otomasyonu](../automation/automation-intro.md) Azure çözümleri yönetmek sık kullanılan tooautomate betikleri sizin için bir yol sağlar.

Merhaba aşağıdaki konular, nasıl toouse Azure Otomasyonu, Resource Manager ve PowerShell tooeffectively yönetim görevlerini gerçekleştirme gösterir:

- Bir runbook oluşturma hakkında daha fazla bilgi için bkz: [ilk PowerShell runbook'um](../automation/automation-first-runbook-textual-powershell.md).
- Komut dosyaları galerileri ile çalışma hakkında daha fazla bilgi için bkz [Azure Otomasyonu Runbook ve modül galerileri](../automation/automation-runbook-gallery.md).
- Başlatma ve durdurma sanal makineleri runbook'lar için bkz: [Azure otomasyonu senaryosu: kullanarak JSON biçimli etiketler toocreate Azure VM başlatma ve kapatma için bir zamanlama](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Başlatma ve durdurma sanal makineleri yoğun olmayan saatlerde runbook'lar için bkz: [Başlat/Durdur VM'ler Otomasyon yoğun olmayan saatlerde çözümde sırasında](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Sonraki adımlar
* Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* Şablonlar, dağıtımı hakkında toolearn bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).
* Mevcut kaynaklar tooa yeni kaynak grubu taşıyabilirsiniz. Örnekler için bkz: [kaynakları taşıma tooNew kaynak grubu veya abonelik](resource-group-move-resources.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

