---
title: "aaaAzure Machine Learning REST API'si hata kodları | Microsoft Docs"
description: "Bu hata kodları, bir Azure Machine Learning web hizmeti üzerinde bir işlemi tarafından döndürülebilir."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Machine Learning REST API hata kodları
 
Merhaba aşağıdaki hata kodları bir Azure Machine Learning web hizmeti üzerinde bir işlemi tarafından döndürülebilir.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (HTTP durum kodu 400)
 
Geçersiz bağımsız değişkeni sağlanmadı.
 
Bu sınıf hataların bir yerde sağlanan bağımsız değişken geçersiz anlamına gelir. Bu kimlik bilgileri veya Azure depolama toosomething toohello web hizmeti geçirilen konumunu olabilir. Lütfen hello hata "code" hello "Ayrıntılar" bölümü toodiagnose hangi belirli bağımsız değişkeni geçersiz alanına bakın.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| BadParameterValue | sağlanan hello parametre değeri hello parametre kural hello parametresi üzerinde uygun değil |
| BadSubscriptionId | Merhaba aboneliği kullanılan tooscore kimliği hello bir hello kaynak mevcut değil. |
| BadVersionCall | Geçersiz sürüm parametresi hello API çağrısı sırasında geçirildi: {0}. Onay hello API hello doğru sürümü geçirme için sayfa yardımcı olmak ve yeniden deneyin. |
| BatchJobInputsNotSpecified | gerekli input(s) aşağıdaki hello hello istekle belirtilmedi: {0}. Lütfen olun tüm giriş verilerini belirtilir ve yeniden deneyin. |
| BatchJobInputsTooManySpecified | Merhaba isteği hello hizmetinde tanımlanan çok daha fazla girişleri belirtilmiş. Kabul edilen input(s) listesi: {0}. Lütfen tüm giriş verilerini doğru belirtildiğinden emin yeniden deneyin. |
| BlobNameTooLong | Tanılama çıktıları uzun için belirtilen azure blob depolama alanı yolu: {0}. Merhaba yolu kısaltın ve yeniden deneyin. |
| BlobNotFound | Azure blob - oluşturulamıyor tooaccess hello {0} sağlanır.  Azure hata iletisi: {1}. |
| ContainerIsEmpty | Hiçbir Azure depolama kapsayıcısı adı sağlandı. Geçerli kapsayıcısı adı sağlayın ve yeniden deneyin. |
| ContainerSegmentInvalid | Geçersiz kapsayıcı adı. Geçerli kapsayıcısı adı sağlayın ve yeniden deneyin. |
| ContainerValidationFailed | BLOB kapsayıcı doğrulama Bu hata ile başarısız oldu: {0}. |
| DataTypeNotSupported | Sağlanan desteklenmeyen veri türü. Geçerli veri türleri sağlayın ve yeniden deneyin. |
| DuplicateInputInBatchCall | Merhaba toplu isteği geçersiz. Hem tek hem de birden çok giriş hello aynı belirtemezsiniz zaman. Bu öğelerden birini hello istekten kaldırın ve yeniden deneyin. |
| ExpiryTimeInThePast | Sağlanan süre sonu zamanı hello geçmiş: {0}. Gelecekte süre sonu zamanı, UTC sağlayın ve yeniden deneyin. toonever sona, sona erme saati tooNULL ayarlayın. |
| IncompleteSettings | Tanılama ayarları eksik. |
| InputBlobRelativeLocationInvalid | Sağlanan Azure depolama blob adı yok. Geçerli blob adı sağlayın ve yeniden deneyin. |
| InvalidBlob | Blob geçersiz blob belirtimi: {0}. Bu bağlantı dizesini doğrulayın / göreli bir yol veya SAS belirteci belirtimi doğru olduğundan ve yeniden deneyin. |
| InvalidBlobConnectionString | Merhaba hello giriş/çıkış BLOB'lar geçersiz biri için belirtilen bağlantı dizesi: {0}. Lütfen bunu düzeltin ve yeniden deneyin. |
| InvalidBlobExtension | Merhaba blob başvurusu: {0} geçersiz veya eksik dosya uzantısına sahip. Bu çıktı türü için desteklenen dosya uzantıları: "{1}". |
| InvalidInputNames | Geçersiz hizmet giriş hello istekte belirtilen adları: {0}. Lütfen hello giriş verisi toohello doğru hizmeti girişleri eşleştirin ve yeniden deneyin. |
| InvalidOutputOverrideName | Geçersiz çıkış adı geçersiz kıl: {0}. Bu ada sahip bir çıkış düğümü Hello hizmet yok. Lütfen doğru çıkış düğüm adı toooverride içinde geçirin (büyük küçük harfe duyarlılığın geçerlidir). |
| InvalidQueryParameter | Geçersiz sorgu parametresi '{0}'. {1} |
| MissingInputBlobInformation | Azure storage blobu bilgileri eksik. Geçerli bağlantı dizesi ve göreli bir yol veya URI sağlayın ve yeniden deneyin. |
| MissingJobId | Hiçbir iş sağlanan kimliği. Bir işi ilk kez Merhaba gönderildiği bir iş kimliği döndürülür. Merhaba iş kimliğini doğru olduğundan ve yeniden deneyin doğrulayın. |
| MissingKeys | Sağlanan anahtar yok veya bir birincil veya ikincil anahtarı sağlanmaz. |
| MissingModelPackage | Model paket kimliği veya sağlanan modeli paketi yok. Geçerli model paket kimliği sağlayın veya paket modeli ve tekrar deneyin. |
| MissingOutputOverrideSpecification | Merhaba isteği çıkış override {0} hello blob belirtimi eksik. Lütfen hello istekle geçerli blob konumunu belirtin veya konumu geçersiz kılma isterseniz hello çıkış belirtimini kaldırın. |
| MissingRequestInput | Merhaba web hizmeti, bir girdi bekliyor, ancak herhangi bir giriş sağlanmadı. Geçerli girişleri sağlanan yayımlanan hello üzerinde olun giriş bağlantı noktaları hello modelindeki ve yeniden deneyin. |
| MissingRequiredGlobalParameters | Tüm web hizmeti parametreleri sağlanan gereklidir. Modüller doğru olduğundan ve yeniden deneyin Merhaba Hello parametre beklenen doğrulayın. |
| MissingRequiredOutputOverrides | Zorunlu toopass içinde olan bir şifrelenmiş Hizmeti uç noktası çağrılırken çıkış tüm hello hizmetin çıkışlar için geçersiz kılar. Şu anda bu çıktıları için geçersiz kılmaları eksik: {0} |
| MissingWebServiceGroupId | Hiçbir web hizmeti grubu kimliği sağlanır. Geçerli web hizmeti grubu kimliği sağlayın ve yeniden deneyin. |
| MissingWebServiceId | Hiçbir web hizmeti sağlanan kimliği. Geçerli web sitesi kimliği sağlayın ve yeniden deneyin. |
| MissingWebServicePackage | Web hizmeti paketi sağlanan. Geçerli web hizmeti paketi girin ve yeniden deneyin. |
| MissingWorkspaceId | Çalışma alanı kimliği girildi. Geçerli çalışma alanı kimliği sağlayın ve yeniden deneyin. |
| ModelConfigurationInvalid | Merhaba modeli paketi yapılandırmasında geçersiz model. Çıkış uç tanımı, standart hata endpoint Hello modeli yapılandırması içerir ve std uç nokta kapatın ve yeniden deneyin emin olun. |
| ModelPackageIdInvalid | Geçersiz model paket kimliği Bu hello modeli paket kimliği doğru olduğunu doğrulayıp yeniden deneyin. |
| RequestBodyInvalid | Hiçbir istek gövdesinde sağlanan veya hello istek gövdesi seri durumdan çıkarılırken hata oluştu. |
| RequestIsEmpty | Sağlanan hiçbir isteği. Geçerli bir istek sağlayın ve yeniden deneyin. |
| UnexpectedParameter | Sağlanan beklenmeyen parametre. Doğrulama tüm parametre adları doğru yazıldığından yalnızca beklenen parametreleri geçirilir ve yeniden deneyin. |
| Başvuruları | Bilinmeyen hata. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | {0} web hizmeti için eş zamanlı istekler gereksinimleri değiştiremezsiniz. |
| WebServiceIdInvalid | Sağlanan geçersiz web hizmeti kimliği. Web hizmeti kimliği geçerli bir GUID olmalıdır. |
| WebServiceTooManyConcurrentRequestRequirement | Eş zamanlı istek gereksinim toomore {0}'den ayarlanamıyor. |
| WebServiceTypeInvalid | Sağlanan geçersiz web hizmeti türü. Merhaba geçerli web hizmeti türü doğru olduğunu doğrulayıp yeniden deneyin. Geçerli web hizmeti türleri: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (HTTP durum kodu 400)
 
Geçersiz kullanıcı bağımsız değişkeni sağlanmadı.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| InputMismatchError | Giriş verisi giriş bağlantı noktası şeması eşleşmiyor. |
| InputParseError | Giriş vektörü başarısız ayrıştırma.  Merhaba giriş vektör hello doğru sayıda sütun ve veri türlerine sahip olduğunu doğrular.  Ek ayrıntıları: {0}. |
| MissingRequiredGlobalParameters | Merhaba web hizmeti tarafından beklenen parametre eksik. Merhaba web hizmeti tarafından beklenen tüm gerekli hello parametrelerin doğru olduğundan emin olun ve yeniden deneyin. |
| UnexpectedParameter | Merhaba web hizmeti tarafından beklenen parametreleri geçirilen yalnızca hello gerekli doğrulayın ve yeniden deneyin. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (HTTP durum kodu 400)
 
Merhaba isteği hello geçerli bağlamda geçersiz.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| CannotStartJob | Merhaba işi {0} durumunda olduğundan başlatılamaz. |
| IncompatibleModel | Merhaba modeli hello isteği sürümüyle uyumlu değil. Merhaba istek sürümü yalnızca tek datatable çıkış modellerini destekler. |
| MultipleInputsNotAllowed | Merhaba model birden çok girişi izin vermiyor. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (HTTP durum kodu 400)
 
Modül yürütme iç kitaplığı hatayla karşılaştı.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (HTTP durum kodu 400)
 
Modül yürütme bir hatayla karşılaştı.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (HTTP durum kodu 400)
 
Geçersiz web hizmeti paketi. Sağlanan hello web hizmeti paketi doğru olduğunu doğrulayıp yeniden deneyin.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| FormatError | Merhaba web hizmeti paketi bozuk. Ayrıntılar: {0} |
| RuntimesError | Merhaba web hizmeti paketi grafik geçersiz. Ayrıntılar: {0} |
| ValidationError | Merhaba web hizmeti paketi grafik geçersiz. Ayrıntılar: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Yetkisiz (HTTP durum kodu 401)
 
İstek yetkisiz tooaccess kaynaktır.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| AdminRequestUnauthorized | Yetkilendirilmemiş |
| ManagementRequestUnauthorized | Yetkilendirilmemiş |
| ScoreRequestUnauthorized | Geçersiz kimlik bilgileri sağlandı. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (HTTP durum kodu 404)
 
Kaynak bulunamadı.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| ModelPackageNotFound | Model paketi bulunamadı. Kimliği doğru olduğundan ve yeniden deneyin hello modeli paketi doğrulayın. |
| WebServiceIdNotFoundInWorkspace | Web hizmeti bulunamadı Bu çalışma alanı altında. Merhaba webServiceId hello Workspaceıd arasında bir uyuşmazlık var. Sağlanan hello web hizmeti hello çalışma alanının parçası olduğunu doğrulayıp yeniden deneyin. |
| WebServiceNotFound | Web hizmeti bulunamadı. Kimliği doğru olduğundan ve yeniden deneyin hello web hizmeti doğrulayın. |
| WorkspaceNotFound | Çalışma alanı bulunamadı. Kimliği doğru olduğundan ve yeniden deneyin başlangıç çalışma doğrulayın. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (HTTP durum kodu 408)
 
Merhaba işlemi zaman izin hello içinde tamamlanamadı.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| RequestCanceled | İstek hello istemcisi tarafından iptal edildi. |
| ScoreRequestTimeout | Yürütme isteği zaman aşımına uğradı. |
 
## <a name="conflict-http-status-code-409"></a>Çakışma (HTTP durum kodu 409)
 
Kaynak zaten var.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Geçersiz çıkış parametre adı. Merhaba meta verileri Düzenleyicisi modülü toorename sütunları kullanmayı deneyin ve yeniden deneyin. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (HTTP durum kodu 413)
 
Merhaba modeli tooit atanan hello bellek kotasını aştı.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| OutOfMemoryLimit | Merhaba modeli için tahsis olandan daha fazla bellek tüketilen. Merhaba modeli için izin verilen maksimum bellekten {0} MB ' dir. Modelinizi sorunları gözden geçirin. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (HTTP durum kodu 500)
 
Yürütme bir iç hatayla karşılaştı.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | Sistem hatası ile Merhaba kapsayıcı işlemi kilitlendi |
| ContainerProcessTerminatedWithUnknownError | Bilinmeyen hata arda hello kapsayıcı işlemi |
| ContainerValidationFailed | BLOB kapsayıcı doğrulama Bu hata ile başarısız oldu: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Sağlanan bağımsız değişkenler. Doğrulayın. geçerli bağımsız değişkenler geçirilir ve yeniden deneyin. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | Bağlantı noktası kimliği = {0} desteklenmeyen bir veri türüne sahip: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Swagger oluşturma başarısız oldu, Ayrıntılar: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| Başvuruları |  |
| UnknownJobStatusCode | Bilinmeyen İş durum kodu: {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, Ayrıntılar: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (HTTP durum kodu 500)
 
Yürütme bir iç hatayla karşılaştı. Sistem bellek yetersiz. Lütfen yeniden deneyin.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (HTTP durum kodu 500)
 
Geçersiz model paketi. Sağlanan hello modeli paketi doğru olduğunu doğrulayıp yeniden deneyin.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (HTTP durum kodu 500)
 
Geçersiz web hizmeti paketi. Sağlanan hello web paketini doğru olduğunu doğrulayıp yeniden deneyin.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| ModuleError | Merhaba web hizmeti paketi grafik geçersiz. Ayrıntılar: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (HTTP durum kodu 503)
 
Hello isteği kapsayıcıları başlatılmış hello yürütülemiyor.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (HTTP durum kodu 503)
 
Hizmet geçici olarak kullanılamıyor.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| NoMoreResources | İstek için kullanılabilir kaynaklar yoktur. |
| RequestThrottled | İstek {0} uç noktası için kısıtlanan. Merhaba uç noktası için en fazla eşzamanlılık Hello {1} ' dir. |
| TooManyConcurrentRequests | Çok sayıda eşzamanlı istek gönderildi. |
| TooManyHostsBeingInitialized | Konumundaki başlatılmakta çok fazla konak aynı hello zaman. Azaltma / yeniden deneniyor göz önünde bulundurun. |
| TooManyHostsBeingInitializedPerModel | Konumundaki başlatılmakta çok fazla konak aynı hello zaman. Azaltma / yeniden deneniyor göz önünde bulundurun. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (HTTP durum kodu 504)
 
Merhaba işlemi zaman izin hello içinde tamamlanamadı.
 
| Hata kodu | Kullanıcı iletisi |
| ---------- |--------------|
| BackendInitializationTimeout | Merhaba web hizmeti başlatma zamanı izin hello içinde tamamlanamadı. |
| BackendScoreTimeout | Merhaba web hizmeti isteği yürütme süresi izin hello içinde tamamlanamadı. |
 
