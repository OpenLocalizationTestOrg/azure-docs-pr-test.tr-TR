---
title: "aaaExport Azure Resource Manager şablonu | Microsoft Docs"
description: "Azure Resource Manager tooexport var olan bir kaynak grubundan bir şablon kullanın."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma
Bu makalede, bilgi nasıl tooexport, aboneliğinizdeki mevcut kaynaklardan bir Resource Manager şablonu. Bu oluşturulan şablonu toogain şablon söz dizimi daha iyi anlamasına kullanabilirsiniz.

Bir şablon iki yolu tooexport vardır:

* Merhaba verebilirsiniz **dağıtımı için kullanılan gerçek şablonu**. Merhaba özgün şablonda tam olarak göründüğü gibi hello dışarı aktarılan şablonu tüm hello parametreler ve değişkenler içerir. Bu yaklaşım hello portalı üzerinden kaynaklarına dağıtıldığında yardımcı olur ve bu kaynakları toosee hello şablonu toocreate istiyorsunuz. Bu şablon kullanıma hazırdır. 
* Dışa aktarabilirsiniz bir **hello hello kaynak grubunun geçerli durumunu temsil eden şablon oluşturdu**. Merhaba dışarı aktarılan şablon dağıtımı için kullanılan herhangi bir şablonu dayanmıyor. Bunun yerine, hello kaynak grubunun bir anlık görüntüdür bir şablon oluşturur. Merhaba dışarı aktarılan şablon birçok sabit kodlu değer ve normalde tanımlayacağınız kadar fazla büyük olasılıkla parametre vardır. Bu yaklaşım, dağıtımdan sonra hello kaynak grubu değiştirdiniz. yararlıdır. Genellikle bu şablonun kullanılabilir olması için önce değişiklikler yapılması gerekir.

Bu konu, her iki yaklaşımın hello portal üzerinden gösterir.

## <a name="deploy-resources"></a>Kaynakları dağıtma
Bir şablon olarak dışarı aktarmak için kullanabileceğiniz kaynakları tooAzure dağıtarak başlayalım. Aboneliğinizi tooexport tooa şablonu istediğiniz bir kaynak grubu zaten varsa, bu bölümü atlayabilirsiniz. Bu makalenin sonraki bölümlerinde Hello hello web uygulaması ve SQL veritabanı çözümü bu bölümde gösterilen dağıttığınız varsayar. Farklı bir çözüme kullanırsanız, deneyiminizi biraz farklı olabilir, ancak aynı tooexport şablon olan hello adımları hello. 

1. Merhaba, [Azure portal](https://portal.azure.com)seçin **yeni**.
   
      ![yeni’yi seçin](./media/resource-manager-export-template/new.png)
2. Arama **web uygulaması + SQL** ve hello kullanılabilir seçeneklerden birini belirleyin.
   
      ![web uygulaması ve SQL’i arayın](./media/resource-manager-export-template/webapp-sql.png)

3. **Oluştur**’u seçin.

      ![oluştur’u seçin](./media/resource-manager-export-template/create.png)

4. Merhaba web uygulaması ve SQL veritabanı için hello gerekli değerleri girin. **Oluştur**’u seçin.

      ![web ve SQL değerini sağlayın](./media/resource-manager-export-template/provide-web-values.png)

Merhaba dağıtım bir dakika sürebilir. Merhaba dağıtım tamamlandıktan sonra aboneliğiniz hello çözüm içerir.

## <a name="view-template-from-deployment-history"></a>Dağıtım geçmişinden şablonu görüntüleme
1. Yeni kaynak grubunuz için toohello kaynak grubu dikey penceresine gidin. Bu hello dikey penceresinde hello son dağıtım hello sonucunu gösterir dikkat edin. Bu bağlantıyı seçin.
   
      ![kaynak grubu dikey penceresi](./media/resource-manager-export-template/select-deployment.png)
2. Merhaba grubu için dağıtım geçmişini görürsünüz. Sizin durumunuzda hello dikey büyük olasılıkla yalnızca bir dağıtım listeler. Bu dağıtımı seçin.
   
     ![son dağıtım](./media/resource-manager-export-template/select-history.png)
3. Merhaba dikey penceresinde hello dağıtım özetini görüntüler. Merhaba Özet hello hello dağıtımının durumunu ve işlemlerini ve parametreleri için sağlanan hello değerleri içerir. Merhaba dağıtımda, select kullanılan toosee hello şablonu **şablonu görüntüleme**.
   
     ![dağıtım özetini görüntüleme](./media/resource-manager-export-template/view-template.png)
4. Kaynak Yöneticisi, sizin için aşağıdaki yedi dosyaları hello alır:
   
   1. **Şablon** -Merhaba, çözümünüz için altyapıyı tanımlayan hello şablonu. Merhaba hello portal üzerinden depolama hesabı oluşturduğunuzda, Resource Manager şablonu toodeploy kullanılan onu ve bu şablonu gelecekte başvurmak üzere kaydetti.
   2. **Parametreleri** -bir parametre dosyası toopass dağıtım sırasında değerleri kullanabilirsiniz. Merhaba ilk dağıtım sırasında sağlanan Başlangıç değerlerini içerir. Merhaba şablonu yeniden dağıtırken bu değerleri değiştirebilirsiniz.
   3. **CLI** -bir Azure komut satırı arabirimi (CLI) betik dosyası toodeploy hello şablonu kullanabilirsiniz.
   3. **CLI 2.0** -bir Azure komut satırı arabirimi (CLI) betik dosyası toodeploy hello şablonu kullanabilirsiniz.
   4. **PowerShell** -bir Azure PowerShell komut dosyası toodeploy hello şablonu kullanabilirsiniz.
   5. **.NET** -toodeploy hello şablon kullanabileceğiniz bir .NET sınıfı.
   6. **Ruby** -A Ruby sınıfı toodeploy hello şablonu kullanabilirsiniz.
      
      Merhaba dosyaları hello dikey pencerelerdeki bağlantılar aracılığıyla ulaşılabilir. Varsayılan olarak, hello dikey penceresinde hello şablonunu görüntüler.
      
       ![şablonu görüntüleme](./media/resource-manager-export-template/see-template.png)
      
Bu şablon hello gerçek şablonu toocreate web uygulaması ve SQL database kullanılır. Dağıtım sırasında tooprovide farklı değerleri etkinleştir parametreleri içeren dikkat edin. bir şablonun hello yapısı hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Merhaba şablonu kaynak grubundan dışarı aktarma
El ile kaynaklarınızı değiştirmiş veya birden çok dağıtımlarda kaynakları eklenen, bir şablon hello dağıtım geçmişini alma hello hello kaynak grubunun geçerli durumunu yansıtmaz. Bu bölümde, nasıl tooexport yansıtan bir şablon hello hello kaynak grubunun geçerli durumunu gösterir. 

> [!NOTE]
> 200’den fazla kaynağı olan bir kaynak grubu için bir şablonu dışarı aktaramazsınız.
> 
> 

1. tooview hello şablonu seçin, kaynak grubu için **Otomasyon betiğini**.
   
      ![kaynak grubunu dışarı aktarma](./media/resource-manager-export-template/select-automation.png)
   
     Resource Manager hello kaynak grubunda hello kaynakları değerlendirir ve bu kaynakları için bir şablon oluşturur. Merhaba şablonu dışarı aktarma işlevini tüm kaynak türleri desteklemez. Merhaba dışarı aktarma ile ilgili bir sorun olduğunu bildiren bir hata görebilirsiniz. Toohandle olanlar nasıl sorunları içinde bilgi hello [dışarı aktarma sorunlarını düzeltme](#fix-export-issues) bölümü.
2. Yeniden tooredeploy hello çözüm kullanabilir hello altı dosyalarına bakın. Ancak, bu zaman hello şablon biraz farklıdır. Oluşturulan şablon hello bildirimi önceki bölümdeki hello şablon sayısından daha az parametre içeriyor. Ayrıca, bu şablon yerine bir parametre değeri kabul sabit kodlanmış birçok hello değerleri (örneğin, konum ve SKU değerleri). Bu şablonu yeniden kullanmadan önce tooedit hello şablonu toomake daha iyi kullanılmasını parametrelerini isteyebilirsiniz. 
   
3. Bir birkaç toowork bu şablonla devam etmek seçeneğiniz vardır. Merhaba şablonunu indirebilir ve üzerinde yerel olarak bir JSON Düzenleyicisi ile çalışır. Veya hello şablon tooyour kitaplığı kaydedin ve hello Portalı aracılığıyla üzerinde çalışır.
   
     Gibi bir JSON düzenleyicisi kullanarak kullanabiliyorsanız [VS Code](https://code.visualstudio.com/) veya [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), yerel olarak hello şablonu indirme ve o düzenleyicisini kullanarak tercih edebilirsiniz. toowork yerel olarak select **karşıdan**.
   
      ![şablonu indirme](./media/resource-manager-export-template/download-template.png)
   
     Bir JSON düzenleyicisiyle ayarlanmayan, hello şablon hello portal üzerinden düzenlemeyi tercih edebilirsiniz. Bu konuda Hello kalanı hello Portalı'nda hello şablon tooyour kitaplığı kaydettiğiniz varsayar. Ancak, aynı hello yaptığınız sözdizimi değişip toohello şablonu hello portal aracılığıyla veya JSON Düzenleyicisi ile yerel olarak çalışma. Merhaba portal üzerinden toowork seçin **toolibrary eklemek**.
   
      ![toolibrary Ekle](./media/resource-manager-export-template/add-to-library.png)
   
     Bir şablon toohello kitaplığı eklerken hello şablonuna bir ad ve açıklama verin. Ardından **Kaydet**’i seçin.
   
     ![şablon değerlerini ayarlama](./media/resource-manager-export-template/save-library-template.png)
4. tooview kitaplığınızda, kaydedilen bir şablon seçin **daha fazla hizmet**, türü **şablonları** toofilter sonuçları, select **şablonları**.
   
      ![şablonları bulma](./media/resource-manager-export-template/find-templates.png)
5. Kaydettiğiniz hello adla Hello şablonu seçin.
   
      ![şablon seçme](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Merhaba şablonunu özelleştirme
toocreate hello istiyorsanız, uygulama ve SQL veritabanı her dağıtım için aynı web ince dışarı hello şablon çalışır. Bununla birlikte Resource Manager, şablonları çok daha fazla esneklikle dağıtabileceğiniz seçenekler sunar. Bu makale size nasıl veritabanı yönetici adı ve parola hello tooadd parametrelerini gösterir. Merhaba şablonundaki diğer değerler için daha fazla esneklik aynı bu yaklaşım tooadd kullanabilirsiniz.

1. toocustomize hello şablonu, select **Düzenle**.
   
     ![şablonu gösterme](./media/resource-manager-export-template/select-edit.png)
2. Merhaba şablonu seçin.
   
     ![şablonu düzenleme](./media/resource-manager-export-template/select-added-template.png)
3. toobe mümkün toopass hello değerleri dağıtımı sırasında toospecify isteyebilirsiniz ekleyin iki parametreleri toohello aşağıdaki hello **parametreleri** hello şablonu bölümünde:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse hello yeni parametreleri değiştirin hello SQL server hello tanımında **kaynakları** bölümü. Şimdi **administratorLogin** ve **administratorLoginPassword** için parametre değerlerinin kullanıldığına dikkat edin.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Seçin **Tamam** düzenleme hello şablon bittiğinde.
7. Seçin **kaydetmek** toosave hello değişiklikleri toohello şablonu.
   
     ![şablonu kaydetme](./media/resource-manager-export-template/save-template.png)
8. tooredeploy güncelleştirilmiş hello şablonu, select **dağıtma**.
   
     ![şablonu dağıtma](./media/resource-manager-export-template/redeploy-template.png)
9. Parametre değerlerini sağlayın ve bir kaynak grubu toodeploy hello kaynakları seçin.


## <a name="fix-export-issues"></a>Dışarı aktarma sorunlarını düzeltme
Merhaba şablonu dışarı aktarma işlevini tüm kaynak türleri desteklemez. el ile bu sorunu tooresolve hello eksik kaynakları şablonunuza ekleyin. Merhaba hata iletisi verilemez hello kaynak türleri içerir. Bu kaynak türünü [Şablon başvurusunda](/azure/templates/) bulun. Örneğin, toomanually bir sanal ağ geçidi eklemek için bkz: [Microsoft.Network/virtualNetworkGateways şablon başvurusu](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Yalnızca, dağıtım geçmişiniz yerine bir kaynak grubundan dışarı aktarma yaparken dışarı aktarma sorunlarıyla karşılaşırsınız. Son dağıtımınız hello hello kaynak grubunun geçerli durumunu doğru şekilde temsil ediyorsa hello şablon hello dağıtım geçmişi engellemeniz hello kaynak grubu vermeniz gerekir. Yalnızca tek bir şablonda tanımlı değil toohello kaynak grubu değişiklikler yaptığınızda kaynak grubundan dışarı aktarın.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Öğrendiğiniz nasıl tooexport hello portalda oluşturduğunuz kaynaklardan bir şablonu.

* Bir şablonu [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) veya [REST API](resource-group-template-deploy-rest.md) aracılığıyla dağıtabilirsiniz.
* tooexport bir şablonu PowerShell aracılığıyla nasıl görürüm toosee [Azure PowerShell kullanarak Azure Resource Manager ile](powershell-azure-resource-manager.md).
* tooexport bir şablonu Azure CLI aracılığıyla nasıl görürüm toosee [kullanım hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](xplat-cli-azure-resource-manager.md).

