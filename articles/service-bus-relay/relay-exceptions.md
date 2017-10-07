---
title: "aaaAzure geçiş özel durumları ve nasıl tooresolve bunları | Microsoft Docs"
description: "Azure geçiş özel durumlar listesini almak ve önerilen eylemler toohelp sürebilir çözümleyin."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Azure geçiş özel durumlar

Bu makalede Azure geçiş API'leri hello tarafından oluşturulan bazı özel durumlar listelenir. Bu başvuru konusu toochange, bu nedenle geri Güncelleştirmeleri denetle.

## <a name="exception-categories"></a>Özel durum kategorileri

Merhaba geçiş API'leri kategorileri aşağıdaki hello dönebilir özel durumları oluşturur. Ayrıca hello özel durumları toohelp Çöz sürebilir önerilen eylemleri listelenmiştir.

*   **Kodlama hatası kullanıcı**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Genel eylem**: devam etmeden önce toofix hello kod deneyin.
*   **Kurulum/yapılandırma hatası**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Genel eylem**: yapılandırmanızı gözden geçirin. Gerekirse, hello yapılandırmasını değiştirin.
*   **Geçici özel durumları**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Genel eylem**: hello işlemi yeniden deneyin veya kullanıcılara bildirin.
*   **Diğer özel durumlar**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Genel eylem**: belirli toohello özel durum türü. Bölümden hello Hello tabloya bakın. 

## <a name="exception-types"></a>Özel durum türleri

Merhaba aşağıdaki tabloda Mesajlaşma özel durum türleri ve bunların nedenleri listelenmektedir. Ayrıca, toohelp çözümleme hello özel durumlar önerilen eylemleri Not alır.

| **Özel durum türü** | **Açıklama** | **Önerilen eylem** | **Otomatik veya hemen yeniden deneme sırasında unutmayın** |
| --- | --- | --- | --- |
| [Zaman aşımı](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Merhaba sunucu istenen toohello yanıt vermedi işlem hello içinde belirtilen tarafından denetlenen zaman [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Sunucu istenen işlemi tamamlanmış hello hello. Bu toonetwork veya diğer altyapı gecikmeler gerçekleşebilir. |Tutarlılık Hello sistem durumunu denetleyin ve sonra gerekirse, yeniden deneyin. Bkz: [TimeoutException](#timeoutexception). |Yeniden deneme bazı durumlarda yardımcı olabilir; yeniden deneme mantığı toocode ekleyin. |
| [Geçersiz işlem](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Merhaba, kullanıcı işlemi hello sunucu veya hizmet içinde izin verilmiyor istedi. Merhaba özel durum iletisi Ayrıntılar için bkz. |Hello kodu ve hello belgelerine bakın. Bu hello işlemi geçerli istenen emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [İşlem iptal edildi.](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Bir deneme tooinvoke zaten kapatılmış, iptal veya atılmış bir nesne üzerinde bir işlemi yapılan. Nadir durumlarda hello ortam işlem zaten atıldı. |Merhaba kodu kontrol edip bırakılmış bir nesne üzerinde işlem çağrılmaz emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [Yetkisiz erişim](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) nesne bir belirteç alınamadı, hello belirteç geçersiz veya hello belirteci hello talep gerekli tooperform hello işlemi içermiyor. |Bu hello belirteç sağlayıcısı hello doğru değerlerle oluşturulduğundan emin olun. Merhaba erişim denetimi hizmeti Hello yapılandırmasını denetleyin. |Yeniden deneme bazı durumlarda yardımcı olabilir; yeniden deneme mantığı toocode ekleyin. |
| [Bağımsız değişken özel](https://msdn.microsoft.com/library/system.argumentexception.aspx),<br /> [Bağımsız değişkeni Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx),<br />[Bağımsız değişkeni aralık dışında](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Bir veya daha fazlasını hello oluştu:<br />Bir veya daha fazla sağlanan bağımsız değişkenler toohello yöntemi geçersiz.<br /> Merhaba URI çok sağlanan[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) veya [oluşturma](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) bir veya daha fazla yol kesimi içeriyor.<br />Merhaba URI şeması sağlanan çok[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) veya [oluşturma](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) geçersiz. <br />Başlangıç özellik değeri, 32 KB'den büyük. |Merhaba çağıran kodu kontrol edip hello bağımsız değişken doğru olduğundan emin olun. |Yeniden deneme yardımcı olmayacaktır. |
| [Sunucu meşgul](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Hizmet mümkün tooprocess hello isteği şu anda değil. |Merhaba istemci bir süre bekleyin sonra hello işlemi yeniden deneyin. |Merhaba istemci belirli bir zaman aralığından sonra yeniden. Yeniden deneme sonuçları farklı bir özel durum, özel durum hello yeniden deneme davranışını kontrol edin. |
| [Kotası aşıldı](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Varlık Mesajlaşma hello izin verilen boyut üst sınırına ulaştı. |Alanı hello varlıktan alıcı iletileri veya onun alt sıralar hello varlık oluşturun. Bkz: [QuotaExceededException](#quotaexceededexception). |İletileri hello sırada kaldırılmışsa yeniden deneme yardımcı olabilir. |
| [İleti boyutu aşıldı](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |İleti yükünü hello 256 KB'lik sınırını aşıyor. Bu hello 256 KB'lik sınırını hello toplam ileti boyutu olduğuna dikkat edin. Merhaba toplam ileti boyutu, Sistem özellikleri ve tüm Microsoft .NET ek yükü içerebilir. |Merhaba ileti yükü Hello boyutunu hello işlemi yeniden deneyin. |Yeniden deneme yardımcı olmayacaktır. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) belirli bir varlık için bir kota aşıldı gösterir.

Geçiş için bu özel durumun hello sarmalar [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), hangi dinleyicileri bu hello maksimum sayısını gösterir. Bu uç nokta için aşıldı. Bu hello belirtilir **MaximumListenersPerEndpoint** hello özel durum iletisi değeri.

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) bir kullanıcı tarafından başlatılan işlem hello işlemi zaman aşımından daha uzun sürüyor gösterir. 

Merhaba Hello değerini denetleyin [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) özelliği. Bu sınır basarsa ayrıca neden olabilecek bir [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Geçiş için geçiş gönderen bağlantısı ilk açtığınızda, zaman aşımı özel durumları alabilirsiniz. Bu özel durumun iki yaygın nedenleri şunlardır:

*   Merhaba [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) değeri (hatta tarafından bir saniyenin,) çok küçük olabilir.
* Bir şirket içi geçiş dinleyicisi yanıt vermiyor olabilir (veya dinleyicileri yeni istemci bağlantılarını kabul etmesini engelleyen güvenlik duvarı kuralları sorunlarla karşılaşabilirsiniz) ve hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) değerinden yaklaşık 20 saniye bir değerdir.

Örnek:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Olası nedenler
Bu hatanın sık karşılaşılan nedenleri şunlardır:

*   **Yanlış yapılandırma**
    
    Merhaba işlem zaman aşımı hello işletimsel koşul için çok küçük olabilir. Merhaba hello hello istemci SDK işlemi zaman aşımı için varsayılan değer 60 saniyedir. Toosee Hello kodunuzda toosomething çok küçük ayarlanan değer olup olmadığını denetleyin. Merhaba ağ CPU kullanımı ve hello koşulu için işlem toocomplete hello süresi etkileyebilir unutmayın. İyi bir fikirdir tooset hello işlemi zaman aşımı tooa çok küçük değer değil.
*   **Geçici hizmet hatası**

    Bazen, hello geçiş hizmeti isteklerini işleme gecikme karşılaşabilirsiniz. Bu, örneğin, yüksek trafik dönemlerde gerçekleşebilir. Bu gerçekleşirse, hello işlemi başarılı olana kadar bir gecikmeden sonra işlemi yeniden deneyin. Merhaba aynı işlem toofail birden çok denemeden sonra devam ederse, hello denetleyin [Azure hizmet durumu site](https://azure.microsoft.com/status/) hizmet kesintileri bilinen vardır, toosee.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure geçiş SSS](relay-faq.md)
* [Geçiş ad alanı oluşturma](relay-create-namespace-portal.md)
* [Azure geçişi ve .NET kullanmaya başlama](relay-hybrid-connections-dotnet-get-started.md)
* [Azure geçişi ve düğüm kullanmaya başlama](relay-hybrid-connections-node-get-started.md)

