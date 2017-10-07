---
title: "Azure mantıksal uygulamaları için aaaCreate dağıtım şablonları | Microsoft Docs"
description: "Dağıtım ve yayın Yönetimi mantıksal uygulamaları için Azure Resource Manager şablonları oluşturma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Dağıtım ve yayın Yönetimi logic apps için şablonlar oluşturma

Bir mantıksal uygulama oluşturulduktan sonra toocreate isteyebilirsiniz bir Azure Resource Manager şablonu olarak.
Bu şekilde hello mantığı uygulama tooany ortamı veya kaynak grubu nerede gereksinim duyabileceğiniz kolayca dağıtabilirsiniz.
Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) ve [dağıtma kaynakları Azure Resource Manager şablonları kullanarak](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Mantıksal uygulama dağıtım şablonu

Bir mantıksal uygulama üç temel bileşeni vardır:

* **Mantıksal uygulama kaynağı**: fiyatlandırma planı, konum ve hello iş akışı tanımı gibi şeyler hakkında bilgiler içerir.
* **İş akışı tanımı**: mantığı uygulamanızın iş akışı adımları ve hello Logic Apps altyapısı hello iş akışı nasıl yürütülecek açıklar.
Bu tanım mantığı uygulamanızın içinde görüntüleyebilirsiniz **kod görünümü** penceresi.
Merhaba mantığı uygulama kaynağında hello bu tanımı bulabilirsiniz `definition` özelliği.
* **Bağlantıları**: güvenli bir bağlantı dizesi ve bir erişim belirteci gibi herhangi bir bağlayıcı bağlantısı ilgili meta verileri depolama tooseparate kaynaklara başvuruyor.
Merhaba mantığı uygulama kaynağında mantıksal uygulamanızı hello bu kaynaklara başvuran `parameters` bölümü.

Mevcut mantıksal uygulamaları bu tüm parçaları gibi bir araç kullanarak görüntüleyebileceğiniz [Azure kaynak Gezgini](http://resources.azure.com).

toomake bir şablonu kaynak grubu dağıtımı ile bir mantıksal uygulama toouse için hello kaynakları tanımlamak ve gerekir gerektiğinde Parametreleştirme.
Örneğin, tooa geliştirme, test ve üretim ortamı dağıtıyorsanız, büyük olasılıkla toouse farklı bağlantı dizeleri tooa SQL veritabanı her ortamda istiyorsunuz.
Ya da farklı Aboneliklerde veya kaynak grupları içindeki toodeploy isteyebilirsiniz.  

## <a name="create-a-logic-app-deployment-template"></a>Bir mantıksal uygulama dağıtım şablonu oluşturma

Merhaba en kolay yolu toohave geçerli mantığı uygulama dağıtım şablonu olan toouse [mantıksal uygulamalar için Visual Studio Araçları](logic-apps-deploy-from-vs.md).
Merhaba Visual Studio Araçları herhangi bir abonelik veya konum arasında kullanılan bir geçerli dağıtım şablonu oluşturun.

Bir mantıksal uygulama dağıtım şablonu oluşturma gibi diğer bazı araçları size yardımcı olabilir.
El ile yazabilirsiniz, diğer bir deyişle, hello kullanarak kaynakları zaten burada toocreate parametrelerini gerektiği gibi ele.
Başka bir seçenektir toouse bir [mantıksal uygulama şablonu oluşturan](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell modülü. Bu açık kaynaklı modül önce hello mantıksal uygulama ve onu kullanıyor ve dağıtımı için gerekli parametreleri hello şablon kaynaklarla oluşturur herhangi bir bağlantısı değerlendirir.
Örneğin, bir Azure hizmet veri yolu kuyruktan bir ileti alır ve verileri tooan Azure SQL veritabanı ekleyen bir mantıksal uygulama varsa, hello aracı tüm hello orchestration mantığı korur ve ayarlanabilir böylece hello SQL ve hizmet veri yolu bağlantı dizeleri parameterizes dağıtım sırasında.

> [!NOTE]
> Bağlantıları hello içinde olmalıdır hello mantıksal uygulama ile aynı kaynak grubunda.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Merhaba mantıksal uygulama şablonu PowerShell modülünü yükleyin
Merhaba en kolay yolu tooinstall hello modülüdür hello [PowerShell Galerisi](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), hello komutunu kullanarak `Install-Module -Name LogicAppTemplate`.  

Merhaba PowerShell modülünü el ile de yükleyebilirsiniz:

1. Merhaba hello en son sürümü karşıdan [mantıksal uygulama şablonu oluşturan](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. PowerShell modülü klasörünüzdeki Hello klasörüne ayıklayın (genellikle `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Merhaba modülü toowork Kiracı ve abonelik erişimi için belirteç ile Merhaba kullanmanızı öneririz [ARMClient](https://github.com/projectkudu/ARMClient) komut satırı aracı.  Bu [blog gönderisi](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) ARMClient daha ayrıntılı olarak anlatılmaktadır.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>PowerShell kullanarak bir mantıksal uygulama şablonu oluştur
PowerShell yüklendikten sonra komutu aşağıdaki hello kullanarak bir şablon oluşturabilirsiniz:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`Hello Azure abonelik kimliği Bu satırı önce bir erişim ARMClient belirtecini alır sonra toohello PowerShell komut dosyası Kanallar ve ardından hello şablonu bir JSON dosyası oluşturur.

## <a name="add-parameters-tooa-logic-app-template"></a>Parametreleri tooa mantıksal uygulama şablonu Ekle
Mantıksal uygulama şablonu oluşturduktan sonra tooadd devam edebilir veya gereksinim duyabileceğiniz parametreleri değiştirin. Örneğin, bir kaynak kimliği tooan Azure işlevi veya iç içe geçmiş iş akışı tek bir dağıtımda toodeploy planlama tanımınızı içeriyorsa, daha fazla kaynakları tooyour şablon ekleyip gerektiğinde kimlikleri Parametreleştirme. Merhaba aynı her kaynak grubu ile toodeploy beklediğiniz tooany başvuruları toocustom API'leri veya Swagger uç noktalar uygular.

## <a name="deploy-a-logic-app-template"></a>Bir mantıksal uygulama şablonu dağıtma

PowerShell, REST API gibi herhangi bir aracı kullanarak şablonunuzu dağıtabilirsiniz [Visual Studio Team Services yayın Yönetimi](#team-services)ve hello Azure portal aracılığıyla şablon dağıtımı.
Ayrıca, parametrelerin toostore hello değerleri, oluşturduğunuz öneririz bir [parametre dosyası](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Nasıl çok öğrenin[PowerShell ve Azure Resource Manager şablonları kaynaklarla dağıtmak](../azure-resource-manager/resource-group-template-deploy.md) veya [kaynakları Azure Resource Manager şablonları ile dağıtma ve Azure portal hello](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>OAuth bağlantılarını yetkilendirmek

Dağıtımdan sonra hello mantıksal uygulama baştan sona geçerli parametrelerle birlikte çalışır.
Ancak, OAuth bağlantıları toogenerate geçerli erişim belirteci hala yetkilendirmeniz gerekir.
tooauthorize OAuth bağlantıları hello mantıksal uygulama hello Logic Apps Tasarımcısı açın ve bu bağlantıları yetkilendirin. Veya otomatik dağıtım için bir komut dosyası tooconsent tooeach OAuth bağlantı kullanabilirsiniz.
Github'da altında bir örnek komut dosyası yok [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) projesi.

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services yayın Yönetimi

Toouse bir mantıksal uygulama dağıtım şablonu ile Visual Studio Team Services, yayın yönetimi gibi bir araç dağıtma ve bir ortam yönetmek için ortak bir senaryodur. Visual Studio Team Services içeren bir [Azure kaynak grubu dağıtma](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) tooany derleme ekleyin veya yayın ardışık düzen görev. Toohave gereken bir [hizmet sorumlusu](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) yetkilendirme için toodeploy ve ardından hello yayın tanımı oluşturabilirsiniz.

1. Yayın yönetimini seçin **boş** böylece boş bir tanımı oluşturun.

    ![Boş tanımı oluşturun][1]

2. Derleme işlemi el ile veya hello parçası olarak oluşturulan bu, büyük olasılıkla dahil olmak üzere hello mantıksal uygulama şablonu için gereksinim duyduğunuz tüm kaynakları seçin.
3. Ekleme bir **Azure kaynak grubu dağıtımı** görev.
4. İle yapılandırma bir [hizmet sorumlusu](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)ve hello şablonu ve şablon parametreleri dosyalarını başvuru.
5. Adımlar toobuild hello yayın işlem başka bir ortam, otomatikleştirilmiş test veya gerektiğinde onaylayanlar için devam edin.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
