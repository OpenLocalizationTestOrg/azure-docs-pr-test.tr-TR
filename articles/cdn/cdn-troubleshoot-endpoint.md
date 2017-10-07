---
title: "404 durumu döndüren aaaTroubleshooting Azure CDN uç noktası | Microsoft Docs"
description: "Azure CDN uç noktası ile 404 yanıt kodlarını sorunlarını giderin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>404 durumları döndüren CDN uç noktası sorunlarını giderme
Bu makale ile ilgili sorunları gidermenize yardımcı [CDN uç noktası](cdn-create-new-endpoint.md) 404 hataları döndürüyor.

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) ve tıklayın **destek alın**.

## <a name="symptom"></a>Belirti
CDN profili ve uç oluşturdunuz, ancak içeriğinizi toobe CDN hello üzerinde kullanılabilir olmadığı görülüyor.  İçeriğinizi hello CDN URL'sine aracılığıyla alırsınız HTTP 404 durum kodları tooaccess denemesi kullanıcılar. 

## <a name="cause"></a>Nedeni
Dahil birkaç olası nedenleri şunlardır:

* Merhaba dosyanın kaynağını görünür toohello CDN değil
* Merhaba endpoint hello yanlış yerinde hello CDN toolook neden yanlış yapılandırılmış
* Merhaba konak hello konak hello CDN başlığından reddediyor
* Hello bitiş saati toopropagate hello CDN boyunca sahip olmayan

## <a name="troubleshooting-steps"></a>Sorun giderme adımları
> [!IMPORTANT]
> Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken bir CDN uç noktası oluşturduktan sonra onu hemen kullanılabilir olmaz.  İçin <b>akamai'den Azure CDN</b> profilleri yayma işlemi genellikle bir dakika içinde tamamlanır.  <b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.  Hello adımları bu belge ve hala 404 yanıtlarını alıyorsunuz, destek bileti açmadan önce birkaç saat toocheck bekleyen göz önünde bulundurun.
> 
> 

### <a name="check-hello-origin-file"></a>Merhaba kaynak dosyasını denetleyin
İlk olarak, biz hello doğrulamalısınız önbelleğe alınmış istiyoruz, hello dosya bizim kaynak üzerinde kullanılabilir ve genel olarak erişilebilir.  In-özel veya Incognito bir oturum tooopen bir tarayıcı olan hızlı şekilde toodo hello ve doğrudan toohello dosyasını bulun.  Yalnızca yazın veya hello URL hello adres kutusuna yapıştırın ve beklediğiniz hello dosyasında sonuçlarının varsa bkz.  Bu örnekte, toouse sahibim adresindeki erişilebilir bir Azure depolama hesabındaki bir dosyayı yapacağım `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Gördüğünüz gibi hello test başarıyla geçirir.

![Başarılı!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Bu hello hızlı ve kolay şekilde tooverify dosyanızı genel olarak kullanılabilir, kuruluşunuzdaki bazı ağ yapılandırmaları sağlayabilir karşın, aslında, yalnızca görünür toousers ağ (olduğunda bu dosyayı genel kullanıma açık olduğunu görünümü hello Azure üzerinde barındırılan olsa bile).  Değil bir mobil cihaz tooyour kuruluşun ağına veya azure'daki bir sanal makineye bağlı olduğu gibi test edebilirsiniz, dış tarayıcı varsa, en iyi olacaktır.
> 
> 

### <a name="check-hello-origin-settings"></a>Merhaba kaynak ayarlarını kontrol edin
Biz doğrulandıktan göre hello dosya genel olarak kullanılabilir Internet Merhaba, kaynak ayarları doğrulamanız gerekir.  Merhaba, [Azure Portal](https://portal.azure.com)tooyour CDN profili göz atın ve sorun giderme hello uç noktasına tıklayın.  Merhaba kaynaklanan içinde **Endpoint** dikey penceresinde hello kaynak'ı tıklatın.  

![Vurgulanan kaynağına sahip uç nokta dikey penceresi](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Merhaba **kaynak** dikey penceresi görünür. 

![Kaynak dikey penceresi](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Kaynak türü ve ana bilgisayar adı
Merhaba doğrulayın **kaynak türü** düzeltin ve hello doğrulayın **kaynak ana bilgisayar adı**.  My örnekte `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, URL hello hello ana bilgisayar adı bölümü `cdndocdemo.blob.core.windows.net`.  Merhaba ekran görüntüsünde gördüğünüz gibi bu doğrudur.  Azure Storage, Web App ve bulut hizmeti kaynakları için hello **kaynak ana bilgisayar adı** alan olup, doğru yazım denetimi hakkında tooworry gerekmez şekilde bir açılır.  Ancak, özel bir kaynak kullanıyorsanız, olmasından *kesinlikle kritik* , ana bilgisayar adı doğru yazıldığından!

#### <a name="http-and-https-ports"></a>HTTP ve HTTPS bağlantı noktaları
Merhaba başka bir şey toocheck olduğundan, **HTTP** ve **HTTPS bağlantı noktalarını**.  Çoğu durumda, 80 ve 443 doğru olduğundan ve hiçbir değişiklik yapılmasını gerektirir.  Ancak, Hello kaynak sunucu farklı bir bağlantı noktasında dinleme yapıyorsanız, burada toobe gerekir.  Emin değilseniz, yalnızca kaynak dosyanızı hello URL'sini bakın.  Merhaba HTTP ve HTTPS belirtimleri hello varsayılan olarak 80 ve 443 numaralı bağlantı noktalarını belirtin. My URL'de `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, bir bağlantı noktası, hello varsayılan 443 olduğu varsayılır ve ayarlarımı doğru şekilde belirtilmedi.  

Ancak, daha önce test, kaynak dosya için hello URL söyleyin `http://www.contoso.com:8080/file.txt`.  Not hello `:8080` hello sonunda hello hostname kesimi.  Merhaba tarayıcı toouse bağlantı noktası söyler `8080` tooconnect toohello web sunucusunda `www.contoso.com`, tooenter 8080 hello içinde gerekir böylece **HTTP bağlantı noktası** alan.  Hangi bağlantı noktası hello endpoint tooretrieve bilgileri hello kaynaktan kullanır Bu bağlantı noktası ayarlarını yalnızca etkileyen önemli toonote olur.

> [!NOTE]
> **Akamai'den Azure CDN** uç noktaları hello tam TCP bağlantı noktası aralığı kaynakları için izin vermez.  İzin verilmeyen kaynak bağlantı noktalarının listesi için bkz. [Akamai'den Azure CDN İzin Verilen Kaynak Bağlantı Noktaları](https://msdn.microsoft.com/library/mt757337.aspx).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Merhaba uç nokta ayarlarını kontrol edin
Hello üzerinde geri **Endpoint** dikey penceresinde hello tıklatın **yapılandırma** düğmesi.

![Uç nokta dikey Yapılandırma düğmesi vurgulanan](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

uç noktanın hello **yapılandırma** dikey penceresi görünür.

![Dikey yapılandırın](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protokoller
İçin **protokolleri**, hello istemcileri tarafından kullanılan hello Protokolü seçili olduğundan emin olun.  Merhaba hello istemci tarafından kullanılan aynı protokol önemli toohave hello kaynak hello önceki bölümde doğru yapılandırılmış bağlantı noktaları olacak şekilde bir tooaccess hello kaynak kullanılan hello olacaktır.  Merhaba endpoint hello varsayılan HTTP ve HTTPS bağlantı noktalarındaki (80 ve 443) hello kaynak bağlantı noktalarının bakılmaksızın yalnızca dinler.

Şimdi tooour kuramsal örnekle dönmek `http://www.contoso.com:8080/file.txt`.  Contoso unutmayın olarak belirtilen `8080` kendi HTTP bağlantı noktası, ancak aynı zamanda belirtilen varsayalım `44300` kendi HTTPS bağlantı noktası olarak.  Adlı bir uç nokta oluşturduysanız `contoso`, kendi CDN uç noktası ana bilgisayar adı olacaktır `contoso.azureedge.net`.  Bir istek için `http://contoso.azureedge.net/file.txt` hello uç noktası HTTP bağlantı noktası 8080 tooretrieve üzerinde kullanacağınız bir HTTP isteğinin olduğundan bu hello kaynaktan.  HTTPS üzerinden güvenli bir isteği `https://contoso.azureedge.net/file.txt`, retriving hello zaman hello kaynak dosyadan hello uç nokta toouse HTTPS bağlantı noktası 44300 neden olur.

#### <a name="origin-host-header"></a>Kaynak ana bilgisayar üstbilgisi
Merhaba **kaynak ana bilgisayar üstbilgisi** toohello kaynak her istek ile gönderilen hello ana bilgisayar üst bilgisi değeri.  Çoğu durumda, bu olması hello aynı hello **kaynak ana bilgisayar adı** biz doğrulamıştınız.  Bu alandaki yanlış bir değere 404 durumları genellikle neden olmaz, ancak büyük olasılıkla toocause hangi hello kaynak bekliyor bağlı olarak diğer 4xx durumlar olur.

#### <a name="origin-path"></a>Kaynak yolu
Son olarak, kimliğinizi doğrulamanız gerekir bizim **kaynak yolu**.  Varsayılan olarak bu boştur.  Toonarrow hello kapsam istiyorsanız, bu alan yalnızca kullanması gereken kaynak barındırılan hello kaynakları istediğiniz toomake CDN hello üzerinde kullanılabilir.  

I sol şekilde Örneğin, Noktam tüm kaynaklar my depolama hesabı toobe üzerinde kullanılabilir istediğim **kaynak yolu** boş.  Bir istek çok buna`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` Noktam öğesinden bir bağlantı için çok sonuçlanır`cdndocdemo.core.windows.net` isteklerine `/publicblob/lorem.txt`.  Benzer şekilde, bir istek için `https://cdndocdemo.azureedge.net/donotcache/status.png` sonuçları hello uç nokta talep edilmesine `/donotcache/status.png` hello kaynaktan.

Ancak ne toouse hello CDN için her yol bilgilerimi kaynak üzerinde istemiyorum?  I söyleyin yalnızca istediği tooexpose hello `publicblob` yolu.  I girerseniz, */publicblob* içinde my **kaynak yolu** hello uç nokta tooinsert neden olacak alan */publicblob* toohello kaynak yapılan her isteği önce.  Bu, o hello talebi anlamına gelir `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` şimdi hello URL hello isteği bölümü gerçekte sürer `/publicblob/lorem.txt`ve ilave `/publicblob` toohello başına. Bu istek için sonuçlanır `/publicblob/publicblob/lorem.txt` hello kaynaktan.  Bu yol tooan gerçek dosya sorunu çözmezse, hello kaynak 404 durumu döndürür.  Merhaba doğru URL tooretrieve lorem.txt Bu örnekte gerçekte olacaktır `https://cdndocdemo.azureedge.net/lorem.txt`.  Hello içerme Not */publicblob* yolu hiç hello isteği kısmı hello URL olduğundan `/lorem.txt` ve hello endpoint ekler `/publicblob`, sonuçta elde edilen içinde `/publicblob/lorem.txt` geçirilen toohello kaynak hello istek bırakılıyor .

