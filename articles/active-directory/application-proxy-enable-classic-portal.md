---
title: "aaaEnable hello Klasik portalındaki Azure AD uygulama proxy'si | Microsoft Docs"
description: "Merhaba Klasik Azure portalında uygulama ara sunucusunu etkinleştirmek ve hello ters proxy hello bağlayıcıları yükleyin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Merhaba Klasik portalında uygulama ara sunucusunu etkinleştirme ve bağlayıcılar indirin
Bu makalede hello adımları tooenable bulut dizininiz için Microsoft Azure AD uygulama proxy'si aracılığıyla Azure AD içinde anlatılmaktadır.

Hangi uygulama proxy'si yapmanıza yardımcı olabilir sahip değilseniz hakkında daha fazla bilgi [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Uygulama Ara Sunucusu önkoşulları
Etkinleştirme ve uygulama ara sunucusu hizmetlerini kullanma önce toohave gerekir:

* [Microsoft Azure AD temel veya premium aboneliği](active-directory-editions.md) ve genel yöneticisi olduğunuz bir Azure AD dizini.
* Windows Server 2012 R2 veya hello uygulama Proxy Bağlayıcısı yükleme 2016 çalıştıran bir sunucu. Merhaba sunucu istekleri toohello uygulama ara sunucusu hizmetlerini hello bulutta gönderir ve yayımladığınız bir HTTP veya HTTPS bağlantı toohello uygulamaları gerekiyor.
  * İçin çoklu oturum açma tooyour yayımlanan uygulamalar, bu makine etki alanı-hello aynı AD etki alanında, yayımlama hello uygulamaları olarak katılması. Bilgi için bkz: [uygulama proxy'si ile çoklu oturum açma](active-directory-application-proxy-sso-using-kcd.md)
* Kuruluşunuz proxy kullanıyorsa Internet sunucuları tooconnect toohello okuma [varolan çalışma şirket içi proxy sunucuları](application-proxy-working-with-proxy-servers.md) hakkında ayrıntılar için tooconfigure bunları.

## <a name="open-your-ports"></a>Bağlantı noktalarını açın

tooprepare ortamınız için Azure AD uygulama proxy'si, önce tooenable iletişimi tooAzure veri merkezleri gerekir. Merhaba yolunda bir güvenlik duvarı varsa, bağlayıcı HTTPS (TCP) yapabilirsiniz, hello toohello uygulama proxy'si bilmediğinden, açık olduğundan emin olun.

1. Açık hello şu bağlantı noktalarının çok**giden** trafiği:

   | Bağlantı noktası numarası | Nasıl kullanılır |
   | --- | --- |
   | 80 | İndirme sertifika iptal listeleri (CRL'ler hello SSL sertifikası doğrulanırken) |
   | 443 | Merhaba uygulama proxy'si hizmeti ile tüm giden iletişim |

   Güvenlik duvarını toooriginating kullanıcılar göre trafiği zorunlu bir ağ hizmeti olarak çalışan Windows hizmetlerinden gelen trafik için şu bağlantı noktalarını açın.

   > [!IMPORTANT]
   > Merhaba tablo bağlayıcı sürümleri 1.5.132.0 hello bağlantı noktası gereksinimleri yansıtır ve daha yeni. Bağlayıcı sürümün hala varsa, bağlantı noktaları aşağıdaki tooenable hello de gerekir: 5671, 8080, 9090, 9091, 9350, 9352 ve 10100 – 10120.
   >
   >Bağlayıcılar toohello en yeni sürüme güncelleştirme hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md#automatic-updates).

2. Güvenlik Duvarı veya proxy DNS uygulamaları güvenilir listeye almayı izin veriyorsa, beyaz liste bağlantıları toomsappproxy.net ve servicebus.windows.net kullanabilirsiniz. Tooallow erişim toohello değil, gerekirse [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653), her hafta güncelleştirilir.

3. Kullanım hello [Azure AD uygulama Proxy Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify Bağlayıcınızı hello uygulama proxy'si hizmeti ulaşabilirsiniz. En azından hello Orta ABD bölgesi ve hello bölgeye en yakın tooyou tüm yeşil onay işaretli olduğundan emin olun. Bunun ötesinde, daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir.

## <a name="enable-application-proxy-in-azure-ad"></a>Azure AD'de uygulama ara sunucusunu etkinleştirme
1. Merhaba içinde bir yönetici olarak oturum açın [Klasik Azure portalı](https://manage.windowsazure.com/).
2. TooActive dizinine gidin ve tooenable uygulama proxy'si istediğiniz hello dizini seçin.

    ![Active Directory - simge](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Seçin **yapılandırma** hello dizin sayfasından ve çok ilerleyin**uygulama proxy'si**.
4. İki durumlu **bu dizin için uygulama ara sunucusu hizmetlerini etkinleştir** çok**etkin**.

    ![Uygulama Ara Sunucusunu etkinleştirme](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. **Download now (Şimdi indir)** seçeneğini belirleyin. Merhaba **Azure AD uygulama ara sunucusu Bağlayıcısı indirme** açar. Okuma ve hello lisans koşullarını kabul edin ve tıklatın **karşıdan** hello Bağlayıcısı için toosave hello Windows Installer dosyasını (.exe).

## <a name="install-and-register-hello-connector"></a>Yükleyin ve hello bağlayıcı kaydedin
1. Çalıştırma **AADApplicationProxyConnectorInstaller.exe** hello sunucuda according toohello Önkoşullar hazır.
2. Merhaba Sihirbazı tooinstall Hello yönergeleri izleyin.
3. Yükleme sırasında istendiğinde tooregister hello Bağlayıcısı hello Azure AD kiracınızın uygulama proxy'si ile demektir.

   * Azure AD genel yönetici kimlik bilgilerinizi sağlayın. Genel yönetici kiracınız, Microsoft Azure kimlik bilgilerinizden farklı olabilir.
   * İçinde hello Bağlayıcıdır yazmaçlar etkinleştirdiğiniz aynı dizinde hello hello Yöneticisi hello uygulama proxy'si hizmeti emin olun. Hello Yöneticisi hello Kiracı etki alanı contoso.com ise, örneğin, olmalıdır admin@contoso.com veya o etki alanındaki başka bir diğer ad.
   * Varsa **IE Artırılmış Güvenlik Yapılandırması** çok ayarlanır**üzerinde** hello sunucuda hello kayıt ekranı engellenebilir. tooallow erişimi, hello hata iletisindeki hello yönergeleri izleyin. Internet Explorer Artırılmış Güvenlik seçeneğinin devre dışı olduğundan emin olun.
   * Bağlayıcı kaydı başarısız olursa bkz. [Uygulama Proxy’si Sorunlarını Giderme](active-directory-application-proxy-troubleshoot.md).  
4. Merhaba yüklemesi tamamlandığında, iki yeni hizmet tooyour server eklendi:

   * **Microsoft AAD Application Proxy Connector** bağlantıyı etkinleştirir

     * **Microsoft AAD Application Proxy Connector Updater** bir otomatik güncelleştirme hizmetidir. Düzenli aralıklarla hello bağlayıcı yeni sürümlerini denetler ve gerektiği gibi hello bağlayıcı güncelleştirir.

     ![Uygulama Ara Sunucusu Bağlayıcısı hizmetleri - ekran görüntüsü](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Tıklatın **son** hello yükleme penceresinde.

Bağlayıcılar hakkında bilgi için bkz. [Azure AD Uygulama Ara Sunucusu bağlayıcıları](application-proxy-understand-connectors.md).

Yüksek düzeyde kullanılabilirlik sağlamak için en az iki bağlayıcı dağıtmanız gerekir. Daha fazla bağlayıcılar toodeploy yineleyin adım 2 ve 3. Her bağlayıcı ayrı ayrı kaydedilmelidir.

Toouninstall hello bağlayıcı istiyorsanız hello bağlayıcı hizmeti ve hello güncelleştirici hizmetini kaldırın. Bilgisayar toofully Kaldır hello hizmetinizi yeniden başlatın.

## <a name="next-steps"></a>Sonraki adımlar
Artık çok hazırsınız[uygulama proxy'si ile uygulama yayımlama](active-directory-application-proxy-publish.md).

Ayrı ağlarda ya da farklı konumlarda uygulamalarınız varsa, bağlayıcı grupları tooorganize hello farklı bağlayıcılar mantıksal birimler halinde kullanabilirsiniz. [Uygulama Proxy bağlayıcıları ile çalışma](active-directory-application-proxy-connectors.md) hakkında daha fazla bilgi edinin.
