---
title: "kimlik doğrulaması ve Azure MFA sunucusu aaaRADIUS | Microsoft Docs"
description: "Bu, RADIUS kimlik doğrulaması ve Azure multi-Factor Authentication Sunucusu'nu dağıtmada yardımcı olacak hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>RADIUS kimlik doğrulamasını ve Azure Multi-Factor Authentication Sunucusuyla tümleştirme
RADIUS kimlik doğrulamasını yapılandırmak ve Azure MFA sunucusu tooenable Hello RADIUS kimlik doğrulaması bölümü kullanın. RADIUS, standart, bu istekleri tooaccept kimlik doğrulama istekleri ve tooprocess protocol ' dir. Hello Azure multi-Factor Authentication sunucusu RADIUS sunucusu olarak işlev görür. RADIUS istemciniz (VPN Gereci) ve Active Directory (AD), LDAP dizini ya da başka bir RADIUS sunucusu tooadd Azure multi-Factor Authentication olabilir, kimlik doğrulama hedefi ekleyin. Azure çok faktörlü kimlik doğrulama (MFA) toofunction için hem hello istemci sunucuları hem de hello kimlik doğrulama hedefi ile iletişim kurabilmesi için hello Azure MFA sunucusu yapılandırmanız gerekir. Hello Azure MFA sunucusu RADIUS istemcisinden gelen istekleri kabul hello kimlik doğrulama hedefi karşı kimlik bilgilerini doğrular, Azure multi-Factor Authentication ekler ve bir yanıtı geri toohello RADIUS istemcisi gönderir. Merhaba birincil kimlik doğrulaması ve hello Azure çok faktörlü kimlik doğrulaması başarılı olursa hello kimlik doğrulama isteği yalnızca başarılı olur.

> [!NOTE]
> Merhaba MFA sunucusu yalnızca PAP (parola kimlik doğrulama protokolü) ve MSCHAPv2 destekler (Microsoft Karşılıklı Kimlik Doğrulama Protokolü) RADIUS protokollerini RADIUS sunucusu olarak hareket ederken.  Merhaba MFA sunucusu bu protokolü destekleyen bir RADIUS proxy tooanother RADIUS sunucusu olarak hareket ettiğinde, EAP (Genişletilebilir Kimlik Doğrulama Protokolü) gibi diğer protokoller kullanılabilir.
>
> Merhaba MFA sunucusu alternatif protokolleri kullanarak başarılı bir RADIUS sınama yanıtı başlatamaz beri bu yapılandırmada, tek yönlü SMS ve OATH belirteçleri çalışmaz.

![Radius Kimlik Doğrulaması](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>RADIUS istemcisi ekleme
tooconfigure RADIUS kimlik doğrulaması, Windows Server yükleme hello Azure çok faktörlü kimlik doğrulama sunucusu. Bir Active Directory ortamınız varsa, hello sunucu birleştirilmiş toohello etki alanı hello ağ içinde olmalıdır. Aşağıdaki yordam tooconfigure hello Azure çok faktörlü kimlik doğrulama sunucusu hello kullan:

1. Hello Azure multi-Factor Authentication sunucusu, hello hello soldaki menüde RADIUS kimlik doğrulaması simgesine tıklayın.
2. Merhaba denetleyin **RADIUS kimlik doğrulamasını etkinleştir** onay kutusu.
3. Hello Azure MFA RADIUS hizmet RADIUS isteklerini standart olmayan bağlantı noktalarına toolisten gerekiyorsa hello istemciler sekmesinde hello kimlik doğrulama ve hesap oluşturma bağlantı noktaları değiştirin.
4. **Ekle**'ye tıklayın.
5. Toohello Azure multi-Factor Authentication sunucusu, bir uygulama adı (isteğe bağlı) ve paylaşılan gizlilik kimliğini doğrulayacak hello gereçte/sunucuda Hello IP adresini girin.

  Merhaba uygulama adı Azure multi-Factor Authentication raporlarında görünür ve SMS veya mobil uygulama kimlik doğrulama iletilerinde görüntülenebilir.

  Merhaba gizli gereksinimlerini toobe hello aynı hem hello Azure çok faktörlü kimlik doğrulama sunucusu ve gereçte/sunucuda paylaşılan.

6. Merhaba denetleyin **multi-Factor Authentication iste kullanıcı eşleşme** tüm kullanıcılar Sunucu'ya aktarılmışsa ya da hello sunucu ve konu toomulti faktörlü kimlik doğrulaması olarak içeri aktarılacak varsa kutusu. Kullanıcıların önemli sayıda sunucu hello henüz içeri aktarılmadı ve/veya iki aşamalı doğrulamayı muaf tutulacaksa hello kutunun işaretini kaldırın.
7. Merhaba denetleyin **etkinleştir geri dönüş OATH belirteci** bir geri dönüş toohello bant dışı olarak telefon araması, SMS, mobil doğrulama uygulamalardan toouse OATH parolalarını istediğiniz ya da anında bildirim kutusu.
8. **Tamam** düğmesine tıklayın.

Gerektiği kadar ek RADIUS istemcileri 8 tooadd 4 adımlarını yineleyin.

## <a name="configure-your-radius-client"></a>RADIUS istemcinizi yapılandırma

1. Merhaba tıklatın **hedef** sekmesi.
2. Hello Azure MFA sunucusu, Active Directory ortamında etki alanına katılmış bir sunucuda yüklüyse, Windows etki alanını seçin.
3. Kullanıcılara LDAP dizinine göre kimlik doğrulaması uygulanması gerekiyorsa **LDAP bağlaması**’nı seçin.

  toouse LDAP bağlaması hello dizin tümleştirme simgesine tıklayın ve böylece hello sunucu tooyour dizin bağlayabilirsiniz hello hello ayarları sekmesinde LDAP yapılandırmasını düzenleyin. LDAP yapılandırma yönergeleri hello bulunabilir [LDAP Proxy Yapılandırma Kılavuzu'nda](multi-factor-authentication-get-started-server-ldap.md).

4. Kullanıcılara başka bir RADIUS sunucusuna göre kimlik doğrulaması yapılması gerekiyorsa, RADIUS sunucularını seçin.
5. Tıklatın **Ekle** tooconfigure hello sunucu toowhich hello Azure MFA sunucusu olacak proxy hello RADIUS istekleri.
6. Merhaba RADIUS sunucusu Ekle iletişim kutusunda başlangıç IP adresi hello RADIUS sunucusu ve paylaşılan gizlilik girin.

  Merhaba gizli gereksinimlerini toobe hello paylaşılan aynı hem hello Azure çok faktörlü kimlik doğrulama sunucusu ve RADIUS sunucusu. Merhaba RADIUS sunucusu tarafından farklı bağlantı noktaları kullanılıyorsa hello kimlik doğrulama bağlantı noktasını ve hesap bağlantı noktasını değiştirin.

7. **Tamam** düğmesine tıklayın.
8. Böylece Azure MFA sunucusu hello tooit gönderilen erişim isteklerini işleyebilir hello Azure MFA sunucusu başka bir RADIUS sunucusuna RADIUS istemcisi olarak hello ekleyin. Aynı paylaşılan gizliliği hello Azure çok faktörlü kimlik doğrulama sunucusu yapılandırılmış hello kullanın.

Daha fazla RADIUS sunucuları bu adımları tooadd yineleyin ve hangi hello Azure MFA sunucusu çağrı bunları ile Merhaba hello sırasını yapılandırın **Yukarı Taşı** ve **Aşağı Taşı** düğmeler.

Bu hello Azure multi-Factor Authentication sunucusu yapılandırmasını tamamlar. Hello sunucu yapılandırılmış hello istemcilerden gelen RADIUS erişim istekleri için yapılandırılan hello bağlantı noktalarını şimdi dinliyor.   

## <a name="radius-client-configuration"></a>RADIUS İstemcisi yapılandırması
tooconfigure hello RADIUS istemcisi hello yönergeleri kullanın:

* Merhaba RADIUS sunucusu olarak hareket edecek RADIUS toohello Azure multi-Factor Authentication Sunucusu'nun IP adresi aracılığıyla, gereçte/sunucuda tooauthenticate yapılandırın.
* Aynı paylaşılan daha önce yapılandırılan gizlilik hello kullanın.
* Var. zaman toovalidate hello kullanıcının kimlik bilgilerini hello RADIUS zaman aşımı too30-60 saniye olarak yapılandırın, iki aşamalı doğrulamayı gerçekleştirmek, bunların yanıtını alma ve sonra toohello RADIUS erişim isteğini yanıtlamaya.
