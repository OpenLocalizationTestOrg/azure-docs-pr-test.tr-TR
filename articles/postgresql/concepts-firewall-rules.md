---
title: "Azure veritabanı PostgreSQL sunucunun güvenlik duvarı kuralları için | Microsoft Docs"
description: "Azure veritabanı PostgreSQL sunucu için güvenlik duvarı kuralları açıklar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Azure veritabanı PostgreSQL sunucunun güvenlik duvarı kuralları için
Güvenlik duvarları iznine sahip olan bilgisayarları belirtmediğiniz sürece tüm erişim tooyour veritabanı sunucusu engeller. Merhaba güvenlik duvarı erişim toohello sunucusu IP adresi her istek kaynaklanan hello üzerinde temel verir.
tooconfigure kabul edilebilir IP adreslerinin aralıklarını belirtmek güvenlik duvarı kuralları oluşturma, güvenlik duvarı. Merhaba sunucu düzeyinde güvenlik duvarı kuralları oluşturabilirsiniz.

**Güvenlik duvarı kuralları:** bu kurallar istemcileri tooaccess tüm Azure veritabanınızı PostgreSQL sunucusu için etkinleştirmek için diğer bir deyişle, içindeki tüm hello veritabanları aynı mantıksal sunucu hello. Sunucu düzeyinde güvenlik duvarı kuralları hello Azure portalında veya Azure CLI komutları kullanarak yapılandırılabilir. toocreate sunucu düzeyinde güvenlik duvarı kuralları, hello abonelik sahibi veya abonelik Katılımcısı olmanız gerekir.

## <a name="firewall-overview"></a>Güvenlik duvarına genel bakış
Tüm veritabanı erişimi tooyour Azure veritabanı PostgreSQL sunucu varsayılan olarak hello güvenlik duvarı tarafından engellendi. sunucunuz başka bir bilgisayardan kullanarak toobegin toospecify bir gereksinim duyduğunuz ya da daha fazla sunucu düzeyinde güvenlik duvarı kuralları tooenable erişim tooyour sunucusu. Merhaba Internet tooallow hangi IP adres aralıkları hello güvenlik duvarı kuralları toospecify kullanın. Erişim toohello Azure portal Web sitesinin kendisini hello güvenlik duvarı kuralları tarafından etkilenmez.
Internet bağlantısı saldırılara karşı hello ve PostgreSQL veritabanınızı ulaşmadan Azure ilk hello güvenlik duvarı üzerinden hello Aşağıdaki diyagramda gösterildiği gibi geçmesi gerekir:

![Örnek akış hello Güvenlik Duvarı nasıl çalışır](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Merhaba Internet ' bağlanma
Sunucu düzeyinde güvenlik duvarı kuralları tooall veritabanları hello Azure veritabanı PostgreSQL sunucusu uygulayın. Başlangıç IP adresi hello isteğinin hello sunucu düzeyinde güvenlik duvarı kurallarında belirtilen hello aralıkları biri içinde ise, hello bağlantısı verilir.
Başlangıç IP adresi hello isteğinin içinde değilse hello aralıkları hello veritabanı düzeyi hiçbirinde belirtilen veya sunucu düzeyinde güvenlik duvarı kuralları, hello bağlantı isteği başarısız olur.
Örneğin, uygulamanız için PostgreSQL JDBC sürücüsü ile bağlanıyorsa, hello bağlantı hello güvenlik duvarı engelleme zaman tooconnect çalışırken bu hatayla karşılaşabilirsiniz.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: Önemli: hiçbir pg\_ana bilgisayar "123.45.67.890", kullanıcı "adminuser" veritabanı "postgresql", SSL için hba.conf giriş

## <a name="programmatically-managing-firewall-rules"></a>Güvenlik duvarı kurallarını programlı bir şekilde yönetme
Ayrıca toohello Azure portal, güvenlik duvarı kuralları olabilir program aracılığıyla Azure CLI kullanarak yönetilen.
Ayrıca bkz. [oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme](howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Merhaba veritabanı güvenlik duvarı sorunlarını giderme
Merhaba beklediğiniz gibi PostgreSQL Server hizmeti için erişim toohello Microsoft Azure veritabanı davranıyor değil, aşağıdaki noktaları göz önünde bulundurun:

* **Değişiklikleri toohello izin verilenler listesine etkili olmamıştır değil:** toohello Azure veritabanı PostgreSQL sunucu güvenlik duvarı yapılandırması tootake efekti için beş dakikalık bir gecikmeyle değişiklikleri kadar olabilir.

* **Merhaba oturum açma yetkisi yok veya hatalı bir parolanın kullanıldı:** kullanılan PostgreSQL sunucu veya hello parola yanlış için bir oturum açma izinleri hello Azure veritabanı üzerinde sahip değilse, PostgreSQL server için bağlantı toohello Azure veritabanı hello engellendi. Bir güvenlik duvarı ayarı oluşturma istemciler yalnızca bir fırsat tooattempt tooyour sunucusuyla bağlantı kuruluyor sağlar; her istemci hello gerekli güvenlik kimlik bilgilerini sağlamanız gerekir.

Örneğin, bir JDBC İstemcisi'ni kullanarak aşağıdaki hata hello görünebilir.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: Önemli: parola kimlik doğrulaması "kullanıcıadınız" kullanıcı için başarısız oldu

* **Dinamik IP adresi:** dinamik IP adresleme ile Internet bağlantınız varsa ve hello güvenlik duvarı üzerinden alma sorun yaşıyorsanız, çözümleri aşağıdaki hello birini deneyebilirsiniz:

* Başlangıç IP adresi aralığı, Internet servis sağlayıcısı (ISS) tooyour istemci bilgisayarları bu erişim hello Azure veritabanı PostgreSQL sunucusu için atanan isteyin ve sonra başlangıç IP adresi aralığı bir güvenlik duvarı kuralı ekleyin.

* Statik IP bunun yerine istemci bilgisayarlarınız için adresleme alın ve ardından güvenlik duvarı kuralları hello IP adreslerini ekleyin.

## <a name="next-steps"></a>Sonraki adımlar
Sunucu ve veritabanı düzeyi güvenlik duvarı kuralları oluşturma hakkında daha fazla makaleler için bkz:
* [Oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme](howto-manage-firewall-using-portal.md)
* [Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme](howto-manage-firewall-using-cli.md)