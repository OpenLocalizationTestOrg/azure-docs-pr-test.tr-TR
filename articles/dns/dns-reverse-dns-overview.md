---
title: "azure'da geriye doğru DNS aaaOverview | Microsoft Docs"
description: "Nasıl geriye doğru DNS çalışır ve Azure'da nasıl kullanılabileceğini öğrenin"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Geriye doğru DNS ve Azure desteği'na genel bakış

Bu makalede, Azure'da desteklenen geriye doğru DNS senaryoları nasıl geriye doğru DNS çalışır ve hello genel bakış sağlar.

## <a name="what-is-reverse-dns"></a>Geriye doğru DNS nedir?

Geleneksel DNS kayıtları bir DNS adı (örneğin, 'www.contoso.com') tooan IP adresi (örneğin, 64.4.6.100) eşlemeyi etkinleştirin.  Geriye doğru DNS IP adresi (64.4.6.100) geri tooa adı ('www.contoso.com') hello çevrilmesi sağlar.

Geriye doğru DNS kayıtları çeşitli durumlar kullanılır. Örneğin, geriye doğru DNS kayıtlarını yaygın olarak e-posta istenmeyen e-posta iletisine hello göndereni doğrulayarak mücadele kullanılır.  Merhaba alıcı posta sunucusu alır sunucunun IP adresini gönderme hello geriye doğru DNS kaydını hello ve, barındırıyorsanız hello yetkili toosend e-posta etki alanı kaynaklanan doğrular. 

## <a name="how-reverse-dns-works"></a>Nasıl geriye doğru DNS çalışır

Geriye doğru DNS kayıtlarını 'ARPA' bölgeleri bilinen özel DNS bölgeleri barındırılır.  Bu bölgeler ayrı bir DNS hiyerarşi paralel "contoso.com" gibi etki alanı barındırma hello normal hiyerarşisi oluşturur.

Örneğin, DNS kaydı 'www.contoso.com' hello hello adı 'contoso.com"Merhaba bölgesinde ' www' ile 'A' DNS kaydı kullanılarak uygulanır.  Bu A kaydı toohello karşılık gelen IP adresini, bu durumda 64.4.6.100 işaret eder.  Merhaba geriye doğru arama, ayrı ayrı '100' hello bölgesinde '6.4.64.in-addr.arpa' (IP adresleri ARPA bölgeleri ters gerektiğini unutmayın.) adlı bir 'PTR' kayıt kullanılarak uygulanır  Doğru şekilde yapılandırılmışsa bu PTR kaydı toohello adı 'www.contoso.com' işaret eder.

Bir kuruluş IP adres bloğu atandığında, bunlar ayrıca hello sağ toomanage hello ilgili ARPA bölgeyi alın. Azure tarafından kullanılan blokları barındırılan ve Microsoft tarafından yönetilen toohello IP adresine karşılık gelen ARPA bölgeleri hello. ISS'niz hello ARPA bölge kendi IP adresleri için sizin için barındırabilir veya hello ARPA bölge bir DNS hizmetinde Azure DNS gibi tercih ettiğiniz tooyou konak sağlayabilir.

> [!NOTE]
> İleriye doğru DNS araması ve geriye doğru DNS araması ayrı, paralel DNS hiyerarşileri uygulanır. Merhaba geriye doğru arama 'www.contoso.com' için olan **değil** "contoso.com" Merhaba bölgesinde barındırılan, bunun yerine, hello ARPA bölgesinde hello karşılık gelen IP adres bloğu için barındırılır. Ayrı bölgeleri için IPv4 ve IPv6 adres bloklarını kullanılır.

### <a name="ipv4"></a>IPv4

bir IPv4 geriye doğru arama bölgesi Hello adı biçimi aşağıdaki hello olmalıdır: `<IPv4 network prefix in reverse order>.in-addr.arpa`.

Örneğin, bir geriye doğru arama bölgesine hello 192.0.2.0/24 önekini olan IP'leri konaklarla için toohost kayıtları oluştururken, hello bölge adı hello adres (192.0.2) ve ardından hello sipariş (2.0.192) ters ve hello ekleme hello ağ öneki yalıtarak oluşturulacak sonek `.in-addr.arpa`.

|Alt ağ sınıfı|Ağ öneki  |Ters ağ öneki  |Standart soneki  |Geriye doğru arama bölgesi adı |
|-------|----------------|------------|-----------------|---------------------------|
|Sınıf A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|B sınıfı|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|C sınıfı|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>Sınıfsız IPv4 temsilci seçme

Bazı durumlarda, tooan kuruluş ayrılan hello IP aralığı C sınıfı küçüktür (/ 24) aralık. Bu durumda, hello IP aralığı bir bölge sınırı içinde hello üzerinde kapsamında değilse `.in-addr.arpa` bölge hiyerarşisini ve bu nedenle bir alt bölge olarak temsil edilemez.

Bunun yerine, farklı bir mekanizma kullanılan tek tek geriye doğru arama (PTR) tootransfer denetimini ayrılmış tooa DNS bölgesi kaydeder. Bu mekanizma her IP aralığı için bir alt bölge atar ve ardından her IP adresi hello eşlemeleri ayrı ayrı CNAME kayıtları kullanarak toothat alt bölgenin aralığı.

Örneğin, bir kuruluşun kendi ISS tarafından hello IP aralığı 192.0.2.128/26 verilir varsayalım. Bu 64 IP adresleri, 192.0.2.128 temsil eden too192.0.2.191. Bu aralık için ters DNS şu şekilde gerçekleştirilir:
- Merhaba kuruluş 128 26.2.0.192.in addr.arpa adlı bir geriye doğru arama bölgesi oluşturur. Merhaba öneki ' 128-26' temsil hello ağ atanan segment toohello kuruluş içinde hello C sınıfı (/ 24) aralık.
- Merhaba ISS NS kayıtları tooset hello hello bölge yukarıda bir DNS temsilci yukarı hello C sınıfı üst bölgeden oluşturur. Ayrıca CNAME kayıtları hello üst (C sınıfı) geriye doğru arama bölgesi içinde hello IP aralığı toohello yeni bölge hello kuruluş tarafından oluşturulan her IP adresi eşleme oluşturur:

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- Merhaba kuruluş hello tek tek PTR kayıtları kendi alt bölgedeki yönetir.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Geriye doğru arama yönelik hello IP adresi '192.0.2.129' sorguları bir PTR kaydı için '129.2.0.192.in-addr.arpa' adlı. Bu sorgu hello üst bölge toohello PTR kaydı hello alt bölgedeki hello CNAME aracılığıyla çözümler.

### <a name="ipv6"></a>IPv6

bir IPv6 geriye doğru arama bölgesi adı Hello form aşağıdaki hello olması gerekir:`<IPv6 network prefix in reverse order>.ip6.arpa`

Örneğin. Geriye doğru arama bölgesine hello 2001:db8:1000:abdc olan IP'leri konaklarla için toohost kayıtları oluşturulurken:: / 64 öneki hello bölge adı oluşturulacaktır hello ağ öneki hello adresinin yalıtarak (2001:db8:abdc::). Sonraki hello IPv6 ağ öneki tooremove genişletin [sıfır sıkıştırma](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), kullanılan tooshorten hello IPv6 adresi öneki ise (2001:0db8:abdc:0000::). Merhaba tersine, bir süre hello önek onaltılık her sayıyı bölücüyü hello gibi kullanarak, ağ öneki toobuild hello ters (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) ve hello soneki eklemek `.ip6.arpa`.


|Ağ öneki  |Genişletilmiş ve ters ağ öneki |Standart soneki |Geriye doğru arama bölgesi adı  |
|---------|---------|---------|---------|
|2001:db8:abdc:: / 64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | . ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102:: / 64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | . ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Geriye doğru DNS Azure desteği

Azure DNS tooreverse ilgili iki ayrı senaryoları destekler:

**Barındırma hello geriye doğru arama bölgesine karşılık gelen tooyour IP adres bloğu.**
Azure DNS çok kullanılabilir[, geriye doğru arama bölgeleri barındıran ve her geriye doğru DNS araması hello PTR kayıtlarını yönetme](dns-reverse-dns-hosting.md), IPv4 ve IPv6 için.  Merhaba temsilci seçmeyi ayarlama ayarı hello (ARPA) geriye doğru arama bölgesi oluşturmak işlemi hello ve PTR yapılandırma kayıtları olan hello aynı normal DNS bölgeleri için olduğu gibi.  Merhaba yalnızca farklar hello temsilci DNS kayıt yerine ISS yapılandırılması gerekir ve yalnızca hello PTR kayıt türü kullanılmalıdır şunlardır.

**Merhaba geriye doğru DNS kaydı tooyour Azure hizmeti atanan başlangıç IP adresi için yapılandırın.** Azure sağlar, çok[hello geriye doğru arama ayrılan hello IP adreslerini tooyour Azure hizmeti için yapılandırma](dns-reverse-dns-for-azure-services.md).  Bu geriye doğru arama hello karşılık gelen ARPA bölgede bir PTR kaydı olarak Azure tarafından yapılandırılır.  Azure tarafından kullanılan tooall hello IP aralıkları karşılık gelen bu ARPA bölgeleri Microsoft tarafından barındırılan

## <a name="next-steps"></a>Sonraki adımlar

Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Nasıl çok öğrenin[konak hello geriye doğru arama bölgesi ISS atanan IP aralığınızı Azure DNS'de için](dns-reverse-dns-for-azure-services.md).
<br>
Nasıl çok öğrenin[, Azure Hizmetleri için ters DNS kayıtlarını yönetme](dns-reverse-dns-for-azure-services.md).

