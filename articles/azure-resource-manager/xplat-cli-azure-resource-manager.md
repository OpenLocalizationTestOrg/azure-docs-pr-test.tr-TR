---
title: hello Azure CLI aaaManage kaynaklarla | Microsoft Docs
description: "Hello Azure komut satırı arabirimi (CLI) toomanage Azure kullanan kaynak ve grupları"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

Hello Azure komut satırı arabirimi (Azure CLI) olan bir çeşitli araçlar toodeploy kullanma ve Kaynak Yöneticisi ile kaynakları yönetme. Bu makale ortak yolları toomanage Azure sunar kaynaklarını ve kaynak gruplarını kullanarak hello Azure CLI Kaynak Yöneticisi modunda. Merhaba CLI toodeploy kaynakları kullanma hakkında daha fazla bilgi için bkz: [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](resource-group-template-deploy-cli.md). Azure kaynakları ve Kaynak Yöneticisi hakkında arka plan için hello ziyaret [Azure Resource Manager'a genel bakış](resource-group-overview.md).

> [!NOTE]
> toomanage Azure kaynakları hello Azure CLI ile ihtiyacınız çok[hello Azure CLI yükleme](../cli-install-nodejs.md), ve [tooAzure içinde oturum](../xplat-cli-connect.md) hello kullanarak `azure login` komutu. CLI Kaynak Yöneticisi modunda olduğundan emin olun hello (çalıştırmak `azure config mode arm`). Bunlardan yaptıysanız, hazır toogo demektir.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Kaynak grupları ve kaynakları alma
### <a name="resource-groups"></a>Kaynak grupları
tooget aboneliğinizi ve konumlarına, tüm kaynak gruplarının bir listesini bu komutu çalıştırın.

    azure group list


### <a name="resources"></a>Kaynaklar
 toolist biriyle gibi bir gruptaki tüm kaynakların ad *testRG*, komutu aşağıdaki hello kullanın:

    azure resource list testRG

tooview adlı bir VM'den gibi hello grup içindeki tek bir kaynağın *MyUbuntuVM*, hello aşağıdaki gibi bir komutu kullanın:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Bildirim hello **Microsoft.Compute/virtualMachines** parametresi. Bu parametre hakkında bilgi isteyen hello kaynak hello türünü gösterir.

> [!NOTE]
> Merhaba kullanırken **azure kaynak** komutları hello dışında **listesi** komutu ile Merhaba hello kaynak hello API sürümü belirtmelidir **-o** parametresi. Hello API sürümü hakkında emin değilseniz, hello şablon dosyası başvurun ve hello kaynak için hello apiVersion alanını bulun. Kaynak Yöneticisi'nde API sürümleri hakkında daha fazla bilgi için bkz: [kaynak sağlayıcıları ve türleri](resource-manager-supported-services.md).
> 
> 

Ayrıntıları bir kaynakta görüntülerken, yararlı toouse hello genellikle olduğu `--json` parametresi. İç içe geçmiş yapılar veya koleksiyonlar bazı değerler olduğu için bu parametreyi hello çıktı daha okunabilir hale getirir. Merhaba aşağıdaki örnekte gösterilmiştir hello döndürmeyi hello sonuçlarını **Göster** JSON belgesi olarak komutu.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Hello JSON veri toofile'hello kullanarak kaydetmek istiyorsanız &gt; karakter toodirect hello çıktı tooa dosyası. Örneğin:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Etiketler
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Kaynakları yönetme
tooadd bir depolama hesabı tooa kaynak grubu gibi bir kaynak için benzer bir komutu çalıştırın:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Ayrıca toospecifying hello hello kaynak API sürümü ile Merhaba **-o** parametresi, kullanım hello **-p** gerekli parametre toopass JSON biçimli dize veya ek özellikler.

bir sanal makine kaynağı gibi mevcut bir kaynağı toodelete hello aşağıdaki gibi bir komutu kullanın:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove varolan kaynakları tooanother kaynak grubuna veya aboneliğe hello kullanın, **azure kaynak taşıma** komutu. örnekte gösterildiği nasıl aşağıdaki hello toomove Redis önbelleği tooa yeni bir kaynak grubu. Merhaba, **-i** parametresi hello kaynak kimliği'nin toomove virgülle ayrılmış bir listesini sağlayın.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Denetim erişim tooresources
Hello Azure CLI toocreate ve ilkeleri toocontrol erişim tooAzure kaynaklarını yönetmek kullanabilirsiniz. İlke tanımları ve atama ilkelerini tooresources hakkında arka plan için bkz: [İlkesi toomanage kaynakları kullanın ve erişimi denetlemenize](resource-manager-policy.md).

Örneğin, ilke toodeny aşağıdaki hello konumu değil Batı ABD veya Kuzey Orta ABD olduğu tüm istekleri tanımlayın ve toohello ilke tanımı dosyası policy.json kaydedin:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

Merhaba çalıştırmak **ilke tanımı oluşturun** komutu:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Bu komut çıktı benzer toohello şunları gösterir:

    + İlke tanımı MyPolicy veri oluşturma: PolicyName: MyPolicy veri: Policydefinitionıd: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    Veri: PolicyType: özel veri: DisplayName: tanımlanmamış veri: Açıklama: tanımlanmamış veri: PolicyRule: alan konumu =, içinde [westus, northcentralus], = etkisi = Reddet

 bir ilke kapsamında istediğiniz hello kullan hello tooassign **Policydefinitionıd** hello önceki komuttan döndürdü. Aşağıdaki örnek hello, bu kapsamı hello abonelik ancak tooresource grupları veya bireysel kaynakları kapsamını belirleyebilirsiniz:

    Azure ilke ataması oluşturma MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### /

Al, değiştirmek veya ilke tanımları hello kullanarak kaldırmak **ilke tanımı Göster**, **ilke tanım kümesini**, ve **ilke tanımı silin** komutları.

Benzer şekilde, alma, değiştirebilir veya hello kullanarak ilke atamalarını kaldırın **ilke ataması Göster**, **ilke ataması kümesi**, ve **ilke atamasını silin** komutları .

## <a name="export-a-resource-group-as-a-template"></a>Bir kaynak grubunu şablon olarak dışarı aktarma
Mevcut bir kaynak grubu için hello kaynak grubu için hello Resource Manager şablonu görüntüleyebilirsiniz. Dışarı aktarma hello şablon iki avantajları sunar:

1. Tüm hello altyapı hello şablonda tanımlı olduğundan hello çözümün gelecekteki dağıtımlar kolayca otomatik hale getirebilirsiniz.
2. Çözümünüzü temsil eden JSON hello bakarak şablon söz dizimi ile tanıdık.

Hello Azure CLI kullanarak, kaynak grubunuzun hello geçerli durumunu temsil eden bir şablonu dışarı veya belirli bir dağıtım için kullanılan hello şablonunu indirebilir.

* **Bir kaynak grubu için Hello şablonu dışarı aktarma** -değişiklikleri tooa kaynak grubuna yapılan ve tooretrieve geçerli durumuna JSON gösterimi hello olduğunda bu yararlıdır. Ancak, parametre ve değişken, yalnızca en az sayıda hello oluşturulan şablonu içerir. Merhaba değerlerinin hello şablonu sabit kodlanmış durumdadır. Merhaba dağıtım farklı ortamlar için özelleştirebileceğiniz şekilde oluşturulan hello şablonunun dağıtmadan önce tooconvert daha fazla hello değeri parametreleri isteyebilir.
  
    Merhaba çalıştırmak bir kaynak grubu tooa yerel dizin için tooexport hello şablonu `azure group export` hello aşağıdaki örnekte gösterildiği gibi komutu. (İşletim sistemi ortamınız için uygun yerel bir dizine değiştirin.)
  
        azure group export testRG ~/azure/templates/
* **Belirli bir dağıtımın Hello şablonunu indirme** --kullanılan toodeploy kaynaklar tooview hello gerçek şablon gerektiğinde bu faydalıdır. tüm parametreler ve değişkenler hello özgün dağıtım için tanımlanan Hello şablonu içerir. Ancak, birisi, kuruluşunuzda değişiklikleri toohello kaynak grubu hello tanımı dışında hello şablonunda yaptıysanız, bu şablonu hello hello kaynak grubunun geçerli durumunu temsil etmez.
  
    Merhaba çalıştırmak belirli dağıtım tooa yerel bir dizin için kullanılan toodownload hello şablonu `azure group deployment template download` komutu. Örneğin:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Şablonu dışarı aktarma Önizleme aşamasındadır ve tüm kaynak türleri şu anda bir şablonu dışarı aktarma desteklemez. Bir şablon tooexport çalışırken, bazı kaynaklar dışarı aktarılmadığı bildiren bir hata görebilirsiniz. El ile gerekirse, bu kaynakları indirdikten sonra şablonunuzda tanımlayın.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Dağıtım işlemlerini tooget ayrıntılarını ve hello Azure CLI ile dağıtım hatalarını giderme bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
* Bir uygulama veya komut dosyası tooaccess kaynakları toouse hello CLI tooset istiyorsanız, bkz: [kullanım Azure CLI toocreate bir hizmet sorumlusu tooaccess kaynakları](resource-group-authenticate-service-principal-cli.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

