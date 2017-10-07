---
title: "Azure CDN dosyalarında sıkıştırma aaaImprove performansı | Microsoft Docs"
description: "Nasıl tooimprove dosya aktarma hızı ve artar sayfa yükleme performansı Azure CDN dosyalarınızda sıkıştırarak öğrenin."
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
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Azure CDN dosyaları sıkıştırarak performansı
Basit ve etkili yöntemi tooimprove dosya aktarım hızı sıkıştırma olduğu ve önceki dosya boyutunu azaltarak sayfa yükleme performansı artırır hello sunucudan gönderilir. Bant genişliği maliyetlerini düşürür ve kullanıcılarınız için daha esnek bir deneyim sağlar.

Tooenable sıkıştırma iki yolu vardır:

* Bu durumda hello hello CDN geçer sıkıştırılmış dosyaları dışarıda bırak ve bunları isteyen sıkıştırılmış dosyaların tooclients teslim kaynak sunucunuzda sıkıştırmasını etkinleştirebilirsiniz.
* Servis talebi hello CDN sıkıştırır dosyaları hello ve hello kaynak sunucu tarafından sıkıştırılmaz olsa bile bunları tooend kullanıcılar, hizmet doğrudan CDN uç sunucularında sıkıştırmasını etkinleştirebilirsiniz.

> [!IMPORTANT]
> CDN yapılandırma değişikliklerini bazı zaman toopropagate hello ağ üzerinden alın.  İçin <b>akamai'den Azure CDN</b> profilleri yayma genellikle bir dakika içinde tamamlanır.  İçin <b>verizon'dan Azure CDN</b> profilleri değişikliklerinizin 90 dakika içinde uygulanması genellikle görürsünüz.  Bu hello sıkıştırmayı ayarlama, CDN uç noktası için ayarladığınız ilk kez kullanıyorsanız, 1-2 saat toobe hello sıkıştırma ayarları sorun giderme önce toohello POP dağıtıldıktan emin bekleyen düşünmelisiniz
> 
> 

## <a name="enabling-compression"></a>Sıkıştırmayı etkinleştirme
> [!NOTE]
> Merhaba standart ve Premium CDN katmanları sağlamak hello aynı sıkıştırma işlevselliği, ancak hello kullanıcı arabirimi farklıdır.  Hello standart ve Premium CDN katmanları arasındaki farklar hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Standart katman
> [!NOTE]
> Bu bölüm çok geçerlidir**verizon'dan Azure CDN standart** ve **akamai'den Azure CDN standart** profilleri.
> 
> 

1. Merhaba CDN profili sayfasından toomanage istediğiniz hello CDN uç noktası'ı tıklatın.
   
    ![CDN profili sayfasını uç noktaları](./media/cdn-file-compression/cdn-endpoints.png)
   
    Merhaba CDN uç noktası sayfası açılır.
2. Merhaba tıklatın **yapılandırma** düğmesi.
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-config-btn.png)
   
    Merhaba CDN yapılandırma sayfası açılır.
3. Aç **sıkıştırma**.
   
    ![CDN sıkıştırma seçenekleri](./media/cdn-file-compression/cdn-compress-standard.png)
4. Merhaba varsayılan türleri kullanın veya dosya türlerini ekleyerek veya çıkararak hello listesini değiştirin.
   
   > [!TIP]
   > While olası ZIP, MP3, MP4, JPG, vb. gibi tooapply sıkıştırma toocompressed biçimleri önerilmez.
   > 
   > 
5. Yaptığınız değişiklikleri yaptıktan sonra hello tıklatın **kaydetmek** düğmesi.

### <a name="premium-tier"></a>Premium katman
> [!NOTE]
> Bu bölüm çok geçerlidir**verizon'dan Azure CDN Premium** profilleri.
> 
> 

1. Merhaba CDN profili sayfasından hello tıklatın **Yönet** düğmesi.
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Merhaba üzerine getirin **HTTP büyük** sekmesini ve ardından hello üzerine getirin **önbellek ayarları** çıkma.  Tıklayın **sıkıştırma**.

    ![Dosya sıkıştırma seçimi](./media/cdn-file-compression/cdn-compress-select.png)
   
    Sıkıştırma seçeneklerini görüntülenir.
   
    ![Dosya sıkıştırma](./media/cdn-file-compression/cdn-compress-files.png)
3. Merhaba tıklayarak sıkıştırmayı etkinleştir **sıkıştırma etkin** radyo düğmesi.  Merhaba MIME türleri bir virgülle ayrılmış liste olarak (boşluksuz) hello toocompress istediğiniz **dosya türlerini** metin kutusu.
   
   > [!TIP]
   > While olası ZIP, MP3, MP4, JPG, vb. gibi tooapply sıkıştırma toocompressed biçimleri önerilmez. 
   > 
   > 
4. Yaptığınız değişiklikleri yaptıktan sonra hello tıklatın **güncelleştirme** düğmesi.

## <a name="compression-rules"></a>Sıkıştırma kuralları
Bu tablo her senaryo için Azure CDN sıkıştırma davranışı açıklar.

> [!IMPORTANT]
> İçin **verizon'dan Azure CDN** (standart ve Premium), yalnızca uygun dosyaları sıkıştırılır.  sıkıştırma için uygun toobe, bir dosya gerekir:
> 
> * 128 bayttan büyük olmalıdır.
> * 1 MB'tan küçük olmalıdır.
> 
> İçin **akamai'den Azure CDN**, tüm dosyalar için sıkıştırma uygundur.
> 
> Tüm Azure CDN ürünü için bir dosya olan bir MIME türü olmalıdır [sıkıştırma için yapılandırılmış](#enabling-compression).
> 
> **Verizon'dan Azure CDN** profilleri (standart ve Premium) Destek **gzip** (GNU zip) **deflate**, **bzıp2**, veya **br** (Brotli) kodlama. Brotli kodlama için hello sıkıştırma yalnızca hello sınırında yapılır. Merhaba istemci/tarayıcı Brotli kodlama için hello istek göndermesi gerekir ve hello sıkıştırılmış varlık hello kaynak tarafında ilk sıkıştırılmış gerekir. 
>
>**Akamai'den Azure CDN** profilleri desteği yalnızca **gzip** kodlama.
> 
> **Akamai'den Azure CDN** uç noktaları her zaman isteği **gzip** kodlanmış hello istemci isteği bakılmaksızın hello kaynak dosyalarından. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Sıkıştırma devre dışı veya dosya sıkıştırma için uygun değil
| İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi) | Önbelleğe alınmış dosya biçimi | CDN yanıt toohello istemci | Notlar |
| --- | --- | --- | --- |
| Sıkıştırılmış |Sıkıştırılmış |Sıkıştırılmış | |
| Sıkıştırılmış |Sıkıştırılmamış |Sıkıştırılmamış | |
| Sıkıştırılmış |Önbelleğe alınmamış |Sıkıştırılmış veya sıkıştırılmamış |Kaynak yanıtta bağlıdır |
| Sıkıştırılmamış |Sıkıştırılmış |Sıkıştırılmamış | |
| Sıkıştırılmamış |Sıkıştırılmamış |Sıkıştırılmamış | |
| Sıkıştırılmamış |Önbelleğe alınmamış |Sıkıştırılmamış | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>Sıkıştırma ve dosya sıkıştırma için uygun
| İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi) | Önbelleğe alınmış dosya biçimi | CDN yanıt toohello istemci | Notlar |
| --- | --- | --- | --- |
| Sıkıştırılmış |Sıkıştırılmış |Sıkıştırılmış |CDN transcodes desteklenen biçimler arasında |
| Sıkıştırılmış |Sıkıştırılmamış |Sıkıştırılmış |CDN sıkıştırır. |
| Sıkıştırılmış |Önbelleğe alınmamış |Sıkıştırılmış |Kaynak sıkıştırılmamış döndürürse CDN sıkıştırır.  **Verizon'dan Azure CDN** geçişleri hello sıkıştırılmamış dosyayı hello ilk isteği ve ardından sıkıştırır ve önbellekleri hello sonraki istekleri için dosya.  İle dosyaları `Cache-Control: no-cache` üstbilgi hiçbir zaman sıkıştırılır. |
| Sıkıştırılmamış |Sıkıştırılmış |Sıkıştırılmamış |CDN açma işlemi gerçekleştirir |
| Sıkıştırılmamış |Sıkıştırılmamış |Sıkıştırılmamış | |
| Sıkıştırılmamış |Önbelleğe alınmamış |Sıkıştırılmamış | |

## <a name="media-services-cdn-compression"></a>CDN sıkıştırma medya Hizmetleri
Medya Hizmetleri CDN akış uç noktalarını etkin sıkıştırma şu içerik türlerini hello için varsayılan olarak etkindir: uygulama/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, uygulama/f4m + xml. Hello sıkıştırma bırakmak olamaz hello Azure portal kullanarak türleri belirtiliyor.  

## <a name="see-also"></a>Ayrıca bkz.
* [CDN dosya sıkıştırma sorunlarını giderme](cdn-troubleshoot-compression.md)    

