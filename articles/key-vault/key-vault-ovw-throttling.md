---
ms.assetid: 
title: "aaaAzure anahtar kasası azaltma Kılavuzu | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Azure anahtar Kasası'nı Kılavuzu azaltma

Azaltma eşzamanlı çağrıları toohello Azure hizmeti tooprevent aşırı kaynakların kullanımı hello sayısını sınırlayan başlatma bir işlemdir. Azure anahtar kasası (AKV) tasarlanmış toohandle istekleri hacmi yüksek olur. Bunaltıcı bir istek sayısı ortaya çıkarsa, istemcinin istek azaltma en iyi performansı ve güvenilirliği hello AKV hizmeti için korumaya yardımcı olur.

Azaltma sınırları hello senaryo göre değişir. Örneğin, büyük hacimli yazma gerçekleştiriyorsanız hello olasılığı azaltma için yalnızca okuma gerçekleştirdiğiniz varsa daha yüksek olur.

## <a name="how-does-key-vault-handle-its-limits"></a>Anahtar kasası sınırlarına nasıl işler?

Anahtar kasası hizmet sınırları tooprevent kötüye kaynakların vardır ve tüm anahtar Kasası'nın istemcileri için hizmet kalitesi emin olun. Bir hizmeti eşiği aşıldığında, anahtar kasası herhangi başka bir istek Bu istemciden gelen bir süre için sınırlar. Bu gerçekleştiğinde, anahtar kasası HTTP durum kodu 429 döndürür (çok sayıda istek), ve hello istekleri başarısız olur. Ayrıca, anahtar kasası tarafından izlenen hello azaltma sınırları doğrultusunda 429 bir sayı döndürür isteği başarısız oldu. 

Daha yüksek azaltma sınırları için geçerli iş durum varsa, lütfen bizimle iletişime geçin.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>Nasıl yanıt tooservice uygulamanızda toothrottle sınırlar

Merhaba şunlardır **en iyi uygulamalar** uygulamanızı azaltma için:
- İstek başına işlemleri Hello sayısını azaltın.
- İstekleri Hello sıklığını azaltın.
- Hemen yeniden deneme kaçının. 
    - Tüm istekler, kullanım sınırları karşı tahakkuk eder.

Uygulamanızın hata işleme uyguladığınızda, kullanım hello HTTP hata kodunu 429 toodetect hello gerekir istemci-tarafı azaltma. Merhaba isteği yeniden HTTP 429 hata koduyla başarısız olursa, bir Azure hizmeti sınırını hala karşılaşıyoruz. İstemci-tarafı azaltma yöntemi, başarılı olana dek hello isteği yeniden deneniyor toouse hello önerilen devam edin.

### <a name="recommended-client-side-throttling-method"></a>Önerilen istemci-tarafı azaltma yöntemi

HTTP hata kodunu 429, üstel geri alma yaklaşımı kullanarak, istemci azaltma başlayın:

1. Yeniden deneme isteği 1 saniye bekleyin
2. Hala 2 saniye bekleyin kısıtlanan, isteği yeniden deneyin
3. Hala 4 saniye bekleyin kısıtlanan, isteği yeniden deneyin
4. Hala 8 saniye bekleyin kısıtlanan, isteği yeniden deneyin
5. Hala 16 saniye bekleyin kısıtlanan, isteği yeniden deneyin

Bu noktada, HTTP 429 yanıt kodları alamıyorsanız.

## <a name="see-also"></a>Ayrıca bkz.

Microsoft Cloud hello üzerinde azaltma daha derin yönlendirmesi için bkz: [azaltma düzeni](https://docs.microsoft.com/azure/architecture/patterns/throttling).

