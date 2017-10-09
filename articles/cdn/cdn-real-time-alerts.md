---
title: "aaaAzure CDN gerçek zamanlı uyarılar | Microsoft Docs"
description: "Microsoft Azure CDN gerçek zamanlı uyarılar. Gerçek zamanlı uyarılar CDN profilinizi hello uç noktalarını hello performansını hakkında bildirimler sağlayın."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Microsoft Azure cdn'de gerçek zamanlı uyarılar
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Genel Bakış
Bu belgede, Microsoft Azure cdn'de gerçek zamanlı uyarılar açıklanmaktadır. Bu işlevsellik, CDN profilinize hello uç noktaları hello performansı hakkında gerçek zamanlı bildirimler sağlar.  E-posta veya temel HTTP uyarılar ayarlayabilirsiniz:

* Bant Genişliği
* Durum kodları
* Önbellek durumları
* Bağlantılar

## <a name="creating-a-real-time-alert"></a>Gerçek zamanlı uyarı oluşturma
1. Merhaba, [Azure Portal](https://portal.azure.com), tooyour CDN profili göz atın.
   
    ![CDN profili dikey penceresi](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
3. Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **gerçek zamanlı İstatistikler** çıkma.  Tıklayın **gerçek zamanlı uyarılar**.
   
    ![CDN Yönetim Portalı](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    var olan uyarı yapılandırmaları (varsa) Hello listesi görüntülenir.
4. Merhaba tıklatın **eklemek uyarı** düğmesi.
   
    ![Uyarı düğme ekleme](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Yeni bir uyarı oluşturmak için bir form görüntülenir.
   
    ![Yeni uyarı formu](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Bu uyarı toobe etkin istiyorsanız tıkladığınızda **kaydetmek**, hello denetleyin **uyarı etkin** onay kutusu.
6. Hello Uyarınız için açıklayıcı bir ad girin **adı** alan.
7. Merhaba, **medya türü** açılan listesinde, select **HTTP büyük nesne**.
   
    ![HTTP büyük seçili nesne medya türüyle](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > Seçmelisiniz **HTTP büyük nesne** hello olarak **medya türü**.  Merhaba diğer seçenekleri tarafından kullanılmaz **verizon'dan Azure CDN**.  Hata tooselect **HTTP büyük nesne** uyarıyı neden olacak toonever tetiklendi.
   > 
   > 
8. Oluşturma bir **ifade** seçerek toomonitor bir **ölçüm**, **işleci**, ve **tetikleyen değer**.
   
   * İçin **ölçüm**, izlenen istediğiniz koşul hello türünü seçin.  **Bant genişliği Mbps** hello saniye başına megabit olarak bant genişliği kullanım miktarı.  **Toplam Bağlantı** hello eşzamanlı HTTP bağlantıları tooour uç sunucuların sayısıdır.  Çeşitli önbellek durumları ve durum kodları hello tanımları için bkz: [Azure CDN önbellek durum kodları](https://msdn.microsoft.com/library/mt759237.aspx) ve [Azure CDN HTTP durum kodları](https://msdn.microsoft.com/library/mt759238.aspx)
   * **İşleç** hello ölçüm ve hello tetikleyici değeri arasında hello ilişki kurar hello matematik işleci.
   * **Tetikleyen değer** bir bildirim gönderilir önce karşılanması gereken hello eşik değeri.
     
     Örnek aşağıda Hello 404 durum kodları hello sayısı 25'den büyük olduğunda bildirim toobe istiyorum oluşturmuş olduğunuz hello ifadeyi belirtir.
     
     ![Gerçek zamanlı uyarı örnek bir ifade](./media/cdn-real-time-alerts/cdn-expression.png)
9. İçin **aralığı**, ne sıklıkta hello ifade Hesaplandı istediğinizi girin.
10. Merhaba, **bildirim** açılan listesinde, zaman toobe hello ifade doğruysa bildirim istediğinizi seçin.
    
    * **Koşul başlangıç** hello koşul algılanan belirtildiğinde bir bildirim gönderileceğini gösterir.
    * **Koşul son** hello koşul artık algıladı belirtildiğinde bir bildirim gönderileceğini gösterir. Belirtilen bu hello bizim ağ sistem izleme saptadıktan sonra yalnızca bu bildirim tetiklenebilir koşulu oluştu.
    * **Sürekli** belirten bir bildirim ağ izleme sistemi hello her zaman algılar belirtilen hello gönderilir koşulu. Bu hello ağ onay kez hello için aralık başına koşul belirtilen yalnızca sistem olacak izleme göz önünde bulundurun.
    * **Koşul başlangıç ve bitiş** hello belirtilen koşulu hello ilk kez algılandı ve bir kez daha zaman hello koşul artık algılandığında bir bildirim gönderileceğini gösterir.
11. E-posta ile tooreceive bildirimleri istiyorsanız hello denetleyin **e-posta ile bildir** onay kutusu.  
    
    ![E-posta formu tarafından bildir](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    Merhaba, **için** alanında, istediğiniz yere bildirimleri gönderdiğiniz hello e-posta adresi girin. İçin **konu** ve **gövde**hello varsayılan bırakabilir veya hello kullanarak selamlama iletisine özelleştirebilir **kullanılabilir anahtar sözcükleri** listesi toodynamically Ekle uyarı verileri zaman Merhaba ileti gönderilir.
    
    > [!NOTE]
    > Merhaba tıklatarak hello e-posta bildirimi sınayabilirsiniz **Test bildirimi** hello uyarı yapılandırma kaydedildikten sonra ancak yalnızca düğme.
    > 
    > 
12. Tooa web sunucusuna gönderilen bildirimler toobe istiyorsanız, hello denetleyin **HTTP Post tarafından bildirim** onay kutusu.
    
    ![HTTP Post formuyla bildir](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    Merhaba, **Url** alanında, istediğiniz yere hello HTTP iletisi deftere hello URL'sini girin. Merhaba, **üstbilgileri** metin kutusuna, hello istekte gönderilen hello HTTP üstbilgileri toobe girin.  İçin **gövde** hello kullanarak selamlama iletisine özelleştirebilir **kullanılabilir anahtar sözcükleri** listesi toodynamically hello ileti gönderildiğinde uyarı verileri ekleyin.  **Üstbilgileri** ve **gövde** tooan XML yükü benzer toohello örnek aşağıda varsayılan.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > Merhaba tıklatarak hello HTTP Post bildirim sınayabilirsiniz **Test bildirimi** hello uyarı yapılandırma kaydedildikten sonra ancak yalnızca düğme.
    > 
    > 
13. Merhaba tıklatın **kaydetmek** toosave uyarı yapılandırmanızı düğmesi.  İşaretlendiğinde, **uyarı etkin** 5. adımda Uyarınız şimdi etkindir.

## <a name="next-steps"></a>Sonraki Adımlar
* Analiz [Azure CDN içindeki gerçek zamanlı İstatistikler](cdn-real-time-stats.md)
* Dıg ile daha derin [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md)
* Analiz [kullanım desenleri](cdn-analyze-usage-patterns.md)

