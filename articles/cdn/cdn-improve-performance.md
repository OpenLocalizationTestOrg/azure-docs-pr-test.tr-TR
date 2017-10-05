---
title: "Azure CDN dosyaları sıkıştırarak performansı | Microsoft Docs"
description: "Dosya aktarım hızı geliştirmeyi öğrenin ve Azure CDN dosyalarınızda sıkıştırarak sayfa yükleme performansı artırır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Azure CDN dosyaları sıkıştırarak performansı
Sıkıştırma, dosya aktarım hızını artırmak ve sunucudan gönderilmeden önce dosya boyutunu azaltarak sayfa yükleme performansı artırmak için basit ve etkili bir yöntemdir. Bant genişliği maliyetlerini düşürür ve kullanıcılarınız için daha esnek bir deneyim sağlar.

Sıkıştırmayı etkinleştirmek için iki yolu vardır:

* Kaynak sunucunuzda çalışması CDN sıkıştırılmış dosyaların geçirir, sıkıştırmayı etkinleştir ve sıkıştırılmış dosyaları bunları isteyen istemcilere teslim edin.
* Sunucularda çalışması CDN dosyaları sıkıştırır doğrudan CDN uç sıkıştırmayı etkinleştir ve kaynak sunucu tarafından sıkıştırılmaz bile, bunları son kullanıcılara hizmet.

> [!IMPORTANT]
> CDN yapılandırma değişiklikleri ağ üzerinden yayılması biraz zaman ayırın.  İçin <b>akamai'den Azure CDN</b> profilleri yayma genellikle bir dakika içinde tamamlanır.  İçin <b>verizon'dan Azure CDN</b> profilleri değişikliklerinizin 90 dakika içinde uygulanması genellikle görürsünüz.  CDN uç noktanız için sıkıştırmayı ayarlama ayarladınız ilk kez kullanıyorsanız, 1-2 saat ayarlarını sorun giderme önce Pop'lere yayılmadan sıkıştırma emin olmak için bekleyen düşünmelisiniz
> 
> 

## <a name="enabling-compression"></a>Sıkıştırmayı etkinleştirme
> [!NOTE]
> Standart ve Premium CDN katmanları için sıkıştırma işlevsellik sağlasa da, kullanıcı arabirimi farklıdır.  Standart ve Premium CDN katmanları arasındaki farklar hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Standart katman
> [!NOTE]
> Bu bölümde uygulandığı **verizon'dan Azure CDN standart** ve **akamai'den Azure CDN standart** profilleri.
> 
> 

1. CDN profili sayfasından yönetmek istediğiniz CDN uç noktası'ı tıklatın.
   
    ![CDN profili sayfasını uç noktaları](./media/cdn-file-compression/cdn-endpoints.png)
   
    CDN uç noktası sayfası açılır.
2. Tıklatın **yapılandırma** düğmesi.
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-config-btn.png)
   
    CDN yapılandırma sayfası açılır.
3. Aç **sıkıştırma**.
   
    ![CDN sıkıştırma seçenekleri](./media/cdn-file-compression/cdn-compress-standard.png)
4. Varsayılan türleri kullanın veya dosya türlerini ekleyerek veya çıkararak listesini değiştirin.
   
   > [!TIP]
   > While olası, onu ZIP, MP3, MP4, JPG, vb. gibi sıkıştırılmış biçimleri sıkıştırma uygulamak için önerilmez.
   > 
   > 
5. Yaptığınız değişiklikleri yaptıktan sonra tıklatın **kaydetmek** düğmesi.

### <a name="premium-tier"></a>Premium katman
> [!NOTE]
> Bu bölümde uygulandığı **verizon'dan Azure CDN Premium** profilleri.
> 
> 

1. CDN profili sayfasından tıklatın **Yönet** düğmesi.
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-manage-btn.png)
   
    CDN Yönetim Portalı'nı açar.
2. Üzerine gelerek **HTTP büyük** sekmesini ve ardından üzerine gelerek **önbellek ayarları** çıkma.  Tıklayın **sıkıştırma**.

    ![Dosya sıkıştırma seçimi](./media/cdn-file-compression/cdn-compress-select.png)
   
    Sıkıştırma seçeneklerini görüntülenir.
   
    ![Dosya sıkıştırma](./media/cdn-file-compression/cdn-compress-files.png)
3. Tıklayarak sıkıştırmayı etkinleştir **sıkıştırma etkin** radyo düğmesi.  İstediğiniz virgülle ayrılmış liste olarak (boşluksuz) sıkıştırmak için MIME türlerini girin **dosya türlerini** metin kutusu.
   
   > [!TIP]
   > While olası, onu ZIP, MP3, MP4, JPG, vb. gibi sıkıştırılmış biçimleri sıkıştırma uygulamak için önerilmez. 
   > 
   > 
4. Yaptığınız değişiklikleri yaptıktan sonra tıklatın **güncelleştirme** düğmesi.

## <a name="compression-rules"></a>Sıkıştırma kuralları
Bu tablo her senaryo için Azure CDN sıkıştırma davranışı açıklar.

> [!IMPORTANT]
> İçin **verizon'dan Azure CDN** (standart ve Premium), yalnızca uygun dosyaları sıkıştırılır.  Sıkıştırma için uygun olması için bir dosya gerekir:
> 
> * 128 bayttan büyük olmalıdır.
> * 1 MB'tan küçük olmalıdır.
> 
> İçin **akamai'den Azure CDN**, tüm dosyalar için sıkıştırma uygundur.
> 
> Tüm Azure CDN ürünü için bir dosya olan bir MIME türü olmalıdır [sıkıştırma için yapılandırılmış](#enabling-compression).
> 
> **Verizon'dan Azure CDN** profilleri (standart ve Premium) Destek **gzip** (GNU zip) **deflate**, **bzıp2**, veya **br** (Brotli) kodlama. Brotli kodlama için sıkıştırma yalnızca sınırında yapılır. İstemci/tarayıcı Brotli kodlama için istek göndermesi gerekir ve sıkıştırılmış varlık kaynak tarafında ilk sıkıştırılmış gerekir. 
>
>**Akamai'den Azure CDN** profilleri desteği yalnızca **gzip** kodlama.
> 
> **Akamai'den Azure CDN** uç noktaları her zaman isteği **gzip** kodlanmış istemci isteği bağımsız olarak kaynak dosyaları. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Sıkıştırma devre dışı veya dosya sıkıştırma için uygun değil
| İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi) | Önbelleğe alınmış dosya biçimi | İstemciye CDN yanıtı | Notlar |
| --- | --- | --- | --- |
| Sıkıştırılmış |Sıkıştırılmış |Sıkıştırılmış | |
| Sıkıştırılmış |Sıkıştırılmamış |Sıkıştırılmamış | |
| Sıkıştırılmış |Önbelleğe alınmamış |Sıkıştırılmış veya sıkıştırılmamış |Kaynak yanıtta bağlıdır |
| Sıkıştırılmamış |Sıkıştırılmış |Sıkıştırılmamış | |
| Sıkıştırılmamış |Sıkıştırılmamış |Sıkıştırılmamış | |
| Sıkıştırılmamış |Önbelleğe alınmamış |Sıkıştırılmamış | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>Sıkıştırma ve dosya sıkıştırma için uygun
| İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi) | Önbelleğe alınmış dosya biçimi | İstemciye CDN yanıtı | Notlar |
| --- | --- | --- | --- |
| Sıkıştırılmış |Sıkıştırılmış |Sıkıştırılmış |CDN transcodes desteklenen biçimler arasında |
| Sıkıştırılmış |Sıkıştırılmamış |Sıkıştırılmış |CDN sıkıştırır. |
| Sıkıştırılmış |Önbelleğe alınmamış |Sıkıştırılmış |Kaynak sıkıştırılmamış döndürürse CDN sıkıştırır.  **Verizon'dan Azure CDN** sıkıştırılmamış dosyayı ilk istek üzerine geçirir ve ardından sıkıştırır ve sonraki istekleri için dosyayı önbelleğe alır.  İle dosyaları `Cache-Control: no-cache` üstbilgi hiçbir zaman sıkıştırılır. |
| Sıkıştırılmamış |Sıkıştırılmış |Sıkıştırılmamış |CDN açma işlemi gerçekleştirir |
| Sıkıştırılmamış |Sıkıştırılmamış |Sıkıştırılmamış | |
| Sıkıştırılmamış |Önbelleğe alınmamış |Sıkıştırılmamış | |

## <a name="media-services-cdn-compression"></a>CDN sıkıştırma medya Hizmetleri
Medya Hizmetleri CDN akış uç noktalarını etkin sıkıştırma aşağıdaki içerik türleri için varsayılan olarak etkindir: uygulama/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, uygulama/f4m + xml. Azure portalını kullanarak belirtilen türleri için sıkıştırma bırakmak olamaz.  

## <a name="see-also"></a>Ayrıca bkz.
* [CDN dosya sıkıştırma sorunlarını giderme](cdn-troubleshoot-compression.md)    

