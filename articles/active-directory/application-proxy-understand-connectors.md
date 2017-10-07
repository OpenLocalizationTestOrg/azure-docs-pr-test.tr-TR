---
title: "aaaUnderstand Azure AD uygulama proxy'si bağlayıcılar | Microsoft Docs"
description: "Merhaba temel Azure AD uygulama proxy'si bağlayıcılar hakkında bilgiler yer almaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Azure AD uygulama proxy'si bağlayıcılar anlama

Bağlayıcılar, hangi Azure AD uygulama proxy'si mümkün kılar ' dir. Bunlar basit ve kolay toodeploy ve bakımını ve Süper güçlü. Bu makalede nasıl çalıştığını, hangi bağlayıcılar olan ve ilgili bazı öneriler ele toooptimize dağıtımınızı. 

## <a name="what-is-an-application-proxy-connector"></a>Bir uygulama Proxy Bağlayıcısı nedir

Bağlayıcılar, şirket içi yaslanın ve hello giden bağlantı toohello uygulama proxy'si hizmeti kolaylaştırmak basit aracılardır. Bağlayıcılar access toohello arka uç uygulaması olan bir Windows sunucusuna yüklenmesi gerekir. Bağlayıcılar trafiği toospecific uygulamaları işleme her grubuyla bağlayıcı gruplar halinde düzenleyebilirsiniz. Bağlayıcılar Yük Dengelemesi otomatik olarak ve toooptimize ağ yapınızı yardımcı olabilir. 

## <a name="requirements-and-deployment"></a>Gereksinimler ve dağıtım

Uygulama proxy'si toodeploy başarılı bir şekilde, en az bir bağlayıcı gerekir, ancak iki veya daha fazla bilgi için büyük esneklik öneririz. Windows Server 2012 R2 veya 2016 makinesinin Hello bağlayıcı yükleyin. Merhaba Bağlayıcısı toobe mümkün toocommunicate yayımlama hello şirket içi uygulamalara yanı sıra hello uygulama proxy'si hizmeti olması gerekir. 

Merhaba bağlayıcı sunucusu hello ağ gereksinimleri hakkında daha fazla bilgi için bkz: [uygulama proxy'si ile çalışmaya başlama ve bağlayıcıyı yükleme](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Bakım
Merhaba bağlayıcılar ve hello hizmet tüm hello yüksek kullanılabilirlik görevlerini dikkatli olun. Bunlar eklenebilir veya dinamik olarak kaldırılmış. Yeni bir istek geldiğinde her zaman şu anda kullanılabilir yönlendirilmiş tooone hello bağlayıcı değil. Bağlayıcıyı geçici olarak kullanılamıyor, toothis trafiği yanıt vermiyor.

Merhaba bağlayıcılar durum bilgisiz ve hiçbir yapılandırma verilerini hello makinede sahip. Merhaba depoladıkları yalnızca hello ayarları hello hizmeti ve kimlik doğrulama sertifikasını bağlanmak için verilerdir. Toohello hizmet bağlandıklarında tüm gerekli hello yapılandırma verilerini çekmek ve her birkaç dakika yenileyin.

Bağlayıcılar da hello sunucu toofind mi çıkışı yoklamak hello Bağlayıcısı'nın daha yeni bir sürümü. Bulunması durumunda hello bağlayıcılar kendilerini güncelleştirin.

Bağlayıcılar, çalışan hello makineden hello olay günlüğü ve performans sayaçlarını kullanarak izleyebilirsiniz. Veya durumlarını hello uygulama proxy'si sayfasından hello Azure portal görüntüleyebilirsiniz:

 ![Azuread'i uygulama Proxy bağlayıcıları](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

Kullanılmayan bağlayıcılarını silip toomanually yok. Bir bağlayıcı çalıştırırken toohello hizmet bağladığı gibi etkin kalır. Kullanılmayan bağlayıcılar olarak etiketlenmiş _etkin olmayan_ ve kaldıktan sonra 10 gün kaldırılır. Ancak, bir bağlayıcı toouninstall istiyorsanız, hello bağlayıcı hizmeti ve hello güncelleştirici hizmetini hello sunucudan kaldırın. Bilgisayar toofully Kaldır hello hizmetinizi yeniden başlatın.

## <a name="automatic-updates"></a>Otomatik güncelleştirmeler

Azure AD dağıttığınız tüm hello bağlayıcıları için otomatik güncelleştirmeler sağlar. Hello Application Proxy Connector Updater hizmetinin çalıştığı sürece, bağlayıcılar otomatik olarak güncelleştirilir. Görmüyorsanız, sunucunuzdaki Connector Updater hizmet Merhaba, çok ihtiyacınız[Bağlayıcınızı yeniden](active-directory-application-proxy-enable.md) tooget herhangi bir güncelleştirme. 

Bir otomatik güncelleştirme toocome tooyour Bağlayıcısı için toowait istemiyorsanız, el ile yükseltme gerçekleştirebilirsiniz. Toohello Git [Bağlayıcısı indirme sayfası](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) bulunduğu ve select Bağlayıcınızı olduğu hello sunucuda **karşıdan**. Bu işlem hello yerel bağlayıcı için bir yükseltme kapalı başlatır. 

Birden çok bağlayıcı, kiracıları için her grubu tooprevent kapalı kalma süresi, ortamınızdaki zamanında bir bağlayıcı hello otomatik güncelleştirmeler hedefleyin. 

Bağlayıcınızı varsa güncelleştirdiğinde kapalı kalma süresi karşılaşabilirsiniz:  
- Yalnızca tek bir bağlayıcıyı gerekir. tooavoid bu kapalı kalma süresi ve yüksek kullanılabilirlik, geliştirmek ikinci bağlayıcısını öneririz ve [bağlayıcı grubu oluşturma](active-directory-application-proxy-connectors-azure-portal.md).  
- Merhaba güncelleştirme başladığındaki bağlayıcı bir işlem hello ortadaki oluştu. Merhaba ilk işlem kaybı olmamasına rağmen tarayıcınızı hello işlemi otomatik olarak yeniden denemeniz gerekir veya, sayfayı yenileyin. Merhaba isteği gönderilir, hello yönlendirilmiş tooa yedekleme bağlayıcı trafiğidir.

## <a name="creating-connector-groups"></a>Bağlayıcı grupları oluşturma

Bağlayıcı grupları tooassign belirli bağlayıcılar tooserve belirli uygulamaları etkinleştirir. Bağlayıcıları çeşitli gruplamak ve her uygulama tooa grubu atayın. 

Bağlayıcı grupları daha kolay toomanage büyük dağıtımları kolaylaştırır. Bunlar aynı zamanda gecikme farklı bölgelerde barındırılan uygulamalar tooserve yalnızca yerel uygulamalar konum temelli bağlayıcı grupları oluşturabileceğinden olan kiracılar için iyileştirir. 

toolearn bağlayıcı grupları hakkında daha fazla bilgi görmek [ayrı ağlar ve konumları bağlayıcı gruplarını kullanarak uygulamaları yayımlama](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Güvenlik ve ağ özellikleri

Bağlayıcılar toosend istekleri toohello uygulama proxy'si hizmeti sağlayan hello ağ üzerinde herhangi bir yerden yüklenebilir. Önemli olan erişim tooyour uygulamaları hello bağlayıcı ayrıca çalıştıran bu hello bilgisayarın vardır ' dir. Bağlayıcılar Kurumsal ağınızın içinde veya hello bulutta çalışan bir sanal makineye yükleyebilirsiniz. Bağlayıcılar sivil bölge (DMZ) içinde çalıştırabilirsiniz, ancak tüm trafik ağınıza güvenli kalması giden olduğu için ise gerekli değildir.

Bağlayıcılar, yalnızca giden istekleri göndermek. Merhaba giden trafiği toohello uygulama proxy'si hizmeti ve toohello gönderilir yayımlanan uygulamaları. Oturum kurulduktan sonra her iki yönde trafik akışlar için bağlantı noktalarını gelen tooopen yok. Yük Dengeleme hello bağlayıcılar arasında yukarı tooset sahip yok ya da, güvenlik duvarları üzerinden gelen erişimi yapılandırmak. 

Giden güvenlik duvarı kuralları yapılandırma hakkında daha fazla bilgi için bkz: [varolan çalışma şirket içi proxy sunucuları](application-proxy-working-with-proxy-servers.md).

Kullanım hello [Azure AD uygulama Proxy Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify Bağlayıcınızı hello uygulama proxy'si hizmeti ulaşabilirsiniz. En azından hello Orta ABD bölgesi ve hello bölgeye en yakın tooyou tüm yeşil onay işaretli olduğundan emin olun. Bunun ötesinde, daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir. 

## <a name="performance-and-scalability"></a>Performans ve ölçeklenebilirlik

Merhaba uygulama proxy'si hizmeti için ölçek saydamdır, ancak ölçek bağlayıcıların bir unsurdur. Yeterli bağlayıcılar toohandle yoğun trafik toohave gerekir. Ancak, bir bağlayıcı grubundaki tüm bağlayıcılar otomatik olarak yük dengelemesi nedeniyle tooconfigure Yük Dengeleme gerekmez.

Bağlayıcılar durum bilgisiz olduğundan, kullanıcılar ya da oturumları hello sayıyla etkilenmez. Bunun yerine, toohello, isteği sayısını ve bunların yükü boyutu yanıt. Standart web trafiği ile ortalama bir makine saniyede birkaç bin istekleri işleyebilir. Merhaba belirli kapasite hello tam makine özelliklerine bağlıdır. 

Merhaba bağlayıcı performansı, CPU ve ağ tarafından bağlıdır. Ağ önemli tooget hızlı bağlantı toohello uygulamaları ve azure'da hello çevrimiçi hizmet ederken CPU performans SSL şifreleme ve şifre çözme, için gereklidir.

Buna karşılık, küçük bir sorun bağlayıcıların bellektir. Merhaba çevrimiçi hizmet hello işleme çoğunu ve tüm kimliği doğrulanmamış trafiği mvc'deki. Merhaba bulutta yapılabilir her şeyi hello bulutta yapılır. 

Performansı etkileyen diğer bir etken hello ağ dahil olmak üzere hello bağlayıcılar arasındaki hello kalitesini şöyledir: 

* **Merhaba çevrimiçi hizmet**: yavaş veya Yüksek gecikmeli bağlantılar toohello uygulama proxy'si hizmeti Azure etkisi hello bağlayıcı performans. Merhaba en iyi performans için kuruluş tooAzure hızlı rota ile bağlanın. Aksi takdirde, bu bağlantıları tooAzure mümkün olduğunca verimli olarak işlenir olun ağ ekibinizin sahip. 
* **Merhaba arka uç uygulamaları**: Bazı durumlarda, hello bağlayıcı ve yavaş veya bağlantıları engelle hello arka uç uygulamalar arasında ek proxy'leri vardır. tootroubleshoot bu senaryo, hello bağlayıcı sunucusundan bir tarayıcı açın ve tooaccess hello uygulamayı deneyin. Azure'da hello bağlayıcılar çalıştırın, ancak şirket içi hello uygulamalardır hello deneyimi ne kullanıcılarınızın beklediğiniz olmayabilir.
* **etki alanı denetleyicileri hello**: hello bağlayıcılar Kerberos Kısıtlı temsilci kullanarak SSO gerçekleştirirseniz, bunlar hello etki alanı denetleyicileri hello isteği toohello arka uç göndermeden önce başvurun. Merhaba bağlayıcılar Kerberos biletlerinin bir önbelleğe sahip, ancak meşgul bir ortamda hello yanıtlama hello etki alanı denetleyicilerinin performansını etkileyebilir. Bu sorunu daha yaygın Azure'da çalıştırın, ancak şirket içi etki alanı denetleyicileriyle iletişim bağlayıcıları için kullanılır. 

Ağınızın en iyi duruma getirme hakkında daha fazla bilgi için bkz: [Azure Active Directory Uygulama proxy'si kullanırken ağ topolojisi hakkında önemli noktalar](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Etki alanına katılma

Bağlayıcılar olmayan etki alanına katılmış bir makinede çalıştırabilirsiniz. Ancak, tümleşik Windows kimlik doğrulaması (IWA) kullanan tek oturum açma (SSO) tooapplications istiyorsanız, bir etki alanına katılmış makine gerekir. Bu durumda, hello bağlayıcı makineler gerçekleştirebilirsiniz birleştirilmiş tooa etki alanı olmalıdır [Kerberos](https://web.mit.edu/kerberos) Kısıtlı temsilci hello hello kullanıcılar adına yayımlanan uygulamalar.

Bağlayıcılar, birleştirilmiş toodomains veya kısmi güven veya yalnızca tooread etki alanı denetleyicilerine sahip ormanları de olabilir.

## <a name="connector-deployments-on-hardened-environments"></a>Sağlamlaştırılmış ortamlarla bağlayıcı dağıtımları

Genellikle, bağlayıcı dağıtım basittir ve özel yapılandırma gerektirmez. Ancak, düşünülmesi gereken bazı benzersiz koşullar vardır:

* Merhaba giden trafiğini sınırlandırmak kuruluşlar gerekir [gerekli bağlantı noktalarını açın](active-directory-application-proxy-enable.md#open-your-ports).
* FIPS uyumlu makineler, gerekli toochange olabilir kendi yapılandırma tooallow bağlayıcı işlemleri toogenerate hello ve bir sertifika deposu.
* Bu sorunu hello isteklerini ağ hello işlemleri temel alan ortamlarına kilitleme kuruluşların toomake iki bağlayıcı Hizmetleri etkin tooaccess tüm gerekli bağlantı noktaları ve IP'leri olduğundan emin vardır.
* Bazı durumlarda, giden iletme proxy'leri hello iki yönlü sertifika kimlik doğrulaması bölme ve hello iletişimi toofail neden.

## <a name="connector-authentication"></a>Bağlayıcı kimlik doğrulaması

tooprovide güvenli bir hizmet, bağlayıcılar tooauthenticate hello hizmeti doğru olduğundan ve hello hizmet hello bağlayıcı doğru tooauthenticate sahiptir. Bu kimlik doğrulaması yapılır hello bağlayıcılar hello bağlantı başlattığınızda istemci ve sunucu sertifikaları kullanarak. Bu şekilde hello yöneticinin kullanıcı adı ve parola hello bağlayıcı makinede depolanmaz.

kullanılan hello belirli toohello uygulama proxy'si hizmeti sertifikalardır. Merhaba ilk kaydı sırasında oluşturulan ve otomatik olarak hello bağlayıcılar tarafından her ay birkaç yenilendi. 

Bir bağlayıcı bağlı değilse toohello hizmeti birkaç ay, kendi sertifikaları için eski olabilir. Bu durumda, kaldırın ve hello bağlayıcı tootrigger kaydı yükleyin. Aşağıdaki PowerShell komutlarını hello çalıştırabilirsiniz:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Merhaba başlık altında

Aynı yönetim araçları Windows olay günlükleri de dahil olmak üzere hello çoğunu sahip oldukları için bağlayıcıları Windows Server Web uygulama proxy'si üzerinde temel alır

 ![Olay günlükleri Olay Görüntüleyicisi'ni hello ile yönetme](./media/application-proxy-understand-connectors/event-view-window.png)

ve Windows performans sayaçları. 

 ![Merhaba Performans İzleyicisi sayaçları toohello bağlayıcısıyla ekleme](./media/application-proxy-understand-connectors/performance-monitor.png)

Hello bağlayıcılar, yönetim ve oturum sahip günlükleri. Hello Yöneticisi günlükleri anahtar olayları ve bunların hataları vardır. Merhaba oturum günlükleri tüm hello işlemleri ve bunların işleme ayrıntılarını içerir. 

toosee hello günlükleri, Git toohello Olay Görüntüleyicisi'ni açık hello **Görünüm** menü ve Etkinleştir **Göster Analitik ve hata ayıklama günlüklerini**. Daha sonra bunları olay toplama toostart etkinleştirin. Merhaba bağlayıcılar sunucudaki daha yeni bir sürüm tabanlı olarak bu günlükler Windows Server 2012 R2'deki Web uygulaması proxy'si görünmez.

Merhaba hello Hizmetleri penceresinde hello hizmetinin durumunu inceleyebilirsiniz. Merhaba bağlayıcı iki Windows Hizmetleri oluşur: hello gerçek Bağlayıcısı ve hello güncelleştirici. Bunların her ikisi de hello zaman çalıştırmanız gerekir.

 ![Azuread'i Hizmetleri yerel](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Sonraki adımlar


* [Ayrı ağlarda ve konumları bağlayıcı gruplarını kullanarak uygulama yayımlama](active-directory-application-proxy-connectors-azure-portal.md)
* [Mevcut şirket içi proxy sunucuları ile çalışma](application-proxy-working-with-proxy-servers.md)
* [Uygulama proxy'si ve bağlayıcı hatalarında sorun giderme](active-directory-application-proxy-troubleshoot.md)
* [Nasıl toosilently yükleme hello Azure AD uygulama ara sunucusu Bağlayıcısı](active-directory-application-proxy-silent-installation.md)

