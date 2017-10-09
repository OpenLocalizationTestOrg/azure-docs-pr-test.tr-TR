---
title: "aaaCloud uygulama bulma güvenlik ve gizlilik konuları | Microsoft Docs"
description: "Bu konuda hello güvenlik ve gizlilik konuları ilgili tooCloud uygulama bulma açıklanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Cloud App Discovery güvenlik ve gizlilik konuları
Microsoft kaydedilmiş tooprotecting gizliliğinizi ve, veri güvenliğini sağlamak için yazılım ve hizmetlerinin, sağlarken kuruluşunuzun hello güvenlik yönetmenize yardımcı olmak.  
Veri tooothers güvenilen yüklediğinizde, o güven sıkı güvenlik mühendislik Yatırımlar ve uzmanlık tooback ister tanımak.
Microsoft Güvenli yazılım geliştirme yaşam döngüsü yöntemler toooperating bir hizmet toostrict uyumluluk ve güvenlik yönergeleri bağlı kalır.  
Güvenli hale getirme ve verileri koruma Microsoft'taki önceliğe sahiptir.

Bu konuda nasıl veri toplanan, işlenen ve Azure Active Directory Cloud App Discovery içinde güvenli açıklanmaktadır

## <a name="overview"></a>Genel Bakış
Cloud App Discovery Azure AD, bir özelliğidir ve Microsoft Azure'da barındırılır.  
Merhaba Cloud App Discovery endpoint agent kullanılan toocollect uygulama bulma yönetilen BT makinelerden verilerdir.  
Merhaba toplanan verileri güvenli bir şekilde bir şifreli kanal toohello Azure AD Cloud App Discovery hizmetine gönderilir.  
Merhaba Cloud App Discovery veri bir kuruluş için daha sonra hello Azure portalında görünür olur. 

![Cloud App Discovery nasıl çalışır?](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Merhaba aşağıdaki bölümlerde bilgi hello akışını izleyin ve kuruluş toohello Cloud App Discovery hizmetine ve toohello Cloud App Discovery portal nihai olarak hareket ederken, güvenliği nasıl sağlanır açıklayın.

## <a name="collecting-data-from-your-organization"></a>Kuruluşunuzdaki verileri toplama
Sipariş toouse Azure Active Directory'nin bulut uygulama bulma özelliği tooget ınsights'ta kuruluşunuzdaki çalışanlar tarafından kullanılan hello uygulamalara toofirst gereksinim duyduğunuz hello Azure AD Cloud App Discovery endpoint agent toomachines kuruluşunuzdaki dağıtın.

Yöneticiler hello Azure Active Directory kiracısı (veya kendi temsilci) hello aracı yükleme paketi hello Azure portal ' indirebilirsiniz. Merhaba Aracısı ya da el ile yüklenebileceğini veya SCCM veya Grup İlkesi kullanarak hello kuruluş içindeki birden çok makinelerde yüklü.

Dağıtım seçenekleri hakkında daha ayrıntılı yönergeler için bkz: [bulut uygulama bulma Grup İlkesi Dağıtım Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Merhaba aracısı tarafından toplanan veriler
tooa Web uygulaması bir bağlantı yapıldığında hello aşağıdaki listede özetlenen hello bilgiler hello aracısı tarafından toplanır. Merhaba yalnızca toplanan bilgiler bu uygulamalar için o hello yönetici bulma için yapılandırdı.  
Merhaba listesini hello Cloud App Discovery dikey penceresinde hello Microsoft aracılığıyla aracı izleyicileri hello bulut uygulamalarını düzenleyebilirsiniz [Azure portal](https://portal.azure.com/)altında **ayarları**->**veri Koleksiyon**->**uygulama koleksiyon listesi**. Daha fazla ayrıntı için bkz: [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Bilgileri kategorisi**: kullanıcı bilgileri  
**Açıklama**:  
bir istek toohello hedef Web uygulaması yapılan hello işlemin Hello Windows kullanıcı adı (ör: etki alanı\kullanıcı adı) hello hello kullanıcının Windows Güvenlik tanımlayıcısı (SID) yanı sıra.

**Bilgileri kategorisi**: işlem bilgileri  
**Açıklama**:  
Merhaba isteği toohello hedef Web uygulaması yapılan hello işlemin Hello adını (örneğin: "iexplore.exe")

**Bilgileri kategorisi**: Makine bilgileri  
**Açıklama**:  
hangi hello üzerinde aracı yüklü hello makine NetBIOS adı.

**Bilgileri kategorisi**: uygulama trafiği bilgileri  
**Açıklama**: 

bağlantı bilgilerini aşağıdaki hello:

* Merhaba kaynak (yerel bilgisayar) ve hedef IP adresleri ve bağlantı noktası numaraları
* Merhaba genel IP adresi hello kuruluşun isteği hangi hello gider.
* Merhaba istek başlangıç zamanı
* Merhaba gönderilen ve alınan trafik hacmi
* Merhaba IP sürümüne (4 veya 6)
* Yalnızca TLS bağlantıları için: hello hedef ana bilgisayar adından hello sunucu adı göstergesi uzantısı veya hello sunucu sertifikası.

HTTP bilgisinden hello:

* Yöntem (GET, POST, vb.)
* Protokol (HTTP/1.1, vb.)
* Kullanıcı aracısı dizesi
* Ana Bilgisayar Adı
* Hedef URI (hariç sorgu dizesi)
* İçerik türü bilgileri
* Başvuran URL bilgileri (sorgu dizesi hariç)

> [!NOTE]
> Merhaba HTTP bilgileri yukarıdaki tüm şifreli olmayan bağlantıları için toplanır.
> Merhaba 'Ayrıntılı İnceleme' ayarı hello Portalı'nda açıldığında TLS bağlantıları için bu bilgileri yalnızca yakalanır. Merhaba 'ON' varsayılan ayardır.
> Daha fazla ayrıntı için aşağıda bkz ve [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

Ayrıca toohello bu hello aracı hello ağ etkinliği hakkında toplar, aynı zamanda hello yazılım ve donanım yapılandırması, hata raporlarını ve hello Aracısı nasıl kullanıldığını hakkında bilgiler hakkında anonim bilgiler toplar.


### <a name="how-hello-agent-works"></a>Merhaba Aracısı nasıl çalışır?
Merhaba aracı yüklemesi, iki bileşenleri içerir:

* Bir kullanıcı modu bileşeni
* Bir çekirdek modu sürücüsü bileşeni (Windows Filtre Platformu'nu sürücüsü)

Hello aracı ilk kez yüklendiğinde bir makineye özel güvenilen sertifika depoları hello makinede hangi BT sonra tooestablish güvenli bir bağlantı ile Merhaba Cloud App Discovery hizmetine kullanır.  
Hello Aracısı, bu güvenli bağlantı üzerinden hello Cloud App Discovery hizmetine ilke yapılandırması düzenli olarak alır.  
Hello İlkesi, hangi bulut uygulamaları toomonitor hakkında bilgi ve otomatik güncelleştirme, diğerlerinin yanında etkinleştirilip etkinleştirilmediğini içerir.

Web trafiği gönderilen ve Internet Explorer ve Chrome hello makineden alınan gibi hello Cloud App Discovery Aracısı hello trafiğini analiz eder ve ilgili meta verileri ayıklayan hello (Merhaba bkz **hello aracısı tarafından toplanan veriler** bölümü yukarıda).  
Dakikada, şifrelenmiş bir kanal üzerinden toplanan hello meta veri toohello Cloud App Discovery hizmetine hello aracı yükler.

Merhaba sürücüsü bileşeni durdurur şifrelenmiş trafik hello ve kendisini hello şifrelenmiş akışa ekler. Merhaba, daha fazla ayrıntı **şifreli bağlantıları (ayrıntılı İnceleme) verilerden kesintiye uğratan** bölümüne bakın.

### <a name="respecting-user-privacy"></a>Saygı kullanıcı gizliliği
Amacımız tooprovide Yöneticiler hello araçları tooset hello arasında bir denge uygulama kullanımı ve kullanıcı gizlilik kuruluşlarında uygun şekilde içine ayrıntılı optik ' dir. toothat son düğmelerini hello Portalı'ndaki hello Ayarları sayfasında aşağıdaki hello sunuyoruz:

* **Veri toplama**: Yöneticiler hangi uygulamaları veya uygulama kategorilerini üzerinde tooget bulma verilerini istedikleri toospecify seçebilirsiniz.
* **Ayrıntılı İnceleme**: hello Aracısı HTTP trafiği için SSL/TLS bağlantılarını topluyorsa, yöneticiler toospecify seçebilirsiniz (diğer adıyla **'Ayrıntılı İnceleme'**). Bu hello sonraki bölümde hakkında daha fazla.
* **Seçenekler onayı**: yöneticiler kullanabilir hello Cloud App Discovery portal toochoose olup toonotify kullanıcılar hello veri toplama hello aracısı tarafından olup toorequire kullanıcı onayı hello Aracısı kullanıcı verilerini toplamaya başlamadan önce.

Merhaba Cloud App Discovery endpoint agent yalnızca hello açıklanan hello bilgiler toplar **hello aracısı tarafından toplanan veriler** yukarıdaki bölümde.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Kesintiye uğratan verileri şifreli bağlantıları (ayrıntılı İnceleme)
Yukarıda belirtildiği gibi hello Aracısı toomonitor verileri şifreli bağlantıları ('ayrıntılı İnceleme') yapılandırabilirler. TLS ([Aktarım Katmanı Güvenliği](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) hello hello Internet üzerinde kullanılan en yaygın protokoller bugün biridir. TLS ile iletişim şifreleyerek güvenli ve özel iletişim kanalı web sunucusu ile bir istemci oluşturabilir; TLS kimlik doğrulama bilgilerini geçirme için temel koruma sağlar ve hassas bilgilerin hello açığa engelleyebilirsiniz.

TLS tarafından sağlanan hello uçtan uca güvenli şifreli kanal önemli güvenlik ve Gizlilik Koruması olanak sağlarken hello Protokolü genellikle kötü amaçlı veya alınan amaçları için kötüye. Çok bu nedenle, aslında, TLS görülür tooas hello "Evrensel güvenlik duvarı geçişini Protokolü" denir. Merhaba kök hello sorununun hello uygulama katmanı veri SSL ile şifrelendiğinden çoğu güvenlik duvarı oluşturulamıyor tooinspect TLS iletişim olmasıdır. Bu bilgiye sahip olmak, saldırganlar sık TLS toodeliver kötü amaçlı yüklerini tooa kullanıcı bile hello en akıllı uygulama katmanı güvenlik duvarları tamamen görme tooTLS olan ve yalnızca TLS iletişim ana bilgisayarlar arasında geçişine izin vermesi emin yararlanın. Son kullanıcılar, sık güvenlik duvarları ve proxy sunucuları, tooconnect toopublic proxy'leri kullanma ve TLS olmayan protokolleri İlkesi tarafından aksi engellenebilir hello güvenlik duvarı üzerinden tünel zorlanan TLS toobypass erişim denetimlerini kullanın.

Ayrıntılı İnceleme hello Cloud App Discovery Aracısı tooact bir güvenilen man-in--middle sağlar. Bir istemci istek yapıldığında tooaccess bir HTTPS korumalı kaynak, hello Endpoint Agent sürücü hello bağlantı durdurur ve SSL sertifikasını hello istemci adına bir yeni bağlantı toohello hedef sunucu tooretrieves oluşturur. Merhaba Aracısı hello sertifika (değil iptal edildi denetimi ve diğer sertifika denetimleri gerçekleştirerek) güvenilir, ve bu başarılı olursa hello Endpoint Agent sonra hello sunucu sertifikasından hello bilgileri kopyalar ve kendi oluşturur sonra doğrular sunucu sertifikası--bu bilgileri kullanarak bir kişiler tarafından ele sertifikası olarak--bilinir. İmzalı üzerinde-çalışma sırasında hello endpoint agent hello Windows güvenilir sertifika deposunda yüklü bir kök sertifikası tarafından Hello kişiler tarafından ele sertifikasıdır. Bu otomatik olarak imzalanan kök sertifikanın dışarı aktarılabilir olmayan olarak işaretlenir ve ACL tooadministrators vardı. Bu hedeflenen toonever bırakın hello makine üzerinde oluşturulmuş olur. Merhaba son kullanıcının istemci uygulaması hello kişiler tarafından ele sertifika aldığında, başarılı bir şekilde tüm hello yolu toohello kök sertifikası hello sertifika zinciri doğrulayabilirsiniz çünkü bunu güvenir. Bu işlem, genellikle bir son kullanıcının bakış açısı aşağıda açıklandığı gibi birkaç uyarılarla saydamdır.

Ayrıntılı İnceleme etkinleştirerek hello Cloud App Discovery Endpoint Agent şifresini çözmek ve şifrelenmiş TLS iletişime hello hizmet tooreduce gürültü izin vererek, inceleyebilir ve şifrelenmiş hello bulut uygulamalarının hello kullanımı hakkında bilgiler.

#### <a name="a-word-of-caution"></a>Bir sözcük uyarı notu
Ayrıntılı İnceleme üzerinde kapatmadan önce amaçları tooyour yasal ve HR Departmanlar iletişim ve bunların onayı almak önemle önerilir. Son kullanıcının özel şifreli iletişim inceleniyor önemli bir konu belirgin nedenleri olabilir. Bir üretim üretimini ayrıntılı inceleme, belirli, Kurumsal güvenlik yapın ve kabul edilebilir kullanım ilkeleri güncelleştirilmiş önce iletişimi şifrelenmiş tooindicate denetlenecek. Kullanıcı bildirimi ve hassas kabul sitelerin (örneğin bankacılık ve tıbbi siteler) muafiyet da olabilir, Cloud App Discovery toomonitor yapılandırırsanız gerekli bunları. Yukarıda belirtildiği gibi Yöneticiler hello Cloud App Discovery portal toochoose olup kullanabilir toonotify kullanıcılar hello aracısı tarafından hello veri toplama ve toorequire kullanıcı onayı olup olmadığını hello Aracısı kullanıcı verilerini toplamaya başlamadan önce.

### <a name="known-issues-and-drawbacks"></a>Bilinen sorunlar ve sakıncaları
Burada TLS kişiler tarafından ele hello son kullanıcı deneyimini etkileyebilecek bazı durumlar vardır:

* Genişletilmiş Doğrulama (EV) sertifikaları, güvenilen bir web sitesini ziyaret ettiğiniz bir görsel ipucu hello web tarayıcısı yeşil tooact hello adres çubuğuna işleyebilir. TLS denetleme EV sertifikaları kullanan web siteleri normal olarak çalışacak şekilde toohello istemci sorunları hello sertifikada EV yineleyemez ancak hello adres çubuğuna yeşil görüntülemez.  
* (Sertifika sabitleme olarak da bilinir) ortak anahtar sabitleme tasarlanan toohelp kullanıcılar man-in--middle saldırılarına karşı koruyun ve standart dışı sertifika yetkilileri. Merhaba kök sertifikası sabitlenmiş bir site için iyi CA'ın bilinen hello birini eşleşmediğinde hello tarayıcı bir hata ile Merhaba bağlantı reddeder. TLS kişiler tarafından ele, aslında bir adam-in--middle, olduğundan bu bağlantıları başarısız olur.
* Kullanıcıların hello tarayıcı Adres çubuğunun tarayıcı tooinspect hello site bilgilerini hello kilit simgesini tıklatın, hello sertifika yetkilisi bitiş zinciri toosign hello Web sitesi sertifikası kullanılır, ancak bunun yerine Windows hello ile biten bir sertifika zinciri görürler değil güvenilen sertifika deposuna.

Bu sorunları hello oluşumları tooreduce, biz bulut hizmetleri izlemek ve toouse bilinen istemci uygulamaları Genişletilmiş Doğrulama veya ortak anahtar sabitleme ve etkilenen bağlantıları kesintiye uğratan hello Endpoint Agent tooavoid isteyin. Bile bu durumda, ancak, bu bulut uygulamalarına hello kullanımını ve aktarılan veri hacmini hello raporları almaya devam, ancak bunlar Denetlenmekte derin olmadığından hello uygulamaları nasıl kullanılan hakkında ayrıntı yok olacak.

## <a name="sending-data-toocloud-app-discovery"></a>Gönderen veri tooCloud uygulama bulma
Meta veri hello aracısı tarafından toplanan sonra tooone minute yukarı hello makinesinde önbelleğe veya hello kadar önbelleğe alınan veriler bir 5 MB cinsinden boyutu. Bunu ardından sıkıştırılır ve güvenli bağlantı toohello Cloud App Discovery hizmetine gönderilir.

Hello Aracısı hello Cloud App Discovery hizmetine herhangi bir nedenle ile oluşturulamıyor toocommunicate ise, hello toplanan meta veriler yalnızca (örneğin, hello Yöneticiler grubu) hello makinedeki ayrıcalıklı kullanıcılar tarafından erişilebilecek bir yerel dosya önbellekte depolanır.  
Merhaba Cloud App Discovery hizmeti tarafından başarıyla alındı kadar hello Aracısı denemeleri tooresend hello meta verileri otomatik olarak önbelleğe.

## <a name="receiving-hello-data-at-hello-service-end"></a>Merhaba hizmet sonunda Hello veri alma
Merhaba aracıları kimlik doğrulaması toohello Cloud App Discovery hello makine belirli istemci kimlik doğrulama sertifikası kullanarak hizmet yukarıda başvurulan ve veri şifrelenmiş bir kanal üzerinden iletir.  
Merhaba Cloud App Discovery hizmetin analytics işlemleri meta verileri her müşteri için ayrı olarak, tüm hello analytics ardışık düzen aşamaları mantıksal olarak bölümleme tarafından kanalı.
Hello meta veri sürücüleri hello hello Portal'daki çeşitli raporlar analiz edilir.

İşlenmemiş meta verileri hello ve analiz hello meta verileri depolanır için too180 günleri. Ayrıca, müşterilerin istediği Azure blob depolama hesabında toocapture analiz hello meta veri seçebilirsiniz.
Bu, uzun bekletme hello veri yanı sıra meta verilerinin çevrimdışı analiz için kullanışlıdır.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Hello Azure portal kullanarak hello verilerine erişme
Toplanan bir çaba tookeep hello meta verilerde güvenli, varsayılan olarak yalnızca genel Yöneticiler hello Kiracı erişim toohello Cloud App Discovery özelliği hello Azure portal sahiptir.  
Bununla birlikte, Yöneticiler bu erişim tooother kullanıcıları veya grupları toodelegate seçebilirsiniz.

> [!NOTE]
> Daha fazla ayrıntı için bkz: [alma başlatılmış olan Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Tüm kullanıcı erişimi hello verileri hello portalında gerekir lisansına bir Azure AD Premium lisansı.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Nasıl ı Kuruluşum içinde kullanılan onaylanmamış bulut uygulamaları bulabilir](active-directory-cloudappdiscovery-whatis.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

