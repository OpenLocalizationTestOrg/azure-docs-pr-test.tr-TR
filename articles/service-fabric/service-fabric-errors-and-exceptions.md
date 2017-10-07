---
title: "oluşturulan aaaCommon FabricClient özel durumları | Microsoft Docs"
description: "Merhaba ortak özel durumlarını ve uygulama ve küme yönetimi işlemleri gerçekleştirirken hello FabricClient API tarafından atılabilen hataları açıklar."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Genel özel durumlar ve hello FabricClient API'leri ile çalışırken hataları
Merhaba [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API'leri küme ve uygulama yöneticileri tooperform yönetim görevlerini temel bir Service Fabric uygulama, hizmet veya küme etkinleştirin. Örneğin, uygulama dağıtımı, yükseltme ve kaldırma, bir küme hello durumu denetleniyor veya bir hizmet test etme. Uygulama geliştiricileri ve küme yöneticileri hello FabricClient API'leri toodevelop araçları hello Service Fabric kümesi ve uygulamaları yönetmek için kullanabilirsiniz.

Farklı türlerde FabricClient kullanılarak gerçekleştirilen işlemler vardır.  Her yöntem tooincorrect giriş, çalışma zamanı hataları veya geçici altyapı sorunları nedeniyle hataları için özel durumlar atabilirsiniz.  Belirli bir yöntemle hangi özel durumlar hello API başvuru belgeleri toofind bakın. Çoğu tarafından oluşturulan bazı özel durumlar, ancak, farklı [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API'leri. Merhaba aşağıdaki tabloda FabricClient API'leri hello arasında ortak olan hello özel durumlar listelenir.

| Özel durum | Ne zaman oluşturulur |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Merhaba [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) nesne kapalı durumda değil. Merhaba dispose [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) nesne kullanıyorsanız ve yeni bir örneğini [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) nesnesi. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |Merhaba işlemi zaman aşımına uğradı. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) hello işlemi birden çok MaxOperationTimeout toocomplete yönlendirdiğinde döndürülür. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Merhaba erişim denetimi hello işlemi başarısız oldu. E_ACCESSDENIED döndürülür. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Merhaba işlemi gerçekleştirilirken bir çalışma zamanı hatası oluştu. Merhaba FabricClient yöntemlerden herhangi birini olası atabilirsiniz [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) özelliği hello tam hello özel durumun nedeni olan gösterir. Hata kodları hello tanımlanmış [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) numaralandırması. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |Merhaba işlem tür tooa geçici hata durumu başarısız oldu. Örneğin, bir çekirdek çoğaltmalarının geçici olarak erişilemediği için bir işlem başarısız olabilir. Geçici özel durumlar yeniden denenebilir toofailed işlemleri karşılık gelir. |

Bazı ortak [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) içinde döndürülen hatalar bir [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException):

| Hata | Koşul |
| --- |:--- |
| CommunicationError |Bir iletişim hatası hello işlemi toofail, yeniden deneme hello işlemi neden oldu. |
| InvalidCredentialType |Merhaba kimlik bilgisi türü geçersiz. |
| InvalidX509FindType |Merhaba X509FindType geçersiz. |
| InvalidX509StoreLocation |Merhaba X509 depolama konumu geçersiz. |
| InvalidX509StoreName |Merhaba X509 depolama adı geçersiz. |
| InvalidX509Thumbprint |Merhaba X509 sertifika parmak izi dizesi geçersiz. |
| InvalidProtectionLevel |Merhaba koruma düzeyi geçersiz. |
| InvalidX509Store |Merhaba X509 sertifika deposu açılamıyor. |
| InvalidSubjectName |Merhaba konu adı geçersiz. |
| InvalidAllowedCommonNameList |ortak ad liste dizesinin Hello biçimi geçersiz. Virgülle ayrılmış bir liste olması gerekir. |

