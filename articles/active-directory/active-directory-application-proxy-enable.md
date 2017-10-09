---
title: "aaaAzure AD uygulaması Proxy - Başlarken bağlayıcısını yükleme | Microsoft Docs"
description: "Hello Azure portalında uygulama ara sunucusunu etkinleştirmek ve hello ters proxy hello bağlayıcıları yükleyin."
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
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Uygulama proxy'si ile başlayın ve hello bağlayıcısını yükleme
Bu makalede hello adımları tooenable bulut dizininiz için Microsoft Azure AD uygulama proxy'si aracılığıyla Azure AD içinde anlatılmaktadır.

Hakkında daha fazla bilgi etmediğinizden henüz hello güvenlik ve verimlilik avantajlarını farkında uygulama proxy'si tooyour kuruluş getirir, [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Uygulama Ara Sunucusu önkoşulları
Etkinleştirme ve uygulama ara sunucusu hizmetlerini kullanma önce toohave gerekir:

* [Microsoft Azure AD temel veya premium aboneliği](active-directory-editions.md) ve genel yöneticisi olduğunuz bir Azure AD dizini.
* Windows Server 2012 R2 veya hello uygulama Proxy Bağlayıcısı yükleme 2016 çalıştıran bir sunucu. toobe mümkün tooconnect toohello uygulama ara sunucusu hizmetlerini hello bulutta Hello sunucu gerekir ve hello içi yayımladığınız uygulamalar.
  * İçin çoklu oturum açma tooyour kısıtlı Kerberos temsilcisi seçme aracılığıyla yayımlanan uygulamalar bu makine etki alanı-hello aynı AD etki alanında, yayımlama hello uygulamaları olarak katılması. Bilgi için bkz: [uygulama proxy'si ile çoklu oturum açma için KCD](active-directory-application-proxy-sso-using-kcd.md).

Kuruluşunuz proxy kullanıyorsa Internet sunucuları tooconnect toohello okuma [varolan çalışma şirket içi proxy sunucuları](application-proxy-working-with-proxy-servers.md) nasıl tooconfigure, önce bunları alma ile ilgili ayrıntılar için uygulama proxy'si ile çalışmaya.

## <a name="open-your-ports"></a>Bağlantı noktalarını açın

tooprepare ortamınız için Azure AD uygulama proxy'si, önce tooenable iletişimi tooAzure veri merkezleri gerekir. Merhaba yolunda bir güvenlik duvarı varsa, bağlayıcı HTTPS (TCP) yapabilirsiniz, hello toohello uygulama proxy'si bilmediğinden, açık olduğundan emin olun.

1. Açık hello şu bağlantı noktalarının çok**giden** trafiği:

   | Bağlantı noktası numarası | Nasıl kullanılır |
   | --- | --- |
   | 80 | İndirme sertifika iptal listeleri (CRL'ler hello SSL sertifikası doğrulanırken) |
   | 443 | Merhaba uygulama proxy'si hizmeti ile tüm giden iletişim |

   Güvenlik duvarını toooriginating kullanıcılar göre trafiği zorunlu bir ağ hizmeti olarak çalışan Windows hizmetlerinden trafik için bu bağlantı noktalarını açın.

   > [!IMPORTANT]
   > Merhaba tablo bağlayıcı sürümleri 1.5.132.0 hello bağlantı noktası gereksinimleri yansıtır ve daha yeni. Bağlayıcı sürümün hala varsa, ek too80 ve 443:5671, 8080, 9090-9091, bağlantı noktası 9350, aşağıdaki tooenable hello ayrıca gerekir 9352, 10100 – 10120.
   >
   >Bağlayıcılar toohello en yeni sürüme güncelleştirme hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md#automatic-updates).

2. Güvenlik Duvarı veya proxy DNS uygulamaları güvenilir listeye almayı izin veriyorsa, beyaz liste bağlantıları toomsappproxy.net ve servicebus.windows.net kullanabilirsiniz. Tooallow erişim toohello değil, gerekirse [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653), her hafta güncelleştirilir.

3. Microsoft, dört adresleri tooverify sertifikaları kullanır. Diğer ürünler için yapmadıysanız aşağıdaki URL'lere erişim toohello izin ver:
   * mscrl.microsoft.com:80
   * CRL.microsoft.com:80
   * OCSP.msocsp.com:80
   * www.microsoft.com:80

4. Bağlayıcınızı hello kayıt işlemi için erişim toologin.windows.net ve login.microsoftonline.net ihtiyacı vardır.

5. Kullanım hello [Azure AD uygulama Proxy Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify Bağlayıcınızı hello uygulama proxy'si hizmeti ulaşabilirsiniz. En azından hello Orta ABD bölgesi ve hello bölgeye en yakın tooyou tüm yeşil onay işaretli olduğundan emin olun. Bunun ötesinde, daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir.

## <a name="install-and-register-a-connector"></a>Yükleyin ve bir bağlayıcı kaydedin
1. Merhaba içinde bir yönetici olarak oturum açın [Azure portal](https://portal.azure.com/).
2. Geçerli dizininiz hello sağ üst köşedeki kullanıcı adınızı altında görüntülenir. Toochange dizinleri ihtiyacınız varsa, bu simgeyi seçin.
3. Çok Git**Azure Active Directory** > **uygulama proxy'si**.

   ![TooApplication Proxy gidin](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Seçin **karşıdan bağlayıcı**.

   ![Bağlayıcıyı indir](./media/active-directory-application-proxy-enable/download_connector.png)

5. Çalıştırma **AADApplicationProxyConnectorInstaller.exe** hello sunucuda according toohello Önkoşullar hazır.
6. Merhaba Sihirbazı tooinstall Hello yönergeleri izleyin. Yükleme sırasında istendiğinde tooregister hello Bağlayıcısı hello Azure AD kiracınızın uygulama proxy'si ile demektir.

   * Azure AD genel yönetici kimlik bilgilerinizi sağlayın. Genel yönetici kiracınız, Microsoft Azure kimlik bilgilerinizden farklı olabilir.
   * İçinde hello Bağlayıcıdır yazmaçlar etkinleştirdiğiniz aynı dizinde hello hello Yöneticisi hello uygulama proxy'si hizmeti emin olun. Hello Yöneticisi hello Kiracı etki alanı contoso.com ise, örneğin, olmalıdır admin@contoso.com veya o etki alanındaki başka bir diğer ad.
   * Varsa **IE Artırılmış Güvenlik Yapılandırması** çok ayarlanır**üzerinde** Merhaba bağlayıcısını yüklediğiniz hello sunucuda hello kayıt ekranı göremeyebilirsiniz. tooget erişimi, hello hata iletisindeki hello yönergeleri izleyin. Internet Explorer Artırılmış Güvenlik seçeneğinin devre dışı olduğundan emin olun.

Yüksek düzeyde kullanılabilirlik sağlamak için en az iki bağlayıcı dağıtmanız gerekir. Her bağlayıcı ayrı ayrı kaydedilmelidir.

## <a name="test-that-hello-connector-installed-correctly"></a>Yüklendiğinden bu hello bağlayıcı test

Bunun için her iki hello Azure portal veya sunucunuzdaki denetleyerek yeni bir bağlayıcı doğru yüklendiğini doğrulayabilirsiniz. 

Azure portal Merhaba, tooyour kiracısı'nda oturum açın ve çok gidin**Azure Active Directory** > **uygulama proxy'si**. Tüm bağlayıcılar ve bağlayıcı gruplarını, bu sayfada görüntülenir. Bir bağlayıcı toosee ayrıntılarını seçin veya farklı bağlayıcı grubuna taşıyın. 

Sunucunuz üzerinde etkin hizmetleri hello bağlayıcı ve hello connector updater hello listesini kontrol edin. Merhaba iki hizmet çalıştırdıktan hemen Başlat ancak Aksi durumda, bunları etkinleştirmek gerekir: 

   * **Microsoft AAD Application Proxy Connector** bağlantıyı etkinleştirir

   * **Microsoft AAD Application Proxy Connector Updater** bir otomatik güncelleştirme hizmetidir. Merhaba güncelleştirici hello bağlayıcı yeni sürümlerini denetler ve güncelleştirmeleri bağlayıcı gerektiği gibi hello.

   ![Uygulama Ara Sunucusu Bağlayıcısı hizmetleri - ekran görüntüsü](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Bağlayıcılar ve toodate nasıl kalırlar hakkında daha fazla bilgi için bkz: [anlamak Azure AD uygulama proxy'si Bağlayıcılar](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Sonraki adımlar
Artık çok hazırsınız[uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).

Ayrı ağlarda ya da farklı konumlarda uygulamalarınız varsa, bağlayıcı grupları tooorganize hello farklı bağlayıcılar mantıksal birimler halinde kullanın. [Uygulama Proxy bağlayıcıları ile çalışma](active-directory-application-proxy-connectors-azure-portal.md) hakkında daha fazla bilgi edinin.
