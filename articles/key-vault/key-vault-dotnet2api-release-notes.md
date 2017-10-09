---
title: "aaaKey Kasa .NET 2.x API Sürüm Notları | Microsoft Docs"
description: ".NET geliştiricileri için Azure anahtar kasası bu API toocode kullanır"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Azure anahtar kasası .NET 2.0 - sürüm notları ve Geçiş Kılavuzu
Merhaba aşağıdaki notları ve rehberlik Azure anahtar kasası .NET ile birlikte çalışan geliştiricilere içindir / C# Kitaplığı. Geçiş Hello hello 1.0 sürümü toohello 2.0 sürümünden güncelleştirme sayısı, hello işlevsel iyileştirmeler toobenefit sırada kodunuzu geçiş işlerinde gerektirir ve ekler gibi özellik bu işlem yapıldı **anahtar kasası sertifikaları** destekler.

## <a name="key-vault-certificates"></a>Anahtar kasası sertifikaları

Anahtar kasası sertifikaları destek sağlar, x509 yönetimi için sertifikaları ve davranışları aşağıdaki hello:  

* Bir sertifika sahibinin toocreate bir anahtar kasası oluşturma işlemi veya varolan bir sertifikayı hello alma aracılığıyla bir sertifika sağlar. Bu otomatik olarak imzalanan hem de içerir ve sertifika yetkilisi sertifikaları oluşturulur.
* Bir anahtar kasası sertifika sahibinin tooimplement güvenli depolama ve Yönetimi X509 verir sertifikaları özel anahtar malzemesi etkileşim olmadan.  
* Bir sertifika sahibinin toocreate anahtar kasası toomanage hello yaşam döngüsü, bir sertifikanın yönlendiren bir ilke sağlar.  
* Sertifika sahipleri tooprovide kişi hakkında bilgi için bildirim yaşam döngüsü olayları geçerlilik süresi ve sertifikanın yenilenmesini sağlar.  
* Otomatik olarak yenilenmesi destekler seçili verenler - anahtar kasası iş ortağı X509 ile sertifika sağlayıcıları / sertifika yetkilileri.
  
  * Not - ortaklık olmayan sağlayıcıları/yetkilileri de izin verilir ancak hello otomatik yenileme özelliği desteklemez.

## <a name="net-support"></a>.NET desteği

* **.NET 4.0** hello Azure anahtar kasası .NET hello 2.0 sürümü tarafından desteklenmeyen / C# Kitaplığı
* **.NET core** hello Azure anahtar kasası .NET hello 2.0 sürümü tarafından desteklenen / C# Kitaplığı

## <a name="namespaces"></a>ad alanları

* ad alanı için hello **modelleri** değiştirilirse **Microsoft.Azure.KeyVault** çok**Microsoft.Azure.KeyVault.Models**.
* Merhaba **Microsoft.Azure.KeyVault.Internal** ad alanı bırakıldı.
* Hello Azure SDK'sı bağımlılıkları ad alanı değiştirildi **Hyak.Common** ve **Hyak.Common.Internals** çok**Microsoft.Rest** ve  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Türü değişiklikleri

* *Gizli* çok değiştirilen*SecretBundle*
* *Sözlük* çok değiştirilen*IDictionary*
* *Liste<T>, string []* çok değiştirilen*IList<T>*
* *NextList* çok değiştirilen *NextPageLink*

## <a name="return-types"></a>Dönüş türleri

* **KeyList** ve **SecretList** döndürülecek *IPage<T>*  yerine *ListKeysResponseMessage*
* oluşturulan hello **BackupKeyAsync** döndürülecek *BackupKeyResult* içeren *değeri* (Yedekleme blob). Merhaba önce yöntemi Sarmalanan ve döndürmeyi yalnızca hello değeri idi.

## <a name="exceptions"></a>Özel durumlar

* *KeyVaultClientException* çok değiştirilir*KeyVaultErrorException*
* Merhaba hizmet hatası değiştirildiğinde *özel durum. Hata* çok*özel durum. Body.Error.Message*.
* Ek bilgi için hata iletisini hello kaldırıldı **[JsonExtensionData]**.

## <a name="constructors"></a>Oluşturucular

* Kabul yerine bir *HttpClient* oluşturucu bağımsız değişkeni olarak yalnızca hello Oluşturucusu kabul *HttpClientHandler* veya *DelegatingHandler []*.

## <a name="downloaded-packages"></a>İndirilen paketler

Bir istemci üzerinde bir bağımlılık işlerken anahtar kasası hello aşağıdaki yüklenen

### <a name="previous-package-list"></a>Önceki paket listesi

* id="Hyak.Common paketini" Sürüm "1.0.2" = targetFramework "net45" =
* id="Microsoft.Azure.Common paketini" Sürüm "2.0.4" = targetFramework "net45" =
* id="Microsoft.Azure.common.Dependencies paketini" Sürüm "1.0.0" = targetFramework "net45" =
* id="Microsoft.Azure.KeyVault paketini" Sürüm "1.0.0" = targetFramework "net45" =
* id="Microsoft.BCL paketini" Sürüm "1.1.9" = targetFramework "net45" =
* id="Microsoft.BCL.Async paketini" Sürüm "1.0.168" = targetFramework "net45" =
* id="Microsoft.BCL.Build paketini" Sürüm "1.0.14" = targetFramework "net45" =
* id="Microsoft.NET.http paketini" Sürüm "2.2.22" = targetFramework "net45" =

### <a name="current-package-list"></a>Geçerli paket listesi

* id="Microsoft.Azure.KeyVault paketini" Sürüm "2.0.0-preview" targetFramework = "net45" =
* id="Microsoft.REST.ClientRuntime paketini" Sürüm "2.2.0" = targetFramework "net45" =
* id="Microsoft.REST.ClientRuntime.Azure paketini" Sürüm "3.2.0" = targetFramework "net45" =

## <a name="class-changes"></a>Sınıf değişiklikleri

* **UnixEpoch** sınıfı kaldırıldı
* **Base64UrlConverter** sınıfı çok yeniden**Base64UrlJsonConverter**

## <a name="other-changes"></a>Diğer değişiklikler

* Merhaba API sürümü toothis KV işlemi geçici hataları yeniden deneme ilkesi hello yapılandırması için destek eklendi.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Döndürülen hello işlemleri için bir *kasa*, hello dönüş türü olan bir kasa özelliği bulunan bir sınıf. Merhaba dönüş türü sunulmuştur *kasa*.
* *PermissionsToKeys* ve *PermissionsToSecrets* artık *Permissions.Keys* ve *Permissions.Secrets*
* Merhaba bazıları toohello kontrol-düzlemi de türleri değişiklikleri uygulamak döndür.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* Merhaba paket parçalara çok**Microsoft.Azure.KeyVault.Extensions** ve **Microsoft.Azure.KeyVault.Cryptography** hello şifreleme işlemleri için.

