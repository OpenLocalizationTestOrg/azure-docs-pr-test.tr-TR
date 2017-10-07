---
title: "aaa \"Azure CDN özel etki alanı üzerinde HTTPS etkinleştirme | Microsoft Docs\""
description: "Bilgi nasıl tooenable HTTPS ile özel bir etki alanı Azure CDN uç noktanız üzerinde."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Azure CDN özel etki alanı üzerinde HTTPS'yi etkinleştir

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Azure CDN özel etki alanları için HTTPS desteği, aktarım sırasında verileri kendi etki alanı adı tooimprove hello güvenliğini kullanarak SSL üzerinden toodeliver güvenli içerik sağlar. Merhaba uçtan uca iş akışı tooenable HTTPS özel etki alanınız için ek ücret ödemeden tüm ile tek tıklatmayla etkinleştirme, eksiksiz bir sertifika yönetimi aracılığıyla basitleştirilmiştir.

Bu kritik tooensure hello gizlilik ve veri bütünlüğü tüm web uygulamaları gizli veriler aktarım sırasında olur. HTTPS protokolü üzerinden gönderildiğinde, hassas verilerin şifrelenmesini sağlar hello kullanarak hello Internet. Sağladığı güven, kimlik doğrulama ve web uygulamalarınızın saldırılara karşı korur. Şu anda Azure CDN bir CDN uç noktası HTTPS destekler. Örneğin, Azure CDN (örneğin https://contoso.azureedge.net) bir CDN uç noktası oluşturursanız, HTTPS varsayılan olarak etkindir. Şimdi, özel etki alanı ile HTTPS, güvenli teslimat özel bir etki alanı (örneğin https://www.contoso.com) için de etkinleştirebilirsiniz. 

Merhaba anahtar öznitelikleri HTTPS özelliğinin bazıları şunlardır:

- Ek ücret ödemeden: sertifika edinme veya yenileme için hiçbir maliyetleri ve HTTPS trafiği için ek ücret ödemeden vardır. Yalnızca hello CDN gelen GB çıkışı için ücret ödersiniz.

- Basit etkinleştirme: bir tıklatın sağlama kullanılabilir hello [Azure portal](https://portal.azure.com). REST API veya diğer geliştirici araçları tooenable hello özelliğini de kullanabilirsiniz.

- Sertifika yönetimi tamamlamak: tüm tedarik sertifika ve yönetim sizin için işlenir. Sertifikaları otomatik olarak sağlanır ve önceki tooexpiration yenilendi. Bu sertifikanın sona ermesinden sonucu olarak hizmet kesintisi hello risklerini tamamen kaldırır.

>[!NOTE] 
>Önceki tooenabling HTTPS desteği, önceden oluşturulmuş gereken bir [Azure CDN özel etki alanı](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>1. adım: hello özelliğini etkinleştirme 

1. Merhaba, [Azure portal](https://portal.azure.com), tooyour Verizon standart veya premium CDN profili göz atın.

2. Uç noktaları Hello listesinde özel etki alanınızı içeren hello endpoint tıklayın.

3. Tooenable HTTPS istediğiniz hello özel etki alanını tıklatın.

    ![Uç nokta dikey penceresi](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Tıklatın **üzerinde** tooenable HTTPS ve hello değişikliği kaydedin.

    ![Özel HTTPS iletişim](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>2. adım: Etki alanı doğrulama

>[!IMPORTANT] 
>HTTPS etkin özel etki alanınızda önce etki alanı doğrulama tamamlamanız gerekir. 6 iş günleri tooapprove hello etki alanı var. 6 iş günü içinde hiçbir onay ile isteği iptal edilecek.  

Özel etki alanınızı üzerindeki HTTPS etkinleştirdikten sonra bizim HTTPS sertifika sağlayıcısı DigiCert etki alanınızın sahipliğini (varsayılan) e-posta veya telefon üzerinden WHOIS registrant bilgilere dayanarak, etki alanı için hello registrant başvurarak doğrular. DigiCert hello doğrulama e-posta toohello adresleri aşağıda da gönderir. WHOIS registrant bilgi özel ise, doğrudan bu adreslerden birinden onaylayabilirsiniz emin olun.

>Yönetici @< bilgisayarınızı-etki-name.com zaman > yönetici @< bilgisayarınızı-etki-name.com zaman >  
>yayımlanması @< bilgisayarınızı-etki-name.com zaman >  
>hostmaster @< bilgisayarınızı-etki-name.com zaman >  
>Yöneticisi @< bilgisayarınızı-etki-name.com zaman >


Merhaba e-posta alındıktan sonra iki doğrulama seçeneğiniz vardır:

1. Aynı hesap Merhaba hello verilen gelecekteki tüm siparişler onaylayabilirsiniz aynı kök etki alanı, örneğin consoto.com. Tooadd ek özel etki alanlarında hello Merhaba gelecekteki planlıyorsanız bu bir önerilen yaklaşımdır aynı kök etki alanı.
 
2. Bu istekte kullanılan hello belirli ana bilgisayar adı yalnızca onaylayabilirsiniz. Ek onay sonraki istekleri için gerekli olacaktır.

    Örnek e-posta:
    
    ![Özel HTTPS iletişim](./media/cdn-custom-ssl/domain-validation-email-example.png)

Onay sonrasında DigiCert özel etki alanı adı toohello SAN sertifikanızı ekler. Merhaba sertifikası bir yıl için geçerli olur ve sona ermeden önce otomatik olarak yenilenir.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>3. adım: hello yayması bekleyin, sonra özelliğini kullanmaya başlama

Merhaba etki alanı adı doğrulandıktan sonra işlemin hello özel etki alanı HTTPS özelliği toobe etkin too6-8 saat sürecek. Merhaba işlemi tamamlandıktan sonra hello Azure portal hello "özel HTTPS" Durum "Enabled" çok ayarlanır. HTTPS ile özel etki alanınızı artık kullanımınız için hazırdır.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

1. *Merhaba sertifika sağlayıcısı ve ne tür bir sertifika kullanılan kim?*

    DigiCert tarafından sağlanan konu alternatif adları (SAN) sertifika kullanırız. Bir SAN sertifika bir sertifika ile birden fazla tam etki alanı adları güvenliğini sağlayabilirsiniz.

2. *My ayrılmış sertifika kullanabilir miyim?*
    
    Şu anda değil ancak onun üzerinde hello yol haritası.

3. *DigiCert ne hello etki alanı doğrulama e-posta alıyorum mu?*

    24 saat içinde bir e-posta almazsanız, lütfen Microsoft'a başvurun.

4. *Ayrılmış bir sertifika az güvenli bir SAN sertifikası kullanıyor?*
    
    Aynı şifreleme ve güvenlik standartları bir ayrılmış sertifika olarak aşağıdaki hello bir SAN sertifika. Verilen tüm SSL sertifikaları SHA-256 Gelişmiş server güvenliği için kullanıyorsunuz.

5. *Akamai'den Azure CDN ile özel etki alanı HTTPS kullanabilir miyim?*

    Şu anda bu özellik yalnızca verizon'dan Azure CDN ile kullanılabilir. Bu özellik akamai'den Azure CDN ile Merhaba önümüzdeki aylarda desteklemeye çalışıyoruz.


## <a name="next-steps"></a>Sonraki adımlar

- Bilgi nasıl tooset oluşturan bir [Azure CDN uç noktanız özel etki alanında](./cdn-map-content-to-custom-domain.md)


