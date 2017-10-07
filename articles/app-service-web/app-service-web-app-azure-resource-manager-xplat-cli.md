---
title: "Azure Web uygulaması için Resource Manager tabanlı platformlar arası komut satırı araçları aaaAzure | Microsoft Docs"
description: "Nasıl toouse hello yeni Azure Resource Manager tabanlı platformlar arası komut satırı araçları toomanage Azure Web Apps hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Azure uygulama hizmeti için Azure Resource Manager tabanlı XPlat CLI kullanma
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Microsoft Azure platformlar arası komut satırı araçları sürüm 0.10.5 Hello sürümle yeni komutları eklenmiştir. Bu komutlar hello kullanıcı hello özelliği toouse Azure Resource Manager tabanlı PowerShell komutları toomanage uygulama hizmeti verin.

Kaynak gruplarını yönetme hakkında toolearn bkz [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Ayrıca, denemenin [Azure CLI 2.0](https://github.com/Azure/azure-cli), yeni nesil CLI hello kaynak yönetimi dağıtım modeli için Python içinde yazılmış.
>
>

## <a name="managing-app-service-plans"></a>Uygulama hizmeti yönetme planları
### <a name="create-an-app-service-plan"></a>Bir uygulama hizmeti planı oluştur
bir uygulama hizmeti planı toocreate hello kullan **azure appserviceplan oluşturma** komutu.

Merhaba farklı parametreler açıklamalarını şunlardır:

* **--kaynak-grubu**: yeni oluşturulan hello uygulama hizmeti planı içeren kaynak grubu.
* **--ad**: hello uygulama hizmeti planının adı.
* **--Konum**: uygulama hizmeti planı konumu.
* **--sku**: hello istenen fiyatlandırma sku (Merhaba Seçenekler şunlardır: F1 (ücretsiz). D1 (paylaşılan). B1 (temel küçük), B2 (temel ortamı) ve B3 (Basic büyük). S1 (standart küçük), S2 (standart ortamı) ve S3 (standart büyük). P1 (Premium küçük), P2 (Premium ortamı) ve P3 (Premium büyük).)
* **--örnekleri**: (varsayılan değer 1'dir) hello uygulama hizmeti planında hello çalışan sayısı.

Örnek toouse Bu cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Linux uygulama hizmeti planı oluştur

Kullanarak, hello aynı **azure appserviceplan oluşturma** hello ile komutu ek parametre **--islinux true**. Not hello kısıtlamaları ve özetlenen bölgeleri [giriş tooApp Linux hizmeti](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Var olan uygulama hizmeti planları listesi
toolist hello var olan uygulama hizmeti planları kullanın **azure appserviceplan listesi** komutu.

toolist belirli kaynak grubundaki tüm uygulama hizmeti planları kullanın:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

tooget belirli uygulama hizmeti planı kullanmak **azure appserviceplan Göster** komutu:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Var olan bir App Service planı Yapılandır
var olan bir uygulama hizmeti planı toochange hello ayarlarını kullan hello **azure appserviceplan config** komutu. Merhaba sku ve çalışan hello sayısı değiştirebilirsiniz 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Bir uygulama hizmeti planı ölçeklendirme
tooscale bir var olan uygulama hizmeti planı, kullanın:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Bir uygulama hizmeti planı SKU'su Hello değiştirme
toochange hello SKU'su bir var olan uygulama hizmeti planı, kullanın:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Var olan bir uygulama hizmeti planı silme
toodelete var olan bir uygulama hizmeti planı, tüm taşınmış veya silinmiş ilk uygulamaları gerek toobe atanır. Hello kullanarak **azure webapp silme** komutu hello uygulama hizmeti planı silebilirsiniz.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Uygulama hizmeti uygulamaları yönetme
### <a name="create-a-web-app"></a>Web uygulaması oluşturma
toocreate bir web uygulaması kullanın hello **azure webapp oluşturmak** komutu.

Merhaba farklı parametreler açıklamalarını şunlardır:

* **--ad**: hello web uygulamasının adı.
* **--planı**: hello hizmet planı toohost hello web uygulaması kullanılan ad.
* **--kaynak-grubu**: hello uygulama hizmeti planı barındıran kaynak grubu.
* **--Konum**: Merhaba web uygulama konumu.

Örnek toouse Bu cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Mevcut bir uygulamayı Sil
Mevcut bir uygulamayı toodelete hello kullanabilir **azure webapp silme** komutu. Toospecify hello hello uygulama adını ve hello kaynak grubu adı gerekiyor.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Var olan uygulamalar listesi
toolist hello mevcut uygulamaları, hello kullanma **azure webapp listesi** komutu.

belirli bir kaynak grubundaki tüm uygulamalar toolist kullanın:

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget belirli bir uygulamayı kullanmak hello **azure webapp Göster** komutu.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Mevcut bir uygulamayı yapılandırma
toochange hello ayarları ve var olan bir uygulama için yapılandırmaları kullanmak hello **azure webapp yapılandırma kümesi** komutu.

(1) örnek: bir uygulamanın hello php sürümünü değiştirme 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

(2) örnek: ekleme veya uygulama ayarlarını değiştirme

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

hangi diğer yapılandırma değiştirilebilir, tooknow kullanım hello **set -h azure webapp config** komutu.

### <a name="change-hello-state-of-an-existing-app"></a>Mevcut bir uygulamayı Hello durumunu değiştir
#### <a name="restart-an-app"></a>Bir uygulamayı yeniden başlatın
toorestart uygulama bir hello uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Bir uygulamayı durdurun
toostop uygulama bir hello uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Bir uygulamayı başlatın
toostart uygulama bir hello uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Uygulama yayımlama profillerini yönet
Her uygulamanın kodunuzu kullanılan toopublish olabilir bir yayımlama profili yok.

#### <a name="get-publishing-profile"></a>Yayımlama profilini Al
Yayımlama profilini bir uygulama kullanmak için tooget hello:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Bu komut, kullanıcı adı ve parola toohello komut satırı profili yayımlama hello görüntülemektedir.

### <a name="manage-app-hostnames"></a>Uygulama ana bilgisayar adlarını yönetme
toomanage konak adı bağlamaları, uygulamanız için kullanmak hello **azure webapp config ana bilgisayar adları** komutu  

#### <a name="list-hostname-bindings"></a>Liste konak adı bağlamaları
bir uygulama tooget hello geçerli konak adı bağlamaları kullanın:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Konak adı bağlamaları Ekle
tooadd konak adı bağlamaları tooan uygulama, kullanın:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Konak adı bağlamaları Sil
toodelete konak adı bağlamaları kullanın:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Sonraki Adımlar
* Azure Resource Manager CLI desteği hakkında toolearn bakın [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* Uygulama hizmeti PowerShell kullanarak yönetme hakkında toolearn bkz [Using Azure Resource Manager-Based PowerShell tooManage Azure Web uygulamaları.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn Linux üzerinde Azure App Service hakkında bkz [giriş tooApp Linux hizmeti](app-service-linux-intro.md)
