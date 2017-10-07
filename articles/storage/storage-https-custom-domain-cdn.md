---
title: "aaaUsing hello Azure CDN tooaccess BLOB'lar ile HTTPS üzerinden özel etki alanları"
description: "Blob depolama tooaccess ile toointegrate hello Azure CDN özel etki alanları ile HTTPS üzerinden nasıl BLOB bilgi edinin"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: 678e24a7dde5cb2f8feea177bb47c92f61035e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>HTTPS üzerinden özel etki alanları ile Hello Azure CDN tooaccess BLOB'ları kullanma

Azure içerik teslim ağı (CDN), artık HTTPS için özel etki alanı adlarını destekler.
HTTPS üzerinden özel etki alanınızı kullanarak bu özelliği tooaccess depolama BLOB'lar yararlanabilirsiniz. toodo bu nedenle, önce tooenable Azure CDN blob uç noktası ve harita hello CDN tooa özel etki alanı adınızın gerekir. Bu adımları uyguladıktan sonra özel etki alanınız için HTTPS'yi etkinleştirme tek tıklatmayla etkinleştirme, eksiksiz bir sertifika yönetimi aracılığıyla ile tüm hiçbir ek maliyet toonormal CDN fiyatlandırması basitleştirilmiştir.

Bu özellik, tooprotect hello gizlilik ve veri bütünlüğü aktarım sırasında hassas web uygulama verilerinizin sağladığından önemlidir. HTTPS üzerinden Hello SSL protokolü tooserve trafik kullanarak sağlar hello gönderildiğinde veri şifrelenir Internet. HTTPS güven ve kimlik doğrulaması sağlar ve web uygulamalarınızın saldırılara karşı korur.

> [!NOTE]
> Ayrıca tooproviding SSL desteği hello Azure CDN özel etki alanı adları için uygulama toodeliver yüksek bant genişliği içeriğinin Merhaba Dünya ölçek yardımcı olabilir.
> daha fazlasını toolearn kullanıma [hello Azure CDN genel bakış](../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Hızlı başlangıç

Merhaba adımlar, gerekli özel blob storage uç noktanız için tooenable HTTPS şunlardır:

1.  [Azure storage hesabı Azure CDN ile tümleştirmek](../cdn/cdn-create-a-storage-account-with-cdn.md).
    Bu makalede, bunu zaten yapmadıysanız, bir depolama hesabı hello Azure Portal oluşturmada size yol gösterilir.
2.  [Harita Azure CDN içerik tooa özel etki alanı](../cdn/cdn-map-content-to-custom-domain.md).
3.  [Azure CDN özel etki alanı üzerinde HTTPS'yi etkinleştirmek](../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>Paylaşılan erişim imzaları

Blob storage uç noktanız yapılandırılmış toodisallow anonim okuma erişimini ise, tooprovide ihtiyacınız olacak bir [paylaşılan erişim imzası (SAS)](storage-dotnet-shared-access-signature-part-1.md) tooyour özel etki alanı yaptığınız her istekte belirteci. Varsayılan olarak, blob depolama uç noktaları anonim okuma erişimini engellemek. Bkz: [kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](storage-manage-access-to-resources.md) paylaşılan erişim imzaları hakkında daha fazla bilgi için.

Azure CDN herhangi bir kısıtlama eklenen toohello SAS belirteci uymaz. Örneğin, tüm SAS belirteci sona erme süresi vardır. Bu içeriği hello CDN uç düğümlerden temizlenir kadar içerik Bunun anlamı ile süresi dolmuş bir SAS hala erişilebilir. Ne kadar veri CDN hello üzerinde hello önbellek yanıt üstbilgisi ayarı tarafından önbelleğe kontrol edebilirsiniz. Bkz: [Azure CDN Azure Storage bloblarında sona erme tarihi yönetme](../cdn/cdn-manage-expiration-of-blob-content.md) yönergeler için.

Hello için birden çok SAS URL'leri oluşturursanız, aynı blob uç öneririz sorgu dizesi, Azure CDN için önbelleğe alma özelliğini açmak. Tooensure budur, her URL benzersiz bir varlık olarak kabul edilir. Bkz: [Azure CDN önbelleğe alma davranışını sorgu dizeleriyle denetleme](../cdn/cdn-query-string.md) daha fazla bilgi için.

## <a name="http-toohttps-redirection"></a>HTTP tooHTTPS yeniden yönlendirme

Tooredirect HTTP trafiği tooHTTPS seçebilirler. Bu verizon'dan Azure CDN premium teklifi hello kullanılmasını gerektirir. Çok ihtiyacınız[Azure CDN kurallar altyapısı kullanarak geçersiz kılma HTTP davranışı](../cdn/cdn-rules-engine.md) şu kurala:

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Cdn uç noktası adı" CDN uç noktanız için yapılandırılan toohello adı gösterir. Bu değer hello aşağı açılır listeden seçebilirsiniz. "Kaynak yolu" Merhaba yol, statik içerik bulunduğu kaynak depolama hesabınızın içinde ifade eder.
Tek bir kapsayıcıdaki tüm statik içerik barındırıyorsa, "kaynak yolu" hello, kapsayıcı adıyla değiştirin.

Merhaba kuralı daha ayrıntılı bilgi edinmek için lütfen bkz [Azure CDN kurallar altyapısı özellikleri](../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Fiyatlandırma ve Faturalama

BLOB'ları Azure CDN eriştiğinizde, ödeme [Blob Depolama fiyatları](https://azure.microsoft.com/pricing/details/storage/blobs/) hello kenar düğümler ve hello kaynak (Blob Depolama) arasındaki trafik için ve [CDN fiyatları](https://azure.microsoft.com/pricing/details/cdn/) hello kenar düğümlerden erişilen veriler için.

Örneğin, bir Azure CDN kullanarak erişiliyor Batı ABD depolama hesabında olduğunu varsayalım. Kişi hello UK hello birini hello CDN yoluyla o depolama hesabındaki BLOB tooaccess çalışırsa, Azure hello kenar düğümüne hello UK bu blob için en yakın ilk denetler. Bulundu, bu kopyayı hello BLOB erişir ve CDN fiyatlandırması, CDN hello üzerinde erişilen için kullanacağı varsa. Bulunamazsa, Azure içinde çıkış neden olacak hello blob toohello kenar düğümünü, kopyalayacak ve işlem ücretleri belirtilen hello olarak Blob storage fiyatlandırması ve CDN faturalama sonuçlanır hello kenar düğümüne hello dosyada erişim.

Hello bakarken [CDN fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cdn/), özel etki alanı adları için HTTPS desteği olduğunu unutmayın yalnızca Verizon ürünleri (standart ve Premium) Azure CDN için kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar

[Blob storage uç noktanız için özel etki alanı adı yapılandırma](storage-custom-domain-name.md)
