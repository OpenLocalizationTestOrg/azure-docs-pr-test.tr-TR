---
title: "B2B izleme - aaaX12 izleme şemaları Azure Logic Apps | Microsoft Docs"
description: "Azure tümleştirme hesabınızda işlemlerdeki izleme şemaları toomonitor B2B iletileri X12 kullanın."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Toomonitor başarı, hata ve ileti özellikleri iletileri başlangıç veya X12 izlemeyi etkinleştir
Şemalar izleme bu X12 kullanabilirsiniz, Azure tümleştirme hesap toohelp işletmeden işletmeye (B2B) işlemleri izleyin:

* X12 işlem izleme şema ayarlayın
* X12 işlem şema izleme onayı ayarlama
* X12 izleme şeması değişimi
* Şema izleme bildirim X12 değişimi
* İzleme şema X12 işlev grubu
* Şema izleme bildirim X12 işlev grubu

## <a name="x12-transaction-set-tracking-schema"></a>X12 işlem izleme şema ayarlayın
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| senderPartnerName | Dize | X12 gönderenin ortak adı iletisi. (İsteğe bağlı) |
| receiverPartnerName | Dize | X12 alıcının ortak adı iletisi. (İsteğe bağlı) |
| senderQualifier | Dize | İş ortağı niteleyicisi gönderin. (Zorunlu) |
| senderIdentifier | Dize | İş ortağı tanımlayıcı gönderin. (Zorunlu) |
| receiverQualifier | Dize | İş ortağı niteleyicisi alırsınız. (Zorunlu) |
| receiverIdentifier | Dize | İş ortağı tanımlayıcısını alır. (Zorunlu) |
| agreementName | Dize | Merhaba X12 sözleşmesi toowhich hello iletileri adını çözümlenir. (İsteğe bağlı) |
| Yönü | Enum | Hello ileti akış yönünü alma veya gönderme. (Zorunlu) |
| interchangeControlNumber | Dize | Değiş tokuş denetim numarası. (İsteğe bağlı) |
| functionalGroupControlNumber | Dize | İşlev denetim sayısı. (İsteğe bağlı) |
| transactionSetControlNumber | Dize | İşlem Denetim numarası ayarlayın. (İsteğe bağlı) |
| correlationMessageId | Dize | Bağıntı ileti kimliği. {AgreementName} bileşimini {*GroupControlNumber*} {TransactionSetControlNumber}. (İsteğe bağlı) |
| messageType | Dize | İşlem ayarlayın veya belge türü. (İsteğe bağlı) |
| isMessageFailed | Boole değeri | Olup hello X12 iletisi başarısız oldu. (Zorunlu) |
| isTechnicalAcknowledgmentExpected | Boole değeri | Olup hello Teknik Bildirim hello X12 anlaşmasında yapılandırılır. (Zorunlu) |
| isFunctionalAcknowledgmentExpected | Boole değeri | Olup hello işlevsel bildirim hello X12 anlaşmasında yapılandırılır. (Zorunlu) |
| needAk2LoopForValidMessages | Boole değeri | Merhaba AK2 döngü için geçerli bir ileti gerekli olup olmadığı. (Zorunlu) |
| segmentsCount | Tamsayı | Merhaba X12 işlemde bölümlerinin sayısını ayarlayın. (İsteğe bağlı) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>X12 işlem şema izleme onayı ayarlama
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| senderPartnerName | Dize | X12 gönderenin ortak adı iletisi. (İsteğe bağlı) |
| receiverPartnerName | Dize | X12 alıcının ortak adı iletisi. (İsteğe bağlı) |
| senderQualifier | Dize | İş ortağı niteleyicisi gönderin. (Zorunlu) |
| senderIdentifier | Dize | İş ortağı tanımlayıcı gönderin. (Zorunlu) |
| receiverQualifier | Dize | İş ortağı niteleyicisi alırsınız. (Zorunlu) |
| receiverIdentifier | Dize | İş ortağı tanımlayıcısını alır. (Zorunlu) |
| agreementName | Dize | Merhaba X12 sözleşmesi toowhich hello iletileri adını çözümlenir. (İsteğe bağlı) |
| Yönü | Enum | Hello ileti akış yönünü alma veya gönderme. (Zorunlu) |
| interchangeControlNumber | Dize | Merhaba işlevsel bildirim denetimi sayısı değişim. İşlev bildirim hello gönderilen iletileri toopartner için burada alınan hello gönderme tarafı için değer doldurur. (İsteğe bağlı) |
| functionalGroupControlNumber | Dize | Merhaba işlevsel bildirim işlevsel Grup denetimi sayısı. İşlev bildirim hello gönderilen iletileri toopartner için burada alınan hello gönderme tarafı için değer doldurur. (İsteğe bağlı) |
| isaSegment | Dize | Selamlama iletisine ISA kesimi. İşlev bildirim hello gönderilen iletileri toopartner için burada alınan hello gönderme tarafı için değer doldurur. (İsteğe bağlı) |
| gsSegment | Dize | Selamlama iletisine GS kesimi. İşlev bildirim hello gönderilen iletileri toopartner için burada alınan hello gönderme tarafı için değer doldurur. (İsteğe bağlı) |
| respondingfunctionalGroupControlNumber | Dize | Değişim kontrol numarası yanıt. (İsteğe bağlı) |
| respondingFunctionalGroupId | Dize | İşlevsel Grup Kimliği yanıt, hangi hello bildirim tooAK101 eşler. (İsteğe bağlı) |
| respondingtransactionSetControlNumber | Dize | Yanıt veren işlem denetim numarası ayarlayın. (İsteğe bağlı) |
| respondingTransactionSetId | Dize | Yanıt veren işlem tooAK201 hello bildirim eşlemeleri kimliği ayarlayın. (İsteğe bağlı) |
| statusCode | Boole değeri | İşlem bildirim durum kodu ayarlayın. (Zorunlu) |
| segmentsCount | Enum | Bildirim durum kodu. İzin verilen değerler **kabul edilen**, **reddedildi**, ve **AcceptedWithErrors**. (Zorunlu) |
| processingStatus | Enum | Merhaba bildirim işlem durumu. İzin verilen değerler **alınan**, **oluşturulan**, ve **gönderilen**. (Zorunlu) |
| correlationMessageId | Dize | Bağıntı ileti kimliği. {AgreementName} bileşimini {*GroupControlNumber*} {TransactionSetControlNumber}. (İsteğe bağlı) |
| isMessageFailed | Boole değeri | Olup hello X12 iletisi başarısız oldu. (Zorunlu) |
| ak2Segment | Dize | Onayı hello işlem kümesinde için işlevsel grubuna aldı. (İsteğe bağlı) |
| ak3Segment | Dize | Veri segmenti hatalarını bildirir. (İsteğe bağlı) |
| ak5Segment | Dize | Merhaba AK2 kesimdeki tanımlanan ayarlamak hello işlem kabul ya da reddedilen ve neden raporlar. (İsteğe bağlı) |

## <a name="x12-interchange-tracking-schema"></a>X12 izleme şeması değişimi
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| senderPartnerName | Dize | X12 gönderenin ortak adı iletisi. (İsteğe bağlı) |
| receiverPartnerName | Dize | X12 alıcının ortak adı iletisi. (İsteğe bağlı) |
| senderQualifier | Dize | İş ortağı niteleyicisi gönderin. (Zorunlu) |
| senderIdentifier | Dize | İş ortağı tanımlayıcı gönderin. (Zorunlu) |
| receiverQualifier | Dize | İş ortağı niteleyicisi alırsınız. (Zorunlu) |
| receiverIdentifier | Dize | İş ortağı tanımlayıcısını alır. (Zorunlu) |
| agreementName | Dize | Merhaba X12 sözleşmesi toowhich hello iletileri adını çözümlenir. (İsteğe bağlı) |
| Yönü | Enum | Hello ileti akış yönünü alma veya gönderme. (Zorunlu) |
| interchangeControlNumber | Dize | Değiş tokuş denetim numarası. (İsteğe bağlı) |
| isaSegment | Dize | İleti ISA kesimi. (İsteğe bağlı) |
| isTechnicalAcknowledgmentExpected | Boole değeri | Olup hello Teknik Bildirim hello X12 anlaşmasında yapılandırılır. (Zorunlu) |
| isMessageFailed | Boole değeri | Olup hello X12 iletisi başarısız oldu. (Zorunlu) |
| isa09 | Dize | X12 belge değişim tarih. (İsteğe bağlı) |
| isa10 | Dize | X12 değişim zaman belge. (İsteğe bağlı) |
| isa11 | Dize | X12 Değişim Denetimi standartları tanımlayıcısı. (İsteğe bağlı) |
| isa12 | Dize | X12 Değişim Denetimi sürüm numarası. (İsteğe bağlı) |
| isa14 | Dize | X12 bildirim istendi. (İsteğe bağlı) |
| isa15 | Dize | Test veya üretim için göstergesi. (İsteğe bağlı) |
| isa16 | Dize | Öğe ayırıcı. (İsteğe bağlı) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>Şema izleme bildirim X12 değişimi
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| senderPartnerName | Dize | X12 gönderenin ortak adı iletisi. (İsteğe bağlı) |
| receiverPartnerName | Dize | X12 alıcının ortak adı iletisi. (İsteğe bağlı) |
| senderQualifier | Dize | İş ortağı niteleyicisi gönderin. (Zorunlu) |
| senderIdentifier | Dize | İş ortağı tanımlayıcı gönderin. (Zorunlu) |
| receiverQualifier | Dize | İş ortağı niteleyicisi alırsınız. (Zorunlu) |
| receiverIdentifier | Dize | İş ortağı tanımlayıcısını alır. (Zorunlu) |
| agreementName | Dize | Merhaba X12 sözleşmesi toowhich hello iletileri adını çözümlenir. (İsteğe bağlı) |
| Yönü | Enum | Hello ileti akış yönünü alma veya gönderme. (Zorunlu) |
| interchangeControlNumber | Dize | Değişim Denetimi ortaklarından alınan hello teknik bildirim sayısı. (İsteğe bağlı) |
| isaSegment | Dize | Ortaklarından alınan hello teknik onayı için ISA kesimi. (İsteğe bağlı) |
| respondingInterchangeControlNumber |Dize | Değiş tokuş ortaklarından alınan hello teknik onayı için Denetim numarası. (İsteğe bağlı) |
| isMessageFailed | Boole değeri | Olup hello X12 iletisi başarısız oldu. (Zorunlu) |
| statusCode | Enum | Bildirim durum kodu değişim. İzin verilen değerler **kabul edilen**, **reddedildi**, ve **AcceptedWithErrors**. (Zorunlu) |
| processingStatus | Enum | Onay durumu. İzin verilen değerler **alınan**, **oluşturulan**, ve **gönderilen**. (Zorunlu) |
| ta102 | Dize | Tarih değişim. (İsteğe bağlı) |
| ta103 | Dize | Zaman değişim. (İsteğe bağlı) |
| ta105 | Dize | Not kodu değişim. (İsteğe bağlı) |

## <a name="x12-functional-group-tracking-schema"></a>İzleme şema X12 işlev grubu
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| senderPartnerName | Dize | X12 gönderenin ortak adı iletisi. (İsteğe bağlı) |
| receiverPartnerName | Dize | X12 alıcının ortak adı iletisi. (İsteğe bağlı) |
| senderQualifier | Dize | İş ortağı niteleyicisi gönderin. (Zorunlu) |
| senderIdentifier | Dize | İş ortağı tanımlayıcı gönderin. (Zorunlu) |
| receiverQualifier | Dize | İş ortağı niteleyicisi alırsınız. (Zorunlu) |
| receiverIdentifier | Dize | İş ortağı tanımlayıcısını alır. (Zorunlu) |
| agreementName | Dize | Merhaba X12 sözleşmesi toowhich hello iletileri adını çözümlenir. (İsteğe bağlı) |
| Yönü | Enum | Hello ileti akış yönünü alma veya gönderme. (Zorunlu) |
| interchangeControlNumber | Dize | Değiş tokuş denetim numarası. (İsteğe bağlı) |
| functionalGroupControlNumber | Dize | İşlev denetim sayısı. (İsteğe bağlı) |
| gsSegment | Dize | İleti GS kesimi. (İsteğe bağlı) |
| isTechnicalAcknowledgmentExpected | Boole değeri | Olup hello Teknik Bildirim hello X12 anlaşmasında yapılandırılır. (Zorunlu) |
| isFunctionalAcknowledgmentExpected | Boole değeri | Olup hello işlevsel bildirim hello X12 anlaşmasında yapılandırılır. (Zorunlu) |
| isMessageFailed | Boole değeri | Olup hello X12 iletisi başarısız oldu. (Zorunlu)|
| gs01 | Dize | İşlev tanımlayıcı kod. (İsteğe bağlı) |
| gs02 | Dize | Uygulama gönderenin kodu. (İsteğe bağlı) |
| gs03 | Dize | Uygulama alıcının kodu. (İsteğe bağlı) |
| gs04 | Dize | İşlev grubunu tarih. (İsteğe bağlı) |
| gs05 | Dize | İşlev grubunu süre. (İsteğe bağlı) |
| gs07 | Dize | Sorumlu Teşkilatı kodu. (İsteğe bağlı) |
| gs08 | Dize | Yayın/sürüm/endüstri tanımlayıcı kod. (İsteğe bağlı) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>Şema izleme bildirim X12 işlev grubu
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| senderPartnerName | Dize | X12 gönderenin ortak adı iletisi. (İsteğe bağlı) |
| receiverPartnerName | Dize | X12 alıcının ortak adı iletisi. (İsteğe bağlı) |
| senderQualifier | Dize | İş ortağı niteleyicisi gönderin. (Zorunlu) |
| senderIdentifier | Dize | İş ortağı tanımlayıcı gönderin. (Zorunlu) |
| receiverQualifier | Dize | İş ortağı niteleyicisi alırsınız. (Zorunlu) |
| receiverIdentifier | Dize | İş ortağı tanımlayıcısını alır. (Zorunlu) |
| agreementName | Dize | Merhaba X12 sözleşmesi toowhich hello iletileri adını çözümlenir. (İsteğe bağlı) |
| Yönü | Enum | Hello ileti akış yönünü alma veya gönderme. (Zorunlu) |
| interchangeControlNumber | Dize | Merhaba doldurur değiş tokuş denetim numarası, iş ortaklarının sunduğu Teknik Bildirim alındığında yan gönderin. (İsteğe bağlı) |
| functionalGroupControlNumber | Dize | İşlev grubunu denetim Merhaba doldurur hello teknik bildirim sayısı, iş ortaklarının sunduğu Teknik Bildirim alındığında yan gönderin. (İsteğe bağlı) |
| isaSegment | Dize | Değişim aynı numarası, ancak belirli durumlarda yalnızca doldurulan kontrol eder. (İsteğe bağlı) |
| gsSegment | Dize | İşlevsel grubuyla aynı numarası, ancak belirli durumlarda yalnızca doldurulan kontrol eder. (İsteğe bağlı) |
| respondingfunctionalGroupControlNumber | Dize | Merhaba özgün işlevsel grup sayısını denetler. (İsteğe bağlı) |
| respondingFunctionalGroupId | Dize | Merhaba bildirim işlevsel grubu kimliği tooAK101 eşlemeleri (İsteğe bağlı) |
| isMessageFailed | Boole değeri | Olup hello X12 iletisi başarısız oldu. (Zorunlu) |
| statusCode | Enum | Bildirim durum kodu. İzin verilen değerler **kabul edilen**, **reddedildi**, ve **AcceptedWithErrors**. (Zorunlu) |
| processingStatus | Enum | Merhaba bildirim işlem durumu. İzin verilen değerler **alınan**, **oluşturulan**, ve **gönderilen**. (Zorunlu) |
| ak903 | Dize | İşlem kümesi alınan sayısı. (İsteğe bağlı) |
| ak904 | Dize | İşlem kümesi sayısı tanımlanan hello işlevsel grubunda kabul edildi. (İsteğe bağlı) |
| ak9Segment | Dize | Merhaba işlevsel hello AK1 kesimdeki belirlenen grubu kabul edilen veya reddedilen olup olmadığını ve neden. (İsteğe bağlı) |

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [B2B iletileri izleme](logic-apps-monitor-b2b-message.md).
* Daha fazla bilgi edinmek [AS2 izleme şemaları](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Daha fazla bilgi edinmek [B2B şemaları izleme özel](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Hakkında bilgi edinin [hello Operations Management Suite portalına B2B iletilerinde izleme](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Merhaba hakkında daha fazla bilgi [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).  
