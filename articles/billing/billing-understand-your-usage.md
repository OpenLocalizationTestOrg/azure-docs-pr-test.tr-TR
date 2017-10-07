---
title: "aaaUnderstand Azure ayrıntılı kullanım | Microsoft Docs"
description: "Bilgi nasıl tooread ve ayrıntılı kullanımınızı CSV Azure aboneliğiniz için hello bölümlerini anlama"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Microsoft Azure ayrıntılı kullanım ücretlerini koşullarınızda anlama 
ayrıntılı kullanım ücretlerini CSV dosyası günlük içerir hello ve hello faturalama dönemi geçerli ölçer düzeyi kullanım ücretlerini. 

tooget ayrıntılı kullanımı dosyanızı bkz [nasıl tooget Azure faturalama fatura ve günlük kullanım verileri](billing-download-azure-invoice-daily-usage-date.md).
Elektronik tablo uygulamasında açabilirsiniz bir virgülle ayrılmış değerler (.csv) dosya biçiminde kullanılabilir. Kullanılabilir iki sürümlerini görürseniz, sürüm 2 indirin. Merhaba en güncel dosya biçiminde olmasıdır.

Kullanım ücretleri olan toplam hello **aylık** bir abonelik giderler. Kullanım ücretleri KREDİLERİ veya indirimleri dikkate yok.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Ayrıntılı hüküm ve ayrıntılı kullanım dosyanızın açıklamaları
Merhaba aşağıdaki bölümlerde sürüm hello ayrıntılı kullanım dosyasını 2 gösterilen hello önemli terimler açıklanmaktadır.

### <a name="statement"></a>Deyimi
Merhaba penceresinin üst kısmında hello hello ayın fatura döneminde kullanılan kullanım CSV dosya gösterir hello Hizmetleri ayrıntılı. Merhaba aşağıdaki tabloda hello hüküm ve bu bölümde gösterilen açıklamaları listelenmektedir.

| Sözleşme Dönemi | Açıklama |
| --- | --- |
|Fatura Dönemi |Merhaba ölçümler kullanıldığında hello fatura dönemi |
|Ölçüm Kategorisi |Merhaba kullanım için üst düzey hizmet Hello tanımlar |
|Ölçüm Alt Kategorisi |Merhaba hızını etkileyebilir Azure hizmeti başlangıç türünü tanımlar |
|Ölçüm Adı |Merhaba ölçü tüketilen hello ölçer tanımlar |
|Ölçüm Bölgesi |Veri merkezi konum temelinde fiyatlandırılır belirli hizmetleri için hello datacenter Hello konumunu tanımlar |
|SKU |Her Azure ölçer Hello benzersiz sistem tanımlayıcısı tanımlar |
|Birim |Merhaba hello hizmet içinde doludur birimi tanımlar. Örneğin, GB, saat, 10.000 s. |
|Kullanılan Miktar |Merhaba fatura döneminde kullanılan hello ölçer Hello miktarı |
|Dahil Edilen Miktar |ücret ödemeden, geçerli fatura dönemi içinde bulunan hello ölçer Hello miktarı |
|Kapasite Aşım Miktarı |Gösterir hello fark arasında Tüketilen Miktar hello ve dahil edilen miktar hello. Bu tutar için fatura. Kullandıkça Öde teklifleri için dahil edilen miktarı ile Merhaba teklif ile bu toplam olduğu hello Tüketilen Miktar hello aynıdır. |
|Taahhüt İçinde |6 veya 12 aylık teklifle ilgili, taahhüdü tutarı çıkartma hello ölçer ücretleri gösterir. Ölçer ücretleri kronolojik sırada düşülür. |
|Para birimi |Geçerli fatura döneminde kullanılan hello para birimi |
|Kapasite Aşımı |6 veya 12 aylık teklifle ilgili, taahhüt tutarı aşan hello ölçer ücretleri gösterir |
|Taahhüt Tarifesi |6 veya 12 aylık teklifle ilgili hello toplam taahhüdü tutarı temel hello taahhüt oranı gösterir |
|Fiyat |Faturalanabilir birim başına ücret ödersiniz hello oranı |
|Değer |Çarpılması hello fazla kullanım miktarı sütun hello oranı sütuna göre Hello sonucunu gösterir. Dahil edilen miktar Tüketilen Miktar aşmadığından hello Merhaba, bu sütunda hiçbir ücret yoktur. |

### <a name="daily-usage"></a>Günlük kullanımı

Merhaba hello CSV dosyası günlük kullanımı bölümü hello fatura oranları etkileyen kullanım ayrıntılarını gösterir. Merhaba aşağıdaki tabloda hello hüküm ve bu bölümde gösterilen açıklamaları listelenmektedir.

| Sözleşme Dönemi | Açıklama |
| --- | --- |
|Kullanım Tarihi |Merhaba ölçer kullanıldığında başlangıç tarihi |
|Ölçüm Kategorisi |Bu kullanım ait olduğu için hello üst düzey hizmet tanımlar |
|Ölçüm Kimliği |Merhaba tooprice fatura kullanım kullandı ölçer tanımlayıcı faturalandırılır. |
|Ölçüm Alt Kategorisi |Merhaba hızını etkileyebilir hello Azure hizmet türünü tanımlar |
|Ölçüm Adı |Merhaba ölçü tüketilen hello ölçer tanımlar |
|Ölçüm Bölgesi |Veri merkezi konum temelinde fiyatlandırılır belirli hizmetleri için hello datacenter Hello konumunu tanımlar |
|Birim |Tanımlayan bu hello ölçer hello birimi dolu içinde. Örneğin, GB, saat, 10.000 s. |
|Kullanılan Miktar |o gün için tüketilen hello ölçer Hello miktarı |
|Kaynak Konumu |Merhaba ölçer çalıştığı hello datacenter tanımlar |
|Kullanılan Hizmet |Merhaba, kullanılan Azure platformu hizmeti |
|Kaynak Grubu |Merhaba kaynak grubu hangi hello dağıtılan ölçer çalışıyor. <br/><br/>Daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|Örnek Kimliği | Merhaba ölçer Hello tanımlayıcısı. <br/><br/> Merhaba tanımlayıcısı oluşturulduğunda hello ölçer belirttiğiniz hello adı içeriyor. Hello kaynağın her iki hello adı olduğu veya hello tam kaynak kimliği Daha fazla bilgi için bkz: [Azure Kaynak Yöneticisi API'si](https://docs.microsoft.com/rest/api/resources/resources). |
|Etiketler | Etiket toohello ölçer atayın. Etiketler toogroup fatura kayıtları kullanın.<br/><br/>Örneğin, etiketleri toodistribute maliyetleri hello ölçer kullanan hello bölümünüzün kullanabilirsiniz. Verme etiketleri destekleyen hizmetlerin olan sanal makineler, depolama ve ağ hizmetlerini hello kullanılarak sağlanan [Azure Kaynak Yöneticisi API'si](https://docs.microsoft.com/rest/api/resources/resources). Daha fazla bilgi için bkz: [etiketlerle Azure kaynaklarınızı düzenleme](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/). |
|Ek Bilgi |Hizmete özgü meta veriler. Örneğin, bir görüntü türü için bir sanal makine. |
|Hizmet Bilgisi 1 |Merhaba hizmet aboneliğinizi tooon ait hello proje adı |
|Hizmet Bilgisi 2 |İsteğe bağlı hizmete özgü meta veriler yakalar eski alan |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>Merhaba ücretleri my ayrıntılı kullanımı dosyasında doğru olduğundan emin nasıl emin?
Daha fazla ayrıntı istediğiniz ayrıntılı kullanımı dosyanızı üzerinde bir ücret ise bakın [Microsoft Azure için faturanızı anlamak.](./billing-understand-your-bill.md)

## <a name="external"></a>Dış servis ücretleri nasıldır?
Dış hizmetler (Market siparişleri olarak da bilinir) bağımsız hizmet satıcıları tarafından sağlanan ve ayrı olarak faturalandırılır. Merhaba ücretleri hello Azure fatura üzerinde gösterme. toolearn daha, fazla [, Azure dış hizmet ücretlerini anlama](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?) hızla çözümlenen sorunu almak için.
