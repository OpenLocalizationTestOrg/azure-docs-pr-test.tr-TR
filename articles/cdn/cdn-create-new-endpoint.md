---
title: "aaaGetting Azure CDN ile çalışmaya | Microsoft Docs"
description: "Bu konu, nasıl tooenable hello Azure içerik teslim ağı (CDN) gösterir. Merhaba öğreticide bir yeni CDN profili ve uç noktası hello oluşturma açıklanmaktadır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Azure CDN kullanmaya başlama
Bu konu başlığında, yeni bir CDN profili ve uç noktası oluşturarak Azure CDN'yi etkinleştirme işlemi boyunca size yol gösterilecektir.

> [!IMPORTANT]
> Bir giriş toohow CDN çalışır, yanı sıra özelliklerinin bir listesi, hello bkz [CDN'ye genel bakış](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Yeni bir CDN profili oluşturma
CDN profili, CDN uç noktaları koleksiyonudur.  Her bir profil, bir veya daha fazla CDN uç noktası içerir.  Birden çok profilleri tooorganize toouse isteyebilir CDN uç noktalarınızı internet etki alanı, web uygulaması veya başka bir ölçüt.

> [!NOTE]
> Varsayılan olarak, tek bir Azure aboneliği sınırlı tooeight CDN profilleri ' dir. Her CDN profili, sınırlı tooten CDN uç noktası değildir.
> 
> CDN fiyatlandırması hello CDN profili düzeyinde uygulanır. Fiyatlandırma katmanlarına Azure CDN bir karışımını toouse istiyorsanız, birden çok CDN profili kullanmanız gerekir.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Yeni bir CDN uç noktası oluşturma
**toocreate yeni bir CDN uç noktası**

1. Merhaba, [Azure Portal](https://portal.azure.com), tooyour CDN profili gidin.  Bu toohello Pano hello önceki adımda sabitlemiş olabilirsiniz.  Bunu tıklayarak bulabilirsiniz değil, varsa **Gözat**, ardından **CDN profili**, ve hello profili tıklatarak tooadd uç noktanızı planladığınız.
   
    Merhaba CDN profili dikey penceresi görünür.
   
    ![CDN profili][cdn-profile-settings]
2. Merhaba tıklatın **uç nokta Ekle** düğmesi.
   
    ![Uç nokta ekle düğmesi][cdn-new-endpoint-button]
   
    Merhaba **bir uç nokta ekleyin** dikey penceresi görünür.
   
    ![Uç nokta ekleme dikey penceresi][cdn-add-endpoint]
3. Bu CDN uç noktası için bir **Ad** girin.  Bu ad kullanılan tooaccess hello etki alanındaki önbelleğe alınmış kaynaklarınıza olacaktır `<endpointname>.azureedge.net`.
4. Merhaba, **kaynak türü** açılan listesinde, başlangıç noktası türünüzü seçin.  Azure Storage hesabı için **Depolama**, Azure Bulut Hizmeti için **Bulut hizmeti**, Azure Web Uygulaması için **Web Uygulaması** veya genel olarak erişilebilen herhangi bir web sunucusu kaynağı (Azure'da veya başka bir konumda barındırılan) için **Özel kaynak** seçeneğini belirleyin.
   
    ![CDN kaynak türü](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. Merhaba, **kaynak ana bilgisayar adı** açılan listesinde, kaynak etki alanınızı yazın veya seçin.  Merhaba açılır 4. adımda belirttiğiniz hello türündeki tüm kullanılabilir kaynakları listeler.  Seçtiyseniz *özel kaynak* olarak, **kaynak türü**, özel kaynağınıza hello etki alanında yazmanız gerekir.
6. Merhaba, **kaynak yolu** metin kutusunda, istediğiniz toocache ya da bırak boş tooallow önbellek 5. adımda belirttiğiniz hello etki alanındaki herhangi bir kaynağa hello yolu toohello kaynakların girin.
7. Merhaba, **kaynak ana bilgisayar üstbilgisi**istediğiniz her istek ile CDN toosend hello hello ana bilgisayar üstbilgisi girin veya hello varsayılan adı bırakın.
   
   > [!WARNING]
   > Bazı Azure Storage ve Web uygulamaları gibi kaynak türleri hello ana bilgisayar üstbilgisi toomatch hello kaynak etki alanı hello gerektirir. Etki alanından farklı bir ana bilgisayar üstbilgisi gerektiren bir kaynağa sahip değilseniz, hello varsayılan değeri bırakmanız gerekir.
   > 
   > 
8. İçin **Protokolü** ve **kaynak bağlantı noktası**, hello protokolleri belirtin ve kullanılan tooaccess hello kaynak üzerindeki bağlantı noktaları.  En az bir protokol (HTTP veya HTTPS) seçilmelidir.
   
   > [!NOTE]
   > Merhaba **kaynak bağlantı noktası** tooretrieve bilgileri hello kaynaktan hangi bağlantı noktası hello uç noktası kullanır, yalnızca etkiler.  Merhaba uç noktanın kendisi yalnızca kullanılabilir tooend istemcilerin hello varsayılan HTTP ve HTTPS bağlantı noktalarındaki (80 ve 443) hello bakılmaksızın olacağını **kaynak bağlantı noktası**.  
   > 
   > **Akamai'den Azure CDN** uç noktaları hello tam TCP bağlantı noktası aralığı kaynakları için izin vermez.  İzin verilmeyen kaynak bağlantı noktalarının listesi için bkz. [Akamai'den Azure CDN İzin Verilen Kaynak Bağlantı Noktaları](https://msdn.microsoft.com/library/mt757337.aspx).  
   > 
   > CDN erişme HTTPS kullanarak içerik kısıtlamaları aşağıdaki hello sahiptir:
   > 
   > * Merhaba CDN tarafından sağlanan hello SSL sertifikası kullanması gerekir. Üçüncü taraf sertifikalar desteklenmez.
   > * Merhaba CDN tarafından sağlanan etki alanı kullanmanız gerekir (`<endpointname>.azureedge.net`) tooaccess HTTPS içeriği. HTTPS desteği Hello CDN şu anda özel sertifikaları desteklemediğinden özel etki alanı adları (CNAME'ler) için kullanılabilir değildir.
   > 
   > 
9. Merhaba tıklatın **Ekle** düğmesini toocreate hello yeni uç noktası.
10. Merhaba uç nokta oluşturulduktan sonra hello profil için uç noktalar listesinde görünür. Merhaba URL toouse tooaccess hello kaynak etki alanının yanı sıra, içeriği önbelleğe Hello liste görünümü gösterir.
    
    ![CDN uç noktası][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken hello uç nokta hemen kullanılabilir olmaz.  <b>Akamai'den Azure CDN</b> profilleri için yayma işlemi genellikle bir dakika içinde tamamlanır.  <b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.
    > 
    > Toouse hello CDN etki alanı adı Hello uç nokta yapılandırması toohello Pop'lere yayılmadan önce deneyen kullanıcılar HTTP 404 yanıt kodlarını alır.  Uç noktanızı oluşturmanızın ardından birkaç saat geçmesine karşın 404 yanıtlarını almaya devam ediyorsanız lütfen bkz. [404 durumu döndüren CDN uç noktası sorunlarını giderme](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>Ayrıca Bkz.
* [İsteklerin önbelleğe alınma davranışını sorgu dizeleriyle denetleme](cdn-query-string.md)
* [Nasıl tooMap CDN içerik tooa özel etki alanı](cdn-map-content-to-custom-domain.md)
* [Azure CDN uç noktasında varlıkları önceden yükleme](cdn-preload-endpoint.md)
* [Azure CDN Uç Noktasını Temizleme](cdn-purge-endpoint.md)
* [404 durumları döndüren CDN uç noktası sorunlarını giderme](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
