---
title: "Kaynak Yöneticisi sağlayıcısı işlemleri aaaAzure | Microsoft Docs"
description: "Merhaba Microsoft Azure Resource Manager kaynak sağlayıcıları kullanılabilir işlemleri ayrıntıları hello"
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Azure Resource Manager kaynak sağlayıcısı işlemleri

Bu belge her Microsoft Azure Resource Manager kaynak sağlayıcısı için kullanılabilir hello işlemleri listeler. Bu özel roller tooprovide ayrıntılı rol tabanlı erişim denetimi (RBAC) izinleri tooresources Azure içinde kullanılabilir. Lütfen bu kapsamlı bir liste değildir ve işlemleri eklenen veya her bir sağlayıcı güncelleştirilmiş kaldırıldıkça unutmayın. İşlemi dizeleri izleyin hello biçimi `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Geçerli ve kapsamlı bir liste için lütfen kullanın `Get-AzureRmProviderOperation` (PowerShell'de) veya `azure provider operations show` (içinde Azure CLI) toolist işlemleri Azure kaynak sağlayıcıları.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| İşlem | Açıklama |
|---|---|
|/ configuration/eylem|Güncelleştirmeler Kiracı yapılandırması.|
|/ services/eylem|Bir hizmet örneği hello Kiracı olarak güncelleştirir.|
|/ configuration/yazma|Bir kiracı yapılandırma oluşturur.|
|/Configuration/Read|Merhaba Kiracı yapılandırması okur.|
|/ services/yazma|Bir hizmet örneği hello Kiracı oluşturur.|
|/Services/Read|Merhaba Kiracı Hello hizmeti örneklerinin okur.|
|/Services/DELETE|Merhaba Kiracı içinde bir hizmet örneği siler.|
|/Services/servicemembers/Action|Bir hizmet üye örneği hello hizmetinde oluşturur.|
|/Services/servicemembers/Read|Merhaba hizmet üye örneği hello hizmetindeki okur.|
|/Services/servicemembers/DELETE|Bir hizmet üye örneği hello hizmetindeki siler.|
|/Services/servicemembers/Alerts/Read|Merhaba uyarılar için bir hizmet üye okur.|
|/Services/Alerts/Read|Bir hizmet için Hello uyarıları okur.|
|/Services/Alerts/Read|Bir hizmet için Hello uyarıları okur.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| İşlem | Açıklama |
|---|---|
|/ generateRecommendations/eylem|Öneriler oluşturur|
|/ suppressions/eylem|/ Suppressions güncelleştirme|
|/ Kayıt/eylem|Merhaba Microsoft Advisor Hello aboneliği kaydeder|
|/generateRecommendations/Read|Önerileri durumuna alır oluştur|
|/Recommendations/Read|Öneriler okur|
|/suppressions/Read|Suppressions alır|
|/suppressions/DELETE|Gizleme siler|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| İşlem | Açıklama |
|---|---|
|/Servers/Read|Merhaba alır hello bilgileri Analysis Server belirtildi.|
|/ sunucuları/yazma|Oluşturur veya güncelleştirir hello belirtilen Analysis Server.|
|/Servers/DELETE|Siler Analysis Server hello.|
|/Servers/suspend/Action|Merhaba Analysis Server askıya alır.|
|/Servers/Resume/Action|Analysis Server hello sürdürür.|
|/ sunucuları/checkNameAvailability<br>/ Eylem|Analysis Server adının geçerli olup olmadığını denetler ve içinde değil kullanın.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| İşlem | Açıklama |
|---|---|
|/ checkNameAvailability/eylem|Hizmet adı kullanılabilir sağladıysanız denetler|
|/ Kayıt/eylem|Microsoft.ApiManagement kaynak sağlayıcısı için abonelik kaydı|
|/ kaydı/eylem|Microsoft.ApiManagement kaynak sağlayıcısı için abonelik kaydı|
|/ service/yazma|API Management hizmeti yeni bir örneğini oluşturma|
|/Service/Read|API Management hizmeti örneği ile ilgili meta verilerini okuma|
|/Service/DELETE|API Management hizmeti örneği Sil|
|/Service/updatehostname/Action|Kurulum, güncelleştirmeniz ya da bir API Management hizmeti için özel etki alanı adlarını kaldırın|
|/Service/uploadcertificate/Action|Bir API Management hizmeti için SSL sertifikasını karşıya yükle|
|/Service/Backup/Action|Yedekleme API Management hizmeti toohello belirtilen kapsayıcıda kullanıcı sağlanan depolama hesabı|
|/Service/Restore/Action|API Management hizmeti bir kullanıcı tarafından sağlanan depolama hesabı belirtilen kapsayıcıda hello geri yükleme|
|/Service/managedeployments/Action|SKU/birimlerini, API Management Hizmet Ekle/Kaldır bölgesel dağıtımları değiştirme|
|/Service/getssotoken/Action|Yönetici olarak API Management hizmet eski portalı içine kullanılan toologin olabilir SSO belirtecini alır|
|/Service/applynetworkconfigurationupdates/Action|Sanal ağ toopick çalışan güncelleştirmeleri hello Microsoft.ApiManagement kaynakları, ağ ayarları güncelleştirildi.|
|/Service/operationresults/Read|Uzun süre çalışan işlemin geçerli durumunu alır|
|/Service/networkStatus/Read|Merhaba ağ erişim kaynakların durumunu alır.|
|/Service/loggers/Read|Günlükçüleri listesini almak veya Günlükçü ayrıntılarını alma|
|/Service/loggers/Write|Yeni Günlükçü ekleme veya güncelleştirme mevcut Günlükçü ayrıntıları|
|/Service/loggers/DELETE|Varolan Günlükçü Kaldır|
|/Service/Users/Read|Kayıtlı kullanıcıların listesini almak veya bir kullanıcı hesabı ayrıntılarını alma|
|/Service/Users/Write|Yeni bir kullanıcı veya varolan bir kullanıcı hesabı ayrıntılarını güncelleştirme kaydetme|
|/Service/Users/DELETE|Kullanıcı hesabını kaldırma|
|/Service/Users/generateSsoUrl/Action|SSO URL oluşturur. Merhaba URL kullanılan tooaccess Yönetici portalı olabilir|
|/Service/Users/Subscriptions/Read|Kullanıcı abonelikleri listesini al|
|/Service/Users/Keys/Read|Kullanıcı anahtarları listesini al|
|/Service/Users/Groups/Read|Kullanıcı gruplarının listesini alma|
|/Service/tenant/operationResults/Read|İşlem sonuçları listesini al veya belirli bir işlemin sonucunu Al|
|/Service/tenant/Policy/Read|Merhaba Kiracı için ilke yapılandırmasını alma|
|/Service/tenant/Policy/Write|Merhaba Kiracı ilke yapılandırmasını ayarlayın|
|/Service/tenant/Policy/DELETE|Merhaba Kiracı için ilke yapılandırmasını kaldırın|
|/Service/tenant/Configuration/Save/Action|Yürütme yapılandırma anlık görüntü toohello belirtilen dalında hello deposu oluşturur|
|/Service/tenant/Configuration/Deploy/Action|Bir dağıtım görev tooapply değişiklikleri hello belirtilen git şube toohello yapılandırmadan veritabanındaki çalıştırır.|
|/Service/tenant/Configuration/Validate/Action|Merhaba belirtilen git şube değişikliklerden doğrular|
|/Service/tenant/Configuration/operationResults/Read|İşlem sonuçları listesini al veya belirli bir işlemin sonucunu Al|
|/Service/tenant/Configuration/syncState/Read|En son git eşitleme durumunu Al|
|/Service/tenant/Access/Read|Kiracı erişmek bilgileri ayrıntıları|
|/Service/tenant/Access/Write|Güncelleştirme Kiracı erişim bilgileri ayrıntıları|
|/Service/tenant/Access/regeneratePrimaryKey/Action|Birincil erişim anahtarını yeniden oluşturma|
|/Service/tenant/Access/regenerateSecondaryKey/Action|İkincil erişim anahtarını yeniden oluşturma|
|/Service/identityProviders/Read|Kimlik sağlayıcısı Get ayrıntıları veya kimlik sağlayıcıları listesini al|
|/Service/identityProviders/Write|Varolan bir kimlik sağlayıcısı'nın yeni bir kimlik sağlayıcısı veya Güncelleştirme ayrıntıları oluşturun|
|/Service/identityProviders/DELETE|Varolan kimlik sağlayıcısı Kaldır|
|/Service/Subscriptions/Read|Ürün Aboneliklerin listesini alın veya ürün aboneliği ayrıntılarını alma|
|/Service/Subscriptions/Write|Varolan bir kullanıcı tooan mevcut ürün abone veya var olan abonelik ayrıntıları güncelleştirin. Bu işlem kullanılan toorenew abonelik olabilir|
|/Service/Subscriptions/DELETE|Aboneliği silin. Bu işlem kullanılan toodelete abonelik olabilir|
|/Service/Subscriptions/regeneratePrimaryKey/Action|Abonelik birincil anahtarını yeniden oluşturma|
|/Service/Subscriptions/regenerateSecondaryKey/Action|Abonelik ikincil anahtarını yeniden oluşturma|
|/Service/backends/Read|Arka uçlarını listesini almak veya arka uç ayrıntılarını alma|
|/Service/backends/Write|Yeni bir arka uç ekleme veya güncelleştirme mevcut arka uç ayrıntıları|
|/Service/backends/DELETE|Varolan arka uç Kaldır|
|/Service/apis/Read|Tüm kayıtlı API veya Get ayrıntılarını API listesini al|
|/Service/apis/Write|Yeni API oluşturma veya güncelleştirme mevcut API ayrıntıları|
|/Service/apis/DELETE|Varolan API Kaldır|
|/Service/apis/Policy/Read|İçin API ilkesi yapılandırma ayrıntılarını alma|
|/Service/apis/Policy/Write|İçin API ilkesi yapılandırma ayrıntılarını ayarlayın|
|/Service/apis/Policy/DELETE|İlke Yapılandırması API öğesinden Kaldır|
|/Service/apis/Operations/Read|Mevcut API işlemleri listesini almak veya API işlemi ayrıntılarını alma|
|/Service/apis/Operations/Write|Yeni API işlemi oluşturma veya güncelleştirme mevcut API işlemi|
|/Service/apis/Operations/DELETE|Varolan API işlemi Kaldır|
|/Service/apis/Operations/Policy/Read|İlke yapılandırma ayrıntılarını alma işlemi için|
|/Service/apis/Operations/Policy/Write|İşlem için ilke yapılandırma ayrıntılarını ayarlayın|
|/Service/apis/Operations/Policy/DELETE|İlke yapılandırma işlemi Kaldır|
|/Service/Products/Read|Ürünlerin listesini al veya ürün ayrıntılarını Al|
|/Service/Products/Write|Yeni ürün oluşturmak veya mevcut ürün ayrıntıları güncelleştir|
|/Service/Products/DELETE|Varolan ürünü kaldırın|
|/Service/Products/Subscriptions/Read|Ürün Aboneliklerin listesini alın|
|/Service/Products/apis/Read|API eklenen tooexisting ürün listesini al|
|/Service/Products/apis/Write|Varolan API tooexisting ürün ekleme|
|/Service/Products/apis/DELETE|Var olan ürün varolan API Kaldır|
|/Service/Products/Policy/Read|Varolan ürünün ilke yapılandırmasını alma|
|/Service/Products/Policy/Write|Varolan bir ürün için ilke yapılandırma kümesi|
|/Service/Products/Policy/DELETE|Var olan ürün ilkesi yapılandırmasını Kaldır|
|/Service/Products/Groups/Read|Ürünle ilişkili Geliştirici gruplarının listesini alma|
|/Service/Products/Groups/Write|Varolan bir geliştirici Grup varolan ürünle ilişkilendirin|
|/Service/Products/Groups/DELETE|Varolan Ürün mevcut Geliştirici grubunun ilişkilendirmesini Sil|
|/Service/openidConnectProviders/Read|Openıd Connect sağlayıcısı Get ayrıntıları veya Openıd Connect sağlayıcıları listesini al|
|/Service/openidConnectProviders/Write|Bağlantı varolan bir Openıd sağlayıcısının yeni bir Openıd Connect sağlayıcısı veya Güncelleştirme ayrıntıları oluşturun|
|/Service/openidConnectProviders/DELETE|Varolan Openıd Connect sağlayıcısını Kaldır|
|/Service/Certificates/Read|Sertifikaların listesini alın veya sertifika ayrıntılarını alma|
|/Service/Certificates/Write|Yeni sertifika Ekle|
|/Service/Certificates/DELETE|Varolan bir sertifikayı Kaldır|
|/Service/Properties/Read|Belirtilen özellik ayrıntılarını alır veya tüm özelliklerinin listesini alır|
|/Service/Properties/Write|Yeni bir özellik oluşturur veya belirtilen özellik için değer güncelleştirir|
|/Service/Properties/DELETE|Özelliği varolan kaldırır|
|/Service/Groups/Read|Grupları veya bir grup alır ayrıntılarını listesini al|
|/Service/Groups/Write|Yeni grubu oluşturmak veya var olan Grup ayrıntılarını güncelleştir|
|/Service/Groups/DELETE|Varolan bir grubu Kaldır|
|/Service/Groups/Users/Read|Grup kullanıcıların listesini al|
|/Service/Groups/Users/Write|Varolan kullanıcı tooexisting grubu Ekle|
|/Service/Groups/Users/DELETE|Varolan bir kullanıcı var olan grubundan Kaldır|
|/Service/authorizationServers/Read|Yetkilendirme sunucularının listesini alın veya yetkilendirme sunucusu ayrıntılarını alma|
|/Service/authorizationServers/Write|Var olan bir yetkilendirme sunucusu Güncelleştirme ayrıntıları veya yeni bir yetkilendirme sunucusu oluşturma|
|/Service/authorizationServers/DELETE|Varolan bir yetkilendirme sunucusu Kaldır|
|/Service/Reports/bySubscription/Read|Abonelik tarafından toplanan rapor alın.|
|/Service/Reports/byRequest/Read|Get istekleri veri raporlama|
|/Service/Reports/byOperation/Read|Rapor işlemleri tarafından toplanan alma|
|/Service/Reports/byGeo/Read|Coğrafi bölgeye göre toplanmış rapor alma|
|/Service/Reports/byUser/Read|Geliştiriciler tarafından toplanan rapor alın.|
|/Service/Reports/byTime/Read|Dönemlere göre toplanmış rapor alma|
|/Service/Reports/byApi/Read|API tarafından toplanan rapor alma|
|/Service/Reports/byProduct/Read|Ürünü tarafından toplanan rapor alın.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| İşlem | Açıklama |
|---|---|
|/ appidentities/okuma|Ağ geçidi hello ile kayıtlı kaynak (web sitesi) döndürür hello.|
|/ appidentities/yazma|Yeni bir uygulama kimliği oluşturur.|
|/ appidentities/Sil|Varolan bir uygulama kimlik siler.|
|/deploymenttemplates/listMetadata/Action|UI hello API uygulaması paket ile ilişkili meta verileri listeler.|
|/deploymenttemplates/Generate/Action|Dağıtım şablonu tooprovision API uygulaması örnekler döndürür.|
|/ ağ geçitleri/okuma|Merhaba ağ geçidi örneği döndürür.|
|/ ağ geçitleri/yazma|Yeni bir ağ geçidi oluşturur veya mevcut kümeyi güncelleştirir.|
|/ ağ geçitleri/Sil|Var olan bir ağ geçidi örneği siler.|
|/Gateways/listLoginUris/Action|Belirteç Deposu doldurur ve OAuth oturum açma URI döndürür.|
|/Gateways/listKeys/Action|Ağ geçidi gizli döndürür.|
|/Gateways/tokens/Write|Merhaba verilen ada sahip yeni bir Zumo belirteci oluşturur.|
|/Gateways/Registrations/Read|Ağ geçidi hello ile kayıtlı kaynak (web sitesi) döndürür hello.|
|/Gateways/Registrations/Write|Bir kaynağı (web sitesi) ağ geçidi hello ile kaydeder.|
|/Gateways/Registrations/DELETE|Merhaba ağ geçidi kaynağı (web sitesi) kaydını siler.|
|/ apiapps/okuma|API uygulaması örneği döndürür hello.|
|/ apiapps/yazma|Yeni bir API uygulaması oluşturur veya mevcut kümeyi güncelleştirir.|
|/ apiapps/Sil|Var olan bir API uygulaması örneğini siler.|
|/apiapps/listStatus/Action|API uygulaması durumu döndürür.|
|/apiapps/listKeys/Action|API uygulaması gizli döndürür.|
|/apiapps/apidefinitions/Read|API uygulamasının API tanımı döndürür.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| İşlem | Açıklama |
|---|---|
|/ elevateAccess/eylem|Arayan hello Kiracı kapsamda kullanıcı erişimi Yöneticisi erişim verir hello|
|/classicAdministrators/Read|Merhaba Yöneticiler hello abonelik için okur.|
|/ classicAdministrators/yazma|Ekleyin veya yönetici tooa abonelik değiştirin.|
|/classicAdministrators/DELETE|Hello Yöneticisi hello abonelikten kaldırır.|
|/Locks/Read|Merhaba alır kilitleri kapsam belirtilmiş.|
|/ kilitleri/yazma|Belirtilen hello kilitleri ekleyin kapsamı.|
|/Locks/DELETE|Merhaba DELETE kilitleri kapsam belirtilmiş.|
|/policyAssignments/Read|İlke ataması hakkında bilgi edinin.|
|/ policyAssignments/yazma|Bir ilke oluşturmak hello atamasının Belirtilen kapsam.|
|/policyAssignments/DELETE|Delete hello ilke atamasının kapsamı belirtilmiş.|
|/Permissions/Read|Merhaba çağıran belirli bir kapsamda sahip olduğu tüm hello izinleri listeler.|
|/roleDefinitions/Read|Rol tanımı hakkında bilgi alın.|
|/ roleDefinitions/yazma|Belirtilen izinlerle ve atanabilir kapsamlarla birlikte özel bir rol tanımı oluşturun veya güncelleştirin.|
|/roleDefinitions/DELETE|Silme hello belirtilen özel rol tanımı.|
|/providerOperations/Read|Tüm kaynak sağlayıcılarına ilişkin işlemleri alın. Bunlar rol tanımlarında kullanılabilir.|
|/policyDefinitions/Read|İlke tanımı hakkında bilgi edinin.|
|/ policyDefinitions/yazma|Bir özel ilke tanımı oluşturun.|
|/policyDefinitions/DELETE|Bir ilke tanımı silin.|
|/roleAssignments/Read|Bir rol ataması hakkında bilgi alın.|
|/ roleAssignments/yazma|Bir rol oluşturmak hello atamasının Belirtilen kapsam.|
|/roleAssignments/DELETE|Delete hello rol atamasının kapsamı belirtilmiş.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| İşlem | Açıklama |
|---|---|
|/automationAccounts/Read|Bir Azure Otomasyonu hesabını alır|
|/ automationAccounts/yazma|Bir Azure Otomasyonu hesabı oluşturur veya güncelleştirir|
|/automationAccounts/DELETE|Bir Azure Otomasyonu hesabını siler|
|/automationAccounts/configurations/readContent/Action|Bir Azure Otomasyonu DSC'SİNİN içeriğini alır|
|/automationAccounts/hybridRunbookWorkerGroups/Read|Karma Runbook çalışanı kaynaklarını okur|
|/automationAccounts/hybridRunbookWorkerGroups/DELETE|Karma Runbook çalışanı kaynaklarını siler|
|/automationAccounts/jobSchedules/Read|Bir Azure Otomasyonu iş zamanlaması alır|
|/automationAccounts/jobSchedules/Write|Bir Azure Otomasyonu iş zamanlaması oluşturur|
|/automationAccounts/jobSchedules/DELETE|Bir Azure Otomasyonu iş zamanlaması silme|
|/automationAccounts/connectionTypes/Read|Bir Azure Otomasyonu bağlantı türü varlığını alır|
|/automationAccounts/connectionTypes/Write|Bir Azure Otomasyonu bağlantı türü varlığı oluşturur|
|/automationAccounts/connectionTypes/DELETE|Bir Azure Otomasyonu bağlantı türü varlığını siler|
|/automationAccounts/Modules/Read|Bir Azure Otomasyonu modülünü alır|
|/automationAccounts/Modules/Write|Oluşturur veya bir Azure Otomasyonu modülü güncelleştirir|
|/automationAccounts/Modules/DELETE|Bir Azure Otomasyonu modülünü siler|
|/automationAccounts/credentials/Read|Bir Azure Otomasyonu kimlik bilgisi varlığı alır|
|/automationAccounts/credentials/Write|Bir Azure Otomasyonu kimlik bilgisi varlığı oluşturur veya güncelleştirir|
|/automationAccounts/credentials/DELETE|Bir Azure Otomasyonu kimlik bilgisi varlığını siler|
|/automationAccounts/Certificates/Read|Bir Azure Otomasyonu sertifika varlığı alır|
|/automationAccounts/Certificates/Write|Bir Azure Otomasyonu sertifika varlığı oluşturur veya güncelleştirir|
|/automationAccounts/Certificates/DELETE|Bir Azure Otomasyonu sertifika varlığını siler|
|/automationAccounts/Schedules/Read|Bir Azure Otomasyonu zamanlama varlığını alır|
|/automationAccounts/Schedules/Write|Bir Azure Otomasyonu zamanlama varlığı oluşturur veya güncelleştirir|
|/automationAccounts/Schedules/DELETE|Bir Azure Otomasyonu zamanlama varlığını siler|
|/automationAccounts/Jobs/Read|Bir Azure Otomasyonu işini alır|
|/automationAccounts/Jobs/Write|Bir Azure Otomasyonu işi oluşturur|
|/automationAccounts/Jobs/Stop/Action|Bir Azure Otomasyonu işini durdurur|
|/automationAccounts/Jobs/suspend/Action|Bir Azure Otomasyonu işini askıya alır|
|/automationAccounts/Jobs/Resume/Action|Bir Azure Otomasyonu işini sürdürür|
|/automationAccounts/Jobs/runbookContent/Action|Merhaba iş yürütme hello aynı anda Hello hello Azure Otomasyonu runbook içeriğini alır|
|/automationAccounts/Jobs/Output/Action|Bir işin Hello çıktısını alır|
|/automationAccounts/Jobs/Read|Bir Azure Otomasyonu işini alır|
|/automationAccounts/Jobs/Write|Bir Azure Otomasyonu işi oluşturur|
|/automationAccounts/Jobs/Stop/Action|Bir Azure Otomasyonu işini durdurur|
|/automationAccounts/Jobs/suspend/Action|Bir Azure Otomasyonu işini askıya alır|
|/automationAccounts/Jobs/Resume/Action|Bir Azure Otomasyonu işini sürdürür|
|/automationAccounts/Jobs/streams/Read|Bir Azure Otomasyonu iş akışını alır|
|/automationAccounts/Connections/Read|Bir Azure Otomasyonu bağlantı varlığı alır|
|/automationAccounts/Connections/Write|Bir Azure Otomasyonu bağlantı varlığı oluşturur veya güncelleştirir|
|/automationAccounts/Connections/DELETE|Bir Azure Otomasyonu bağlantı varlığını siler|
|/automationAccounts/variables/Read|Bir Azure Otomasyonu değişken varlığını okur|
|/automationAccounts/variables/Write|Bir Azure Otomasyonu değişken varlığı oluşturur veya güncelleştirir|
|/automationAccounts/variables/DELETE|Bir Azure Otomasyonu değişken varlığını siler|
|/automationAccounts/runbooks/readContent/Action|Hello bir Azure Otomasyonu runbook içeriğini alır|
|/automationAccounts/runbooks/Read|Bir Azure Otomasyonu runbook'unu alır|
|/automationAccounts/runbooks/Write|Oluşturur veya bir Azure Otomasyonu runbook'u güncelleştirir|
|/automationAccounts/runbooks/DELETE|Bir Azure Otomasyonu runbook'unu siler|
|/automationAccounts/runbooks/Draft/readContent/Action|Hello Azure Otomasyonu runbook taslağının içeriğini alır|
|/automationAccounts/runbooks/Draft/writeContent/Action|Hello bir Azure Otomasyonu runbook taslağının içeriğini oluşturur|
|/automationAccounts/runbooks/Draft/Read|Bir Azure Otomasyonu runbook taslağı alır|
|/automationAccounts/runbooks/Draft/Publish/Action|Bir Azure Otomasyonu runbook taslağı yayımlar|
|/automationAccounts/runbooks/Draft/undoEdit/Action|Düzenlemeleri tooan Azure Otomasyonu runbook taslağı Geri Al|
|/automationAccounts/runbooks/Draft/testJob/Read|Bir Azure Otomasyonu runbook taslağı test işini alır|
|/automationAccounts/runbooks/Draft/testJob/Write|Bir Azure Otomasyonu runbook taslağı test işi oluşturur|
|/automationAccounts/runbooks/Draft/testJob/Stop/Action|Bir Azure Otomasyonu runbook taslağı test işini durdurur|
|/automationAccounts/runbooks/Draft/testJob/suspend/Action|Bir Azure Otomasyonu runbook taslağı test işini askıya alır|
|/automationAccounts/runbooks/Draft/testJob/Resume/Action|Bir Azure Otomasyonu runbook taslağı test işini sürdürür|
|/automationAccounts/webhooks/Read|Bir Azure Otomasyonu Web kancasını okur|
|/automationAccounts/webhooks/Write|Oluşturur veya bir Azure Otomasyonu Web kancası güncelleştirir|
|/automationAccounts/webhooks/DELETE|Bir Azure Otomasyonu Web kancasını siler |
|/automationAccounts/webhooks/generateUri/Action|Bir Azure Otomasyonu Web kancası için URI oluşturur|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Bu sağlayıcı tam bir ARM sağlayıcı ve ARM işlemleri sağlamaz.

## <a name="microsoftbatch"></a>Microsoft.Batch

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello toplu kaynak sağlayıcısı için aboneliği kaydeder ve toplu işlem hesaplarını hello oluşturulmasını sağlar|
|/ batchAccounts/yazma|Yeni bir Batch hesabı oluşturur veya var olan bir toplu işlem hesabını güncelleştirir|
|/batchAccounts/Read|Toplu işlem hesaplarını listeler veya toplu işlem hesabı hello özelliklerini alır|
|/batchAccounts/DELETE|Batch hesabını siler|
|/batchAccounts/listkeys/Action|Bir toplu işlem hesabı için anahtarlar erişim listeleri|
|/batchAccounts/regeneratekeys/Action|Erişim anahtarları bir toplu işlem hesabı için yeniden oluşturur|
|/batchAccounts/syncAutoStorageKeys/Action|Toplu işlem hesabı için yapılandırılmış hello otomatik depolama hesabının erişim anahtarlarını eşitler|
|/batchAccounts/Applications/Read|Uygulamaları listeler veya bir uygulamanın hello özelliklerini alır|
|/batchAccounts/Applications/Write|Yeni bir uygulama oluşturur veya varolan bir uygulamayı güncelleştirir|
|/batchAccounts/Applications/DELETE|Bir uygulamayı siler|
|/batchAccounts/Applications/Versions/Read|Bir uygulama paketi Hello özelliklerini alır|
|/batchAccounts/Applications/Versions/Write|Yeni bir uygulama paketi oluşturur veya var olan uygulama paketini güncelleştirir|
|/batchAccounts/Applications/Versions/Activate/Action|Bir uygulama paketi etkinleştirir|
|/batchAccounts/Applications/Versions/DELETE|Bir uygulama paketini siler|
|/Locations/Quotas/Read|Merhaba alır toplu kotaları hello belirtilen Azure bölgesi aboneliğinizi belirtilen|

## <a name="microsoftbilling"></a>Microsoft.Billing

| İşlem | Açıklama |
|---|---|
|/invoices/Read|Listeleri kullanılabilir faturalar|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| İşlem | Açıklama |
|---|---|
|/ mapApis/okuma|Okuma işlemi|
|/ mapApis/yazma|Yazma işlemi|
|/ mapApis/Sil|Silme işlemi|
|/mapApis/regenerateKey/Action|Başlangıç anahtarı oluşturur|
|/mapApis/listSecrets/Action|Liste hello gizli|
|/mapApis/listSingleSignOnToken/Action|Okuma tek oturum üzerinde Yetkilendirme belirteci için kaynak hello|
|/ Operations/okuma|Merhaba işlemi açıklaması.|

## <a name="microsoftcache"></a>Microsoft.Cache

| İşlem | Açıklama |
|---|---|
|/ checknameavailability/eylem|Yeni bir Redis önbelleği ile kullanmak için bir ad olup olmadığını denetler|
|/ Kayıt/eylem|Merhaba 'Microsoft.Cache' kaynak sağlayıcısı ile bir aboneliği kaydeder|
|/ kaydı/eylem|Bir abonelikle Hello 'Microsoft.Cache' kaynak sağlayıcısı kaydını siler|
|/ redis/yazma|Merhaba Redis Önbelleği'nin ayarlarını ve yapılandırmasını hello Yönetim Portalı'nda değiştirme|
|/redis/Read|Merhaba Redis Önbelleği'nin ayarlarını ve yapılandırmasını hello yönetim portalında görüntüleyin|
|/redis/DELETE|Delete hello tüm Redis önbelleği|
|/redis/listKeys/Action|Görünüm hello hello Yönetim Portalı'nda Redis önbelleği erişim anahtarlarının değerini|
|/redis/regenerateKey/Action|Redis önbelleği erişim anahtarlarının hello Yönetim Portalı'nda Hello değerini değiştirin|
|/redis/import/Action|Birden çok blob'dan belirli bir biçimdeki verileri Redis'e aktar|
|/redis/Export/Action|Redis veri tooprefixed depolama BLOB'lar belirtilen biçiminde dışarı aktarma|
|/redis/forceReboot/Action|Veri kaybı olasılığı olan bir önbellek örneği yeniden başlatmayı zorlayın.|
|/redis/Stop/Action|Bir önbellek örneği durdurun.|
|/redis/Start/Action|Bir önbellek örneği başlatın.|
|/redis/metricDefinitions/Read|Redis önbelleği için Hello kullanılabilir ölçümleri alır|
|/redis/firewallRules/Read|Merhaba IP güvenlik duvarı kuralları bir Redis önbelleği Al|
|/redis/firewallRules/Write|Merhaba IP güvenlik duvarı kuralları bir Redis önbelleği Düzenle|
|/redis/firewallRules/DELETE|IP güvenlik duvarı kuralları bir Redis önbelleği Sil|
|/redis/listUpgradeNotifications/Read|Liste hello önbellek kiracısı için en son yükseltme bildirimlerini hello.|
|/redis/linkedservers/Read|Bağlantılı bir redis önbelleği ile ilişkilendirilen sunucular alın.|
|/redis/linkedservers/Write|Bağlantılı sunucu tooa Redis önbelleği ekleme|
|/redis/linkedservers/DELETE|Bağlantılı sunucu bir Redis Önbelleği'nden silin|
|/redis/patchSchedules/Read|Merhaba, Redis önbelleği zamanlamasını düzeltme eki uygulama alır|
|/redis/patchSchedules/Write|Bir Redis önbelleği zamanlama düzeltme eki uygulama hello değiştirme|
|/redis/patchSchedules/DELETE|Redis önbelleği Hello düzeltme zamanlaması silme|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| İşlem | Açıklama |
|---|---|
|/ provisionGlobalAppServicePrincipalInUserTenant/eylem|Hizmet uygulaması sorumlusu için hizmet asıl sağlama|
|/ validateCertificateRegistrationInformation/eylem|Sertifika satın alma nesnesi gönderme olmadan doğrula|
|/ Kayıt/eylem|Merhaba aboneliği için Hello Microsoft Certificates kaynak sağlayıcısı kaydetme|
|/ certificateOrders/yazma|Yeni bir certificateOrder eklemek veya mevcut bir güncelleştirme|
|/ certificateOrders/Sil|Varolan bir AppServiceCertificate Sil|
|/ certificateOrders/okuma|CertificateOrders Hello listesini al|
|/certificateOrders/reissue/Action|Varolan bir certificateorder yeniden gönderin|
|/certificateOrders/renew/Action|Varolan bir certificateorder yenileme|
|/certificateOrders/retrieveCertificateActions/Action|Sertifika eylemlerin Hello listesini alma|
|/certificateOrders/retrieveEmailHistory/Action|Sertifika e-posta geçmişini alma|
|/certificateOrders/resendEmail/Action|Yeniden Gönder sertifika e-posta|
|/certificateOrders/verifyDomainOwnership/Action|Etki alanı sahipliğini doğrulayın|
|/certificateOrders/resendRequestEmails/Action|İstek e-postaları tooanother e-posta adresi yeniden gönderin|
|/certificateOrders/resendRequestEmails/Action|Site korumalı için verilen bir uygulama hizmet sertifikası alma|
|/certificateOrders/Certificates/Write|Yeni bir sertifika ekleyin veya mevcut bir güncelleştirme|
|/certificateOrders/Certificates/DELETE|Varolan bir sertifikayı Sil|
|/certificateOrders/Certificates/Read|Merhaba sertifikaların listesini al|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|TooClassic işlem kaydetme|
|/ checkDomainNameAvailability/eylem|Verilen etki alanı adı Hello kullanılabilirliğini denetler.|
|/ moveSubscriptionResources/eylem|Tüm Klasik kaynaklar tooa farklı aboneliğe taşıyın.|
|/ validateSubscriptionMoveAvailability/eylem|Klasik taşıma işlemi için Hello aboneliğin kullanılabilirlik doğrulayın.|
|/operatingSystemFamilies/Read|Merhaba konuk işletim sistemi aileleri Microsoft Azure'da kullanılabilen listeler ve ayrıca hello işletim sistemi sürümleri için her f kullanılabilir listeler
|/Capabilities/Read|Merhaba özelliklerini gösterir|
|/operatingSystems/Read|Merhaba Microsoft Azure üzerinde şu anda kullanılabilir hello konuk işletim sistemi sürümleri listelenmiştir.|
|/resourceTypes/skus/Read|Desteklenen kaynak türleri için Hello Sku listesini alır.|
|/domainNames/Read|Kaynaklar için Hello etki alanı adlarını döndürür.|
|/ domainNames/yazma|Ekleyin veya kaynaklar için hello etki alanı adlarını değiştirin.|
|/domainNames/DELETE|Kaynaklar için Hello etki alanı adlarını kaldırın.|
|/domainNames/Swap/Action|Hazırlama yuvası toohello üretim yuvasına hello değiştirir.|
|/domainNames/serviceCertificates/Read|Kullanılan hizmet sertifikalarını döndürür hello.|
|/domainNames/serviceCertificates/Write|Ekleyin veya kullanılan hello hizmet sertifikaları değiştirin.|
|/domainNames/serviceCertificates/DELETE|Kullanılan hello hizmet sertifikalarını silin.|
|/domainNames/serviceCertificates/operationStatuses/Read|Merhaba hello etki alanı adları hizmet sertifikaları için işlem durumunu okur.|
|/domainNames/Capabilities/Read|Merhaba etki alanı adı özelliklerini gösterir|
|/domainNames/Extensions/Read|Etki alanı adı uzantılarını döndürür hello.|
|/domainNames/Extensions/Write|Merhaba etki alanı adı uzantıları ekleyin.|
|/domainNames/Extensions/DELETE|Merhaba etki alanı adı uzantılarını kaldırın.|
|/domainNames/Extensions/operationStatuses/Read|Merhaba hello etki alanı adları uzantıları için işlem durumunu okur.|
|/domainNames/Active/Write|Merhaba etkin etki alanı adını ayarlar.|
|/domainNames/slots/Read|Merhaba dağıtım yuvaları gösterir.|
|/domainNames/slots/Write|Oluşturur veya hello dağıtım güncelleştirin.|
|/domainNames/slots/DELETE|Bir dağıtım yuvasını siler.|
|/domainNames/slots/Start/Action|Bir dağıtım yuvası başlatır.|
|/domainNames/slots/Stop/Action|Merhaba dağıtım yuvası askıya alır.|
|/domainNames/slots/operationStatuses/Read|Merhaba hello etki alanı adı yuvaları için işlem durumunu okur.|
|/domainNames/slots/Roles/Read|Merhaba rol hello dağıtım yuvası için alın.|
|/domainNames/slots/Roles/extensionReferences/Read|Merhaba dağıtım yuvası rolü uzantı başvurusunu döndürür hello.|
|/domainNames/slots/Roles/extensionReferences/Write|Ekleyin veya hello dağıtım yuvası rolü uzantı başvurusunu hello değiştirin.|
|/domainNames/slots/Roles/extensionReferences/DELETE|Merhaba hello dağıtım yuvası rolü uzantı başvurusunu kaldırın.|
|/domainNames/slots/Roles/extensionReferences/operationStatuses/Read|Merhaba hello etki alanı adı yuvaları uzantı başvuruları için işlem durumunu okur.|
|/domainNames/slots/Roles/roleInstances/Read|Merhaba rol örneğini alır.|
|/domainNames/slots/Roles/roleInstances/restart/Action|Rol örneği yeniden başlatır.|
|/domainNames/slots/Roles/roleInstances/reimage/Action|Reimages hello rol örneği.|
|/domainNames/slots/Roles/roleInstances/operationStatuses/Read|Merhaba hello etki alanı adı yuvası rolleri rol örnekleri için işlem durumunu okur.|
|/domainNames/slots/State/Start/Write|Değişiklikleri dağıtım yuvası durumunu toostopped hello.|
|/domainNames/slots/State/stop/Write|Değişiklikleri dağıtım yuvası durumunu toostarted hello.|
|/domainNames/slots/upgradeDomain/Write|Yükseltme hello etki alanı yol.|
|/domainNames/internalLoadBalancers/Read|Merhaba iç yük dengeleyicileri alır.|
|/domainNames/internalLoadBalancers/Write|Yeni bir iç yük dengeleme oluşturur.|
|/domainNames/internalLoadBalancers/DELETE|Yeni bir iç yük dengelemeyi kaldırın.|
|/domainNames/internalLoadBalancers/operationStatuses/Read|Merhaba etki alanı adları iç yük dengeleyicileri için hello işlem durumunu okur.|
|/domainNames/loadBalancedEndpointSets/Read|Merhaba yük dengeli uç nokta kümelerini gösterir|
|/domainNames/loadBalancedEndpointSets/operationStatuses/Read|Yük dengeli uç nokta kümelerini Hello etki alanı adları için hello işlem durumunu okur.|
|/domainNames/availabilitySets/Read|Hello kaynak ayarlanan hello kullanılabilirliğini gösterir.|
|/Quotas/Read|Merhaba kota hello abonelik için alın.|
|/virtualMachines/Read|Sanal makinelerin listesini alır.|
|/ virtualMachines/yazma|Sanal makineleri ekleyin veya değiştirin.|
|/virtualMachines/DELETE|Sanal makineler kaldırır.|
|/virtualMachines/Start/Action|Merhaba sanal makineyi başlatın.|
|/virtualMachines/Redeploy/Action|Merhaba sanal makine yeniden dağıtır.|
|/virtualMachines/restart/Action|Sanal makineler yeniden başlatır.|
|/virtualMachines/Stop/Action|Sanal makine durakları hello.|
|/virtualMachines/Shutdown/Action|Merhaba sanal makinesi kapatılamadı.|
|/virtualMachines/attachDisk/Action|Bir veri diski tooa sanal makineye iliştirir.|
|/virtualMachines/detachDisk/Action|Bir veri diskini sanal makineden ayırır.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/Action|Sanal makine için Hello RDP dosyasını indirir.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups/okuma|Merhaba Hello ağ arabirimiyle ilişkilendirilmiş ağ güvenlik grubunu alır.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups/yazma|Merhaba ağ arabirimiyle ilişkilendirilmiş ağ güvenlik grubu ekler.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups/silme|Merhaba Hello ağ arabirimiyle ilişkilendirilmiş ağ güvenlik grubunu siler.|
|/virtualMachines/networkInterfaces /<br>associatedNetworkSecurityGroups/operationStatuses/okuma|Ağ güvenlik gruplarıyla ilişkili hello sanal makineler için Hello işlem durumunu okur.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/Read|Merhaba ölçümleri tanımlarını alır.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/Read|Merhaba tanılama ayarlarını al.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/Write|Tanılama ayarlarını ekleyin veya değiştirin.|
|/virtualMachines/Metrics/Read|Merhaba ölçümleri alır.|
|/virtualMachines/operationStatuses/Read|Merhaba hello sanal makineler için işlem durumunu okur.|
|/virtualMachines/Extensions/Read|Merhaba sanal makine uzantısını alır.|
|/virtualMachines/Extensions/Write|Merhaba sanal makine uzantısını yerleştirir.|
|/virtualMachines/Extensions/operationStatuses/Read|Merhaba hello sanal makine uzantıları için işlem durumunu okur.|
|/virtualMachines/asyncOperations/Read|Merhaba olası zaman uyumsuz işlemleri alır|
|/virtualMachines/Disks/Read|Veri disklerinin listesini alır|
|/virtualMachines/associatedNetworkSecurityGroups/Read|Merhaba Hello sanal makineyle ilişkilendirilmiş ağ güvenlik grubunu alır.|
|/virtualMachines/associatedNetworkSecurityGroups/Write|Merhaba sanal makineyle ilişkilendirilmiş ağ güvenlik grubu ekler.|
|/virtualMachines/associatedNetworkSecurityGroups/DELETE|Merhaba Hello sanal makineyle ilişkilendirilmiş ağ güvenlik grubunu siler.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/Read|Ağ güvenlik gruplarıyla ilişkili hello sanal makineler için Hello işlem durumunu okur.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|TooClassic ağ kaydetme|
|/gatewaySupportedDevices/Read|Desteklenen aygıtlar Hello listesini alır.|
|/reservedIps/Read|Ayrılmış IP'ler alır hello|
|/ ReservedIP/yazma|Yeni bir ayrılmış IP ekleyin|
|/reservedIps/DELETE|Ayrılmış bir IP'yi silin.|
|/reservedIps/Link/Action|Ayrılmış bir IP'ye bağlantı oluşturun|
|/reservedIps/Join/Action|Ayrılmış bir IP'ye katılın|
|/reservedIps/operationStatuses/Read|Merhaba hello ayrılmış IP'ler için işlem durumunu okur.|
|/virtualNetworks/Read|Merhaba sanal ağ alın.|
|/ virtualNetworks/yazma|Yeni bir sanal ağ ekleyin.|
|/virtualNetworks/DELETE|Merhaba sanal ağ siler.|
|/virtualNetworks/Peer/Action|Bir sanal ağı başka bir sanal ağ ile eşler.|
|/virtualNetworks/Join/Action|Merhaba sanal ağ birleştirir.|
|/virtualNetworks/checkIPAddressAvailability/Action|Bir sanal ağdaki belirli bir IP adresi Hello kullanılabilirliğini denetler.|
|/virtualNetworks/Capabilities/Read|Merhaba özelliklerini gösterir|
|/virtualNetworks/alt ağlar /<br>associatedNetworkSecurityGroups/okuma|Merhaba Hello alt ağ ile ilişkilendirilmiş ağ güvenlik grubunu alır.|
|/virtualNetworks/alt ağlar /<br>associatedNetworkSecurityGroups/yazma|Merhaba alt ağ ile ilişkilendirilmiş ağ güvenlik grubu ekler.|
|/virtualNetworks/alt ağlar /<br>associatedNetworkSecurityGroups/silme|Merhaba Hello alt ağ ile ilişkilendirilmiş ağ güvenlik grubunu siler.|
|/virtualNetworks/alt ağlar /<br>associatedNetworkSecurityGroups/operationStatuses/okuma|Merhaba hello sanal ağ ağ güvenlik grubuyla alt ağı için işlem durumunu okur.|
|/virtualNetworks/operationStatuses/Read|Merhaba hello sanal ağlar için işlem durumunu okur.|
|/virtualNetworks/Gateways/Read|Merhaba sanal ağ geçitlerini alır.|
|/virtualNetworks/Gateways/Write|Bir sanal ağ geçidi ekler.|
|/virtualNetworks/Gateways/DELETE|Merhaba sanal ağ geçidini siler.|
|/virtualNetworks/Gateways/startDiagnostics/Action|Merhaba sanal ağ geçidi için tanılamayı başlatır.|
|/virtualNetworks/Gateways/stopDiagnostics/Action|Merhaba sanal ağ geçidi için tanılamayı durdurur hello.|
|/virtualNetworks/Gateways/downloadDiagnostics/Action|Merhaba ağ geçidi tanılama indirir.|
|/virtualNetworks/Gateways/listCircuitServiceKey/Action|Merhaba devre hizmet anahtarını alır.|
|/virtualNetworks/Gateways/downloadDeviceConfigurationScript/Action|Merhaba cihaz yapılandırma betiğini indirir.|
|/virtualNetworks/Gateways/listPackage/Action|Merhaba sanal ağ geçidi paketini listeler.|
|/virtualNetworks/Gateways/operationStatuses/Read|Merhaba hello sanal ağ geçitleri için işlem durumunu okur.|
|/virtualNetworks/Gateways/Packages/Read|Merhaba sanal ağ geçidi paketini alır.|
|/virtualNetworks/Gateways/Connections/Read|Merhaba bağlantıların listesini alır.|
|/virtualNetworks/Gateways/Connections/Connect/Action|Bir site toosite ağ geçidi bağlantısına bağlanır.|
|/virtualNetworks/Gateways/Connections/Disconnect/Action|Bir site toosite ağ geçidi bağlantısını keser.|
|/virtualNetworks/Gateways/Connections/test/Action|Bir site toosite ağ geçidi bağlantısını test eder.|
|/virtualNetworks/Gateways/clientRevokedCertificates/Read|Okuma hello istemci sertifikalarını iptal etti.|
|/virtualNetworks/Gateways/clientRevokedCertificates/Write|Bir istemci sertifikasını iptal eder.|
|/virtualNetworks/Gateways/clientRevokedCertificates/DELETE|Bir istemci sertifikası iptalini geri alır.|
|/virtualNetworks/Gateways/clientRootCertificates/Read|Merhaba istemci kök sertifikalarını bulun.|
|/virtualNetworks/Gateways/clientRootCertificates/Write|Yeni bir istemci kök sertifikasını karşıya yükler.|
|/virtualNetworks/Gateways/clientRootCertificates/DELETE|Merhaba sanal ağ geçidi istemci sertifikasını siler.|
|/virtualNetworks/Gateways/clientRootCertificates/download/Action|Parmak izine göre sertifika indirir.|
|/virtualNetworks/Gateways/clientRootCertificates/listPackage/Action|Merhaba sanal ağ geçidi sertifika paketini listeler.|
|/networkSecurityGroups/Read|Merhaba ağ güvenlik grubunu alır.|
|/ networkSecurityGroups/yazma|Yeni bir ağ güvenlik grubu ekler.|
|/networkSecurityGroups/DELETE|Merhaba ağ güvenlik grubunu siler.|
|/networkSecurityGroups/operationStatuses/Read|Merhaba hello ağ güvenlik grubu için işlem durumunu okur.|
|/networkSecurityGroups/securityRules/Read|Merhaba güvenlik kuralı alır.|
|/networkSecurityGroups/securityRules/Write|Güvenlik kuralı alır veya güncelleştirir.|
|/networkSecurityGroups/securityRules/DELETE|Merhaba güvenlik kuralını siler.|
|/networkSecurityGroups/securityRules/operationStatuses/Read|Merhaba ağ güvenlik grubu güvenlik kuralları için Hello işlem durumunu okur.|
|/Quotas/Read|Merhaba kota hello abonelik için alın.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Kayıt tooClassic depolama|
|/ checkStorageAccountAvailability/eylem|Bir depolama hesabı hello kullanılabilirliğini denetler.|
|/Capabilities/Read|Merhaba özelliklerini gösterir|
|/publicImages/Read|Merhaba genel sanal makine görüntüsünü alır.|
|/images/Read|Merhaba resim döndürür.|
|/storageAccounts/Read|Merhaba depolama hesabı hesabın verilen hello ile döndürür.|
|/ storageAccounts/yazma|Yeni bir depolama hesabı ekler.|
|/storageAccounts/DELETE|Merhaba depolama hesabı silin.|
|/storageAccounts/listKeys/Action|Merhaba hello depolama hesapları için erişim anahtarlarını listeler.|
|/storageAccounts/regenerateKey/Action|Merhaba depolama hesabı için Hello var olan erişim anahtarlarını yeniden oluşturur.|
|/storageAccounts/operationStatuses/Read|Merhaba kaynak için Hello işlem durumunu okur.|
|/storageAccounts/images/Read|Depolama hesabı görüntüsünü döndürür hello.|
|/storageAccounts/images/DELETE|Belirli bir depolama hesabı görüntüsünü siler.|
|/storageAccounts/Disks/Read|Depolama hesabı disk döndürür hello.|
|/storageAccounts/Disks/Write|Depolama hesabı diski ekler.|
|/storageAccounts/Disks/DELETE|Verilen depolama hesabı diskini siler.|
|/storageAccounts/Disks/operationStatuses/Read|Merhaba kaynak için Hello işlem durumunu okur.|
|/storageAccounts/osImages/Read|Depolama hesabı işletim sistemi görüntüsünü döndürür hello.|
|/storageAccounts/osImages/DELETE|Belirtilen bir depolama hesabı işletim sistemi görüntüsünü siler.|
|/storageAccounts/Services/Read|Merhaba kullanılabilir hizmetler alın.|
|/storageAccounts/Services/metricDefinitions/Read|Merhaba ölçümleri tanımlarını alır.|
|/storageAccounts/Services/Metrics/Read|Merhaba ölçümleri alır.|
|/storageAccounts/Services/diagnosticSettings/Read|Merhaba tanılama ayarlarını al.|
|/storageAccounts/Services/diagnosticSettings/Write|Tanılama ayarlarını ekleyin veya değiştirin.|
|/Disks/Read|Depolama hesabı disk döndürür hello.|
|/osImages/Read|Merhaba işletim sistemi görüntüsünü döndürür.|
|/Quotas/Read|Merhaba kota hello abonelik için alın.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| İşlem | Açıklama |
|---|---|
|/Accounts/Read|API hesapları okur.|
|/ hesapları/yazma|API hesapları yazar.|
|/Accounts/DELETE|API hesapları siler|
|/Accounts/listKeys/Action|Liste anahtarları|
|/Accounts/regenerateKey/Action|Anahtarı yeniden|
|/Accounts/skus/Read|Mevcut bir kaynağı için kullanılabilir SKU'lar okur.|
|/Accounts/usages/Read|Merhaba kota kullanımı için mevcut bir kaynağı alın.|
|/ Operations/okuma|Merhaba işlemi açıklaması.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| İşlem | Açıklama |
|---|---|
|/ RateCard/okuma|Veri, kaynak/ölçer meta verileri ve abonelik verilen hello için hızlarını döndürür sunar.|
|/ UsageAggregates/okuma|Microsoft Azure'nın tüketim abonelik tarafından alır. Merhaba sonucunu içerir toplamalar kullanım verileri, abonelik ve kaynak ilgili bilgi için belirli bir zaman aralığı.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Aboneliği Microsoft.Compute kaynak sağlayıcısına kaydeder|
|/restorePointCollections/Read|Bir geri yükleme noktası koleksiyon Hello özelliklerini alır|
|/ restorePointCollections/yazma|Yeni bir geri yükleme noktası koleksiyonu oluşturur veya mevcut kümeyi güncelleştirir|
|/restorePointCollections/DELETE|Siler hello geri yükleme noktası toplama ve içerilen geri yükleme noktaları|
|/restorePointCollections/restorePoints/Read|Bir geri yükleme noktası Hello özelliklerini alır|
|/restorePointCollections/restorePoints/Write|Yeni bir geri yükleme noktası oluşturur|
|/restorePointCollections/restorePoints/DELETE|Merhaba geri yükleme noktası siler|
|/restorePointCollections/restorePoints/retrieveSasUris/Action|Bir geri yükleme noktası blob SAS URI'ler birlikte Hello özelliklerini alır|
|/virtualMachineScaleSets/Read|Bir sanal makine ölçek kümesi Hello özelliklerini alır|
|/ virtualMachineScaleSets/yazma|Yeni bir sanal makine ölçek kümesi oluşturur veya mevcut kümeyi güncelleştirir|
|/virtualMachineScaleSets/DELETE|Merhaba sanal makine ölçek kümesini siler|
|/virtualMachineScaleSets/Start/Action|Merhaba sanal makine ölçek kümesinin örneklerini başlatır hello|
|/virtualMachineScaleSets/powerOff/Action|Merhaba hello sanal makine ölçek kümesinin örneklerini kapatır|
|/virtualMachineScaleSets/restart/Action|Merhaba hello sanal makine ölçek kümesinin örneklerini yeniden başlatır|
|/virtualMachineScaleSets/deallocate/Action|Kapatır ve hello hello sanal makine ölçek kümesinin örneklerini sürümleri hello işlem kaynakları |
|/virtualMachineScaleSets/manualUpgrade/Action|El ile Merhaba sanal makine ölçek kümesinin örneklerini toolatest modeli güncelleştirir|
|/virtualMachineScaleSets/Scale/Action|İçinde ölçeklendirmek / ölçeği Genişlet örnek sayısını var olan bir sanal makine ölçek kümesi|
|/virtualMachineScaleSets/instanceView/Read|Merhaba sanal makine ölçek kümesi Hello örnek görünümünü alır|
|/virtualMachineScaleSets/skus/Read|Varolan bir sanal makine ölçek kümesi için geçerli SKU'ları listeler hello|
|/virtualMachineScaleSets/virtualMachines/Read|Merhaba VM ölçek kümesindeki bir sanal makinenin özelliklerini alır.|
|/virtualMachineScaleSets/virtualMachines/DELETE|VM Ölçek Kümesindeki belirli bir Sanal Makineyi silin.|
|/virtualMachineScaleSets/virtualMachines/Start/Action|VM Ölçek Kümesindeki bir Sanal Makine örneğini başlatır.|
|/virtualMachineScaleSets/virtualMachines/powerOff/Action|VM Ölçek Kümesindeki bir Sanal Makine örneğini kapatır.|
|/virtualMachineScaleSets/virtualMachines/restart/Action|VM Ölçek Kümesindeki bir Sanal Makine örneğini yeniden başlatır.|
|/virtualMachineScaleSets/virtualMachines/deallocate/Action|Kapatır ve sürümler hello işlem kaynakları VM ölçek kümesindeki bir sanal makine için.|
|/virtualMachineScaleSets/virtualMachines/instanceView/Read|VM ölçek kümesindeki bir sanal makine Hello örnek görünümünü alır.|
|/images/Read|Merhaba görüntü Hello özelliklerini alır|
|/ görüntüleri/yazma|Yeni bir görüntü oluşturur veya mevcut kümeyi güncelleştirir|
|/images/DELETE|Merhaba görüntüsünü siler|
|/Operations/Read|Microsoft.Compute kaynak sağlayıcısındaki kullanılabilir işlemleri listele|
|/Disks/Read|Bir Disk Hello özelliklerini alır|
|/ diskleri/yazma|Yeni bir Disk oluşturur veya mevcut Diski güncelleştirir|
|/Disks/DELETE|Disk siler hello|
|/Disks/beginGetAccess/Action|Blob erişimi için Hello hello Disk SAS URI'sini Al|
|/Disks/endGetAccess/Action|Merhaba hello Disk SAS URI'sini iptal etme|
|/snapshots/Read|Bir anlık görüntü Hello özelliklerini alır|
|/ Anlık görüntüler/yazma|Yeni bir Anlık Görüntü oluşturur veya mevcut Anlık Görüntüyü güncelleştirir|
|/snapshots/DELETE|Anlık Görüntüyü siler|
|/availabilitySets/Read|Bir kullanılabilirlik kümesi Hello özelliklerini alır|
|/ availabilitySets/yazma|Yeni bir kullanılabilirlik kümesi oluşturur veya mevcut kümeyi güncelleştirir|
|/availabilitySets/DELETE|Merhaba kullanılabilirlik kümesini siler|
|/availabilitySets/vmSizes/Read|Oluşturma veya güncelleştirme hello kullanılabilirlik kümesindeki sanal makine için kullanılabilir boyutları Listele|
|/virtualMachines/Read|Bir sanal makine Hello özelliklerini alır|
|/ virtualMachines/yazma|Yeni bir sanal makine oluşturur veya mevcut sanal makineyi güncelleştirir|
|/virtualMachines/DELETE|Merhaba sanal makinesini siler|
|/virtualMachines/Start/Action|Başlatır hello sanal makine|
|/virtualMachines/powerOff/Action|Merhaba sanal makineyi kapatır. Sanal makine hello Not faturalandırılır toobe devam eder.|
|/virtualMachines/Redeploy/Action|Sanal makine yeniden dağıtır|
|/virtualMachines/restart/Action|Merhaba sanal makine yeniden başlatılıyor|
|/virtualMachines/deallocate/Action|Merhaba sanal makine ve sürümler hello işlem kaynakları kapatır|
|/virtualMachines/generalize/Action|Merhaba sanal makine durumu tooGeneralized ayarlar ve hello sanal makineyi yakalama için hazırlar|
|/virtualMachines/Capture/Action|Sanal sabit diskleri kopyalayarak Hello sanal makineyi yakalar ve kullanılan toocreate benzer sanal makineler olabilir bir şablon oluşturur|
|/virtualMachines/convertToManagedDisks/Action|Merhaba blob tabanlı disklerin hello sanal makine toomanaged disklerin dönüştürür|
|/virtualMachines/vmSizes/Read|Merhaba sanal makine güncelleştirmek için kullanılabilir boyutları listeler|
|/virtualMachines/instanceView/Read|Ayrıntılı çalışma zamanı durumunu hello sanal makine ve kaynaklarının alır hello|
|/virtualMachines/Extensions/Read|Bir sanal makine uzantısı Hello özelliklerini alır|
|/virtualMachines/Extensions/Write|Yeni bir sanal makine uzantısı oluşturur veya mevcut uzantıyı güncelleştirir|
|/virtualMachines/Extensions/DELETE|Merhaba sanal makine uzantısını siler|
|/Locations/vmSizes/Read|Bir konumdaki kullanılabilir sanal makine boyutlarını listeler|
|/Locations/usages/Read|Hizmet sınırları ve geçerli kullanım miktarlarını hello aboneliğin işlem kaynakları için bir konumda alır.|
|/Locations/Operations/Read|Zaman uyumsuz bir işlem Hello durumunu alır|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello kapsayıcı kayıt kaynak sağlayıcısı için aboneliği kaydeder ve kapsayıcı kayıt defterleri hello oluşturulmasını sağlar.|
|/checknameavailability/Read|Bu kayıt defteri adının geçerli olduğundan ve kullanımda olup olmadığını denetler.|
|/registries/Read|Kapsayıcı kayıt defterleri listesini döndürür hello veya hello belirtilen kapsayıcı kayıt defteri özelliklerini alır hello.|
|/ kayıt defterleri/yazma|Kapsayıcı kayıt defteri ile oluşturur hello belirtilen parametreleri veya hello özellikleri veya etiketleri hello belirtilen kapsayıcı kayıt defteri için güncelleştirin.|
|/registries/DELETE|Varolan bir kapsayıcı kayıt siler.|
|/registries/listCredentials/Action|Merhaba belirtilen kapsayıcı kayıt defteri Hello oturum açma kimlik bilgileri listeler.|
|/registries/regenerateCredential/Action|Merhaba belirtilen kapsayıcı kayıt defteri Hello oturum açma kimlik bilgilerini yeniden oluşturur.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| İşlem | Açıklama |
|---|---|
|/containerServices/Subscriptions/Read|Merhaba aboneliğe göre belirtilen kapsayıcı hizmetlerini Al|
|/containerServices/resourceGroups/Read|Merhaba kaynak grubuna göre belirtilen kapsayıcı hizmetlerini Al|
|/containerServices/resourceGroups/ContainerServiceName/Read|Kapsayıcı hizmetini alır hello belirtilen|
|/containerServices/resourceGroups/ContainerServiceName/Write|Kapsayıcı hizmetini yerleştirir veya güncelleştirmeleri hello belirtilen|
|/containerServices/resourceGroups/ContainerServiceName/DELETE|Kapsayıcı hizmetini siler hello belirtilen|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| İşlem | Açıklama |
|---|---|
|/ updateCommunicationPreference/eylem|Güncelleştirme iletişim tercihi|
|/ listCommunicationPreference/eylem|Liste iletişim tercihi|
|/Applications/Read|Okuma işlemi|
|/ uygulamalar/yazma|Yazma işlemi|
|/ uygulamalar/yazma|Yazma işlemi|
|/Applications/DELETE|Silme işlemi|
|/Applications/listSecrets/Action|Gizli anahtarları listeleme|
|/Applications/listSingleSignOnToken/Action|Çoklu oturum açma belirteçleri okuma|
|/Operations/Read|okuma işlemleri|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| İşlem | Açıklama |
|---|---|
|/hubs/Read|Tüm Azure müşteri Öngörüler hub'ı okuyun|
|/ hubs/yazma|Tüm Azure müşteri Öngörüler Hub güncelle|
|/hubs/DELETE|Tüm Azure müşteri Öngörüler hub'ını silmek|
|/hubs/providers/Microsoft.Insights/metricDefinitions/Read|Kaynak için Hello kullanılabilir ölçümleri alır|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/Read|Hello hello kaynağın tanılama ayarını alır|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/Write|Oluşturur veya hello kaynağın tanılama ayarını hello güncelleştirir|
|/hubs/providers/Microsoft.Insights/logDefinitions/Read|Kaynak için Hello kullanılabilir günlüklerini alır|
|/hubs/authorizationPolicies/Read|Herhangi bir Azure müşteri öngörü paylaşılan erişim imzası İlkesi okuma|
|/hubs/authorizationPolicies/Write|Herhangi bir Azure müşteri Öngörüler paylaşılan erişim imzası ilke güncelle|
|/hubs/authorizationPolicies/DELETE|Tüm Azure müşteri Öngörüler paylaşılan erişim imzası ilkelerini Sil|
|/hubs/authorizationPolicies/regeneratePrimaryKey/Action|Azure müşteri Öngörüler paylaşılan erişim imzası ilkesinin birincil anahtarını yeniden oluşturma|
|/hubs/authorizationPolicies/regenerateSecondaryKey/Action|Azure müşteri Öngörüler paylaşılan erişim imzası İlkesi ikincil anahtarını yeniden oluşturma|
|/hubs/Profiles/Read|Tüm Azure müşteri Öngörüler profilini okuma|
|/hubs/Profiles/Write|Herhangi bir Azure müşteri Öngörüler profil yazma|
|/hubs/Kpi/Read|Tüm Azure müşteri Öngörüler ana performans göstergesinin okuma|
|/hubs/Kpi/Write|Tüm Azure müşteri Öngörüler ana performans göstergesinin güncelle|
|/hubs/Kpi/DELETE|Tüm Azure müşteri Öngörüler ana performans göstergesinin Sil|
|/hubs/Views/Read|Herhangi bir Azure müşteri Öngörüler uygulama görünümü okuma|
|/hubs/Views/Write|Herhangi bir Azure müşteri Öngörüler uygulama Görünümü güncelle|
|/hubs/Views/DELETE|Herhangi bir Azure müşteri Öngörüler uygulama Görünümü Sil|
|/hubs/interactions/Read|Azure müşteri Öngörüler etkileşimi okuma|
|/hubs/interactions/Write|Azure müşteri Öngörüler etkileşimi güncelle|
|/hubs/roleAssignments/Read|Herhangi bir Azure müşteri Öngörüler Rbac atama okuma|
|/hubs/roleAssignments/Write|Herhangi bir Azure müşteri Öngörüler Rbac atama güncelle|
|/hubs/roleAssignments/DELETE|Tüm Azure müşteri Öngörüler Rbac atamasını silin|
|/hubs/connectors/Read|Tüm Azure müşteri Öngörüler Bağlayıcısı okuma|
|/hubs/connectors/Write|Tüm Azure müşteri Öngörüler Bağlayıcısı güncelle|
|/hubs/connectors/DELETE|Tüm Azure müşteri Öngörüler bağlayıcısını silin|
|/hubs/connectors/Mappings/Read|Tüm Azure müşteri Öngörüler Bağlayıcısı eşleme okuma|
|/hubs/connectors/Mappings/Write|Oluşturma veya güncelleştirme tüm Azure müşteri Öngörüler Bağlayıcısı eşlemesi|
|/hubs/connectors/Mappings/DELETE|Tüm Azure müşteri Öngörüler Bağlayıcısı eşleme Sil|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| İşlem | Açıklama |
|---|---|
|/ checkNameAvailability/eylem|Kiracı için katalog adı kullanılabilirliğini denetler.|
|/Catalogs/Read|Katalog ya da kataloglar abonelik veya kaynak grubu altında için özellikleri alır.|
|/ kataloglar/yazma|Katalog veya güncelleştirmeler hello etiketleri ve hello katalog özelliklerini oluşturur.|
|/Catalogs/DELETE|Başlangıç kataloğu siler.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| İşlem | Açıklama |
|---|---|
|/datafactories/Read|Veri Fabrikası okur.|
|/ datafactories/yazma|Veri Fabrikası güncelle|
|/datafactories/DELETE|Veri Fabrikası siler.|
|/datafactories/datapipelines/Read|Ardışık Düzen okur.|
|/datafactories/datapipelines/DELETE|Ardışık Düzen siler.|
|/datafactories/datapipelines/pause/Action|Duraklatır ardışık düzen.|
|/datafactories/datapipelines/Resume/Action|Ardışık Düzen sürdürür.|
|/datafactories/datapipelines/Update/Action|Güncelleştirmeleri ardışık düzen.|
|/datafactories/datapipelines/Write|Ardışık Düzen güncelle|
|/datafactories/linkedServices/Read|Bağlantılı hizmeti okur.|
|/datafactories/linkedServices/DELETE|Bağlantılı hizmeti siler.|
|/datafactories/linkedServices/Write|Oluşturma veya güncelleştirme bağlı hizmet|
|/datafactories/Tables/Read|Tablo okur.|
|/datafactories/Tables/DELETE|Tablo siler.|
|/datafactories/Tables/Write|Tablo güncelle|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| İşlem | Açıklama |
|---|---|
|/Accounts/Read|Merhaba DataLakeAnalytics hesabı hakkında bilgi alın.|
|/ hesapları/yazma|Oluşturun veya hello DataLakeAnalytics hesabı güncelleştirin.|
|/Accounts/DELETE|Merhaba DataLakeAnalytics hesabı silin.|
|/Accounts/firewallRules/Read|Bir güvenlik duvarı kuralı hakkında bilgi alın.|
|/Accounts/firewallRules/Write|Oluşturun veya bir güvenlik duvarı kuralı güncelleştirin.|
|/Accounts/firewallRules/DELETE|Bir güvenlik duvarı kuralını siler.|
|/Accounts/storageAccounts/Read|Bağlantılı Depolama hesabı Merhaba DataLakeAnalytics hesap alın.|
|/Accounts/storageAccounts/Write|Bir depolama hesabı toohello DataLakeAnalytics hesabı bağlayın.|
|/Accounts/storageAccounts/DELETE|Merhaba DataLakeAnalytics hesabı depolama hesabından bağlantısını.|
|/Accounts/storageAccounts/Containers/Read|Depolama hesabı hello altında kapsayıcıları Al|
|/Accounts/storageAccounts/Containers/listSasTokens/Action|Merhaba depolama kapsayıcısı için SAS belirteci listesi|
|/Accounts/dataLakeStoreAccounts/Read|Bağlantılı DataLakeStore hesabı Merhaba DataLakeAnalytics hesabı edinin.|
|/Accounts/dataLakeStoreAccounts/Write|DataLakeStore hesap toohello DataLakeAnalytics hesabı bağlayın.|
|/Accounts/dataLakeStoreAccounts/DELETE|Merhaba DataLakeAnalytics hesap DataLakeStore hesabından bağlantısını.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| İşlem | Açıklama |
|---|---|
|/Accounts/Read|Var olan bir DataLakeStore hesabı hakkında bilgi alın.|
|/ hesapları/yazma|Yeni bir DataLakeStore hesabı oluşturun veya var olan bir DataLakeStore hesabı güncelleştirin.|
|/Accounts/DELETE|Önceden DataLakeStore hesap silme.|
|/Accounts/firewallRules/Read|Bir güvenlik duvarı kuralı hakkında bilgi alın.|
|/Accounts/firewallRules/Write|Oluşturun veya bir güvenlik duvarı kuralı güncelleştirin.|
|/Accounts/firewallRules/DELETE|Bir güvenlik duvarı kuralını siler.|
|/Accounts/trustedIdProviders/Read|Güvenilen kimlik sağlayıcısı hakkında bilgi alın.|
|/Accounts/trustedIdProviders/Write|Oluşturun veya bir güvenilen kimlik sağlayıcısı güncelleştirin.|
|/Accounts/trustedIdProviders/DELETE|Güvenilen kimlik sağlayıcısı silin.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba Iothub kaynak sağlayıcısı ve etkinleştirir hello oluşturulması için Iothub kaynakları Hello abonelik kaydı|
|/ checkNameAvailability/eylem|Onay, Iothub adı kullanılamıyor|
|/ kullanımları/okuma|Abonelik bu sağlayıcı için kullanım ayrıntıları alın.|
|/ operations/okuma|Tüm ResourceProvider işlemleri Al|
|/ iotHubs/okuma|Merhaba Iothub kaynaklar alır|
|/ iotHubs/yazma|Iothub kaynak güncelle|
|/ iotHubs/Sil|Iothub kaynağı silme|
|/iotHubs/listkeys/Action|Tüm Iothub anahtarları alma|
|/iotHubs/exportDevices/Action|Dışarı aktarma cihazları|
|/iotHubs/importDevices/Action|Cihazları içeri aktarma|
|/ IotHubs/metricDefinitions/okuma|Merhaba Iothub hizmet Hello kullanılabilir ölçümleri alır|
|/iotHubs/iotHubKeys/listkeys/Action|Iothub anahtar hello verilen ad|
|/iotHubs/iotHubStats/Read|Iothub istatistiklerini alın|
|/iotHubs/quotaMetrics/Read|Kota ölçümleri alma|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|EventHub tüketici grubu oluşturma|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|EventHub tüketici grubu Al|
|/iotHubs/eventHubEndpoints/consumerGroups/DELETE|EventHub tüketici grubu Sil|
|/iotHubs/Routing/Routes/$ testall/eylem|Bir ileti tüm var olan yollar karşı test etme|
|/iotHubs/Routing/Routes/$ testnew/eylem|Bir ileti sağlanan test rota karşı test etme|
|/ IotHubs/diagnosticSettings/okuma|Hello hello kaynağın tanılama ayarını alır|
|/ IotHubs/diagnosticSettings/yazma|Oluşturur veya hello kaynağın tanılama ayarını hello güncelleştirir|
|/iotHubs/skus/Read|Geçerli Iothub SKU'ları alma|
|/iotHubs/Jobs/Read|İş ayrıntıları Iothub gönderme|
|/iotHubs/routingEndpointsHealth/Read|Bir Iothub için tüm yönlendirme uç noktaları Hello durumunu alır|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| İşlem | Açıklama |
|---|---|
|/ Abonelik/kayıt/eylem|Merhaba aboneliği kaydeder|
|/Labs/DELETE|Labs silin.|
|/Labs/Read|Labs okuyun.|
|/ labs/yazma|Ekleyin veya labs değiştirin.|
|/Labs/ListVhds/Action|Liste disk görüntülerini özel görüntü oluşturma için kullanılabilir.|
|/Labs/GenerateUploadUri/Action|Özel disk görüntüleri tooa Laboratuvar yüklemek için bir URI oluşturur.|
|/Labs/CreateEnvironment/Action|Sanal makineler bir laboratuar ortamında oluşturun.|
|/Labs/ClaimAnyVm/Action|Merhaba Laboratuvar rastgele claimable sanal makinede talep.|
|/Labs/ExportResourceUsage/Action|Dışarı aktarma bir depolama hesabına Laboratuvar kaynak kullanımı hello|
|/Labs/Users/DELETE|Kullanıcı profillerini silin.|
|/Labs/Users/Read|Kullanıcı profillerini okuyun.|
|/Labs/Users/Write|Ekleyin veya kullanıcı profillerini değiştirin.|
|/Labs/Users/Secrets/DELETE|Gizli silin.|
|/Labs/Users/Secrets/Read|Gizli okuyun.|
|/Labs/Users/Secrets/Write|Ekleyin veya gizli değiştirin.|
|/Labs/Users/Environments/DELETE|Ortamlar silin.|
|/Labs/Users/Environments/Read|Ortamlar okuyun.|
|/Labs/Users/Environments/Write|Ekleyin veya ortamlar değiştirin.|
|/Labs/Users/Disks/DELETE|Diskleri silin.|
|/Labs/Users/Disks/Read|Diskleri okuyun.|
|/Labs/Users/Disks/Write|Ekleyin veya diskleri değiştirin.|
|/Labs/Users/Disks/Attach/Action|Ekleme ve hello kira hello disk toohello sanal makine oluşturun.|
|/Labs/Users/Disks/detach/Action|Ayırma ve sonu hello kira hello diskin toohello sanal makineye bağlı.|
|/Labs/customImages/DELETE|Özel resimler silin.|
|/Labs/customImages/Read|Özel resimler okuyun.|
|/Labs/customImages/Write|Ekleyin veya özel resimler değiştirin.|
|/Labs/serviceRunners/DELETE|Hizmet koşucular silin.|
|/Labs/serviceRunners/Read|Hizmet koşucular okuyun.|
|/Labs/serviceRunners/Write|Ekleyin veya hizmet koşucular değiştirin.|
|/Labs/artifactSources/DELETE|Yapı kaynaklarını silin.|
|/Labs/artifactSources/Read|Yapı kaynaklarını okuyun.|
|/Labs/artifactSources/Write|Ekleyin veya Yapı kaynaklarını değiştirin.|
|/Labs/artifactSources/artifacts/Read|Yapıları okuyun.|
|/Labs/artifactSources/artifacts/GenerateArmTemplate/Action|Yapı verilen hello için bir ARM şablonu oluşturur, gerekli hello dosyaları tooa depolama hesabı yükler ve oluşturulan hello yapı doğrular.|
|/Labs/artifactSources/armTemplates/Read|Azure resource manager şablonları okuyun.|
|/Labs/costs/Read|Maliyetleri okuyun.|
|/Labs/costs/Write|Ekleyin veya maliyetleri değiştirin.|
|/Labs/virtualNetworks/DELETE|Sanal ağlar silin.|
|/Labs/virtualNetworks/Read|Sanal ağlar okuyun.|
|/Labs/virtualNetworks/Write|Ekleyin veya sanal ağları değiştirin.|
|/Labs/Formulas/DELETE|Formülleri silin.|
|/Labs/Formulas/Read|Formülleri okuyun.|
|/Labs/Formulas/Write|Ekleyin veya formüller değiştirin.|
|/Labs/Schedules/DELETE|Zamanlamalar silin.|
|/Labs/Schedules/Read|Zamanlamalar okuyun.|
|/Labs/Schedules/Write|Ekleyin veya zamanlamalarını değiştirin.|
|/Labs/Schedules/Execute/Action|Bir zamanlama yürütün.|
|/Labs/Schedules/ListApplicable/Action|Tüm geçerli zamanlamaları listeler|
|/Labs/galleryImages/Read|Galeri görüntüleri okuyun.|
|/Labs/policySets/EvaluatePolicies/Action|Laboratuvar ilkeyi değerlendirir.|
|/Labs/policySets/Policies/DELETE|İlkeleri silin.|
|/Labs/policySets/Policies/Read|İlkeleri okuyun.|
|/Labs/policySets/Policies/Write|Ekleyin veya ilkeleri değiştirin.|
|/Labs/virtualMachines/DELETE|Sanal makineleri silin.|
|/Labs/virtualMachines/Read|Sanal makineler okuyun.|
|/Labs/virtualMachines/Write|Sanal makineleri ekleyin veya değiştirin.|
|/Labs/virtualMachines/Start/Action|Bir sanal makineyi başlatın.|
|/Labs/virtualMachines/Stop/Action|Bir sanal makineyi durdurma|
|/Labs/virtualMachines/ApplyArtifacts/Action|Yapıları toovirtual makine uygulayın.|
|/Labs/virtualMachines/AddDataDisk/Action|Yeni veya var olan veri diski toovirtual makine ekleyin.|
|/Labs/virtualMachines/DetachDataDisk/Action|Merhaba belirtilen hello sanal makinede diski kullanımdan çıkarın.|
|/Labs/virtualMachines/Claim/Action|Var olan bir sanal makine sahipliğini alın|
|/Labs/virtualMachines/ListApplicableSchedules/Action|Tüm geçerli zamanlamaları listeler|
|/Labs/virtualMachines/Schedules/DELETE|Zamanlamalar silin.|
|/Labs/virtualMachines/Schedules/Read|Zamanlamalar okuyun.|
|/Labs/virtualMachines/Schedules/Write|Ekleyin veya zamanlamalarını değiştirin.|
|/Labs/virtualMachines/Schedules/Execute/Action|Bir zamanlama yürütün.|
|/Labs/notificationChannels/DELETE|Notificationchannels silin.|
|/Labs/notificationChannels/Read|Notificationchannels okuyun.|
|/Labs/notificationChannels/Write|Ekleyin veya notificationchannels değiştirin.|
|/Labs/notificationChannels/Notify/Action|Bildirim tooprovided kanalı gönderin.|
|/Schedules/DELETE|Zamanlamalar silin.|
|/Schedules/Read|Zamanlamalar okuyun.|
|/ zamanlamaları/yazma|Ekleyin veya zamanlamalarını değiştirin.|
|/Schedules/Execute/Action|Bir zamanlama yürütün.|
|/Schedules/Retarget/Action|Bir zamanlama ait hedef kaynak kimliği güncelleştirir|
|/Locations/Operations/Read|Okuma işlemleri.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| İşlem | Açıklama |
|---|---|
|/databaseAccountNames/Read|Ad kullanılabilirliğini denetler.|
|/databaseAccounts/Read|Veritabanı hesabı okur.|
|/ databaseAccounts/yazma|Bir veritabanı hesaplarını güncelleştirin.|
|/databaseAccounts/listKeys/Action|Veritabanı hesabı listesi anahtarları|
|/databaseAccounts/regenerateKey/Action|Veritabanı hesabı anahtarlarını döndürün|
|/databaseAccounts/listConnectionStrings/Action|Merhaba bağlantı dizeleri için bir veritabanı hesabı edinin|
|/databaseAccounts/changeResourceGroup/Action|Veritabanı hesabı, kaynak grubu Değiştir|
|/databaseAccounts/failoverPriorityChange/Action|Veritabanı hesabı bölgelerinin yük devretme önceliklerini değiştirin. Kullanılan tooperform el ile yük devretme işlemi budur|
|/databaseAccounts/DELETE|Merhaba veritabanı hesaplarını siler.|
|/databaseAccounts/metricDefinitions/Read|Merhaba veritabanı hesabı ölçümleri tanımları okur.|
|/databaseAccounts/Metrics/Read|Merhaba veritabanı hesabı ölçümleri okur.|
|/databaseAccounts/usages/Read|Merhaba veritabanı hesabı kullanımları okur.|
|/databaseAccounts/Databases/Collections/metricDefinitions/Read|Merhaba koleksiyonu ölçüm tanımlarını okur.|
|/databaseAccounts/Databases/Collections/Metrics/Read|Merhaba koleksiyonu ölçümleri okur.|
|/databaseAccounts/Databases/Collections/usages/Read|Merhaba koleksiyonu kullanımları okur.|
|/databaseAccounts/Databases/metricDefinitions/Read|Merhaba veritabanı ölçüm tanımlarını okur|
|/databaseAccounts/Databases/Metrics/Read|Merhaba veritabanı ölçümleri okur.|
|/databaseAccounts/Databases/usages/Read|Merhaba veritabanı kullanımları okur.|
|/databaseAccounts/readonlykeys/Read|Merhaba veritabanı hesabı readonly anahtarları okur.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| İşlem | Açıklama |
|---|---|
|/ generateSsoRequest/eylem|Etki alanı denetim Merkezi'nde oturum için bir istek oluşturun.|
|/ validateDomainRegistrationInformation/eylem|Etki alanı satın alma nesnesi gönderme olmadan doğrula|
|/ checkDomainAvailability/eylem|Bir etki alanı satın almak için uygun olup olmadığını denetleyin|
|/ listDomainRecommendations/eylem|Anahtar sözcüklere dayalı hello liste etki alanı önerileri Al|
|/ Kayıt/eylem|Merhaba aboneliği için Hello Microsoft Domains kaynak sağlayıcısı kaydetme|
|/ etki alanı/okuma|Merhaba etki alanlarının listesini alın|
|/ etki alanı/yazma|Yeni bir etki alanı eklemek veya mevcut bir güncelleştirme|
|/ etki alanı/Sil|Varolan bir etki alanını silin.|
|/Domains/operationresults/Read|Bir etki alanı işlemi Al|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| İşlem | Açıklama |
|---|---|
|/lcsprojects/Read|Tooa kullanıcıya ait görüntü Microsoft Dynamics yaşam döngüsü Hizmetleri projeleri|
|/ lcsprojects/yazma|Oluşturun ve toohello kullanıcıya ait Microsoft Dynamics yaşam döngüsü Hizmetleri projeleri güncelleştirin. Yalnızca hello ad ve açıklama özellikleri güncelleştirilebilir. Merhaba abonelik ve konumda hello projeyle ilişkili oluşturulduktan sonra güncelleştirilemiyor|
|/lcsprojects/DELETE|Toohello kullanıcıya ait Microsoft Dynamics yaşam döngüsü Hizmetleri projeleri sil|
|/lcsprojects/clouddeployments/Read|Microsoft Dynamics AX 2012 R3 değerlendirme dağıtımları tooa kullanıcıya ait bir Microsoft Dynamics yaşam döngüsü Hizmetleri projesinde görüntüleme|
|/lcsprojects/clouddeployments/Write|Microsoft Dynamics AX 2012 R3 değerlendirme dağıtımı tooa kullanıcı ait bir Microsoft Dynamics yaşam döngüsü Hizmetleri projesi oluşturun. Azure Yönetim Portalı'ndan dağıtımları yönetilebilir.|
|/lcsprojects/connectors/Read|Tooa Microsoft Dynamics yaşam döngüsü Hizmetleri Proje ait bağlayıcılar okuma|
|/lcsprojects/connectors/Write|Oluşturma ve tooa Microsoft Dynamics yaşam döngüsü Hizmetleri Proje ait bağlayıcılar güncelleştirme|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| İşlem | Açıklama |
|---|---|
|/ checkNameAvailability/eylem|İlgili abonelikte ad alanının kullanılabilirliğini denetler.|
|/ Kayıt/eylem|Merhaba hello EventHub kaynak sağlayıcısı için aboneliği kaydeder ve EventHub kaynak hello oluşturmayı etkinleştirir|
|/ ad alanları/yazma|Namespace kaynak oluşturun ve özelliklerini güncelleştirin. Etiketleri ve hello Namespace durumunu, güncelleştirilebilir hello özelliklerdir.|
|/namespaces/Read|Namespace kaynak açıklaması Hello listesini al|
|/ ad alanları/Sil|Namespace kaynağı silme|
|/namespaces/metricDefinitions/Read|Namespace ölçümleri kaynak açıklamaları listesini al|
|/namespaces/authorizationRules/Read|Ad alanları yetkilendirme kuralları açıklama Hello listesini alın.|
|/namespaces/authorizationRules/Write|Namespace düzeyi yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/authorizationRules/DELETE|Namespace yetkilendirme kuralını silin. Merhaba varsayılan Namespace yetkilendirme kuralı silinemez. |
|/namespaces/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi toohello Namespace Al|
|/namespaces/authorizationRules/regenerateKeys/Action|Merhaba birincil veya ikincil anahtarı toohello kaynak yeniden oluştur|
|/namespaces/eventhubs/Write|Oluşturma veya güncelleştirme EventHub özellikleri.|
|/namespaces/eventhubs/Read|EventHub kaynak açıklamaları listesini al|
|/namespaces/eventhubs/DELETE|İşlem toodelete EventHub kaynak|
|/namespaces/eventHubs/consumergroups/Write|Oluşturma veya güncelleştirme ConsumerGroup özellikleri.|
|/namespaces/eventHubs/consumergroups/Read|ConsumerGroup kaynak açıklamaları listesini al|
|/namespaces/eventHubs/consumergroups/DELETE|İşlem toodelete ConsumerGroup kaynak|
|/namespaces/eventhubs/authorizationRules/Read| EventHub yetkilendirme kuralları Hello listesini al|
|/namespaces/eventhubs/authorizationRules/Write|EventHub yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/eventhubs/authorizationRules/DELETE|İşlem toodelete EventHub yetkilendirme kuralları|
|/namespaces/eventhubs/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi tooEventHub Al|
|/namespaces/eventhubs/authorizationRules/regenerateKeys/Action|Merhaba birincil veya ikincil anahtarı toohello kaynak yeniden oluştur|
|/namespaces/diagnosticSettings/Read|Namespace tanılama ayarları kaynak açıklamaları listesini al|
|/namespaces/diagnosticSettings/Write|Namespace tanılama ayarları kaynak açıklamaları listesini al|
|/namespaces/logDefinitions/Read|Namespace günlükleri kaynak açıklamaları listesini al|

## <a name="microsoftfeatures"></a>Microsoft.Features

| İşlem | Açıklama |
|---|---|
|/providers/Features/Read|Belirtilen kaynak sağlayıcısındaki bir abonelik Hello özelliğini alır.|
|/providers/Features/Register/Action|Belirli kaynak sağlayıcısındaki bir abonelik Hello özelliğini kaydeder.|
|/Features/Read|Bir aboneliğin Hello özelliklerini alır.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| İşlem | Açıklama |
|---|---|
|/ kümeleri/yazma|Hdınsight kümesi güncelle|
|/Clusters/Read|Hdınsight kümesi hakkında bilgi almak|
|/Clusters/DELETE|Bir Hdınsight kümesi Sil|
|/Clusters/changerdpsetting/Action|Hdınsight kümesi RDP ayarını değiştirme|
|/Clusters/configurations/Action|Hdınsight küme yapılandırmasını güncelleştirme|
|/Clusters/configurations/Read|Hdınsight küme yapılandırmalarını alma|
|/Clusters/Roles/resize/Action|Bir Hdınsight kümesi yeniden boyutlandırma|
|/Locations/Capabilities/Read|Abonelik özelliklerini al|
|/Locations/checkNameAvailability/Read|Ad kullanılabilirliğini denetleme|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello içeri/dışarı aktarma kaynak sağlayıcısı için aboneliği kaydeder ve içeri/dışarı aktarma işleri hello oluşturulmasını sağlar.|
|/ işleri/yazma|Bir işin oluşturur hello belirtilen parametreleri veya hello özellikleri veya etiketleri hello belirtilen iş için güncelleştirin.|
|/Jobs/Read|Merhaba belirtilen proje için Hello özelliklerini alır veya hello işlerin listesini döndürür.|
|/Jobs/listBitLockerKeys/Action|Merhaba belirtilen iş için Hello BitLocker anahtarları alır.|
|/Jobs/DELETE|Var olan bir işi siler.|
|/Locations/Read|Merhaba özellikleri hello belirtilen konum veya verir hello listesi konumları için alır.|

## <a name="microsoftinsights"></a>Microsoft.ınsights

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba microsoft Öngörüler sağlayıcısını Kaydet|
|/ AlertRules/yazma|Yazma tooan uyarı kuralı yapılandırma|
|/ AlertRules/silme|Uyarı kuralı yapılandırması siliniyor|
|/ AlertRules/okuma|Uyarı kuralı yapılandırması okunuyor|
|/ AlertRules/etkinleştirilmiş/eylem|Uyarı kuralı etkinleştirildi|
|/ AlertRules/çözülmüş/eylem|Çözümlenen uyarı kuralı|
|/ AlertRules/kısıtlanan/eylem|Uyarı kuralı kısıtlanan|
|/ AlertRules/olaylar/okuma|Uyarı kuralı olayı yapılandırması okunuyor|
|/ MetricDefinitions/okuma|Ölçüm tanımlarını oku|
|/eventtypes/Values/Read|Yönetim olayı tür değerlerini oku|
|/eventtypes/digestevents/Read|Yönetim olayı türü özetini oku|
|/ Ölçümleri/okuma|Ölçümleri|
|/ LogProfiles/yazma|Tooa günlük profili yapılandırması yazma|
|/ LogProfiles/silme|Günlük profilleri yapılandırmasını silme|
|/ LogProfiles/okuma|Okuma günlük profilleri|
|/ AutoscaleSettings/yazma|Tooan otomatik ölçeklendirme ayarı yapılandırması yazma|
|/ AutoscaleSettings/silme|Otomatik ölçek ayarı yapılandırması siliniyor|
|/ AutoscaleSettings/okuma|Otomatik ölçek ayarı yapılandırması okunuyor|
|/ AutoscaleSettings/Scaleup/eylem|Otomatik Ölçek ölçeği artırma işlemi|
|/ AutoscaleSettings/Scaledown/eylem|Otomatik ölçeklendirme ölçek işlemi|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Ölçüm tanımlarını oku|
|/ ActivityLogAlerts/etkinleştirilmiş/eylem|Etkinlik günlüğü uyarı tetiklenen hello|
|/ DiagnosticSettings/yazma|Yazma toodiagnostic ayarlarını yapılandırma|
|/ DiagnosticSettings/silme|Tanılama ayarları yapılandırması siliniyor|
|/ DiagnosticSettings/okuma|Tanılama ayarları yapılandırmasını okuma|
|/ LogDefinitions/okuma|Okuma günlük tanımları|
|/ ExtendedDiagnosticSettings/yazma|Yazma tooextended tanılama ayarlarını yapılandırma|
|/ ExtendedDiagnosticSettings/silme|Genişletilmiş tanılama ayarlarını yapılandırması siliniyor|
|/ ExtendedDiagnosticSettings/okuma|Genişletilmiş tanılama ayarlarını yapılandırma okuma|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Bir aboneliği kaydeder|
|/checkNameAvailability/Read|Bir anahtar kasası adının geçerli ve kullanımda olup olmadığını denetler|
|/vaults/Read|Bir anahtar kasası hello özelliklerini görüntüleme|
|/ kasalar/yazma|Yeni bir anahtar kasası veya güncelleştirme hello özellikleri olan bir anahtar kasası oluşturma|
|/vaults/DELETE|Bir anahtar kasasını silme|
|/vaults/Deploy/Action|Azure kaynaklarını dağıtırken etkinleştirir toosecrets bir anahtar kasasına erişim|
|/vaults/Secrets/Read|Bir gizli anahtar, ancak kendi değer hello özellikleri görüntüle|
|/vaults/Secrets/Write|Yeni bir parola veya güncelleştirme hello değeri var olan bir gizli oluşturun|
|/vaults/accessPolicies/Write|Varolan bir erişim ilkesi birleştirme veya değiştirerek güncelleştirmek veya yeni bir erişim ilkesi tooa kasası ekleyin.|
|/deletedVaults/Read|Geçici silinen anahtar kasalarını hello özelliklerini görüntüleme|
|/Locations/operationResults/Read|Bir uzun çalışma işleminin onay hello sonucu|
|/Locations/deletedVaults/Read|Bir geçici silinen anahtar kasası hello özelliklerini görüntüleme|
|/Locations/deletedVaults/PURGE/Action|Bir geçici silinen anahtar kasası Temizle|

## <a name="microsoftlogic"></a>Microsoft.Logic

| İşlem | Açıklama |
|---|---|
|/workflows/Read|Merhaba iş akışını okur.|
|/ İş akışları/yazma|Oluşturur veya hello iş akışı güncelleştirir.|
|/workflows/DELETE|Merhaba iş akışı siler.|
|/workflows/Run/Action|Merhaba iş akışı bir farklı çalıştır başlatır.|
|/workflows/disable/Action|Merhaba iş akışını devre dışı bırakır.|
|/workflows/Enable/Action|Merhaba iş akışı sağlar.|
|/workflows/Validate/Action|Merhaba iş akışı doğrular.|
|/workflows/Move/Action|İş akışı, var olan abonelik kimliği, kaynak grubu ve/veya ad tooa farklı bir abonelik kimliği, kaynak grubu ve/veya ad taşır.|
|/workflows/listSwagger/Action|Merhaba iş akışı swagger tanımlarını alır.|
|/workflows/regenerateAccessKey/Action|Merhaba erişim anahtar parolaları yeniden oluşturur.|
|/workflows/listCallbackUrl/Action|Merhaba geri çağırma URL'si için iş akışı alır.|
|/workflows/Versions/Read|Merhaba iş akışı sürümü okur.|
|/workflows/Versions/Triggers/listCallbackUrl/Action|Merhaba geri çağırma URL'si için tetikleyici alır.|
|/ İş akışları/çalışan/okuma|Merhaba iş akışını çalıştırmak okur.|
|/workflows/Runs/Cancel/Action|Bir iş akışının Hello çalıştırma iptal eder.|
|/workflows/Runs/Actions/Read|Merhaba iş akışı eylemini çalıştırmak okur.|
|/workflows/Runs/Operations/Read|Merhaba iş akışı çalıştırılması işlem durumunu okur.|
|/workflows/Triggers/Read|Merhaba tetikleyici okur.|
|/workflows/Triggers/Run/Action|Merhaba tetikleyici yürütür.|
|/workflows/Triggers/listCallbackUrl/Action|Merhaba geri çağırma URL'si için tetikleyici alır.|
|/workflows/Triggers/histories/Read|Merhaba tetikleyici geçmişlerini okur.|
|/workflows/Triggers/histories/resubmit/Action|Merhaba iş akışı tetikleyici yeniden gönderir.|
|/workflows/accessKeys/Read|Merhaba erişim tuşu okur.|
|/workflows/accessKeys/Write|Merhaba erişim anahtarını güncelleştirir veya oluşturur.|
|/workflows/accessKeys/DELETE|Merhaba erişim anahtarı siler.|
|/workflows/accessKeys/List/Action|Merhaba erişim anahtarı gizli anahtarları listeler.|
|/workflows/accessKeys/Regenerate/Action|Merhaba erişim anahtar parolaları yeniden oluşturur.|
|/Locations/workflows/Validate/Action|Merhaba iş akışı doğrular.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello machine learning web hizmeti kaynak sağlayıcısı için aboneliği kaydeder ve web hizmetleri hello oluşturulmasını sağlar.|
|/ Webservices'a/eylem|Desteklenen bölgeler için bölgesel Web hizmeti özellikleri oluşturma|
|/commitmentPlans/Read|Taahhüt Plan öğrenme herhangi bir makineye okuma|
|/ commitmentPlans/yazma|Herhangi bir Machine Learning taahhüt planının güncelle|
|/commitmentPlans/DELETE|Taahhüt Plan öğrenme herhangi bir makineye Sil|
|/commitmentPlans/Join/Action|Taahhüt Plan öğrenme herhangi bir makineye katılma|
|/commitmentPlans/commitmentAssociations/Read|Taahhüt Plan ilişkilendirme öğrenme herhangi bir makineye okuma|
|/commitmentPlans/commitmentAssociations/Move/Action|Taahhüt Plan ilişkilendirme öğrenme herhangi bir makineye taşıma|
|/ Workspaces/okuma|Çalışma alanı öğrenme herhangi bir makineye okuma|
|/ Workspaces/yazma|Çalışma alanı öğrenme makine oluşturulamıyor veya güncelleştirilemiyor|
|/ Workspaces/silme|Bir Machine Learning çalışma alanı silme|
|/ Workspaces/listworkspacekeys/eylem|Bir Machine Learning çalışma alanı listesi tuşları|
|/ Workspaces/resyncstoragekeys/eylem|Machine Learning çalışma alanı için yapılandırılan depolama hesabı anahtarlarını yeniden eşitleme|
|/webServices/Read|Bir Machine Learning Web hizmeti okuma|
|/ Webservices'a/yazma|Bir Machine Learning Web hizmeti güncelle|
|/webServices/DELETE|Bir Machine Learning Web hizmeti Sil|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| İşlem | Açıklama |
|---|---|
|/agreements/Offers/plans/Read|Verilen Market öğesi için bir anlaşma Döndür|
|/agreements/Offers/plans/Sign/Action|Bir anlaşma verilen Market öğesi için oturum açın|
|/agreements/Offers/plans/Cancel/Action|Verilen Market öğesi için bir sözleşmeyi iptal et|

## <a name="microsoftmedia"></a>Microsoft.Media

| İşlem | Açıklama |
|---|---|
|/mediaservices/Read||
|/ mediaservices/yazma||
|/mediaservices/DELETE||
|/mediaservices/regenerateKey/Action||
|/mediaservices/listKeys/Action||
|/mediaservices/syncStorageKeys/Action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba aboneliği kaydeder|
|/ kaydı/eylem|Merhaba abonelik kaydını siler|
|/ checkTrafficManagerNameAvailability/eylem|Trafik Yöneticisi göreli DNS adı Hello kullanılabilirliğini denetler.|
|/dnszones/Read|JSON biçiminde Hello DNS bölgesini alın. Etiketler, etag, numberOfRecordSets ve maxNumberOfRecordSets Hello bölge özellikleri içerir. Bu komut hello bölge içindeki kayıt kümelerini hello almıyorsa unutmayın.|
|/ dnszones/yazma|Oluşturun veya bir kaynak grubunda DNS bölgesi güncelleştirin.  Bir DNS bölgesi kaynağındaki kullanılan tooupdate hello etiketler. Bu komut kullanılan toocreate veya güncelleştirme kayıt kümelerini hello bölgedeki olamaz unutmayın.|
|/dnszones/DELETE|JSON biçiminde Hello DNS bölgesini silin. Etiketler, etag, numberOfRecordSets ve maxNumberOfRecordSets Hello bölge özellikleri içerir.|
|/dnszones/MX/Read|'MX' Hello türündeki kayıt kümesini JSON biçiminde alın. Hello kayıt kümesi TTL hello yanı sıra kayıtların listesini, etiketleri ve etag'i içerir.|
|/dnszones/MX/Write|Oluşturun veya bir DNS bölgesi içinde 'MX' türündeki bir kayıt kümesini güncelleştirin. Belirtilen hello hello kayıt kümesindeki geçerli kayıt hello kayıtlarla değiştirilir.|
|/dnszones/MX/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' MX' yazın.|
|/dnszones/NS/Read|DNS NS türündeki kayıt kümesini alır|
|/dnszones/NS/Write|Oluşturur veya DNS NS türündeki kayıt kümesini güncelleştirir|
|/dnszones/NS/DELETE|Merhaba DNS NS türündeki kayıt kümesini siler|
|/dnszones/AAAA/Read|'AAAA' Hello türündeki kayıt kümesini JSON biçiminde alın. Hello kayıt kümesi TTL hello yanı sıra kayıtların listesini, etiketleri ve etag'i içerir.|
|/dnszones/AAAA/Write|Oluşturun veya bir DNS bölgesi içinde 'AAAA' türündeki bir kayıt kümesini güncelleştirin. Belirtilen hello hello kayıt kümesindeki geçerli kayıt hello kayıtlarla değiştirilir.|
|/dnszones/AAAA/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' AAAA' yazın.|
|/dnszones/CNAME/Read|'CNAME' Hello türündeki kayıt kümesini JSON biçiminde alın. Merhaba kayıt kümesi hello TTL, etiketler ve etag'in içerir.|
|/dnszones/CNAME/Write|Oluşturun veya bir DNS bölgesi içinde 'CNAME' türündeki bir kayıt kümesini güncelleştirin. Belirtilen hello hello kayıt kümesindeki geçerli kayıt hello kayıtlarla değiştirilir.|
|/dnszones/CNAME/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' CNAME' yazın.|
|/dnszones/SOA/Read|DNS SOA türündeki kayıt kümesini alır|
|/dnszones/SOA/Write|Oluşturur veya DNS SOA türündeki kayıt kümesini güncelleştirir|
|/dnszones/SRV/Read|'SRV' Hello türündeki kayıt kümesini JSON biçiminde alın. Hello kayıt kümesi TTL hello yanı sıra kayıtların listesini, etiketleri ve etag'i içerir.|
|/dnszones/SRV/Write|SRV türündeki kayıt kümesini oluştur veya güncelleştir|
|/dnszones/SRV/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' SRV' yazın.|
|/dnszones/PTR/Read|'PTR' Hello türündeki kayıt kümesini JSON biçiminde alın. Hello kayıt kümesi TTL hello yanı sıra kayıtların listesini, etiketleri ve etag'i içerir.|
|/dnszones/PTR/Write|Oluşturun veya bir DNS bölgesi içinde 'PTR' türündeki bir kayıt kümesini güncelleştirin. Belirtilen hello hello kayıt kümesindeki geçerli kayıt hello kayıtlarla değiştirilir.|
|/dnszones/PTR/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' PTR' yazın.|
|/dnszones/A/Read|Merhaba 'A' türündeki kayıt kümesini JSON biçiminde alın. Hello kayıt kümesi TTL hello yanı sıra kayıtların listesini, etiketleri ve etag'i içerir.|
|/dnszones/A/Write|Oluşturun veya bir DNS bölgesi içinde 'A' türündeki bir kayıt kümesini güncelleştirin. Belirtilen hello hello kayıt kümesindeki geçerli kayıt hello kayıtlarla değiştirilir.|
|/dnszones/A/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' A' yazın.|
|/dnszones/txt/Read|'TXT' Hello türündeki kayıt kümesini JSON biçiminde alın. Hello kayıt kümesi TTL hello yanı sıra kayıtların listesini, etiketleri ve etag'i içerir.|
|/dnszones/txt/Write|Oluşturun veya bir DNS bölgesi içinde 'TXT' türündeki bir kayıt kümesini güncelleştirin. Belirtilen hello hello kayıt kümesindeki geçerli kayıt hello kayıtlarla değiştirilir.|
|/dnszones/txt/DELETE|Verilen ada Hello kayıt kümesini kaldırın ve DNS bölgesinden ' TXT' yazın.|
|/dnszones/Recordsets/Read|DNS kayıt kümelerini türleri arasında alır|
|/networkInterfaces/Read|Ağ arabirimi tanımını alır. |
|/ networkInterfaces/yazma|Bir ağ arabirimi oluşturur veya mevcut bir ağ arabirimini güncelleştirir. |
|/networkInterfaces/Join/Action|Bir sanal makine tooa ağ arabirimiyle birleştirir|
|/networkInterfaces/DELETE|Bir ağ arabirimi siler|
|/networkInterfaces/effectiveRouteTable/Action|Yol tablosu hello Vm ağ arabiriminde yapılandırılan Al|
|/networkInterfaces/effectiveNetworkSecurityGroups/Action|Ağ güvenlik grupları yapılandırılmış üzerinde ağ arabirimi, hello Vm Al|
|/networkInterfaces/loadBalancers/Read|Alır ağ arabirimi hello tüm hello yük dengeleyicileri parçasıdır|
|/networkInterfaces/ipconfigurations/Read|Ağ arabirimi IP yapılandırması tanımını alır. |
|/publicIPAddresses/Read|Bir genel ip adresi tanımını alır.|
|/ Publicıpaddresses/yazma|Bir ortak IP adresi oluşturur veya mevcut bir ortak IP adresini güncelleştirir. |
|/publicIPAddresses/DELETE|Bir ortak IP adresini siler.|
|/publicIPAddresses/Join/Action|Bir genel ip adresine katılır|
|/routeFilters/Read|Bir rota filtre tanımını alır|
|/routeFilters/Join/Action|Bir rota filtre birleştirir|
|/routeFilters/DELETE|Bir rota filtre tanımını siler|
|/ routeFilters/yazma|Bir rota filtre oluşturur veya varolan bir yol filtreyi güncelleştirir|
|/routeFilters/Rules/Read|Bir rota filtre kuralı tanımını alır|
|/routeFilters/Rules/Write|Bir rota filtre kuralı oluşturur veya mevcut bir rota filtre kuralını güncelleştirir|
|/routeFilters/Rules/DELETE|Bir rota filtre kuralı tanımını siler|
|/networkWatchers/Read|Merhaba Ağ İzleyicisi tanımını Al|
|/ networkWatchers/yazma|Ağ İzleyicisi oluşturur veya mevcut bir Ağ İzleyicisi'ni güncelleştirir|
|/networkWatchers/DELETE|Ağ İzleyicisi siler|
|/networkWatchers/configureFlowLog/Action|Akış günlüğü hedef kaynak için yapılandırır.|
|/networkWatchers/ipFlowVerify/Action|Merhaba paket izin verilen veya belirli bir hedef tooor reddedildi döndürür.|
|/networkWatchers/nextHop/Action|Belirtilen hedef ve hedef IP adresi, hello sonraki atlama türü dönün ve sonraki IP adresi umuyoruz.|
|/networkWatchers/queryFlowLogStatus/Action|Bir kaynak günlüğü akış Hello durumunu alır.|
|/networkWatchers/queryTroubleshootResult/Action|Daha önce hello veya sorun giderme işlemi şu anda çalışan sonucundan sorun giderme hello alır.|
|/networkWatchers/securityGroupView/Action|Yapılandırılmış hello ve etkili ağ güvenlik grubu kurallarının bir VM üzerinde uygulanan görüntüleyin.|
|/networkWatchers/topology/Action|Ağ düzeyinde görünümünü kaynakları ve ilişkilerini bir kaynak grubunda alır.|
|/networkWatchers/Troubleshoot/Action|Bir ağ kaynağına Azure sorun giderme başlar.|
|/networkWatchers/packetCaptures/queryStatus/Action|Özellikleri ve paket yakalama kaynak durumu hakkındaki bilgileri alır.|
|/networkWatchers/packetCaptures/Stop/Action|Paket yakalama oturumu çalıştıran hello durdurun.|
|/networkWatchers/packetCaptures/Read|Merhaba paket yakalama tanımını Al|
|/networkWatchers/packetCaptures/Write|Paket yakalama oluşturur|
|/networkWatchers/packetCaptures/DELETE|Paket yakalama siler|
|/loadBalancers/Read|Yük Dengeleyici tanımını alır|
|/ loadBalancers/yazma|Bir yük dengeleyici oluşturur veya mevcut bir Yük Dengeleyiciyi güncelleştirir|
|/loadBalancers/DELETE|Bir yük dengeleyici siler|
|/loadBalancers/networkInterfaces/Read|Bir yük dengeleyici altındaki tooall hello ağ arabirimlerine başvuruları alır|
|/loadBalancers/loadBalancingRules/Read|Yük Dengeleyici Yük Dengeleme kuralı tanımını alır|
|/loadBalancers/backendAddressPools/Read|Yük Dengeleyici arka uç adres havuzu tanımını alır|
|/loadBalancers/backendAddressPools/Join/Action|Bir yük dengeleyici arka uç adres havuzuna katılır|
|/loadBalancers/inboundNatPools/Read|Bir yük dengeleyici alır gelen nat havuzu tanımını|
|/loadBalancers/inboundNatPools/Join/Action|Katıldığı bir yük dengeleyici gelen nat havuzu|
|/loadBalancers/inboundNatRules/Read|Bir yük dengeleyici alır gelen nat kuralı tanımını|
|/loadBalancers/inboundNatRules/Write|Yük Dengeleyici gelen nat kuralı oluşturur veya mevcut bir yük dengeleyici gelen nat kuralını güncelleştirir|
|/loadBalancers/inboundNatRules/DELETE|Yük Dengeleyici gelen nat kuralını siler|
|/loadBalancers/inboundNatRules/Join/Action|Bir yük dengeleyici gelen nat kuralına katılır|
|/loadBalancers/outboundNatRules/Read|Yük Dengeleyici giden nat kuralı tanımını alır|
|/loadBalancers/probes/Read|Yük Dengeleyici araştırmasını alır|
|/loadBalancers/virtualMachines/Read|Bir yük dengeleyici altındaki tooall hello sanal makineleri başvuruları alır|
|/loadBalancers/frontendIPConfigurations/Read|Yük Dengeleyici ön uç IP yapılandırması tanımını alır|
|/trafficManagerGeographicHierarchies/Read|Merhaba trafik Yöneticisi Geographic hiyerarşisi coğrafi trafik yönlendirme yöntemini hello ile kullanılabilen bölgeler içeren alır|
|/bgpServiceCommunities/Read|BGP hizmet toplulukları Al|
|/applicationGatewayAvailableWafRuleSets/Read|Uygulama ağ geçidi kullanılabilir Waf kural kümesi alır|
|/virtualNetworks/Read|Merhaba sanal ağ tanımını Al|
|/ virtualNetworks/yazma|Bir sanal ağ oluşturur veya mevcut bir sanal ağı güncelleştirir|
|/virtualNetworks/DELETE|Bir sanal ağ siler|
|/virtualNetworks/Peer/Action|Başka bir sanal ağ ile sanal ağ eşleri|
|/virtualNetworks/virtualNetworkPeerings/Read|Sanal ağ eşleme tanımını alır|
|/virtualNetworks/virtualNetworkPeerings/Write|Bir sanal ağ eşlemesi oluşturur veya mevcut bir sanal ağ eşlemesi güncelleştirir|
|/virtualNetworks/virtualNetworkPeerings/DELETE|Bir sanal ağ eşlemesi siler|
|/virtualNetworks/Subnets/Read|Bir sanal ağ alt ağı tanımını alır|
|/virtualNetworks/Subnets/Write|Bir sanal ağ alt ağı oluşturur veya varolan bir sanal ağ alt ağı güncelleştirir|
|/virtualNetworks/Subnets/DELETE|Bir sanal ağ alt ağını siler|
|/virtualNetworks/Subnets/Join/Action|Bir sanal ağ birleştirir|
|/virtualNetworks/Subnets/joinViaServiceTunnel/Action|Depolama hesabı veya SQL veritabanı tooa etkin hizmet tünel alt ağ olarak kaynak birleştirir.|
|/virtualNetworks/Subnets/virtualMachines/Read|Bir sanal ağ alt ağında tooall hello sanal makinelere başvuruları alır|
|/virtualNetworks/checkIpAddressAvailability/Read|IP adresi hello belirtilen sanal ağda kullanılabilir olup olmadığını denetleyin|
|/virtualNetworks/virtualMachines/Read|Sanal bir ağa tooall hello sanal makinelere başvuruları alır|
|/expressRouteServiceProviders/Read|Hızlı rota hizmeti sağlayıcılarını alır|
|/dnsoperationresults/Read|DNS İşlem sonuçlarını alır|
|/localnetworkgateways/Read|LocalNetworkGateway alır|
|/ localnetworkgateways/yazma|Oluşturur veya mevcut bir LocalNetworkGateway güncelleştirir|
|/localnetworkgateways/DELETE|LocalNetworkGateway siler|
|/trafficManagerProfiles/Read|Merhaba trafik Yöneticisi Profil yapılandırmasını alın. Bu, DNS ayarlarını, trafik yönlendirme ayarlarını, uç nokta izleme ayarlarını ve hello Bu trafik Yöneticisi profili tarafından yönlendirilen uç noktaların listesini içerir.|
|/ trafficManagerProfiles/yazma|Trafik Yöneticisi profili oluşturun veya var olan bir Traffic Manager profilini hello yapılandırmasını değiştirin. Bu, etkinleştirme veya bir profili devre dışı bırakma ve DNS ayarlarını, trafik yönlendirme ayarlarını veya uç nokta izleme ayarlarını değiştirme içerir. Merhaba trafik Yöneticisi profili tarafından yönlendirilen uç noktaların eklenen, etkin devre dışı veya kaldırılabilir.|
|/trafficManagerProfiles/DELETE|Merhaba trafik Yöneticisi profilini silin. Trafik Yöneticisi profili Hello ile ilişkili tüm ayarlar kaybedilir ve hello profil artık olabilir tooroute trafiği kullanılır.|
|/dnsoperationstatuses/Read|Bir DNS işlemin durumunu alır |
|/Operations/Read|Kullanılabilir işlemleri Al|
|/expressRouteCircuits/Read|Bir ExpressRouteCircuit Al|
|/ expressRouteCircuits/yazma|Oluşturur veya mevcut bir ExpressRouteCircuit güncelleştirir|
|/expressRouteCircuits/DELETE|Bir ExpressRouteCircuit siler|
|/expressRouteCircuits/stats/Read|Bir ExpressRouteCircuit Stat alır|
|/expressRouteCircuits/peerings/Read|Bir ExpressRouteCircuit eşliği alır|
|/expressRouteCircuits/peerings/Write|Oluşturur veya mevcut bir eşleme ExpressRouteCircuit güncelleştirir|
|/expressRouteCircuits/peerings/DELETE|Bir ExpressRouteCircuit eşliği siler|
|/expressRouteCircuits/peerings/arpTables/Action|Bir ExpressRouteCircuit eşliği ArpTable alır|
|/expressRouteCircuits/peerings/routeTables/Action|Bir ExpressRouteCircuit eşliği RouteTable alır|
|/expressRouteCircuits/eşlemeler /<br>routeTablesSummary/eylem|Bir ExpressRouteCircuit eşliği RouteTable özeti alır|
|/expressRouteCircuits/peerings/stats/Read|Bir ExpressRouteCircuit çubuklu eşliği alır|
|/expressRouteCircuits/authorizations/Read|ExpressRouteCircuit yetkilendirme alır|
|/expressRouteCircuits/authorizations/Write|Oluşturur veya mevcut bir ExpressRouteCircuit yetkilendirme güncelleştirir|
|/expressRouteCircuits/authorizations/DELETE|ExpressRouteCircuit yetkilendirme siler|
|/Connections/Read|ConnectionType(hypernet/routebased) türündeki VirtualNetworkGatewayConnection alır|
|/ bağlantıları/yazma|Oluşturur veya mevcut bir ConnectionType(hypernet/routebased) türündeki VirtualNetworkGatewayConnection güncelleştirir|
|/Connections/DELETE|ConnectionType(hypernet/routebased) türündeki VirtualNetworkGatewayConnection siler|
|/Connections/sharedKey/Read|ConnectionType(hypernet/routebased) türündeki VirtualNetworkGatewayConnection SharedKey alır|
|/Connections/sharedKey/Write|Oluşturur veya mevcut bir ConnectionType(hypernet/routebased) türündeki VirtualNetworkGatewayConnection SharedKey güncelleştirir|
|/networkSecurityGroups/Read|Ağ güvenlik grubu tanımını alır|
|/ networkSecurityGroups/yazma|Bir ağ güvenlik grubu oluşturur veya mevcut bir ağ güvenlik grubunu güncelleştirir|
|/networkSecurityGroups/DELETE|Ağ güvenlik grubunu siler|
|/networkSecurityGroups/Join/Action|Ağ güvenlik grubuna katılır|
|/networkSecurityGroups/defaultSecurityRules/Read|Varsayılan güvenlik kuralı tanımını alır|
|/networkSecurityGroups/securityRules/Read|Güvenlik kuralı tanımını alır|
|/networkSecurityGroups/securityRules/Write|Bir güvenlik kuralı oluşturur veya mevcut bir güvenlik kuralını güncelleştirir|
|/networkSecurityGroups/securityRules/DELETE|Bir güvenlik kuralını siler|
|/applicationGateways/Read|Bir uygulama ağ geçidini alır|
|/ applicationGateways/yazma|Bir uygulama ağ geçidi oluşturur veya bir uygulama ağ geçidini güncelleştirir|
|/applicationGateways/DELETE|Bir uygulama ağ geçidini siler|
|/applicationGateways/backendhealth/Action|Bir uygulama ağ geçidi arka uç durumunu alır|
|/applicationGateways/Start/Action|Bir uygulama ağ geçidi başlatır|
|/applicationGateways/Stop/Action|Bir uygulama ağ geçidi durdurur|
|/applicationGateways/backendAddressPools/Join/Action|Bir uygulama ağ geçidi arka uç adres havuzuna katılır|
|/routeTables/Read|Yol tablosu tanımını alır|
|/ routeTables/yazma|Bir yol tablosu oluşturur veya mevcut bir yol tablosunu güncelleştirir|
|/routeTables/DELETE|Yol tablosu tanımını siler|
|/routeTables/Join/Action|Bir yol tablosu birleştirir|
|/routeTables/Routes/Read|Bir rota tanımını alır|
|/routeTables/Routes/Write|Bir yol oluşturur veya mevcut bir yolu güncelleştirir|
|/routeTables/Routes/DELETE|Bir rota tanımını siler|
|/Locations/operationResults/Read|Bir zaman uyumsuz POST veya DELETE işleminin işlem sonucunu alır|
|/Locations/checkDnsNameAvailability/Read|Merhaba DNS etiketi yoksa denetimleri konumu belirtilen|
|/Locations/usages/Read|Merhaba kaynak kullanımı ölçümlerini alır|
|/Locations/Operations/Read|Zaman uyumsuz bir işlemin durumunu gösteren işlem kaynağını alır|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello NotifciationHubs kaynak sağlayıcısı için aboneliği kaydeder ve ad alanları ve NotificationHubs hello oluşturulmasını sağlar|
|/ CheckNamespaceAvailability/eylem|Verilen Namespace kaynak adı NotificationHub hizmet hello içinde kullanılabilir olup olmadığını denetler.|
|/ Ad alanları/yazma|Namespace kaynak oluşturun ve özelliklerini güncelleştirin. Etiketleri ve hello Namespace durumunu, güncelleştirilebilir hello özelliklerdir.|
|/ Ad alanları/okuma|Namespace kaynak açıklaması Hello listesini al|
|/ Ad alanları/silme|Namespace kaynağı silme|
|/ Ad alanları/authorizationRules/eylem|Ad alanları yetkilendirme kuralları açıklama Hello listesini alın.|
|/ Ad alanları/CheckNotificationHubAvailability/eylem|Belirli bir NotificationHub adının bir Ad Alanı içinde kullanılabilir olup olmadığını denetler.|
|/ Ad alanları/authorizationRules/yazma|Namespace düzeyi yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/ Ad alanları/authorizationRules/okuma|Ad alanları yetkilendirme kuralları açıklama Hello listesini alın.|
|/ Ad alanları/authorizationRules/silme|Namespace yetkilendirme kuralını silin. Merhaba varsayılan Namespace yetkilendirme kuralı silinemez. |
|/ Ad alanları/authorizationRules/listkeys/eylem|Merhaba bağlantı dizesi toohello Namespace Al|
|/ Ad alanları/authorizationRules/regenerateKeys/eylem|Namespace yetkilendirme kuralı yeniden birincil/SecondaryKey, belirt hello toobe gereken anahtar yeniden oluşturuldu|
|/ Ad alanları/NotificationHubs/yazma|Bildirim hub'ı oluşturun ve özelliklerini güncelleştirin. Özelliklerini çoğunlukla PNS kimlik bilgilerini içerir. Yetkilendirme kuralları ve TTL|
|/ Ad alanları/NotificationHubs/okuma|Notification Hub Kaynak Açıklamalarının listesini alın|
|/ Ad alanları/NotificationHubs/silme|Bildirim hub'ı kaynağı silme|
|/ Ad alanları/NotificationHubs/authorizationRules/eylem|Bildirim hub'ı yetkilendirme kuralları Hello listesini al|
|/ Ad alanları/NotificationHubs/pnsCredentials/eylem|Tüm bildirim hub'ı PNS kimlik bilgilerini alın. Bu içerir, WNS, MPNS, APNS, GCM ve Baidu kimlik bilgileri|
|/ Ad alanları/NotificationHubs/debugSend/eylem|Test amaçlı bir anında iletme bildirimi gönderin.|
|/ Ad alanları/NotificationHubs/metricDefinitions/okuma|Namespace ölçümleri kaynak açıklamaları listesini al|
|/Namespaces/NotificationHubs /<br>authorizationRules/yazma|Bildirim hub'ı yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/Namespaces/NotificationHubs /<br>authorizationRules/okuma|Bildirim hub'ı yetkilendirme kuralları Hello listesini al|
|/Namespaces/NotificationHubs /<br>authorizationRules/silme|NotificationHub Yetkilendirme Kurallarını Sil|
|/Namespaces/NotificationHubs /<br>listkeys/authorizationRules/eylem|Merhaba bağlantı dizesi toohello bildirim hub'ı alın|
|/Namespaces/NotificationHubs /<br>regenerateKeys/authorizationRules/eylem|Bildirim hub'ı yetkilendirme kuralı yeniden birincil/SecondaryKey, belirt hello toobe gereken anahtar yeniden oluşturuldu|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Bir abonelik tooa kaynak sağlayıcısı kaydedin.|
|/linkTargets/Read|Bir Azure aboneliği ile ilişkili olmayan var olan hesapları listeler. toolink bu Azure aboneliği tooa çalışma alanı, kullanımı, bir müşteri kimliği özelliğinde hello Müşteri Kimliği hello çalışma alanı oluşturma işlemi bu işlem tarafından döndürülen.|
|/ workspaces/yazma|Yeni çalışma alanında ya da bağlantılar tooan mevcut çalışma hello Müşteri Kimliği hello varolan çalışma alanından sağlayarak oluşturur.|
|/Workspaces/Read|Var olan bir çalışma alır|
|/Workspaces/DELETE|Bir çalışma alanı siler. Merhaba çalışma bağlanmışsa sonra oluşturulma zamanında mevcut çalışma tooan silinmez bağlantılı toois olduğu çalışma hello.|
|/Workspaces/generateregistrationcertificate/Action|Kayıt sertifikası için hello çalışma alanı oluşturur. Bu sertifika kullanılan tooconnect Microsoft System Center Operation Manager toohello çalışma alanıdır.|
|/Workspaces/sharedKeys/Action|Merhaba çalışma alanı için paylaşılan hello anahtarları alır. Bu anahtarları kullanılan tooconnect Microsoft operasyonel Öngörüler aracıları toohello çalışma ' dir.|
|/Workspaces/Search/Action|Bir arama sorgusunu çalıştırır|
|/Workspaces/Datasources/Read|Veri kaynakları bir çalışma alanı altında alın.|
|/Workspaces/Datasources/Write|Veri kaynakları çalışma alanı altında oluştur/güncelleştir.|
|/Workspaces/Datasources/DELETE|Çalışma alanı altında veri kaynakları silin.|
|/Workspaces/managementGroups/Read|Merhaba adları ve meta verileri için System Center Operations Manager Yönetim grupları bağlı toothis çalışma alır.|
|/Workspaces/Schema/Read|Merhaba arama şeması için hello çalışma alır.  Arama şeması kullanıma sunulan hello alanları ve bunların türlerini içerir.|
|/Workspaces/usages/Read|Merhaba çalışma alanı tarafından okunan veriler hello miktarı dahil olmak üzere bir çalışma alanı için kullanım verilerini alır.|
|/Workspaces/intelligencepacks/Read|Verilen worksapce için görünür olan tüm Intelligence paketlerini listeler ve hello paketi etkin veya bu çalışma alanı için devre dışı olup olmadığını da listeler.|
|/Workspaces/intelligencepacks/Enable/Action|Belirli bir çalışma alanı için bir destek paketi sağlar.|
|/Workspaces/intelligencepacks/disable/Action|Belirli bir çalışma alanı için bir destek paketi devre dışı bırakır.|
|/Workspaces/sharedKeys/Read|Merhaba çalışma alanı için paylaşılan hello anahtarları alır. Bu anahtarları kullanılan tooconnect Microsoft operasyonel Öngörüler aracıları toohello çalışma ' dir.|
|/Workspaces/savedSearches/Read|Kaydedilmiş bir arama sorgusunu alır|
|/Workspaces/savedSearches/Write|Kaydedilmiş bir arama sorgusunu oluşturur|
|/Workspaces/savedSearches/DELETE|Kaydedilmiş bir arama sorgusunu siler|
|/Workspaces/storageinsightconfigs/Write|Yeni depolama yapılandırması oluşturur. Bu yapılandırmalar, mevcut bir depolama hesabını konumundan kullanılan toopull verilerdir.|
|/Workspaces/storageinsightconfigs/Read|Bir depolama yapılandırmasını alır.|
|/Workspaces/storageinsightconfigs/DELETE|Bir depolama yapılandırması siler. Bu, Microsoft operasyonel Öngörüler'hello depolama hesabından veri okuma durdurur.|
|/Workspaces/configurationScopes/Read|Yapılandırma kapsam Al|
|/Workspaces/configurationScopes/Write|Yapılandırma kapsamını ayarlama|
|/Workspaces/configurationScopes/DELETE|Yapılandırma kapsamını Sil|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Bir abonelik tooa kaynak sağlayıcısı kaydedin.|
|/ solutions/yazma|Yeni bir OMS çözümü oluşturun|
|/Solutions/Read|OMS çözüm çıkma Al|
|/Solutions/DELETE|Varolan bir OMS çözümü Sil|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| İşlem | Açıklama |
|---|---|
|/ Kasalar/backupJobsExport/eylem|Dışarı aktarma işleri|
|/ Kasalar/yazma|Kasa Oluştur işlemi, 'vault' türünde bir Azure kaynağı oluşturur|
|/ Kasalar/okuma|Merhaba kasası alma işlemi hello Azure kaynak türü 'Kasası' temsil eden bir nesneyi alır|
|/ Kasalar/silme|Azure kaynak türü 'Kasası' Hello kasa silme işlemi siler hello belirtildi|
|/ Kasalar/refreshContainers/okuma|Merhaba kapsayıcı listesini yeniler|
|/ Kasalar/backupJobsExport/operationResults/okuma|Döndürür hello dışarı aktarma işi işleminin sonucu.|
|/ Kasalar/backupOperationResults/okuma|Kurtarma Hizmetleri Kasası için Yedekleme işleminin Sonucunu döndürür.|
|/ Kasalar/monitoringAlerts/okuma|Merhaba uyarıları hello kurtarma Hizmetleri kasası için alır.|
|/Vaults/monitoringAlerts / {uniqueAlertId} / okuma|Merhaba hello uyarı ayrıntılarını alır.|
|/ Kasalar/backupSecurityPIN/okuma|Güvenlik PIN döndürür bilgi kurtarma Hizmetleri kasası.|
|/vaults/replicationEvents/Read|Tüm olayları okuma|
|/ Kasalar/backupProtectableItems/okuma|Tüm Korunabilir Öğelerin listesini döndürür.|
|/vaults/replicationFabrics/Read|Tüm yapıları okuma|
|/vaults/replicationFabrics/Write|Tüm yapıları güncelle|
|/vaults/replicationFabrics/Remove/Action|Doku Kaldır|
|/vaults/replicationFabrics/checkConsistency/Action|Merhaba doku tutarlılık denetimleri|
|/vaults/replicationFabrics/DELETE|Tüm yapıları sil|
|/vaults/replicationFabrics/renewcertificate/Action||
|/vaults/replicationFabrics/deployProcessServerImage/Action|İşlem sunucusu görüntüsünü Dağıt|
|/vaults/replicationFabrics/reassociateGateway/Action|Ağ geçidi yeniden ilişkilendirin|
|/ kasalar/replicationFabrics/replicationRecoveryServicesProviders /<br>Okuma|Tüm kurtarma Hizmetleri sağlayıcılarını okuma|
|/ kasalar/replicationFabrics/replicationRecoveryServicesProviders /<br>kaldırma/eylem|Kurtarma Hizmetleri sağlayıcısını Kaldır|
|/ kasalar/replicationFabrics/replicationRecoveryServicesProviders /<br>Sil|Tüm kurtarma Hizmetleri sağlayıcılarını Sil|
|/ kasalar/replicationFabrics/replicationRecoveryServicesProviders /<br>refreshProvider/eylem|Sağlayıcı Yenile|
|/vaults/replicationFabrics/replicationStorageClassifications/Read|Tüm depolama sınıflandırmaları okuma|
|/ kasalar/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/okuma|Tüm depolama sınıflandırması eşlemeleri okuma|
|/ kasalar/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/yazma|Tüm depolama sınıflandırması eşlemeleri güncelle|
|/ kasalar/replicationFabrics/replicationStorageClassifications /<br>replicationStorageClassificationMappings/silme|Tüm depolama sınıflandırması eşlemeleri silme|
|/vaults/replicationFabrics/replicationvCenters/Read|Herhangi bir işi okuma|
|/vaults/replicationFabrics/replicationvCenters/Write|Tüm işleri oluşturun veya güncelleştirin|
|/vaults/replicationFabrics/replicationvCenters/DELETE|Herhangi bir işi Sil|
|/vaults/replicationFabrics/replicationNetworks/Read|Herhangi bir ağa okuma|
|/ kasalar/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/okuma|Tüm ağ eşlemeleri okuma|
|/ kasalar/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/yazma|Tüm ağ eşlemeleri güncelle|
|/ kasalar/replicationFabrics/replicationNetworks /<br>replicationNetworkMappings/silme|Tüm ağ eşlemeleri silme|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>Okuma|Herhangi bir koruma kapsayıcıdaki okuma|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>discoverProtectableItem/eylem|Korunabilir öğe Bul|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>yazma|Herhangi bir koruma kapsayıcıdaki güncelle|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>kaldırma/eylem|Koruma kapsayıcısı Kaldır|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>switchprotection/eylem|Anahtar koruma kapsayıcısı|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectableItems/okuma|Korunabilir tüm öğeleri okuma|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/okuma|Koruma kapsayıcısı eşlemeleri okuma|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/yazma|Koruma kapsayıcısı eşlemeleri güncelle|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>kaldırma/replicationProtectionContainerMappings/eylem|Koruma kapsayıcısı eşlemesini Kaldır|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectionContainerMappings/silme|Koruma kapsayıcısı eşlemeleri silme|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/okuma|Tüm korumalı öğeleri okuma|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/yazma|Tüm korumalı maddeleri oluştur veya güncelleştir|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/silme|Korunan öğeleri silin|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>kaldırma/replicationProtectedItems/eylem|Korumalı öğe kaldırma|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>plannedFailover/replicationProtectedItems/eylem|Planlanan yük devretme|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>unplannedFailover/replicationProtectedItems/eylem|Yük devretme|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>testFailover/replicationProtectedItems/eylem|Yük devretme sınaması|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>testFailoverCleanup/replicationProtectedItems/eylem|Yük devretme sınaması temizliğini|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>failoverCommit/replicationProtectedItems/eylem|Yük devretmenin yürütülmesi|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>yeniden koruma/replicationProtectedItems/eylem|Korumalı öğe koruyun|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>updateMobilityService/replicationProtectedItems/eylem|Mobility hizmeti güncelleştirmesi|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>repairReplication/replicationProtectedItems/eylem|Onarım çoğaltma|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>applyRecoveryPoint/replicationProtectedItems/eylem|Kurtarma noktası Uygula|
|/ kasalar/replicationFabrics/replicationProtectionContainers /<br>replicationProtectedItems/recoveryPoints/okuma|Bir çoğaltma kurtarma noktası okuma|
|/vaults/replicationPolicies/Read|Tüm ilkeleri okuma|
|/vaults/replicationPolicies/Write|Tüm ilkeler güncelle|
|/vaults/replicationPolicies/DELETE|Herhangi bir ilkeyi Sil|
|/vaults/replicationRecoveryPlans/Read|Tüm kurtarma planlarını okuma|
|/vaults/replicationRecoveryPlans/Write|Tüm kurtarma planları oluştur veya güncelleştir|
|/vaults/replicationRecoveryPlans/DELETE|Tüm kurtarma planlarını Sil|
|/vaults/replicationRecoveryPlans/plannedFailover/Action|Planlanan yük devretme kurtarma planı|
|/vaults/replicationRecoveryPlans/unplannedFailover/Action|Yük devretme kurtarma planı|
|/vaults/replicationRecoveryPlans/testFailover/Action|Test yük devretme kurtarma planı|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/Action|Test yük devretmesi temizliğini kurtarma planı|
|/vaults/replicationRecoveryPlans/failoverCommit/Action|Yük devretmenin yürütülmesi kurtarma planı|
|/vaults/replicationRecoveryPlans/reProtect/Action|Kurtarma planı koruyun|
|/ Kasalar/extendedInformation/okuma|Merhaba genişletilmiş bilgi al işlemi hello Azure kaynak türü temsil eden bir nesnenin genişletilmiş bilgisi alır? kasası?|
|/ Kasalar/extendedInformation/yazma|Merhaba genişletilmiş bilgi al işlemi hello Azure kaynak türü temsil eden bir nesnenin genişletilmiş bilgisi alır? kasası?|
|/ Kasalar/extendedInformation/silme|Merhaba genişletilmiş bilgi al işlemi hello Azure kaynak türü temsil eden bir nesnenin genişletilmiş bilgisi alır? kasası?|
|/ Kasalar/backupManagementMetaData/okuma|Kurtarma Hizmetleri Kasası için Yedekleme Yönetimi Meta Verilerini döndürür.|
|/ Kasalar/backupProtectionContainers/okuma|Tüm kapsayıcıları ait toohello abonelik döndürür|
|/ Kasalar/backupFabrics/operationResults/okuma|Merhaba işlemin durumunu döndürür|
|/ Kasalar/backupFabrics/protectionContainers/okuma|Tüm kayıtlı kapsayıcıları döndürür|
|/ Kasalar/backupFabrics/protectionContainers /<br>operationResults/okuma|Koruma Kapsayıcısı üzerinde gerçekleştirilen İşlemin sonuçlarını alır.|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/okuma|Merhaba korumalı öğesi ayrıntılarını döndürür nesnesi|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/yazma|Bir yedekleme korumalı öğesi oluşturma|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/silme|Öğe silme korumalı|
|/ Kasalar/backupFabrics/protectionContainers /<br>Yedekleme/protectedItems/eylem|Korumalı Öğe için Yedekleme gerçekleştirir.|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/operationResults/okuma|Korumalı Öğeler üzerinde Gerçekleştirilen İşlemin Sonuçlarını alın.|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/operationStatus/okuma|Korumalı öğeler üzerinde gerçekleştirilen işlemin hello durumunu döndürür.|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints/okuma|Korumalı Öğeler için Kurtarma Noktalarını alın.|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>geri yükleme/eylem|Korumalı Öğeler için Kurtarma Noktalarını geri yükleyin.|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>provisionInstantItemRecovery/eylem|Korumalı öğe için sağlama anlık öğe kurtarma|
|/ Kasalar/backupFabrics/protectionContainers /<br>protectedItems/recoveryPoints /<br>revokeInstantItemRecovery/eylem|Anlık öğe kurtarma için korumalı öğe iptal etme|
|/ Kasalar/kullanımları/okuma|Bir Kurtarma Hizmetleri Kasası için kullanım ayrıntılarını döndürür.|
|/vaults/usages/Read|Herhangi bir kasa kullanımı okuma|
|/ Kasalar/sertifika/yazma|Merhaba güncelleştirme kaynak sertifika işlemi hello kaynak/kasa kimlik bilgileri sertifikası güncelleştirir.|
|/ Kasalar/tokenInfo/okuma|Kurtarma Hizmetleri kasası için belirteç bilgileri döndürür.|
|/vaults/replicationAlertSettings/Read|Tüm uyarı ayarlarını okuma|
|/vaults/replicationAlertSettings/Write|Tüm uyarı ayarlarını güncelle|
|/ Kasalar/backupOperations/okuma|Yedekleme işlemi döndürür durum kurtarma Hizmetleri kasası.|
|/ Kasalar/storageConfig/okuma|Döndürür depolama yapılandırması kurtarma Hizmetleri kasası.|
|/ Kasalar/storageConfig/yazma|Güncelleştirmeler depolama yapılandırması kurtarma Hizmetleri kasası.|
|/ Kasalar/backupUsageSummaries/okuma|Özetleri korunan öğeler ve korunan sunucular için bir kurtarma Hizmetleri döndürür.|
|/ Kasalar/backupProtectedItems/okuma|Tüm korumalı öğeler hello listesi döndürür.|
|/ Kasalar/backupconfig/vaultconfig/okuma|Döndürür yapılandırma kurtarma Hizmetleri kasası.|
|/ Kasalar/backupconfig/vaultconfig/yazma|Güncelleştirmeler yapılandırması kurtarma Hizmetleri kasası.|
|/ Kasalar/registeredIdentities/yazma|Merhaba hizmet kapsayıcısı kaydetme işlemi kullanılan tooregister kurtarma hizmeti ile bir kapsayıcı olabilir.|
|/ Kasalar/registeredIdentities/okuma|Merhaba alma işlemi kullanılabilir kapsayıcıları için bir kaynak kayıtlı Merhaba kapsayıcılara alın.|
|/ Kasalar/registeredIdentities/silme|Merhaba kaydı kapsayıcı işlemi kullanılan toounregister bir kapsayıcı olabilir.|
|/ Kasalar/registeredIdentities/operationResults/okuma|Merhaba alma işlemi işlemi kullanılan get hello işlem durumunu olması ve hello için zaman uyumsuz olarak neden sonuçları işlemi gönderildi|
|/vaults/replicationJobs/Read|Herhangi bir işi okuma|
|/vaults/replicationJobs/Cancel/Action|İşi iptal et|
|/vaults/replicationJobs/restart/Action|İşi yeniden başlatın|
|/vaults/replicationJobs/Resume/Action|İşi sürdürme|
|/ Kasalar/backupPolicies/okuma|Tüm koruma ilkeleri döndürür|
|/ Kasalar/backupPolicies/yazma|Koruma ilkesi oluşturur|
|/ Kasalar/backupPolicies/silme|Bir koruma ilkesini Sil|
|/ Kasalar/backupPolicies/operationResults/okuma|İlke İşleminin Sonuçlarını alın.|
|/ Kasalar/backupPolicies/operationStatus/okuma|İlke işlemin durumunu alın.|
|/ Kasalar/vaultTokens/okuma|Merhaba kasası belirteci işlemi kullanılan tooget kasası belirteci kasası düzeyi arka uç işlemleri için olabilir.|
|/ Kasalar/monitoringConfigurations/notificationConfiguration/okuma|Merhaba kurtarma Hizmetleri kasası bildirim yapılandırmasını alır.|
|/ Kasalar/backupJobs/okuma|Tüm iş nesneleri döndürür|
|/ Kasalar/backupJobs/iptal/eylem|Merhaba işi iptal et|
|/ Kasalar/backupJobs/operationResults/okuma|Döndürür hello iş işleminin sonucu.|
|/Locations/allocateStamp/Action|AllocateStamp hizmeti tarafından kullanılan iç bir işlemdir|
|/Locations/allocatedStamp/Read|GetAllocatedStamp, hizmet tarafından kullanılan iç işlemdir.|

## <a name="microsoftrelay"></a>Microsoft.Relay

| İşlem | Açıklama |
|---|---|
|/ checkNamespaceAvailability/eylem|İlgili abonelikte ad alanının kullanılabilirliğini denetler.|
|/ Kayıt/eylem|Hello hello geçiş kaynak sağlayıcısı için aboneliği kaydeder ve geçiş kaynak hello oluşturmayı etkinleştirir|
|/ ad alanları/yazma|Namespace kaynak oluşturun ve özelliklerini güncelleştirin. Etiketleri ve hello Namespace durumunu, güncelleştirilebilir hello özelliklerdir.|
|/namespaces/Read|Namespace kaynak açıklaması Hello listesini al|
|/ ad alanları/Sil|Namespace kaynağı silme|
|/namespaces/authorizationRules/Write|Namespace düzeyi yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/authorizationRules/DELETE|Namespace yetkilendirme kuralını silin. Merhaba varsayılan Namespace yetkilendirme kuralı silinemez. |
|/namespaces/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi toohello Namespace Al|
|/namespaces/HybridConnections/Write|Oluşturma veya güncelleştirme HybridConnection özellikleri.|
|/namespaces/HybridConnections/Read|HybridConnection kaynak açıklamaları listesini al|
|/namespaces/HybridConnections/DELETE|İşlem toodelete HybridConnection kaynak|
|/namespaces/HybridConnections/authorizationRules/Write|HybridConnection yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/HybridConnections/authorizationRules/DELETE|İşlem toodelete HybridConnection yetkilendirme kuralları|
|/namespaces/HybridConnections/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi tooHybridConnection Al|
|/namespaces/WcfRelays/Write|Oluşturma veya güncelleştirme WcfRelay özellikleri.|
|/namespaces/WcfRelays/Read|WcfRelay kaynak açıklamaları listesini al|
|/namespaces/WcfRelays/DELETE|İşlem toodelete WcfRelay kaynak|
|/namespaces/WcfRelays/authorizationRules/Write|WcfRelay yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/WcfRelays/authorizationRules/DELETE|İşlem toodelete WcfRelay yetkilendirme kuralları|
|/namespaces/WcfRelays/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi tooWcfRelay Al|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| İşlem | Açıklama |
|---|---|
|/ AvailabilityStatuses/okuma|Kapsam alır hello kullanılabilirlik durumlarını hello tüm kaynakları için belirtilen|
|/ AvailabilityStatuses/geçerli/okuma|Kaynak alır hello kullanılabilirlik durumu hello belirtildi|

## <a name="microsoftresources"></a>Microsoft.Resources

| İşlem | Açıklama |
|---|---|
|/ checkResourceName/eylem|Merhaba kaynak adının geçerliliğini denetle.|
|/providers/Read|Merhaba sağlayıcıların listesini al.|
|/Subscriptions/Read|Merhaba Aboneliklerin listesini alır.|
|/Subscriptions/operationresults/Read|Merhaba abonelik İşlem sonuçlarını alır.|
|/Subscriptions/providers/Read|Kaynak sağlayıcılarını alır veya listeler.|
|/Subscriptions/tagNames/Read|Abonelik etiketlerini alır veya listeler.|
|/Subscriptions/tagNames/Write|Bir abonelik etiketi ekler.|
|/Subscriptions/tagNames/DELETE|Bir abonelik etiketini siler.|
|/Subscriptions/tagNames/tagValues/Read|Abonelik etiketi değerlerini alır veya listeler.|
|/Subscriptions/tagNames/tagValues/Write|Bir abonelik etiketi değeri ekler.|
|/Subscriptions/tagNames/tagValues/DELETE|Bir abonelik etiketi değerini siler.|
|/subscriptions/resources/Read|Bir aboneliğin kaynaklarını alır.|
|/Subscriptions/resourceGroups/Read|Kaynak gruplarını alır veya listeler.|
|/Subscriptions/resourceGroups/Write|Kaynak grubunu oluşturur veya güncelleştirir.|
|/Subscriptions/resourceGroups/DELETE|Bir kaynak grubunu ve tüm kaynaklarını siler.|
|/Subscriptions/resourceGroups/moveResources/Action|Kaynakları bir kaynak grubu tooanother taşır.|
|/Subscriptions/resourceGroups/validateMoveResources/Action|Bir kaynak grubu tooanother kaynakların taşımak doğrulayın.|
|/Subscriptions/resourcegroups/Resources/Read|Merhaba kaynak grubu için Hello kaynakları alır.|
|/Subscriptions/resourcegroups/Deployments/Read|Dağıtımları alır veya listeler.|
|/Subscriptions/resourcegroups/Deployments/Write|Bir dağıtımı oluşturur veya güncelleştirir.|
|/Subscriptions/resourcegroups/Deployments/operationstatuses/Read|Alır veya dağıtım işlemi durumları listeler.|
|/Subscriptions/resourcegroups/Deployments/Operations/Read|Dağıtım işlemlerini alır veya listeler.|
|/Subscriptions/Locations/Read|Merhaba desteklenen konumların listesini alır.|
|/Links/Read|Kaynak bağlantılarını alır veya listeler.|
|/ bağlantılar/yazma|Bir kaynak bağlantısını oluşturur veya güncelleştirir.|
|/Links/DELETE|Bir kaynak bağlantısını siler.|
|/tenants/Read|Kiracılar Hello listesini alır.|
|/Resources/Read|Filtrelere göre kaynak Hello listesini alın.|
|/Deployments/Read|Dağıtımları alır veya listeler.|
|/ dağıtımları/yazma|Bir dağıtımı oluşturur veya güncelleştirir.|
|/Deployments/DELETE|Bir dağıtımı siler.|
|/Deployments/Cancel/Action|Bir dağıtımı iptal eder.|
|/Deployments/Validate/Action|Bir dağıtımı doğrular.|
|/Deployments/Operations/Read|Dağıtım işlemlerini alır veya listeler.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| İşlem | Açıklama |
|---|---|
|/jobcollections/Read|İş koleksiyonu Al|
|/ eyleminde/yazma|İş koleksiyonu oluşturur veya güncelleştirir.|
|/jobcollections/DELETE|Koleksiyon silme iş.|
|/jobcollections/Enable/Action|Etkinleştirir koleksiyonu işi.|
|/jobcollections/disable/Action|Devre dışı bırakır, koleksiyon işi.|
|/jobcollections/Jobs/Read|İş alır.|
|/jobcollections/Jobs/Write|İş oluşturur veya güncelleştirir.|
|/jobcollections/Jobs/DELETE|İşi siler.|
|/jobcollections/Jobs/Run/Action|İşi çalıştırır.|
|/jobcollections/Jobs/generateLogicAppDefinition/Action|Bir Scheduler İşini temel alarak Mantıksal Uygulama tanımı oluşturur.|
|/jobcollections/Jobs/jobhistories/Read|Alır geçmişi işi.|

## <a name="microsoftsearch"></a>Microsoft.Search

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello arama kaynak sağlayıcısı için aboneliği kaydeder ve arama hizmetleri hello oluşturulmasını sağlar.|
|/ checkNameAvailability/eylem|Merhaba hizmet adı kullanılabilirliğini denetler.|
|/ searchServices/yazma|Oluşturur veya hello arama hizmeti güncelleştirir.|
|/searchServices/Read|Merhaba arama hizmeti okur.|
|/searchServices/DELETE|Merhaba arama hizmeti siler.|
|/searchServices/Start/Action|Merhaba arama hizmetini başlatır.|
|/searchServices/Stop/Action|Merhaba arama hizmetini durdurur.|
|/searchServices/listAdminKeys/Action|Merhaba yönetici anahtarları okur.|
|/searchServices/regenerateAdminKey/Action|Merhaba yönetici anahtarını yeniden oluşturur.|
|/searchServices/createQueryKey/Action|Merhaba sorgu anahtarı oluşturur.|
|/searchServices/queryKey/Read|Merhaba sorgu anahtarları okur.|
|/searchServices/queryKey/DELETE|Merhaba sorgu anahtarını siler.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| İşlem | Açıklama |
|---|---|
|/jitNetworkAccessPolicies/Read|Merhaba yalnızca zaman ağ erişim ilkelerini alır|
|/ jitNetworkAccessPolicies/yazma|Yeni bir tam zamanı ağ erişim ilkesi oluşturur veya mevcut kümeyi güncelleştirir|
|/jitNetworkAccessPolicies/initiate/Action|Yalnızca zaman ağ erişim ilkesi başlatır|
|/securitySolutionsReferenceData/Read|Merhaba güvenlik çözümleri başvuru verileri alır|
|/securityStatuses/Read|Merhaba güvenlik sistem durumlarını için Azure kaynaklarını alır.|
|/webApplicationFirewalls/Read|Merhaba web uygulaması güvenlik duvarı alır|
|/ webApplicationFirewalls/yazma|Yeni bir web uygulaması güvenlik duvarı oluşturur veya mevcut kümeyi güncelleştirir|
|/webApplicationFirewalls/DELETE|Bir web uygulaması güvenlik duvarı siler|
|/securitySolutions/Read|Merhaba güvenlik çözümleri alır|
|/ securitySolutions/yazma|Yeni bir güvenlik çözümü oluşturur veya mevcut kümeyi güncelleştirir|
|/securitySolutions/DELETE|Bir güvenlik çözümü siler|
|/Tasks/Read|Tüm kullanılabilir güvenlik önerileri alır|
|/Tasks/dismiss/Action|Güvenlik açısından kapatın|
|/Tasks/Activate/Action|Güvenlik açısından etkinleştir|
|/Policies/Read|Merhaba güvenlik ilkesini alır|
|/ ilkeler/yazma|Güvenlik İlkesi güncelleştirmeleri hello|
|/applicationWhitelistings/Read|Merhaba uygulama whitelistings alır|
|/ applicationWhitelistings/yazma|Yeni uygulamaları güvenilir listesine ekleme oluşturur veya mevcut kümeyi güncelleştirir|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| İşlem | Açıklama |
|---|---|
|/ subscriptions/yazma|Oluşturur veya bir abonelik güncelleştirir|
|/ ağ geçitleri/yazma|Oluşturur veya bir ağ geçidi güncelleştirir|
|/Gateways/DELETE|Bir ağ geçidini siler|
|/Gateways/Read|Bir ağ geçidi alır|
|/Gateways/regenerateprofile/Action|Merhaba ağ geçidi profili oluşturur|
|/Gateways/upgradetolatest/Action|Yükseltmeler hello ağ geçidi toohello en son sürümü|
|/ düğümleri/yazma|oluşturur veya bir düğüm güncelleştirir|
|/Nodes/DELETE|Bir düğüm siler|
|/Nodes/Read|Bir düğüm alır|
|/ oturumları/yazma|Oluşturur veya bir oturum güncelleştirir|
|/Sessions/Read|Bir oturum alır|
|/Sessions/DELETE|Bir oturumu siler|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| İşlem | Açıklama |
|---|---|
|/ checkNameAvailability/eylem|İlgili abonelikte ad alanının kullanılabilirliğini denetler.|
|/ Kayıt/eylem|Merhaba hello ServiceBus kaynak sağlayıcısı için aboneliği kaydeder ve ServiceBus kaynak hello oluşturmayı etkinleştirir|
|/ ad alanları/yazma|Namespace kaynak oluşturun ve özelliklerini güncelleştirin. Etiketleri ve hello Namespace durumunu, güncelleştirilebilir hello özelliklerdir.|
|/namespaces/Read|Namespace kaynak açıklaması Hello listesini al|
|/ ad alanları/Sil|Namespace kaynağı silme|
|/namespaces/metricDefinitions/Read|Namespace ölçümleri kaynak açıklamaları listesini al|
|/namespaces/authorizationRules/Write|Namespace düzeyi yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/authorizationRules/Read|Ad alanları yetkilendirme kuralları açıklama Hello listesini alın.|
|/namespaces/authorizationRules/DELETE|Namespace yetkilendirme kuralını silin. Merhaba varsayılan Namespace yetkilendirme kuralı silinemez. |
|/namespaces/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi toohello Namespace Al|
|/namespaces/authorizationRules/regenerateKeys/Action|Merhaba birincil veya ikincil anahtarı toohello kaynak yeniden oluştur|
|/namespaces/diagnosticSettings/Read|Namespace tanılama ayarları kaynak açıklamaları listesini al|
|/namespaces/diagnosticSettings/Write|Namespace tanılama ayarları kaynak açıklamaları listesini al|
|/namespaces/Queues/Write|Oluşturma veya güncelleştirme sıra özellikleri.|
|/namespaces/Queues/Read|Sıra kaynak açıklamaları listesini al|
|/namespaces/Queues/DELETE|İşlem toodelete sırası kaynağı|
|/namespaces/Queues/authorizationRules/Write|Sıra yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/Queues/authorizationRules/Read| Sıra yetkilendirme kuralları Hello listesini al|
|/namespaces/Queues/authorizationRules/DELETE|İşlem toodelete sıra yetkilendirme kuralları|
|/namespaces/Queues/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi tooQueue Al|
|/namespaces/Queues/authorizationRules/regenerateKeys/Action|Merhaba birincil veya ikincil anahtarı toohello kaynak yeniden oluştur|
|/namespaces/logDefinitions/Read|Namespace günlükleri kaynak açıklamaları listesini al|
|/namespaces/topics/Write|Oluşturma veya güncelleştirme konu özellikleri.|
|/namespaces/topics/Read|Konu kaynak açıklamaları listesini al|
|/namespaces/topics/DELETE|İşlem toodelete konu kaynak|
|/namespaces/topics/authorizationRules/Write|Konu yetkilendirme kuralları oluşturun ve özelliklerini güncelleştirin. Merhaba yetkilendirme kuralları erişim hakları, hello birincil ve ikincil anahtarları güncelleştirilebilir.|
|/namespaces/topics/authorizationRules/Read| Konu yetkilendirme kuralları Hello listesini al|
|/namespaces/topics/authorizationRules/DELETE|İşlem toodelete konu yetkilendirme kuralları|
|/namespaces/topics/authorizationRules/listkeys/Action|Merhaba bağlantı dizesi tooTopic Al|
|/namespaces/topics/authorizationRules/regenerateKeys/Action|Merhaba birincil veya ikincil anahtarı toohello kaynak yeniden oluştur|
|/namespaces/topics/Subscriptions/Write|Oluşturma veya güncelleştirme TopicSubscription özellikleri.|
|/namespaces/topics/Subscriptions/Read|TopicSubscription kaynak açıklamaları listesini al|
|/namespaces/topics/Subscriptions/DELETE|İşlem toodelete TopicSubscription kaynak|
|/namespaces/topics/Subscriptions/Rules/Write|Oluşturma veya güncelleştirme kuralı özellikleri.|
|/namespaces/topics/Subscriptions/Rules/Read|Kuralın kaynak açıklamaları listesini al|
|/namespaces/topics/Subscriptions/Rules/DELETE|İşlem toodelete kuralı kaynağı|

## <a name="microsoftsql"></a>Microsoft.Sql

| İşlem | Açıklama |
|---|---|
|/Servers/Read|Bir abonelikte bir kaynak grubunda sunucularının bir listesini döndürür|
|/ sunucuları/yazma|Yeni bir sunucu oluşturun veya bir kaynak grubunda bir abonelik üzerinde var olan sunucu özelliklerini değiştirin|
|/Servers/DELETE|Bir sunucuyu ve tüm kapsanan veritabanları ve esnek havuzlar silin|
|/Servers/import/Action|Şema ve veri DacPac paketinden hello sunucuda yeni bir veritabanı oluşturun ve dağıtın|
|/Servers/Upgrade/Action|Yeni işlevsellik hello en son sürümünü sunucu üzerinde kullanılabilir etkinleştirin ve veritabanları edition dönüştürme harita belirtin|
|/Servers/VulnerabilityAssessmentScans/Action|Güvenlik Açığı değerlendirmesi sunucu tarama yürütme|
|/Servers/operationResults/Read|İşlem kullanılan alt sürüm toohigher sunucu yükseltme tootrack ilerlemesi|
|/Servers/operationResults/DELETE|Sunucu sürüm yükseltme devam eden durdurma|
|/Servers/securityAlertPolicies/Read|Belirli bir sunucuda yapılandırılan hello sunucu tehdit algılama ilkesi ayrıntılarını alma|
|/Servers/securityAlertPolicies/Write|Merhaba sunucu tehdit algılama verilen bir sunucu için değiştirme|
|/Servers/securityAlertPolicies/operationResults/Read|Tehdit algılama İlkesi ayarlama işlemi hello sunucusunun sonuçları Al|
|/Servers/Administrators/Read|Sunucu Yöneticisi ile ilgili ayrıntıları alma|
|/Servers/Administrators/Write|Sunucu Yöneticisi güncelle|
|/Servers/Administrators/DELETE|Sunucu Yöneticisi hello sunucusundan silin|
|/Servers/recoverableDatabases/Read|Bu işlem, Canlı veritabanı toorestore veritabanı toolast bilinen iyi yedekleme noktası olağanüstü durum kurtarma için kullanılır. Merhaba en son iyi yedeklemeden hakkında bilgi verir, ancak gerçekte hello veritabanını geri değil.|
|/Servers/serviceObjectives/Read|Hizmet düzeyi hedefleri (performans katmanı olarak da bilinir) belirli bir sunucuda bulunan listesini alma|
|/Servers/firewallRules/Read|Sunucu güvenlik duvarı kuralı ayrıntıları alma|
|/Servers/firewallRules/Write|IP adresi aralığı tooconnect toohello sunucu izin denetimleri sunucu güvenlik duvarı kuralı oluştur veya güncelleştir|
|/Servers/firewallRules/DELETE|Merhaba sunucusundan güvenlik duvarı kuralını siler|
|/Servers/administratorOperationResults/Read|Sunucu Yöneticisi işlem sonuçları Al|
|/Servers/recommendedElasticPools/Read|Esnek veritabanı havuzları tooreduce maliyet için öneri almak veya historica kaynak kullanımı temelinde performansı|
|/Servers/recommendedElasticPools/Metrics/Read|Verilen bir sunucu için önerilen esnek veritabanı havuzlarına ilişkin ölçümleri alma|
|/Servers/recommendedElasticPools/Databases/Read|Önerilen esnek veritabanı havuzu verilen bir sunucu için uygulamasına eklenmelidir veritabanları alma|
|/Servers/elasticPools/Read|Verilen bir sunucu üzerinde esnek veritabanı havuzu ayrıntılarını alma|
|/Servers/elasticPools/Write|Yeni bir oluşturun veya var olan bir esnek veritabanı havuzu özelliklerini değiştir|
|/Servers/elasticPools/DELETE|Var olan esnek veritabanı havuzunu silme|
|/Servers/elasticPools/operationResults/Read|Verilen esnek veritabanı havuzu işlemle ilgili ayrıntıları alma|
|/Servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions/okuma|Dönüş türleri esnek veritabanı havuzları için kullanılabilir ölçümleri|
|/Servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/okuma|Hello hello kaynağın tanılama ayarını alır|
|/Servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/yazma|Oluşturur veya hello kaynağın tanılama ayarını hello güncelleştirir|
|/Servers/elasticPools/Metrics/Read|Esnek veritabanı havuzu kaynak kullanımı ölçümlerini Döndür|
|/Servers/elasticPools/elasticPoolDatabaseActivity/Read|Etkinlikleri ve esnek veritabanı havuzu parçası olan belirli bir veritabanı üzerinde ayrıntıları alma|
|/Servers/elasticPools/advisors/Read|Danışmanlar hello esnek havuz için kullanılabilir bir listesini döndürür|
|/Servers/elasticPools/advisors/Write|Güncelleştirme otomatik yürütme esnek havuz düzeyde bir advisor durumu.|
|/Servers/elasticPools/advisors/recommendedActions/Read|Belirtilen Danışmanı hello esnek havuz için önerilen eylemleri listesini döndürür|
|/Servers/elasticPools/advisors/recommendedActions/Write|Önerilen eylem hello esnek havuz üzerinde hello Uygula|
|/Servers/elasticPools/elasticPoolActivity/Read|Etkinlikleri ve verilen esnek veritabanı havuzu ayrıntıları alma|
|/Servers/elasticPools/Databases/Read|Liste ve esnek veritabanı havuzu verilen bir sunucu üzerinde bir parçası olan veritabanları ayrıntılarını alma|
|/Servers/auditingPolicies/Read|Denetim İlkesi belirli bir sunucuda yapılandırılan hello varsayılan sunucu tablosu ayrıntılarını alma|
|/Servers/auditingPolicies/Write|Belli bir sunucu için Denetim hello varsayılan sunucu Tablo değiştirme|
|/Servers/disasterRecoveryConfiguration/operationResults/Read|Olağanüstü durum kurtarma yapılandırması İşlem sonuçlarını alır|
|/Servers/advisors/Read|Danışmanlar hello sunucu için kullanılabilir bir listesini döndürür|
|/Servers/advisors/Write|Güncelleştirmeleri otomatik-sunucu düzeyinde bir Danışmanı durumunu yürütün.|
|/Servers/advisors/recommendedActions/Read|Belirtilen Danışmanı hello sunucu için önerilen eylemleri listesini döndürür|
|/Servers/advisors/recommendedActions/Write|Önerilen eylem hello sunucuda hello Uygula|
|/Servers/usages/Read|Merhaba sunucu içindeki tüm veritabanları tarafından sunucu DTU kota ve geçerli DTU tüketim döndürür|
|/Servers/elasticPoolEstimates/Read|Zaten bu sunucu için oluşturulan esnek havuz tahminler listesini döndürür|
|/Servers/elasticPoolEstimates/Write|Sağlanan veritabanı listesi için yeni esnek havuz tahmini oluşturur|
|/Servers/auditingSettings/Read|Denetim İlkesi belirli bir sunucuda yapılandırılan hello sunucu blob ayrıntılarını alma|
|/Servers/auditingSettings/Write|Merhaba sunucu blob belli bir sunucu için Denetim değiştirme|
|/Servers/auditingSettings/operationResults/Read|Sonuç İlkesi ayarlama işlemi denetim hello sunucu BLOB alma|
|/Servers/backupLongTermRetentionVaults/Read|Bu işlem kullanılan tooget bir yedekleme uzun süreli saklama kasası olur. Merhaba kasaya kayıtlı toothis sunucusu hakkında bilgi döndürür.|
|/Servers/backupLongTermRetentionVaults/Write|Bir yedekleme uzun süreli saklama kasası kaydetme|
|/Servers/restorableDroppedDatabases/Read|Hala bekletme ilkesi içinde olan belirli bir sunucuda bırakılan veritabanlarının bir listesini alır. Bu işlem, veritabanlarını ve silme tarihi gibi ilişkili meta verileri listesini döndürür.|
|/Servers/Databases/Read|Bir abonelikte bir kaynak grubunda sunucularının bir listesini döndürür|
|/Servers/Databases/Write|Yeni bir sunucu oluşturun veya bir kaynak grubunda bir abonelik üzerinde var olan sunucu özelliklerini değiştirin|
|/Servers/Databases/DELETE|Bir sunucuyu ve tüm kapsanan veritabanları ve esnek havuzlar silin|
|/Servers/Databases/Export/Action|Şema ve veri DacPac paketinden hello sunucuda yeni bir veritabanı oluşturun ve dağıtın|
|/Servers/Databases/VulnerabilityAssessmentScans/Action|Güvenlik Açığı değerlendirmesi veritabanı taraması yürütün.|
|/Servers/Databases/pause/Action|Veri ambarı edition veritabanı duraklatılamadı|
|/Servers/Databases/Resume/Action|Veri ambarı edition veritabanı sürdürülemedi|
|/Servers/Databases/operationResults/Read|İşlem kullanılır tootrack ilerleme durumunu ölçek gibi uzun süren veritabanı işlemi.|
|/Servers/Databases/replicationLinks/Read|Belirli bir veritabanı için kurulmuş yineleme bağlantıları hakkında dönüş ayrıntıları|
|/Servers/Databases/replicationLinks/DELETE|Zorla ve olası veri kaybı ile Merhaba çoğaltma ilişkisi Sonlandır|
|/Servers/Databases/replicationLinks/unlink/Action|Merhaba çoğaltma ilişkisi zorla veya hello ortağıyla eşitlemeden sonra Sonlandır|
|/Servers/Databases/replicationLinks/Failover/Action|Yük devretme hello birincil, tüm değişiklikleri eşitlemeden sonra bu veritabanını hello çoğaltma ilişkinin birincil ve yapmayı hello uzak birincil ikincil bir siteyi içine duruma getirme|
|/Servers/Databases/replicationLinks/forceFailoverAllowDataLoss/Action|Bu veritabanı hello çoğaltma ilişkinin birincil ve yapmayı hello uzaktan ikincil birincil yapmadan yük devretme olası veri kaybı olmadan hemen|
|/Servers/Databases/replicationLinks/updateReplicationMode/Action|Çoğaltma modu bağlantı toosynchronous için veya zaman uyumsuz moddayken güncelleştirme|
|/Servers/Databases/replicationLinks/operationResults/Read|Veritabanı çoğaltma bağlantılarında uzun süre çalışan işlemlerinin durumunu Al|
|/Servers/Databases/dataMaskingPolicies/Read|İlke verilen bir veritabanı üzerinde yapılandırılan maskeleme hello veri ayrıntılarını alma|
|/Servers/Databases/dataMaskingPolicies/Write|İlke verilen bir veritabanı için maskeleme verileri değiştirme|
|/Servers/Databases/dataMaskingPolicies/Rules/Read|Belirli bir veritabanı üzerinde yapılandırılan ilke kuralı maskeleme hello veri ayrıntılarını alma|
|/Servers/Databases/dataMaskingPolicies/Rules/Write|Verilen bir veritabanı için ilke kuralı maskeleme verileri değiştirme|
|/Servers/Databases/securityAlertPolicies/Read|Belirli bir veritabanı üzerinde yapılandırılan hello tehdit algılama ilkesi ayrıntılarını alma|
|/Servers/Databases/securityAlertPolicies/Write|Verilen bir veritabanı için Hello tehdit algılama ilkesini değiştirme|
|/Servers/Databases/providers/Microsoft.Insights/<br>metricDefinitions/okuma|Dönüş türleri veritabanları için kullanılabilir ölçümleri|
|/Servers/Databases/providers/Microsoft.Insights/<br>diagnosticSettings/okuma|Hello hello kaynağın tanılama ayarını alır|
|/Servers/Databases/providers/Microsoft.Insights/<br>diagnosticSettings/yazma|Oluşturur veya hello kaynağın tanılama ayarını hello güncelleştirir|
|/Servers/Databases/providers/Microsoft.Insights/<br>logDefinitions/okuma|Veritabanları için Hello kullanılabilir günlüklerini alır|
|/Servers/Databases/topQueries/Read|Döndürür seçili sorgu için çalışma zamanı istatistikleri seçilen zaman aralığı içinde toplanır.|
|/Servers/Databases/topQueries/queryText/Read|Seçili sorgu kimliği için Hello Transact-SQL metnini döndürür|
|/Servers/Databases/topQueries/Statistics/Read|Döndürür seçili sorgu için çalışma zamanı istatistikleri seçilen zaman aralığı içinde toplanır.|
|/Servers/Databases/connectionPolicies/Read|Belirli bir veritabanı üzerinde yapılandırılan hello bağlantı ilkesi ayrıntılarını alma|
|/Servers/Databases/connectionPolicies/Write|Verilen bir veritabanı için bağlantı ilkesini değiştirme|
|/Servers/Databases/Metrics/Read|Veritabanı kaynak kullanımı ölçümlerini Döndür|
|/Servers/Databases/auditRecords/Read|Merhaba veritabanı blob Denetim kayıtlarını alma|
|/Servers/Databases/transparentDataEncryption/Read|Durum ve verilen bir veritabanı için saydam veri şifreleme güvenlik özelliği ayrıntılarını alma|
|/Servers/Databases/transparentDataEncryption/Write|Etkinleştirmek veya devre dışı verilen bir veritabanı için saydam veri şifreleme|
|/Servers/Databases/transparentDataEncryption/operationResults/Read|Durum ve verilen bir veritabanı için saydam veri şifreleme güvenlik özelliği ayrıntılarını alma|
|/Servers/Databases/auditingPolicies/Read|Verilen bir veritabanı üzerinde yapılandırılmış hello tablo denetim ilkesi ayrıntılarını alma|
|/Servers/Databases/auditingPolicies/Write|Verilen bir veritabanı için Hello tablo denetim ilkesini değiştirme|
|/Servers/Databases/dataWarehouseQueries/Read|Seçili sorgu kimliği için Hello veri ambarı dağıtım sorgu bilgilerini döndürür|
|/ sunucuları / / dataWarehouseQueries/veritabanları<br>dataWarehouseQuerySteps/okuma|Seçili adımı kimliği için veri ambarı sorgusu sorgu adım bilgiler verir hello dağıtılmış|
|/Servers/Databases/serviceTierAdvisors/Read|Sorgu yürütme istatistikleri tooimprove performansına dayalı veritabanı yukarı veya aşağı Ölçeklendirmesi hakkında öneri dönün veya maliyetini azaltmak|
|/Servers/Databases/advisors/Read|Danışmanlar hello veritabanı için kullanılabilir bir listesini döndürür|
|/Servers/Databases/advisors/Write|Güncelleştirme otomatik yürütme veritabanı düzeyinde bir advisor durumu.|
|/Servers/Databases/advisors/recommendedActions/Read|Önerilen Eylemler hello veritabanı için belirtilen Danışmanı'nın listesini döndürür|
|/Servers/Databases/advisors/recommendedActions/Write|Önerilen eylem hello veritabanında hello Uygula|
|/Servers/Databases/usages/Read|Ulaşılabilen dönüş veritabanı maksimum boyutu ve verilerle dolu geçerli boyutu|
|/Servers/Databases/queryStore/Read|Merhaba veritabanı için Query Store ayarlarının geçerli değerleri döndürür|
|/Servers/Databases/queryStore/Write|Yazılım güncelleştirmelerinin hello veritabanı için Query Store ayarı|
|/Servers/Databases/auditingSettings/Read|Verilen bir veritabanı üzerinde yapılandırılmış hello blob denetim ilkesi ayrıntılarını alma|
|/Servers/Databases/auditingSettings/Write|Verilen bir veritabanı için Hello blob denetim ilkesini değiştirme|
|/Servers/Databases/schemas/Tables/recommendedIndexes/Read|Bir veritabanı üzerinde dizin önerileri listesini alma|
|/Servers/Databases/schemas/Tables/recommendedIndexes/Write|Dizin önerisi Uygula|
|/Servers/Databases/schemas/Tables/Columns/Read|Bir tablodaki sütunların listesini alma|
|/Servers/Databases/missingindexes/Read|Veritabanı dizinleri toocreate ilgili öneriler dönmek, değiştirmek veya sipariş tooimprove sorgu performansı silme|
|/Servers/Databases/missingindexes/Write|Belirli bir veritabanında veritabanı dizin önerilerini kullanın|
|/Servers/Databases/importExportOperationResults/Read|Veritabanı alma ayrıntılarını döndürür veya depolama hesabında bulunan DacPac'den dışarı aktarma işlemi|
|/Servers/importExportOperationResults/Read|Veritabanı alma işlemleri belirli bir sunucuda depolama hesabından ayrıntılarla dönüş hello listesi|

## <a name="microsoftstorage"></a>Microsoft.Storage

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|Merhaba hello depolama kaynak sağlayıcısı için aboneliği kaydeder ve hello depolama hesaplarının oluşturulmasını etkinleştirir.|
|/checknameavailability/Read|Hesap adının geçerliliğini ve kullanımda olup olmadığını denetler.|
|/ storageAccounts/yazma|Belirtilen hello ile bir depolama hesabı oluşturur parametreleri güncelleştirme hello özellikleri veya etiketleri veya özel ekler hello için etki alanı belirtilen depolama hesabı.|
|/storageAccounts/DELETE|Mevcut bir depolama hesabını siler.|
|/storageAccounts/listkeys/Action|Belirtilen depolama hesaba hello hello erişim anahtarlarını döndürür.|
|/storageAccounts/regeneratekey/Action|Belirtilen depolama hesaba hello hello erişim anahtarlarını yeniden oluşturur.|
|/storageAccounts/Read|Depolama hesaplarının listesini döndürür hello veya hello alır hello özelliklerini depolama hesabı belirtildi.|
|/storageAccounts/listAccountSas/Action|Döndürür hello hesap SAS belirteci hello için depolama hesabı belirtilmedi.|
|/storageAccounts/listServiceSas/Action|Depolama hizmet SAS belirteci|
|/storageAccounts/Services/diagnosticSettings/Write|Depolama hesabı tanılama ayarlarını oluştur/güncelleştir.|
|/skus/Read|Merhaba Microsoft.Storage tarafından desteklenen SKU'ları listeler.|
|/usages/Read|Sınır döndürür hello ve abonelik hello hello kaynaklarında geçerli kullanım sayısını belirtilen|
|/Operations/Read|Zaman uyumsuz bir işlem yoklamalar hello durumu.|
|/Locations/deleteVirtualNetworkOrSubnets/Action|Sanal ağ veya alt ağ silindiğinden emin Microsoft.Storage bildirir|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| İşlem | Açıklama |
|---|---|
|/managers/clearAlerts/Action|Merhaba Aygıt Yöneticisi ile ilişkili tüm hello uyarıların temizleyin.|
|/managers/getActivationKey/Action|Merhaba Aygıt Yöneticisi'ni etkinleştirme anahtarı edinin.|
|/managers/regenerateActivationKey/Action|Merhaba Aygıt Yöneticisi'ni etkinleştirme anahtarı yeniden oluşturun.|
|/managers/regenarateRegistationCertificate/Action|Kayıt sertifikası hello cihaz yöneticileri için yeniden oluşturun.|
|/managers/getEncryptionKey/Action|Merhaba Aygıt Yöneticisi'ni için şifreleme anahtarı alma.|
|/managers/Read|Merhaba cihaz Yöneticileri alır veya listeler|
|/managers/DELETE|Merhaba cihaz yöneticileri siler|
|/ yöneticileri/yazma|Merhaba cihaz yöneticileri güncelle|
|/managers/configureDevice/Action|Bir aygıt yapılandırır|
|/managers/listActivationKey/Action|Merhaba StorSimple Aygıt Yöneticisi'ni Hello etkinleştirme anahtarı alır.|
|/managers/listPublicEncryptionKey/Action|Ortak şifreleme anahtarlarını bir StorSimple cihaz Yöneticisi'nin listeleyin.|
|/managers/listPrivateEncryptionKey/Action|Özel şifreleme anahtarı için bir StorSimple cihaz Yöneticisi alır.|
|/managers/provisionCloudAppliance/Action|Yeni bir bulut uygulaması oluşturun.|
|/ Yöneticileri/yazma|Kasa Oluştur işlemi, 'vault' türünde bir Azure kaynağı oluşturur|
|/ Yöneticileri/okuma|Merhaba kasası alma işlemi hello Azure kaynak türü 'Kasası' temsil eden bir nesneyi alır|
|/ Yöneticileri/silme|Azure kaynak türü 'Kasası' Hello kasa silme işlemi siler hello belirtildi|
|/managers/storageAccountCredentials/Write|Oluşturma veya hello depolama hesabının kimlik bilgilerini güncelleştirme|
|/managers/storageAccountCredentials/Read|Merhaba depolama hesabının kimlik bilgilerini alır veya listeler|
|/managers/storageAccountCredentials/DELETE|Merhaba depolama hesabının kimlik bilgilerini siler|
|/managers/storageAccountCredentials/listAccessKey/Action|Depolama hesabı kimlik bilgileri listesi erişim tuşları|
|/managers/accessControlRecords/Read|Merhaba erişim denetimi kayıtları alır veya listeler|
|/managers/accessControlRecords/Write|Merhaba erişim denetimi kayıtları oluştur veya güncelleştir|
|/managers/accessControlRecords/DELETE|Merhaba erişim denetimi kayıtları siler|
|/managers/Metrics/Read|Merhaba ölçümleri alır veya listeler|
|/managers/bandwidthSettings/Read|Liste hello bant genişliği ayarları (yalnızca 8000 Series)|
|/managers/bandwidthSettings/Write|Yeni bir oluşturur veya güncelleştirir bant genişliği ayarları (yalnızca 8000 Series)|
|/managers/bandwidthSettings/DELETE|Var olan bir bant genişliği ayarları siler (yalnızca 8000 Series)|
|/ Yöneticileri/extendedInformation/okuma|Merhaba genişletilmiş bilgi al işlemi hello Azure kaynak türü temsil eden bir nesnenin genişletilmiş bilgisi alır? kasası?|
|/ Yöneticileri/extendedInformation/yazma|Merhaba genişletilmiş bilgi al işlemi hello Azure kaynak türü temsil eden bir nesnenin genişletilmiş bilgisi alır? kasası?|
|/ Yöneticileri/extendedInformation/silme|Merhaba genişletilmiş bilgi al işlemi hello Azure kaynak türü temsil eden bir nesnenin genişletilmiş bilgisi alır? kasası?|
|/managers/Alerts/Read|Merhaba uyarıları alır veya listeler|
|/managers/storageDomains/Read|Merhaba depolama etki alanları alır veya listeler|
|/managers/storageDomains/Write|Oluşturma veya güncelleme hello depolama etki alanları|
|/managers/storageDomains/DELETE|Merhaba depolama etki alanları siler|
|/managers/Devices/scanForUpdates/Action|Bir cihaz güncelleştirmeleri için tarama.|
|/managers/Devices/download/Action|Bir aygıt için dowload güncelleştirmeler.|
|/managers/Devices/install/Action|Bir cihazda güncelleştirmeleri yükleyin.|
|/managers/Devices/Read|Merhaba aygıtları alır veya listeler|
|/managers/Devices/Write|Merhaba aygıtları güncelle|
|/managers/Devices/DELETE|Merhaba aygıtları siler|
|/managers/Devices/Deactivate/Action|Bir aygıtı devre dışı bırakır.|
|/managers/Devices/publishSupportPackage/Action|Destek paketi Microsoft Support sorun giderme için bir cihazın yayımlayın.|
|/managers/Devices/Failover/Action|Merhaba aygıt yük devretmesi.|
|/managers/Devices/sendTestAlertEmail/Action|Tooconfigured e-posta alıcılarını test uyarı e-posta gönderin.|
|/managers/Devices/installUpdates/Action|Merhaba cihazlarda güncelleştirmeleri yükler|
|/managers/Devices/listFailoverSets/Action|Liste hello yük devretme için varolan bir cihazın ayarlar.|
|/managers/Devices/listFailoverTargets/Action|Merhaba aygıtların listesi yük devri hedefleri|
|/managers/Devices/publicEncryptionKey/Action|Merhaba Aygıt Yöneticisi'nin listesini ortak şifreleme anahtarı|
|/ yöneticileri/aygıtları/hardwareComponentGroups /<br>Okuma|Liste hello donanım bileşen grupları|
|/ yöneticileri/aygıtları/hardwareComponentGroups /<br>changeControllerPowerState/eylem|Donanım bileşen grupları denetleyicisi güç durumunu değiştir|
|/managers/Devices/Metrics/Read|Merhaba ölçümleri alır veya listeler|
|/managers/Devices/chapSettings/Write|Oluşturma veya güncelleştirme hello Chap ayarları|
|/managers/Devices/chapSettings/Read|Merhaba Chap ayarları alır veya listeler|
|/managers/Devices/chapSettings/DELETE|Merhaba Chap ayarları siler|
|/managers/Devices/backupScheduleGroups/Read|Merhaba Yedekleme Zamanlama grupları alır veya listeler|
|/managers/Devices/backupScheduleGroups/Write|Merhaba yedekleme zamanlaması grupları oluştur veya güncelleştir|
|/managers/Devices/backupScheduleGroups/DELETE|Merhaba Yedekleme Zamanlama grupları siler|
|/managers/Devices/updateSummary/Read|Merhaba güncelleştirme özeti alır veya listeler|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>Alma/eylem|Geçiş için kaynak yapılandırmaları alma|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>startMigrationEstimate/eylem|Bir iş tooestimate hello süresi hello geçiş işlemi başlatın.|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>startMigration/eylem|Kaynak yapılandırmaları kullanarak geçiş Başlat|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>confirmMigration/eylem|Başarılı bir geçiş doğrular ve onu uygulayın.|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>fetchMigrationEstimate/eylem|Merhaba durum hello geçiş tahmin işinin getirin.|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>fetchMigrationStatus/eylem|Merhaba durum hello geçiş için getirin.|
|/ yöneticileri/aygıtları/migrationSourceConfigurations /<br>fetchConfirmMigrationStatus/eylem|Fetch hello geçişinin durumunu doğrulayın.|
|/managers/Devices/alertSettings/Read|Merhaba uyarı ayarlarını alır veya listeler|
|/managers/Devices/alertSettings/Write|Oluşturma veya hello uyarı ayarlarını güncelleştirme|
|/managers/Devices/networkSettings/Read|Merhaba ağ ayarlarını alır veya listeler|
|/managers/Devices/networkSettings/Write|Yeni bir oluşturur veya ağ ayarlarını güncelleştirir|
|/managers/Devices/Jobs/Read|Merhaba işleri alır veya listeler|
|/managers/Devices/Jobs/Cancel/Action|Bir çalışan işi iptal etme|
|/managers/Devices/metricsDefinitions/Read|Merhaba ölçümleri tanımlarını alır veya listeler|
|/managers/Devices/volumeContainers/Write|Yeni bir oluşturur veya güncelleştirir birim kapsayıcıları (yalnızca 8000 Series)|
|/managers/Devices/volumeContainers/Read|Liste hello birim kapsayıcıları (yalnızca 8000 Series)|
|/managers/Devices/volumeContainers/DELETE|Var olan bir birim kapsayıcıları siler (yalnızca 8000 Series)|
|/managers/Devices/volumeContainers/listEncryptionKeys/Action|Birim kapsayıcıları şifreleme anahtarlarının listesi|
|/managers/Devices/volumeContainers/rolloverEncryptionKey/Action|Geçiş şifreleme anahtarlarının birim kapsayıcıları|
|/managers/Devices/volumeContainers/Metrics/Read|Liste hello ölçümleri|
|/managers/Devices/volumeContainers/Volumes/Read|Liste hello birimleri|
|/managers/Devices/volumeContainers/Volumes/Write|Yeni bir oluşturur veya birimleri güncelleştirir|
|/managers/Devices/volumeContainers/Volumes/DELETE|Var olan birimler siler|
|/managers/Devices/volumeContainers/Volumes/Metrics/Read|Liste hello ölçümleri|
|/managers/Devices/volumeContainers/Volumes/metricsDefinitions/Read|Liste hello ölçümleri tanımları|
|/managers/Devices/volumeContainers/metricsDefinitions/Read|Liste hello ölçümleri tanımları|
|/managers/Devices/iscsiservers/Read|Merhaba iSCSI sunucuları alır veya listeler|
|/managers/Devices/iscsiservers/Write|Merhaba iSCSI sunucuları güncelle|
|/managers/Devices/iscsiservers/DELETE|Merhaba iSCSI sunucuları siler|
|/managers/Devices/iscsiservers/Backup/Action|Bir iSCSI sunucusu yedek alın.|
|/managers/Devices/iscsiservers/Metrics/Read|Merhaba ölçümleri alır veya listeler|
|/managers/Devices/iscsiservers/Disks/Read|Merhaba diskleri alır veya listeler|
|/managers/Devices/iscsiservers/Disks/Write|Merhaba diskleri güncelle|
|/managers/Devices/iscsiservers/Disks/DELETE|Merhaba diskleri siler|
|/managers/Devices/iscsiservers/Disks/Metrics/Read|Merhaba ölçümleri alır veya listeler|
|/managers/Devices/iscsiservers/Disks/metricsDefinitions/Read|Merhaba ölçümleri tanımlarını alır veya listeler|
|/managers/Devices/iscsiservers/metricsDefinitions/Read|Merhaba ölçümleri tanımlarını alır veya listeler|
|/managers/Devices/Backups/Read|Merhaba yedekleme kümesi alır veya listeler|
|/managers/Devices/Backups/DELETE|Yedekleme kümesi siler hello|
|/managers/Devices/Backups/Restore/Action|Tüm hello birimleri yedekleme kümesinden geri yükleyin.|
|/managers/Devices/Backups/Elements/Clone/Action|Bir paylaşımı veya bir yedekleme öğesi kullanarak birimi kopyalama.|
|/managers/Devices/backupPolicies/Write|Yeni bir oluşturur veya yedekleme ilkeleri güncelleştirir (yalnızca 8000 Series)|
|/managers/Devices/backupPolicies/Read|Liste hello yedekleme ilkeleri (yalnızca 8000 Series)|
|/managers/Devices/backupPolicies/DELETE|Mevcut bir yedekleme ilkeleri siler (yalnızca 8000 Series)|
|/managers/Devices/backupPolicies/Backup/Action|El ile yedekleme toocreate isteğe hello İlkesi tarafından korunan tüm hello birimlerin yedek alın.|
|/managers/Devices/backupPolicies/Schedules/Write|Yeni bir oluşturur veya zamanlamaları güncelleştirir|
|/managers/Devices/backupPolicies/Schedules/Read|Liste hello zamanlamaları|
|/managers/Devices/backupPolicies/Schedules/DELETE|Var olan zamanlamalar siler|
|/managers/Devices/securitySettings/Update/Action|Merhaba güvenlik ayarlarını güncelleştirin.|
|/managers/Devices/securitySettings/Read|Liste hello güvenlik ayarları|
|/ yöneticileri/aygıtları/securitySettings /<br>syncRemoteManagementCertificate/eylem|Bir aygıt için Hello uzak yönetim sertifikası eşitleyin.|
|/managers/Devices/securitySettings/Write|Yeni bir oluşturur veya güvenlik ayarlarını güncelleştirir|
|/managers/Devices/fileservers/Read|Merhaba dosya sunucuları alır veya listeler|
|/managers/Devices/fileservers/Write|Oluşturma veya güncelleştirme hello dosya sunucuları|
|/managers/Devices/fileservers/DELETE|Merhaba dosya sunucuları siler|
|/managers/Devices/fileservers/Backup/Action|Bir dosya sunucusunda yedekleme gerçekleştirin.|
|/managers/Devices/fileservers/Metrics/Read|Merhaba ölçümleri alır veya listeler|
|/managers/Devices/fileservers/Shares/Write|Merhaba paylaşımları güncelle|
|/managers/Devices/fileservers/Shares/Read|Merhaba paylaşımları alır veya listeler|
|/managers/Devices/fileservers/Shares/delete|Merhaba paylaşımları siler|
|/managers/Devices/fileservers/Shares/Metrics/Read|Merhaba ölçümleri alır veya listeler|
|/managers/Devices/fileservers/Shares/metricsDefinitions/Read|Merhaba ölçümleri tanımlarını alır veya listeler|
|/managers/Devices/fileservers/metricsDefinitions/Read|Merhaba ölçümleri tanımlarını alır veya listeler|
|/managers/Devices/timeSettings/Read|Merhaba saat ayarlarını alır veya listeler|
|/managers/Devices/timeSettings/Write|Yeni bir oluşturur veya saat ayarlarını güncelleştirir|
|/ Yöneticileri/sertifika/yazma|Merhaba güncelleştirme kaynak sertifika işlemi hello kaynak/kasa kimlik bilgileri sertifikası güncelleştirir.|
|/managers/cloudApplianceConfigurations/Read|Liste hello bulut Gereci desteklenen yapılandırmalar|
|/managers/metricsDefinitions/Read|Merhaba ölçümleri tanımlarını alır veya listeler|
|/managers/encryptionSettings/Read|Merhaba şifreleme ayarlarını alır veya listeler|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| İşlem | Açıklama |
|---|---|
|/streamingjobs/Start/Action|Akış analizi işi Başlat|
|/streamingjobs/Stop/Action|Stream Analytics işini durdurma|
|/ streamingjobs/okuma|Akış analizi işi okuma|
|/ streamingjobs/yazma|Akış analizi işi yazma|
|/ streamingjobs/Sil|Akış analizi işi Sil|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/Read|İçin streamingjobs Hello kullanılabilir ölçümleri alır|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/Read|Tanılama ayarını okuyun.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/Write|Tanılama ayarını yazma.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/Read|İçin streamingjobs Hello kullanılabilir günlüklerini alır|
|/streamingjobs/Transformations/Read|Okuma Stream Analytics işi dönüştürme|
|/streamingjobs/Transformations/Write|Stream Analytics işi dönüştürme yazma|
|/streamingjobs/Transformations/DELETE|Stream Analytics işi dönüştürme Sil|
|/streamingjobs/inputs/Read|Okuma Stream Analytics işi giriş|
|/streamingjobs/inputs/Write|Stream Analytics işi giriş yazma|
|/streamingjobs/inputs/DELETE|Stream Analytics işi giriş silme|
|/streamingjobs/Outputs/Read|Okuma Stream Analytics işi çıkış|
|/streamingjobs/Outputs/Write|Stream Analytics işi çıkış yazma|
|/streamingjobs/Outputs/DELETE|Stream Analytics işi çıkış Sil|

## <a name="microsoftsupport"></a>Microsoft.Support

| İşlem | Açıklama |
|---|---|
|/ Kayıt/eylem|TooSupport kaynak sağlayıcısını kaydeder|
|/supportTickets/Read|(Durum, önem derecesi, kişi ayrıntıları ve iletişimler dahil) destek biletleri ayrıntılarını alır veya Aboneliklerdeki destek biletleri hello listesini alır.|
|/ supportTickets/yazma|Oluşturur veya bir destek bileti güncelleştirir. Bir destek bileti oluşturabilirsiniz teknik için faturalama, kota veya abonelik yönetimi ile ilgili sorunlar. Önem derecesi, kişi ayrıntıları ve iletişimler için mevcut destek biletlerinin güncelleştirebilirsiniz.|

## <a name="microsoftweb"></a>Microsoft.Web

| İşlem | Açıklama |
|---|---|
|/ kaydı/eylem|Merhaba aboneliği için Microsoft.Web kaynak sağlayıcısı kaydını silin.|
|/ Doğrula/eylem|Doğrulayın.|
|/ Kayıt/eylem|Microsoft.Web kaynak sağlayıcısı hello abonelik için kaydolun.|
|/ hostingEnvironments/okuma|Uygulama hizmeti ortamı'Hello özelliklerini alır|
|/ hostingEnvironments/yazma|Yeni bir uygulama hizmeti ortamı oluşturma veya varolan bir güncelleştirme|
|/ hostingEnvironments/Sil|Bir uygulama hizmeti ortamını silme|
|/hostingEnvironments/reboot/Action|Uygulama hizmeti ortamı'nda tüm makineleri yeniden başlatın|
|/hostingenvironments/Resume/Action|Barındırma ortamları sürdürün.|
|/hostingenvironments/suspend/Action|Barındırma ortamları askıya alın.|
|/hostingenvironments/metricdefinitions/Read|Ortamlar ölçüm tanımlarını barındırma alın.|
|/hostingEnvironments/workerPools/Read|Bir uygulama hizmeti ortamı çalışan havuzunda Hello özelliklerini alır|
|/hostingEnvironments/workerPools/Write|Uygulama hizmeti ortamı'nda yeni bir çalışan havuzu oluşturmak veya mevcut bir güncelleştirme|
|/hostingenvironments/workerpools/metricdefinitions/Read|Ortamlar Workerpools ölçüm tanımlarını barındırma alın.|
|/hostingenvironments/workerpools/Metrics/Read|Ortamlar Workerpools ölçümleri barındırma alın.|
|/hostingenvironments/workerpools/skus/Read|Ortamlar Workerpools SKU'ları barındırma alın.|
|/hostingenvironments/workerpools/usages/Read|Ortamlar Workerpools kullanımları barındırma alın.|
|/hostingenvironments/Sites/Read|Barındırma ortamları Web uygulamaları alın.|
|/hostingenvironments/serverfarms/Read|Barındırma ortamları uygulama hizmeti planları alın.|
|/hostingenvironments/usages/Read|Ortamlar kullanımları barındırma alın.|
|/hostingenvironments/capacities/Read|Ortamlar kapasiteleri barındırma alın.|
|/hostingenvironments/Operations/Read|Ortamlar işlemleri barındırma alın.|
|/hostingEnvironments/multiRolePools/Read|Bir uygulama hizmeti ortamı ön uç havuzunda Hello özelliklerini alır|
|/hostingEnvironments/multiRolePools/Write|Uygulama hizmeti ortamı'nda yeni bir ön uç havuzu oluşturmak veya mevcut bir güncelleştirme|
|/hostingenvironments/multirolepools/metricdefinitions/Read|Ortamlar birden havuzları ölçüm tanımlarını barındırma alın.|
|/hostingenvironments/multirolepools/Metrics/Read|Ortamlar birden havuzları ölçümleri barındırma alın.|
|/hostingenvironments/multirolepools/skus/Read|Ortamlar birden havuzları SKU'ları barındırma alın.|
|/hostingenvironments/multirolepools/usages/Read|Ortamlar birden havuzları kullanımları barındırma alın.|
|/hostingenvironments/Diagnostics/Read|Ortamlar tanılama barındırma alın.|
|/publishingusers/Read|Kullanıcılar yayımlanıyor alın.|
|/ publishingusers/yazma|Kullanıcılar yayımlanıyor güncelleştirin.|
|/checknameavailability/Read|Kaynak adı kullanılabilir olup olmadığını denetleyin.|
|/ geoRegions/okuma|Coğrafi bölgeler Hello listesini alın.|
|/ Siteler/okuma|Bir Web uygulaması Hello özelliklerini alır|
|/ Siteler/yazma|Yeni bir Web uygulaması oluşturun veya var olan bir güncelleştirme|
|/ Siteler/Sil|Var olan bir Web uygulamasının Sil|
|/Sites/Backup/Action|Yeni bir web uygulaması yedekleme oluşturma|
|/Sites/publishxml/Action|Bir Web uygulaması için profil xml yayımlama Al|
|/Sites/Publish/Action|Bir Web uygulaması yayımlama|
|/Sites/restart/Action|Bir Web uygulaması yeniden|
|/Sites/Start/Action|Bir Web uygulaması başlatın|
|/Sites/Stop/Action|Bir Web uygulamasını Durdur|
|/Sites/slotsswap/Action|Web uygulaması dağıtım yuvalarını değiştirme|
|/Sites/slotsdiffs/Action|Web uygulaması yuvaları arasındaki farklar yapılandırmasında Al|
|/Sites/applySlotConfig/Action|Hedef yuva toohello geçerli web uygulamasından Web uygulaması yuvası yapılandırmasını Uygula|
|/Sites/resetSlotConfig/Action|Web uygulaması yapılandırmasında Sıfırla|
|/Sites/Functions/Action|İşlevler Web uygulamaları.|
|/Sites/listsyncfunctiontriggerstatus/Action|Liste eşitleme işlevi tetikleyici durum Web uygulamaları.|
|/Sites/networktrace/Action|Ağ izleme Web uygulamaları.|
|/Sites/NewPassword/Action|#Newpassword Web uygulamaları.|
|/Sites/Sync/Action|Eşitleme Web uygulamaları.|
|/Sites/operationresults/Read|Web Apps İşlem sonuçlarını alır.|
|/Sites/webjobs/Read|Web uygulamalarını Web işlerini alma.|
|/ Siteler/yedekleme/okuma|Web uygulamaları yedek alın.|
|/Sites/Backup/Write|Web uygulamaları yedekleme güncelleştirin.|
|/Sites/metricdefinitions/Read|Web uygulamaları ölçüm tanımlarını alın.|
|/Sites/Metrics/Read|Web uygulamaları ölçümlerini alın.|
|/Sites/continuouswebjobs/DELETE|Web uygulamaları sürekli Web işleriniz silin.|
|/Sites/continuouswebjobs/Read|Web uygulamaları sürekli Web işleriniz alın.|
|/Sites/continuouswebjobs/Start/Action|Web uygulamaları sürekli Web işleriniz başlatın.|
|/Sites/continuouswebjobs/Stop/Action|Web uygulamaları sürekli Web işleriniz durdurun.|
|/Sites/domainownershipidentifiers/Read|Web Apps etki alanı sahipliğini tanımlayıcıları alın.|
|/Sites/domainownershipidentifiers/Write|Web Apps etki alanı sahipliğini tanımlayıcıları güncelleştirin.|
|/Sites/premieraddons/DELETE|Web uygulamaları Premier alabilecekleri silin.|
|/Sites/premieraddons/Read|Web uygulamaları Premier alabilecekleri alın.|
|/Sites/premieraddons/Write|Web uygulamaları Premier alabilecekleri güncelleştirin.|
|/Sites/triggeredwebjobs/DELETE|Web uygulamaları tetiklenen Web işleri silin.|
|/Sites/triggeredwebjobs/Read|Web uygulamaları tetiklenen Web işlerini alma.|
|/Sites/triggeredwebjobs/Run/Action|Web uygulamaları tetiklenen WebJobs çalıştırın.|
|/Sites/hostnamebindings/DELETE|Web uygulamaları konak adı bağlamaları silin.|
|/Sites/hostnamebindings/Read|Web uygulamaları konak adı bağlamaları alın.|
|/Sites/hostnamebindings/Write|Web uygulamaları konak adı bağlamaları güncelleştirin.|
|/Sites/virtualnetworkconnections/DELETE|Web uygulamaları sanal ağ bağlantıları silin.|
|/Sites/virtualnetworkconnections/Read|Web uygulamaları sanal ağ bağlantıları alın.|
|/Sites/virtualnetworkconnections/Write|Web uygulamaları sanal ağ bağlantıları güncelleştirin.|
|/Sites/virtualnetworkconnections/Gateways/Read|Web uygulamaları sanal ağ bağlantıları ağ geçitleri alın.|
|/Sites/virtualnetworkconnections/Gateways/Write|Web uygulamaları sanal ağ bağlantıları Gateway bileşenlerini güncelleştirin.|
|/Sites/publishxml/Read|Web uygulamalarını XML yayımlama alır.|
|/Sites/hybridconnectionrelays/Read|Web uygulamaları karma bağlantı geçişler alın.|
|/Sites/perfcounters/Read|Web uygulamaları performans sayaçlarını alın.|
|/Sites/usages/Read|Web uygulamaları kullanımları alın.|
|/Sites/slots/Write|Yeni bir Web uygulaması yuvası oluşturma veya var olan bir güncelleştirme|
|/Sites/slots/DELETE|Var olan bir Web uygulaması yuvası Sil|
|/Sites/slots/Backup/Action|Yeni Web uygulaması yuvası yedeği oluştur.|
|/Sites/slots/publishxml/Action|Web uygulaması yuvası için profil xml yayımlama Al|
|/Sites/slots/Publish/Action|Bir Web uygulaması yuvası yayımlama|
|/Sites/slots/restart/Action|Bir Web uygulaması yuvası yeniden başlatın|
|/Sites/slots/Start/Action|Bir Web uygulaması yuvası Başlat|
|/Sites/slots/Stop/Action|Bir Web uygulaması yuvası Durdur|
|/Sites/slots/slotsswap/Action|Web uygulaması dağıtım yuvalarını değiştirme|
|/Sites/slots/slotsdiffs/Action|Web uygulaması yuvaları arasındaki farklar yapılandırmasında Al|
|/Sites/slots/applySlotConfig/Action|Web uygulaması yuvası yapılandırması yuvadan hedef yuva toohello geçerli uygulayın.|
|/Sites/slots/resetSlotConfig/Action|Web uygulaması yuvası yapılandırması Sıfırla|
|/Sites/slots/Read|Bir Web uygulaması dağıtım yuvası Hello özelliklerini alır|
|/Sites/slots/NewPassword/Action|#Newpassword Web Apps yuvaları.|
|/Sites/slots/Sync/Action|Eşitleme Web Apps yuvaları.|
|/Sites/slots/operationresults/Read|Web uygulamaları yuvaları İşlem sonuçlarını alır.|
|/Sites/slots/webjobs/Read|Web uygulamaları yuvaları WebJobs alın.|
|/Sites/slots/Backup/Write|Web uygulamaları yuvaları yedeklemeyi güncelleştirin.|
|/Sites/slots/metricdefinitions/Read|Web uygulamaları yuvaları ölçüm tanımlarını alın.|
|/Sites/slots/Metrics/Read|Web uygulamaları yuvaları ölçümlerini alın.|
|/Sites/slots/continuouswebjobs/DELETE|Web uygulamaları yuvaları sürekli Web işleriniz silin.|
|/Sites/slots/continuouswebjobs/Read|Web uygulamaları yuvaları sürekli Web işleriniz alın.|
|/Sites/slots/continuouswebjobs/Start/Action|Web uygulamaları yuvaları sürekli Web işleriniz başlatın.|
|/Sites/slots/continuouswebjobs/Stop/Action|Web uygulamaları yuvaları sürekli Web işleriniz durdurun.|
|/Sites/slots/premieraddons/DELETE|Web uygulamaları yuvaları Premier alabilecekleri silin.|
|/Sites/slots/premieraddons/Read|Web uygulamaları yuvaları Premier alabilecekleri alın.|
|/Sites/slots/premieraddons/Write|Web uygulamaları yuvaları Premier alabilecekleri güncelleştirin.|
|/Sites/slots/triggeredwebjobs/DELETE|Web uygulamaları yuvası harekete WebJobs silin.|
|/Sites/slots/triggeredwebjobs/Read|Web uygulamaları yuvası harekete Web işlerini alma.|
|/Sites/slots/triggeredwebjobs/Run/Action|Web uygulamaları yuvası harekete Web işleri'ni çalıştırın.|
|/Sites/slots/hostnamebindings/DELETE|Web uygulamaları yuvaları konak adı bağlamaları silin.|
|/Sites/slots/hostnamebindings/Read|Web uygulamaları yuvaları konak adı bağlamaları alın.|
|/Sites/slots/hostnamebindings/Write|Web uygulamaları yuvaları konak adı bağlamaları güncelleştirin.|
|/Sites/slots/phplogging/Read|Web uygulamaları yuvaları Phplogging alın.|
|/Sites/slots/virtualnetworkconnections/DELETE|Web uygulamaları yuvaları sanal ağ bağlantıları silin.|
|/Sites/slots/virtualnetworkconnections/Read|Web uygulamaları yuvaları sanal ağ bağlantıları alın.|
|/Sites/slots/virtualnetworkconnections/Write|Web uygulamaları yuvaları sanal ağ bağlantıları güncelleştirin.|
|/Sites/slots/virtualnetworkconnections/Gateways/Write|Web uygulamaları yuvaları sanal ağ bağlantıları Gateway bileşenlerini güncelleştirin.|
|/Sites/slots/usages/Read|Web uygulamaları yuvaları kullanımları alın.|
|/Sites/slots/hybridconnection/DELETE|Web uygulamaları yuvaları karma bağlantısını silin.|
|/Sites/slots/hybridconnection/Read|Web uygulamaları yuvaları karma bağlantı alın.|
|/Sites/slots/hybridconnection/Write|Web uygulamaları yuvaları karma bağlantı güncelleştirin.|
|/Sites/slots/config/Read|Web uygulaması yuvanın yapılandırma ayarlarını al|
|/Sites/slots/config/List/Action|Kimlik bilgileri, uygulama ayarlarının ve bağlantı dizeleri yayımlama gibi Web uygulama yuvanın hassas, güvenlik ayarlarını Listele|
|/Sites/slots/config/Write|Web uygulaması yuvanın yapılandırma ayarlarını güncelleştirme|
|/Sites/slots/config/DELETE|Web uygulamaları yuvaları Config silin.|
|/Sites/slots/instances/Read|Web uygulamaları yuvaları örnekleri alın.|
|/Sites/slots/instances/Processes/Read|Web uygulamaları yuvaları örnekleri işlemleri alın.|
|/Sites/slots/instances/Deployments/Read|Web uygulamaları yuvaları örnekleri dağıtımları alın.|
|/Sites/slots/sourcecontrols/Read|Web uygulaması yuvası'nın kaynak denetimi yapılandırma ayarlarını al|
|/Sites/slots/sourcecontrols/Write|Web uygulaması yuvası'nın kaynak denetimini yapılandırma ayarlarını güncelleştirme|
|/Sites/slots/sourcecontrols/DELETE|Web uygulaması yuvası'nın kaynak denetimini yapılandırma ayarlarını Sil|
|/Sites/slots/Restore/Read|Web uygulamaları yuvaları geri alın.|
|/Sites/slots/analyzecustomhostname/Read|Web alma uygulamaları yuvaları analiz özel ana bilgisayar adı.|
|/Sites/slots/Backups/Read|Bir web uygulaması yuvaları yedekleme Hello özelliklerini alır|
|/Sites/slots/Backups/List/Action|Liste Web Apps yuvaları yedeklemeler.|
|/Sites/slots/Backups/Restore/Action|Web uygulamaları yuvaları yedekleri geri yükleyin.|
|/Sites/slots/Deployments/DELETE|Web uygulamaları yuvaları dağıtımları silin.|
|/Sites/slots/Deployments/Read|Web uygulamaları yuvaları dağıtımları alın.|
|/Sites/slots/Deployments/Write|Web uygulamaları yuvaları dağıtımları güncelleştirin.|
|/Sites/slots/Deployments/log/Read|Web uygulamaları yuvaları dağıtımları günlük alın.|
|/Sites/hybridconnection/DELETE|Web uygulamaları karma bağlantısını silin.|
|/Sites/hybridconnection/Read|Web uygulamaları karma bağlantı alın.|
|/Sites/hybridconnection/Write|Web uygulamaları karma bağlantı güncelleştirin.|
|/Sites/recommendationhistory/Read|Web uygulamaları öneri geçmişi alın.|
|/Sites/Recommendations/Read|Web uygulaması için öneriler Hello listesini alın.|
|/Sites/Recommendations/disable/Action|Web uygulamaları önerileri devre dışı bırakın.|
|/Sites/config/Read|Web uygulaması yapılandırma ayarlarını al|
|/Sites/config/List/Action|Kimlik bilgileri, uygulama ayarlarının ve bağlantı dizeleri yayımlama gibi Web uygulamanızın hassas, güvenlik ayarlarını Listele|
|/Sites/config/Write|Web uygulamanızın yapılandırma ayarlarını güncelleştirme|
|/Sites/config/DELETE|Web uygulamaları Config silin.|
|/Sites/instances/Read|Web uygulamaları örnekleri alın.|
|/Sites/instances/Processes/DELETE|Web uygulamaları örnekleri işlemleri silin.|
|/Sites/instances/Processes/Read|Web uygulamaları örnekleri işlemleri alın.|
|/Sites/instances/Deployments/Read|Web uygulamaları örnekleri dağıtımları alın.|
|/Sites/sourcecontrols/Read|Web uygulamanızın kaynak denetimini yapılandırma ayarlarını al|
|/Sites/sourcecontrols/Write|Web uygulamanızın kaynak denetimini yapılandırma ayarlarını güncelleştirme|
|/Sites/sourcecontrols/DELETE|Web uygulamanızın kaynak denetimini yapılandırma ayarlarını Sil|
|/Sites/Restore/Read|Web uygulamaları geri alın.|
|/Sites/analyzecustomhostname/Read|Özel ana bilgisayar adını analiz edin.|
|/Sites/Backups/Read|Web uygulamanızın yedekleme Hello özelliklerini alır|
|/Sites/Backups/List/Action|Liste Web Apps yedeklemeler.|
|/Sites/Backups/Restore/Action|Web uygulamaları yedekleri geri yükleyin.|
|/Sites/snapshots/Read|Web uygulamaları anlık görüntülerini alın.|
|/Sites/Functions/DELETE|Web uygulamaları işlevleri silin.|
|/Sites/Functions/listsecrets/Action|Liste gizli Web Apps işlevleri.|
|/Sites/Functions/Read|Web uygulamaları işlevleri alın.|
|/Sites/Functions/Write|Web uygulamaları işlevleri güncelleştirin.|
|/Sites/Deployments/DELETE|Web uygulamaları dağıtımları silin.|
|/Sites/Deployments/Read|Web uygulamaları dağıtımları alın.|
|/Sites/Deployments/Write|Web uygulamaları dağıtımları güncelleştirin.|
|/Sites/Deployments/log/Read|Web uygulamaları dağıtımları günlük alın.|
|/Sites/Diagnostics/Read|Web Apps tanılama alın.|
|/Sites/Diagnostics/workerprocessrecycle/Read|Web Apps tanılama çalışan işlem geri dönüştürme alın.|
|/Sites/Diagnostics/workeravailability/Read|Web Apps tanılama Workeravailability alın.|
|/Sites/Diagnostics/runtimeavailability/Read|Web Apps tanılama çalışma zamanı kullanılabilirliğini alın.|
|/Sites/Diagnostics/cpuanalysis/Read|Web Apps tanılama Cpuanalysis alın.|
|/Sites/Diagnostics/servicehealth/Read|Web Apps Tanılama Hizmeti durumunu alın.|
|/Sites/Diagnostics/frebanalysis/Read|Web Apps tanılama FREB analiz alın.|
|/availablestacks/Read|Kullanılabilir yığınları alın.|
|/isusernameavailable/Read|Kullanıcı adı kullanılabilir olup olmadığını denetleyin.|
|/Microsoft.Web/apiManagementAccounts/<br>API/okuma|API Hello listesini alın.|
|/Microsoft.Web/apiManagementAccounts/<br>API/yazma|Yeni bir API eklemek veya var olan bir güncelleştirin.|
|/Microsoft.Web/apiManagementAccounts/<br>API/silme|Varolan bir API silin.|
|/Microsoft.Web/apiManagementAccounts/<br>API/bağlantıları/okuma|Merhaba bağlantıların listesini alır.|
|/Microsoft.Web/apiManagementAccounts/<br>API/bağlantıları/yazma|Var olan bir güncelleştirme ya da yeni bir bağlantı kaydedin.|
|/Microsoft.Web/apiManagementAccounts/<br>API/bağlantıları/silme|Varolan bir bağlantıyı silin.|
|/Microsoft.Web/apiManagementAccounts/<br>API/bağlantıları/connectionAcls/okuma|ConnectionAcls okuma|
|/Microsoft.Web/apiManagementAccounts/<br>API/bağlantıları/connectionAcls/yazma|Ekleyin veya ConnectionAcl güncelleştirin|
|/Microsoft.Web/apiManagementAccounts/<br>API/bağlantıları/connectionAcls/silme|ConnectionAcl Sil|
|/Microsoft.Web/apiManagementAccounts/<br>API/connectionAcls/okuma|İçin API ConnectionAcls okuma|
|/Microsoft.Web/apiManagementAccounts/<br>API/apiAcls/okuma|ConnectionAcls okuma|
|/Microsoft.Web/apiManagementAccounts/<br>API/apiAcls/yazma|API ACL'ler güncelle|
|/Microsoft.Web/apiManagementAccounts/<br>API/apiAcls/silme|API ACL'ler Sil|
|/ ServerFarm öğesine verilir/okuma|Bir uygulama hizmeti planı üzerinde Hello özelliklerini alma|
|/ ServerFarm öğesine verilir/yazma|Yeni bir uygulama hizmeti planı oluşturma veya var olan bir güncelleştirme|
|/ ServerFarm öğesine verilir/Sil|Var olan bir uygulama hizmeti planı silme|
|/serverfarms/restartSites/Action|Tüm Web uygulamaları bir uygulama hizmeti planı'nda yeniden başlatın.|
|/serverfarms/operationresults/Read|Uygulama hizmeti planları İşlem sonuçlarını alır.|
|/serverfarms/Capabilities/Read|App Service planları özelliklerini alın.|
|/serverfarms/metricdefinitions/Read|Uygulama hizmeti planları ölçüm tanımlarını alın.|
|/serverfarms/Metrics/Read|Uygulama hizmeti planları ölçümlerini alın.|
|/serverfarms/hybridconnectionplanlimits/Read|Uygulama hizmeti planları karma bağlantı planı sınırlarını alın.|
|/serverfarms/virtualnetworkconnections/Read|Uygulama hizmeti planları sanal ağ bağlantıları alın.|
|/serverfarms/virtualnetworkconnections/Routes/DELETE|Uygulama hizmeti planları sanal ağ bağlantıları yolları silin.|
|/serverfarms/virtualnetworkconnections/Routes/Read|Uygulama hizmeti planları sanal ağ bağlantıları rotaları alabilir.|
|/serverfarms/virtualnetworkconnections/Routes/Write|Uygulama hizmeti planları sanal ağ bağlantıları yolları güncelleştirin.|
|/serverfarms/virtualnetworkconnections/Gateways/Write|Uygulama hizmeti planları sanal ağ bağlantıları Gateway bileşenlerini güncelleştirin.|
|/serverfarms/firstpartyapps/Settings/DELETE|Uygulama hizmeti planları birinci taraf uygulama ayarları silin.|
|/serverfarms/firstpartyapps/Settings/Read|Uygulama hizmeti planları birinci taraf uygulama ayarları alın.|
|/serverfarms/firstpartyapps/Settings/Write|Uygulama hizmeti planları birinci taraf uygulama ayarları güncelleştirin.|
|/serverfarms/Sites/Read|Uygulama hizmeti planları Web uygulamalarını alır.|
|/serverfarms/workers/reboot/Action|Uygulama hizmeti planları çalışanları yeniden başlatın.|
|/serverfarms/hybridconnectionrelays/Read|Uygulama hizmeti planları karma bağlantı geçişler alın.|
|/serverfarms/skus/Read|Uygulama hizmeti planları SKU'ları alır.|
|/serverfarms/usages/Read|Uygulama hizmeti planları kullanımları alın.|
|/serverfarms/hybridconnectionnamespaces/relays/Sites/Read|Uygulama hizmeti planları karma bağlantı ad alanları geçişler Web uygulamalarını alır.|
|/ishostnameavailable/Read|Ana bilgisayar adı kullanılabilir olup olmadığını denetleyin.|
|/ connectionGateways/okuma|Bağlantı ağ geçidi Hello listesi alın.|
|/ connectionGateways/yazma|Oluşturur veya bir bağlantı ağ geçidi güncelleştirir.|
|/ connectionGateways/Sil|Bir bağlantı ağ geçidi siler.|
|/connectionGateways/Join/Action|Bir bağlantı ağ geçidi birleştirir.|
|/classicmobileservices/Read|Klasik mobil hizmet edinebilirsiniz.|
|/skus/Read|SKU'ları alır.|
|/ Sertifika/okuma|Merhaba sertifikaların listesini alın.|
|/ Sertifika/yazma|Yeni bir sertifika ekleyin veya mevcut bir güncelleştirin.|
|/ Sertifika/Sil|Varolan bir sertifikayı silin.|
|/Operations/Read|İşlemleri alın.|
|/ önerileri/okuma|Abonelikler için öneriler Hello listesini alın.|
|/ishostingenvironmentnameavailable/Read|Barındırma ortamı adı olup olmadığını alır.|
|/ apiManagementAccounts/okuma|ApiManagementAccounts Hello listesini alın.|
|/ apiManagementAccounts/yazma|Yeni bir ApiManagementAccount eklemek veya mevcut bir güncelleştirme|
|/ apiManagementAccounts/Sil|Varolan bir ApiManagementAccount Sil|
|/apiManagementAccounts/connectionAcls/Read|Bağlantı ACL'ler Hello listesini alın.|
|/apiManagementAccounts/apiAcls/Read|ConnectionAcls okuma|
|/ bağlantıları/okuma|Merhaba bağlantıların listesini alır.|
|/ bağlantıları/yazma|Oluşturur veya bağlantı güncelleştirir.|
|/ bağlantıları/Sil|Bir bağlantı siler.|
|/Connections/Join/Action|Bir bağlantı birleştirir.|
|/Connections/confirmconsentcode/Action|Bağlantıları onay kodunu onaylayın.|
|/Connections/listconsentlinks/Action|Bağlantılar için liste onay bağlantılar.|
|/deploymentlocations/Read|Dağıtım konumlarında alın.|
|/sourcecontrols/Read|Kaynak denetimleri alın.|
|/ sourcecontrols/yazma|Kaynak denetimleri güncelleştirin.|
|/managedhostingenvironments/Read|Barındırma ortamları yönetilen.|
|/managedhostingenvironments/Sites/Read|Barındırma ortamları Web uygulamaları yönetilen.|
|/managedhostingenvironments/serverfarms/Read|Barındırma ortamları uygulama hizmeti planları yönetilen.|
|/Locations/managedapis/Read|Konumları yönetilen API'ler alın.|
|/Locations/apioperations/Read|Konumları API işlemleri alın.|
|/Locations/connectiongatewayinstallations/Read|Konumları bağlantı ağ geçidi yüklemeleri alın.|
|/ listSitesAssignedToHostName/okuma|Toohostname atanmış siteler adlarını alır.|

## <a name="next-steps"></a>Sonraki adımlar

- Nasıl çok öğrenin[özel bir rol oluşturmak](role-based-access-control-custom-roles.md).

- Gözden geçirme hello [yerleşik RBAC roller](role-based-access-built-in-roles.md).

- Nasıl toomanage erişim atamalarını öğrenin [kullanıcı tarafından](role-based-access-control-manage-assignments.md) veya [kaynak tarafından](role-based-access-control-configure.md) 
