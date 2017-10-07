---
title: "aaaLog Analytics veri güvenliği | Microsoft Docs"
description: "Nasıl günlük analizi gizliliğinizi korur ve verilerinizin güvenliğini sağlama hakkında bilgi edinin."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Günlük analizi veri güvenliği
Microsoft kaydedilmiş tooprotecting gizliliğinizi ve, veri güvenliğini sağlamak için yazılım ve hizmetlerinin, sunarken Merhaba, kuruluşunuzun BT altyapısı yönetmenize yardımcı olur. Veri tooothers güvenilen bu güven sıkı güvenlik gerektiren farkındayız. Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen.

Güvenli hale getirme ve verileri koruma Microsoft'taki önceliğe sahiptir. Herhangi bir sorunuz, öneriler veya sorunlar hakkında bilgi bizim güvenlik ilkeleri de dahil olmak üzere, aşağıdaki hello hiçbirini ile başvuracaklarını [Azure destek seçenekleri](http://azure.microsoft.com/support/options/).

Bu makalede nasıl veri toplanan, işlenen ve günlük analizi tarafından hello Operations Management Suite (OMS) güvenli açıklanmaktadır. Aracıları tooconnect toohello web hizmetini kullanmak, System Center Operations Manager toocollect işletimsel verileri kullanma veya günlük analizi tarafından kullanılmak üzere Azure Tanılama verileri almak. Merhaba toplanan verileri hello Internet gönderilen sertifika tabanlı kimlik doğrulaması ve SSL 3 toohello günlük analizi hizmeti kullanarak, hangi barındırılan Microsoft Azure'da. Gönderilmeden önce veri hello aracısı tarafından sıkıştırılır.

Merhaba günlük analizi hizmeti yöntemler aşağıdaki hello kullanarak bulut tabanlı verilerinizi güvenli bir şekilde yönetir:

* veriler arasında ayrım yapma
* veri saklama
* Fiziksel güvenlik
* Olay yönetimi
* Uyumluluk
* güvenlik standartları sertifikaları

## <a name="data-segregation"></a>veriler arasında ayrım yapma
Müşteri verileri hello OMS hizmet boyunca her bir bileşende mantıksal olarak ayrı tutulur. Tüm veriler kuruluşa göre etiketlenir. Bu etiketleme hello veri yaşam döngüsü boyunca devam ederse ve her hello hizmet katmanında uygulanır. Her bir müşteri hello uzun vadeli veri kaynakları barındıran ayrılmış bir Azure blob var.

## <a name="data-retention"></a>Veri saklama
Dizinli günlük arama verilerin depolandığı ve planı fiyatlandırma according tooyour korunur. Daha fazla bilgi için bkz: [günlük analizi fiyatlandırma](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft, 30 gün hello OMS çalışma kapatıldıktan sonra müşteri verilerini siler. Microsoft Azure depolama hesabı hello veri bulunduğu hello da siler. Müşteri verileri kaldırıldığında, fiziksel sürücü yok yok.

Aşağıdaki tablonun hello hello kullanılabilir OMS çözümlerinde bazıları listeler ve bunlar toplamak veri türleri örnekler hello.

| **Çözüm** | **Veri türleri** |
| --- | --- |
| Yapılandırma Değerlendirmesi |Yapılandırma verileri, meta verileri ve durum verileri |
| Kapasite Planlaması |Performans verilerini ve meta veriler |
| Kötü Amaçlı Yazılımdan Koruma |Yapılandırma verileri, meta veriler |
| Sistem Güncelleştirme Değerlendirmesi |Meta verileri ve durum verileri |
| Günlük Yönetimi |Kullanıcı tanımlı olay günlükleri, Windows olay günlüklerini ve/veya IIS günlükleri |
| Değişiklik İzleme |Yazılım envanteri ve Windows hizmeti meta verileri |
| SQL ve Active Directory değerlendirme |WMI verilerini, kayıt defteri verilerini, performans verileri ve SQL Server dinamik yönetim sonuçları görüntüleyin |

Aşağıdaki tablonun hello veri türlerinin örnekleri gösterilir:

| **Veri türü** | **Alanları** |
| --- | --- |
| Uyarı |Ad, uyarı açıklaması, Basemanagedentityıd, sorun kimliği, IsMonitorAlert, RuleId, çözünürlük durumu, önceliği, önem derecesi, kategori, sahibi, çözüm bulan, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount Uyarısı TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Yapılandırma |CustomerID, Agentıd, Entityıd, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Olay |Olay Kimliği, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, sayı, kategori, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Not:** toohello Windows olay günlüğüne özel alanlar olaylarla yazdığınızda, OMS bunları toplar. |
| Meta Veriler |Basemanagedentityıd, ObjectStatus, kuruluş birimi, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IP adresi, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Adres, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Performans |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, görüntülendiğinden, TimeSampled, TimeAdded |
| Durum |StateChangeEventId, stateId, NewHealthState, OldHealthState, bağlam, TimeGenerated, TimeAdded, StateId2, Basemanagedentityıd, Monitorıd, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Fiziksel güvenlik
Merhaba günlük analizi OMS hizmetindeki Microsoft personeli tarafından manned ve tüm etkinlikler günlüğe kaydedilir ve denetlenebilir. Merhaba hizmeti tamamen Azure üzerinde çalışır ve Azure ortak mühendislik ölçütler hello ile uyumludur. Başlangıç sayfası 18 hello fiziksel güvenlik Azure varlıklarını ilgili ayrıntıları görüntüleyebilirsiniz [Microsoft Azure güvenlik genel bakış](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Fiziksel erişim hakları toosecure alanları artık hello OMS hizmetinde, aktarım ve sonlandırma gibi sorumluluğu olan herkes için bir iş günü içinde değişir. Merhaba genel fiziksel altyapı kullanırız adresindeki hakkında bilgi edinebilirsiniz [Microsoft Datacenters](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Olay yönetimi
OMS tüm Microsoft hizmetlerini uygun bir olay Yönetimi işlemini sahiptir. toosummarize, biz:

* Kullanım güvenlik sorumluluk bir kısmı tooMicrosoft ve bir kısmını ait olduğu bir paylaşılan sorumluluk modeli toohello müşterinin ait
* Azure güvenlik olayları yönetme
  * Bir olay algılandığında bir araştırma Başlat
  * Merhaba etki ve bir olay yanıtlama çağrısı ekip üyesi tarafından bir olayın önem değerlendirin. Üzerinde bulgu göre hello değerlendirme olabilir veya daha fazla yükseltme toohello güvenlik yanıtı takım sağlamayabilir.
  * Bir olay güvenlik yanıtı uzmanlar tooconduct hello teknik veya adli araştırma tarafından Tanılama, kapsama, azaltma ve çözüm stratejilerini belirleme. Merhaba güvenlik ekibi müşteri verilerini gösterilen tooan yasadışı veya yetkisiz duruma gelmiş olabilir inanırsa hello müşteri olay bildirim işlemi, tek tek, Paralel yürütme paralel olarak başlar.  
  * Sabitle ve hello olaydan kurtarın. Merhaba olay yanıtlama takım, bir kurtarma planı toomitigate hello sorunu oluşturur. Etkilenen sistemleri karantinaya alma gibi kriz kapsama adımları hemen ve Tanılama ile paralel ortaya çıkabilir. Uzun vadeli Azaltıcı Etkenler hello hemen risk geçtikten sonra oluşan planlanan.  
  * Merhaba olayı kapatın ve bir Proje Sonrası-Değerlendirme yürütün. Merhaba olay yanıtlama takım hello amacınıza toorevise ilkeleri, yordamları ve işlemler tooprevent hello olay yinelenmesini bir proje sonrası-hello hello ayrıntılarını özetleyen değerlendirme olay, oluşturur.
* Güvenlik olayları müşterileri bildir
  * Etkilenen müşteriler ve tooprovide Hello kapsamını mümkün olduğunca bildiren bir duyuru ayrıntılı olarak etkilenen herkes belirleme
  * Bir bildirim tooprovide müşteriler yeterince ayrıntılı bilgilerle oluşturun, böylece bunların ucunda bir araştırma yapabileceğiniz ve değil unduly hello bildirim işlemi geciktirme sırasında tootheir son kullanıcılar yaptığınız verilmesini sağlayın.
  * Onayla ve gerektiği gibi hello olay bildirin.
  * Bir olay bildirimi aşırı gecikme olmadan ve yasal veya sözleşme taahhüt göre müşterilerle bildirin. Güvenlik olayları bildirimleri herhangi bir yöntem Microsoft seçer, e-posta aracılığıyla dahil olmak üzere tooone veya daha fazla müşteri'nin Yöneticiler teslim edilir.
* Takım hazırlık ve eğitim gerçekleştir
  * Microsoft personeli gerekli toocomplete güvenlik ve tooidentify ve güvenlik sorunları şüpheli rapor yardımcı tanıma Eğitim ' dir.  
  * Microsoft Azure hizmet Hello üzerinde çalışan operatörlerinin müşteri verilerini barındırma erişim toosensitive sistemlerini çevreleyen toplama eğitim sorumlulukları vardır.
  * Microsoft Güvenlik Yanıt personeli kendi rolleri için özelleştirilmiş eğitim alma

Tüm Müşteri verilerinin kaybına ortaya çıkarsa, size bir gün içinde her bir müşteri bildirin. Ancak, müşteri veri kaybı ile OMS hiçbir zaman oluştu. Ayrıca, biz oluşturulduğu veri kopyalarını bulundurmak ve coğrafi olarak dağıtılmış.

Microsoft toosecurity olayları nasıl yanıt vereceğini hakkında daha fazla bilgi için bkz: [Microsoft Azure güvenlik hello bulut yanıtta](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Uyumluluk
OMS yazılım geliştirme ve hizmet ekibin bilgi güvenliği hello ve idare program kendi iş gereksinimlerini destekleyen ve toolaws ve düzenlemelere konusunda açıklandığı gibi aynılarını [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) ve [Microsoft Güven Merkezi Uyumluluk](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Nasıl OMS güvenlik gereksinimlerini oluşturur, güvenlik denetimleri tanımlar, yönetir ve riskleri izleyen de açıklanmaktadır vardır. Yıllık, biz gözden geçirme ilkeler, standartlar, yordamlar ve yönergeleri.

Her OMS geliştirme ekibi üyesi resmi uygulama güvenlik eğitimi alır. Dahili olarak, sürüm denetimi sistemi yazılım geliştirme için kullanırız. Her yazılım projesi hello sürüm denetimi sistemi tarafından korunur.

Microsoft, denetlediği ve tüm Microsoft hizmetlerinde değerlendirir güvenlik ve uyumluluk bir ekip sahiptir. Bilgi güvenliği görevlileri hello takım yapmak ve bunlar OMS geliştirmek Departmanlar mühendislik hello ile ilişkili değil. Merhaba güvenlik görevlileri kendi yönetim zinciri sahip ve ürün ve Hizmetleri tooensure güvenlik ve uyumluluk bağımsız değerlendirmeleri yürütün.

Microsoft'un Panosu Yönetim kurulu tüm bilgi güvenliği programlarını Microsoft'taki hakkında yıllık bir rapor olarak bildirilir.

Merhaba, OMS yazılım geliştirme ve hizmet ekibinin etkin olarak çeşitli sertifikalar hello Microsoft Legal ve uyumluluk ekipleri ve diğer endüstri iş ortaklarının tooacquire ile çalışmaktadır.

## <a name="certifications-and-attestations"></a>Sertifikaları ve attestations
OMS günlük analizi hello gereksinimleri aşağıdaki uyuyor:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Ödeme Kartı endüstrisi (PCI uyumlu) veri güvenliği standardı (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) hello PCI güvenlik standartları Council tarafından.
* [Hizmet kuruluş denetimleri (SOC) 1 Type 1 ve SOC 2 tür 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2) uyumlu
* [HIPAA ve HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) HIPAA iş ilişkilendirmek anlaşması olan şirketler için
* Windows ortak mühendislik ölçütler
* Microsoft Güvenilir Bilgi İşlem
* Bir Azure hizmeti OMS kullandığı hello bileşenlerinin tooAzure uyumluluk gereksinimlerini uyması. Hakkında daha fazla bilgi edinebilirsiniz [Microsoft Güven Merkezi Uyumluluk](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> Bazı sertifikalar/attestations içinde günlük analizi eski adı altında listelenir *operasyonel Öngörüler*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Güvenlik veri akışı bulut
Merhaba Aşağıdaki diyagramda bir bulut güvenlik mimarisini bilgi hello akış halinde şirketinizden gösterir ve onu olarak güvenliği nasıl sağlanır toohello günlük analizi hizmeti, sonuçta sizin tarafınızdan hello OMS portalında göründüğü taşır. Her adım hakkında daha fazla bilgi hello diyagramı izler.

![OMS veri toplama ve güvenlik görüntüsü](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Günlük analizi ve veri toplama için kaydolun
Kuruluş toosend veri tooLog için Analytics, Windows aracıları, Azure sanal makineleri veya OMS aracıları için Linux çalıştıran aracılar yapılandırın. Operations Manager aracıları kullanın, sonra hello Operations Konsolu tooconfigure Yapılandırma Sihirbazı'nı kullanmanız durumunda bunları. (Bu da, diğer tek tek kullanıcılara veya bir grup kişi olabilir) kullanıcıların bir veya daha fazla OMS hesapları (OMS çalışma alanları) oluşturun ve aracıları hesapları aşağıdaki hello birini kullanarak kaydedin:

* [Kuruluş Kimliği](../active-directory/sign-up-organization.md)
* [Microsoft hesabı - Outlook Office Live, MSN](http://www.microsoft.com/account/default.aspx)

Burada veri, bir araya getirilir, analiz, sunulan ve toplanan bir OMS çalışma alanıdır. Bir çalışma alanı öncelikle anlamına gelir toopartition verileri olarak kullanılır ve her çalışma benzersizdir. Örneğin, bir OMS çalışma ve test verileri başka bir çalışma alanıyla yönetilen üretim verilerinizi yönetilen toohave isteyebilirsiniz. Çalışma alanları, bir yönetici denetim kullanıcı erişimi toohello verileri de yardımcı olur. Her çalışma kendisiyle ilişkili birden çok kullanıcı hesabı olabilir ve her kullanıcı hesabı birden çok OMS çalışma erişebilir. Veri Merkezi bölgeye göre çalışma alanları oluşturun. Çoğaltılmış tooother veri merkezleri OMS hizmet kullanılabilirliği için öncelikle hello bölgede her çalışma alanıdır.

Merhaba Yapılandırma Sihirbazı tamamlandığında, Operations Manager için her Operations Manager yönetim grubu hello günlük analizi hizmeti ile bir bağlantı kurar. Ardından hangi bilgisayarların hello yönetim grubundaki toosend veri toohello hizmeti izin hello bilgisayarlar Ekleme Sihirbazı'nı toochoose kullanabilirsiniz. Diğer Aracısı türleri için her güvenli bir şekilde toohello OMS hizmetine bağlanır.

Merhaba günlük analizi hizmeti ile bağlı sistemler arasındaki tüm iletişimi şifrelenir.  Merhaba TLS (HTTPS) protokolü, şifreleme için kullanılır.  Merhaba Microsoft SDL işlem ardından tooensure günlük analizi şifreleme protokolleri en son gelişmeleri hello güncel.

Aracısı her tür için günlük analizi veri toplar. Merhaba toplanan veri türünde kullanılan çözüm hello türleri bağlıdır. Veri toplama sırasında özetini görebilirsiniz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Ayrıca, daha ayrıntılı bilgi çoğu çözümleri için kullanılabilir. Bir çözüm önceden tanımlanmış görünümleri, günlük arama sorguları, veri toplama kuralları ve işleme mantığı paketidir. Yalnızca Yöneticiler günlük analizi tooimport bir çözüm kullanabilirsiniz. Merhaba çözüm içeri aktarıldıktan sonra bu (kullanılıyorsa) taşınan toohello Operations Manager yönetim sunucuları ve seçmiş olduğunuz tooany aracıları olur. Daha sonra hello aracıları hello veri toplar.

## <a name="2-send-data-from-agents"></a>2. Aracılardan verileri gönder
Tüm aracı türleri bir kayıt anahtarı ile kaydeder ve hello aracı ve sertifika tabanlı kimlik doğrulaması ve SSL bağlantı noktası 443 ile kullanarak hello günlük analizi hizmeti arasında güvenli bir bağlantı oluşturulur. OMS gizli deposu toogenerate kullanır ve anahtarlarını güncelleştirin. Özel anahtarları her 90 günde döndürülür ve Azure'da depolanır ve hello Azure tarafından yönetilen katı yasal düzenleme ve uyumluluk uygulamaları izleyin işlemleri.

Operations Manager ile Merhaba günlük analizi hizmeti ile bir çalışma alanı kaydetmek ve hello Operations Manager yönetim sunucusu arasında güvenli bir HTTPS bağlantısı kurulur.

Azure sanal makinelerde çalışan Windows aracılar için kullanılan tooread Tanılama Olayları Azure tablolardaki bir salt okunur depolama anahtardır.

Tüm aracı herhangi bir nedenle yüklenemiyor toocommunicate toohello service ise, hello toplanan verileri yerel olarak geçici bir önbellekte depolanır ve hello yönetim sunucusu tooresend hello veri sekiz dakikada iki saat çalışır. Merhaba aracısının önbelleğe alınmış verileri hello işletim sisteminin kimlik bilgisi deposunu tarafından korunur. Merhaba hizmet hello veri iki saat sonra işleyemezse hello aracıları hello veri sırası. Merhaba sıra dolduğunda, veri türleri, performans verileri ile başlayan bırakarak OMS başlatır. Böylece, gerekirse değiştirebilirsiniz hello Aracısı kuyruk sınırı bir kayıt defteri anahtarıdır. Toplanan veriler sıkıştırılmış ve tüm yük toothem eklemez şekilde şirket içi veritabanlarını atlayarak toohello hizmet gönderilir. Merhaba toplanan veriler gönderilir, hello önbellekten kaldırıldı.

Yukarıda açıklandığı gibi aracılarınızı verilerden SSL tooMicrosoft Azure veri merkezleri gönderilir. İsteğe bağlı olarak, ExpressRoute tooprovide ek güvenlik için hello verileri kullanabilirsiniz. Çok protokollü etiket anahtarlama (MPLS) VPN, bir ağ hizmeti sağlayıcısı tarafından sağlanan gibi bir şekilde toodirectly bağlanmak tooAzure mevcut WAN ağınız, expressroute'dur. Daha fazla bilgi için bkz: [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. hello günlük analizi hizmeti alır ve verileri işler
Merhaba günlük analizi hizmeti gelen verilerin güvenilir bir kaynaktan sertifikalar ve Azure kimlik doğrulaması ile Merhaba veri bütünlüğünü doğrulayarak olmasını sağlar. Merhaba işlenmemiş ham veriler daha sonra bir BLOB depolanır [Microsoft Azure depolama](../storage/common/storage-introduction.md) ve şifreli değil. Bununla birlikte, her bir Azure depolama blob erişilebilir yalnızca toothat kullanıcı benzersiz anahtarlar kümesi kümesi vardır. depolanan verilerin türünü Hello alınan ve kullanılan toocollect veri çözümlerinin hello türlerine bağlıdır. Ardından, hello günlük analizi hizmeti hello Azure depolama blobunu hello ham verileri işler.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Günlük analizi tooaccess hello verileri kullanma
TooLog Analytics hello OMS portalında hello kuruluş hesabı veya önceden ayarladığınız Microsoft hesabını kullanarak kaydolabilirsiniz. Merhaba OMS portalı OMS günlük analizi arasındaki tüm trafiği güvenli bir HTTPS kanal üzerinden gönderilir. Merhaba OMS portalı kullanırken, bir oturum kimliği hello Kullanıcı istemcide (web tarayıcısı) oluşturulur ve hello oturumu sonlanana kadar verileri yerel önbellekte depolanır. Sonlandırılmış hello önbellek silinir. Kişisel bilgi içermez, istemci-tarafı tanımlama bilgilerini otomatik olarak kaldırılmaz. Oturum tanımlama bilgileri HTTPOnly işaretlenir ve güvenli hale getirilir. Önceden belirlenen boşta kalma süresi hello OMS portalı oturum sonlandırıldı.

Merhaba OMS portalı kullanarak veri tooa CSV dosyasını dışarı aktarabilirsiniz ve arama API'lerini kullanarak verilere erişebilirsiniz. CSV verme sınırlı too50, verme ve API veri başına 000 satır kısıtlı too5, arama başına 000 satır.

## <a name="next-steps"></a>Sonraki adımlar
* [Günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md) toolearn günlük analizi ve get dakika içinde çalışır durumda hakkında daha fazla bilgi.
