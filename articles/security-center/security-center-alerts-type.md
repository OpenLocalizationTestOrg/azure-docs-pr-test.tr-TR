---
title: "Azure Güvenlik Merkezi'nde türüne göre aaaSecurity uyarıları | Microsoft Docs"
description: "Bu makalede Azure Güvenlik Merkezi'nde kullanılabilir güvenlik uyarılarını hello farklı türleri açıklanmaktadır."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Azure Güvenlik Merkezi'ndeki güvenlik uyarılarını anlama
Bu makale, güvenlik uyarıları ve Azure Güvenlik Merkezi'nde kullanılabilir olan ilgili Öngörüler toounderstand hello farklı türleri yardımcı olur. Toomanage uyarılar ve olaylar, nasıl görürüm hakkında daha fazla bilgi için [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> Güvenlik Merkezi standart yükseltme tooAzure tooset Gelişmiş algılamalar ayarlama. 60 günlük ücretsiz deneme sürümü mevcuttur. tooupgrade, select **fiyatlandırma katmanı** hello içinde [Güvenlik İlkesi](security-center-policies.md). toolearn daha, hello fazla [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Hangi tür uyarılar mevcuttur?
Azure Güvenlik Merkezi, çeşitli kullanır [algılama özellikleri](security-center-detection-capabilities.md) tooalert müşteriler toopotential saldırıları ortamlarını hedefleme. Bu uyarılar ne tetiklenen uyarı, hedeflenen, hello kaynakları hello ve kaynak hello saldırı hello hello hakkında önemli bilgiler içerir. bir uyarı eklenen hello bilgileri kullanılan analytics toodetect hello tehdit hello türünün göre değişir. Tehdit inceleme sırasında yararlı olabilecek ek bağlamsal bilgiler olaylarda da bulunabilir.  Bu makalede şu uyarı türlerini hello hakkında bilgi sağlar:

* Sanal Makine Davranış Analizi (VMBA)
* Ağ Analizi
* Kaynak Analizi
* Bağlamsal Bilgiler

## <a name="virtual-machine-behavioral-analysis"></a>Sanal makine davranış analizi
Azure Güvenlik Merkezi sanal makine olay günlüklerinin analize dayalı davranış analizi tehlikeye tooidentify kaynakları kullanabilir. Örneğin, İşlem Oluşturma Olayları ve Oturum Açma Olayları. Ayrıca, yaygın bir kampanyanın kanıt desteklemek için diğer sinyaller toocheck ile bağıntı yoktur.

> [!NOTE]
> Güvenlik Merkezi algılama özelliklerinin nasıl çalıştığı hakkında daha fazla bilgi için bkz. [Azure Güvenlik Merkezi algılama özellikleri](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Kilitlenme analizi
Kilitlenme döküm bellek analizi olduğu kullanılan yöntemi toodetect mümkün tooevade geleneksel güvenlik çözümlerden karmaşık kötü amaçlı yazılımlar. Kötü amaçlı yazılım çeşitli biçimlerde virüsten koruma ürünleri tarafından hiçbir zaman toodisk yazma ya da toodisk yazılmış yazılım bileşenlerini şifreleyerek algılanan tooreduce hello ihtimalini deneyin. Bu, hello kötü amaçlı yazılım zor toodetect geleneksel kötü amaçlı yazılımdan koruma yaklaşımlar kullanılarak hale getirir. Kötü amaçlı yazılım, sipariş toofunction bellekte izlemeleri bırakmanız gerekir çünkü ancak, bu tür bir kötü amaçlı yazılım bellek analizi kullanılarak algılanabilir.

Yazılım kilitlendiğinde bir kilitlenme dökümü hello kilitlenme hello aynı anda belleğin bir kısmını yakalar. Merhaba kilitlenme nedeni kötü amaçlı yazılım, genel uygulama veya sistem sorunları. Merhaba kilitlenme döküm Hello bellekte çözümleyerek, Güvenlik Merkezi teknikleri tooexploit güvenlik açıkları yazılım kullanılan algılayabilir, gizli verilere erişmek ve içinde tehlikeye giren bir makineye gizlice kalır. Merhaba analiz Güvenlik Merkezi geri bitiş hello tarafından gerçekleştirilir gibi bu en düşük performans etkisi toohosts ile gerçekleştirilir.

alanları aşağıdaki hello bu makalenin sonraki bölümlerinde görünen ortak toohello kilitlenme döküm uyarı örnekler şunlardır:

* DUMPFILE: Merhaba kilitlenme bilgi döküm dosyası adı.
* İŞLEMADI: İşlem kilitlenen hello adı.
* PROCESSVERSION: İşlem kilitlenen hello sürümü.

### <a name="shellcode-discovered"></a>Kabuk kodu bulundu
Shellcode kötü amaçlı yazılım güvenlik açığından yararlanan sonra çalıştırılan hello yükü var. Bu uyarı, kilitlenme dökümü analizinin kötü amaçlı yükler tarafından yaygın olarak gerçekleştirilen davranışları sergileyen yürütülebilir kodlar algıladığını belirtir. Bu davranış kötü amaçlı olmayan yazılımlar tarafından gerçekleştiriliyor olabilir, ancak normal yazılım geliştirme uygulamaları için alışıldık bir davranış değildir.

Merhaba Shellcode uyarı örneği ek alan aşağıdaki hello sağlar:

* ADRESİ: Merhaba shellcode bellek hello konum.

İşte bu tür bir uyarı örneği:

![Kabuk kodu uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Modül ele geçirme bulundu
Windows, dinamik bağlantı kitaplıklarını (DLL'ler) tooallow yazılım tooutilize ortak Windows sistem işlevselliğini kullanır. Kötü amaçlı yazılım belleğe hello DLL yükleme sırası tooload kötü amaçlı yüklerini değiştiğinde DLL ele geçirme rastgele kod yürütüldüğü gerçekleşir. Bu uyarı hello kilitlenme döküm analiz iki farklı yoldan yüklenen benzer ada bir modül algıladığını belirtir. Yüklenen hello yollarından biri, bir ortak Windows sistemi ikili konumundan gelir.

Yasal yazılım geliştiricileri bazen hello DLL yükleme sırası düzenleme, Windows işletim sistemi hello genişletme veya bir Windows uygulaması genişletme gibi kötü amaçlı olmayan nedenlerle değiştirin. DLL yükleme sırası toohelp ayırt kötü amaçlı ve olası zararsız değişiklikleri toohello arasında Azure Güvenlik Merkezi yüklenen bir modülün tooa şüpheli profili uyumlu olup olmadığını denetler. Bu denetimin sonucuna Hello hello uyarının hello "İmza" alanı tarafından gösterilen ve önem derecesi hello uyarı, uyarının açıklamasına ve uyarı düzeltme adımları hello içinde yansıtılır. tooresearch hello modülü yasal veya kötü niyetli olup modül ele geçirme hello disk kopyası üzerinde hello çözümleyin. Örneğin, hello dosyanın dijital imzasını doğrulamak veya bir virüsten koruma taraması çalıştırın.

Ayrıca hello önceki "Shellcode bulunan" bölümünde açıklanan toohello ortak alanlar bu uyarı alanları izleyen hello sağlar:

* İmza: modül ele geçirme hello tooa şüpheli davranış profili uyup uymadığını gösterir.
* HIJACKEDMODULE: Windows Sistem Modülü hello hello adını sağlayarak.
* HIJACKEDMODULEPATH: hello hello yolunu Windows Sistem Modülü sağlayarak.
* HIJACKINGMODULEPATH: Merhaba Geçirme Modülü hello yolu.

İşte bu tür bir uyarı örneği:

![Modül ele geçirme uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Kendini gizleyen Windows modulü algılandı
Kötü amaçlı yazılım Windows sistem ikili dosyalarını (örneğin, SVCHOST. ortak adlarını kullanabilir EXE) veya modülleri (örneğin, NTDLL. DLL) çok*karışım* ve sistem yöneticileri kötü amaçlı yazılımlardan hello hello yapısını soyutlamaması. Bu uyarı hello kilitlenme döküm analiz bu hello kilitlenme bilgi döküm dosyası Windows Sistem modül adlarını kullanın, ancak Windows modüllerini tipik olan diğer ölçütleri karşılamadığı modüller içerir algıladığını belirtir. Merhaba maskelenmiş modülü disk kopyası üzerinde çözümlenirken hello Bu modülün hello yasal veya kötü amaçlı doğası hakkında daha fazla bilgi sağlayabilir. Analiz şunları içerebilir:

* Söz konusu hello dosyayı yasal yazılım paketinin bir parçası olarak gönderilen onaylayın.
* Merhaba dosyanın dijital imzasını doğrular.
* Virüsten koruma taraması hello dosyasını çalıştırın.

Ayrıca daha önce hello "Shellcode bulunan" bölümünde açıklanan toohello ortak alanlar bu uyarı ek alanlar aşağıdaki hello sağlar:

* AYRINTILAR: hello modülünün meta veriler geçerli olup ve hello modülü sistem yolundan yüklenmesinden olup olmadığını açıklar.
* ADI: Merhaba maskelenmiş Windows Modül hello adı.
* YOL: hello yolu toohello maskelenmiş Windows modülü.

Bu uyarı ayrıca ayıklar ve belirli alanları "Sağlama" ve "Zaman damgası." gibi hello modülünün PE başlığından görüntüler Merhaba alanlar hello modülde varsa bu alanlar yalnızca görüntülenir. Merhaba bkz [Microsoft PE ve COFF belirtimi](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) bu alanlar hakkında ayrıntılı bilgi için.

İşte bu tür bir uyarı örneği:

![Kendini gizleyen Windows uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Değiştirilen sistem ikili dosyası bulundu
Kötü amaçlı yazılım çekirdek sistem ikili dosyalarını sipariş toocovertly erişim veri öğesini değiştirin veya gizlice güvenliği aşılmış bir sistemde kalır. Bu uyarı hello kilitlenme döküm analiz bellek veya disk üzerindeki çekirdek Windows işletim sistemi ikili dosyaları değiştirilmiş algıladığını belirtir.

Yasal uygulama geliştiricileri, Sapmalar veya uygulama uyumluluğu gibi kötü amaçlı olmayan nedenlerle bellekte sistem modüllerini nadiren değiştirir. toohelp ayırt kötü amaçlı ve olası yasal modülleri arasında Azure Güvenlik Merkezi hello değiştirilmiş modülü tooa şüpheli profili uyumlu olup olmadığını denetler. Bu denetimin sonucuna Hello hello uyarı, uyarının açıklamasına ve uyarı düzeltme adımları hello önem derecesine göre belirtilir.

Ayrıca daha önce hello "Shellcode bulunan" bölümünde açıklanan toohello ortak alanlar bu uyarı ek alanlar aşağıdaki hello sağlar:

* MODULENAME: Hello adını sistem ikili değiştirdi.
* MODULEVERSION: Hello sürümü sistem ikili değiştirdi.

İşte bu tür bir uyarı örneği:

![Sistem ikili dosyası uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Şüpheli işlem yürütüldü
Güvenlik Merkezi hello hedef sanal makinede çalışan ve uyarıyı tetikleyen şüpheli bir işlemi tanımlar. Merhaba algılama hello belirli ad için görünmüyor ancak hello yürütülebilir dosyanın parametresi için görünüyor. Bu nedenle, Hello saldırgan hello yürütülebilir adlandırdığında bile Güvenlik Merkezi hala hello şüpheli işlem algılayabilir.

İşte bu tür bir uyarı örneği:

![Şüpheli işlem uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Birden fazla etki alanı hesabı sorgulandı
Güvenlik Merkezi, birden çok şey olduğu tooquery Active Directory etki alanı hesaplarında çalışır algılayabilir ağ keşif sırasında genellikle saldırganlar tarafından gerçekleştirilir. Saldırganlar Bu teknik tooquery hello etki alanı tooidentify hello kullanıcıları yararlanın, hello etki alanı yönetici hesapları tanımlamak, etki alanı denetleyicileri ve ayrıca hello olası etki alanı güven ilişkisi diğer etki alanları tanımlamak hello bilgisayarları belirleyin.

İşte bu tür bir uyarı örneği:

![Birden fazla etki alanı hesabı uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Yerel Yöneticiler grubunun üyeleri numaralandırılmıştır

Windows Server 2016 ve Windows 10 Hello güvenlik olayı 4798, Tetiklenemiyor zaman Güvenlik Merkezi tootrigger bir uyarı geçiyor. Bu durum, yerel yönetici grupları numaralandırıldığında gerçekleşir ve genellikle ağ keşfi sırasında saldırganlar tarafından gerçekleştirilir. Saldırganlar yönetimsel ayrıcalıklara sahip kullanıcılar bu teknik tooquery hello kimliğini yararlanabilirsiniz.

İşte bu tür bir uyarı örneği:

![Yerel yönetici](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Büyük ve küçük harflerin anormal karışımı

Güvenlik Merkezi, büyük ve küçük harfler hello komut satırında bir karışımını hello kullanımını algıladığında bir uyarı tetikleyecek. Karma tabanlı makine kuralının veya bazı saldırganlar Bu teknik toohide büyük küçük harfe duyarlı gelen kullanabilir.

İşte bu tür bir uyarı örneği:

![Anormal karışım](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Şüpheli Kerberos Altın Bilet saldırısı

Güvenliği aşılmış bir [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) anahtarı, bir saldırganın toocreate Kerberos "Altın hello saldırgan tooimpersonate istedikleri herhangi bir kullanıcı izin vererek biletlerini" kullanılabilir. Bu tür bir etkinlik algıladığında Güvenlik Merkezi tootrigger bir uyarı geçiyor.

> [!NOTE] 
> Kerberos Altın Bileti hakkında daha fazla bilgi için [Windows 10 kimlik bilgisi hırsızlığı azaltma kılavuzunu](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx) okuyun.

İşte bu tür bir uyarı örneği:

![Altın bilet](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Şüpheli hesap oluşturuldu

Yerleşik yönetici ayrıcalıklarına sahip olan mevcut bir hesaba çok benzeyen bir hesap oluşturulduğunda, Güvenlik Merkezi bir uyarı tetikler. Bu teknik bir dolandırıcı hesap tarafından İnsan doğrulama fark tooavoid saldırganlar toocreate tarafından kullanılabilir.
 
İşte bu tür bir uyarı örneği:

![Şüpheli hesap](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Şüpheli Güvenlik Duvarı kuralı oluşturuldu

Saldırganlar komut ve Denetim ile özel bir güvenlik duvarı kuralları tooallow kötü amaçlı uygulamalar toocommunicate oluşturarak toocircumvent ana bilgisayar güvenlik deneyebilir veya toolaunch saldırıları hello aracılığıyla hello ağ üzerinden konak tehlikeye. Güvenlik Merkezi, şüpheli bir konumda yürütülebilir bir dosyadan yeni bir güvenlik duvarı kuralı oluşturulduğunu algılandığında bir uyarı tetikler.
 
İşte bu tür bir uyarı örneği:

![Güvenlik duvarı kuralı](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>HTA ve PowerShell şüpheli birleşimi

Güvenlik Merkezi, bir Microsoft HTML Uygulama Ana Bilgisayarının (HTA) PowerShell komutları başlattığını algıladığında bir uyarı tetikler. Bu, saldırganların toolaunch kötü amaçlı PowerShell komut dosyaları tarafından kullanılan bir tekniktir.
 
İşte bu tür bir uyarı örneği:

![HTA ve PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Ağ analizi
Güvenlik Merkezi ağ tehdidi algılaması, Azure IPFIX (İnternet Protokolü Akış Bilgileri Verme) trafiğinizden güvenlik verilerini otomatik olarak toplayarak çalışır. Genellikle birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri çözümler.

### <a name="suspicious-outgoing-traffic-detected"></a>Şüpheli giden trafik algılandı
Ağ aygıtlarını bulunan ve kadar hello profili diğer türlerde sistemleri aynı şekilde. Saldırganlar genellikle bağlantı noktası tarama veya bağlantı noktası süpürme ile işe başlarlar. Hello sonraki örnekte, bir VM'den gelen şüpheli güvenli Kabuk (SSH) trafiği vardır. Bu senaryoda, bir dış kaynağa karşı SSH deneme yanılma saldırısı veya bağlantı noktası süpürme saldırısı yapılabilir.

![Şüpheli giden trafik uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Bu uyarının Bu saldırının kullanılan tooinitiate edildi tooidentify hello kaynak kullanabileceğiniz bilgileri verir. Bu uyarı, makine, hello algılama saati artı hello protokolü ve kullanılan bağlantı noktasını tooidentify hello tehlikeye bilgiler de sağlar. Bu dikey ayrıca için düzeltme adımları listesini sağlar kullanılan toomitigate bu sorunu olabilir.

### <a name="network-communication-with-a-malicious-machine"></a>Kötü amaçlı bir makine ile ağ iletişimi
Microsoft tehdit bilgileri akışlarından yararlanan Azure Güvenlik Merkezi, kötü amaçlı IP adresleriyle iletişim kuran riskli makineleri algılayabilir. Çoğu durumda, hello kötü amaçlı bir komut ve denetim merkezi adresidir. Bu durumda, Güvenlik Merkezi hello iletişimi midilli yükleyicisi kötü amaçlı yazılım kullanarak yapıldığını algıladı (olarak da bilinen [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![ağ iletişimi uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Bu uyarının Bu saldırının kullanılan tooinitiate edildi tooidentify hello kaynak sağlayan bilgiler sağlar, kaynak, hello kurban IP, hello saldırgan IP ve hello algılama zamanı hello saldırıya.

> [!NOTE]
> Dinamik IP adresleri gizlilik amacıyla bu ekran görüntüsünden kaldırılmıştır.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Olası giden hizmet reddi saldırısı algılandı
Bir sanal makineden kaynaklandığı anormal ağ trafiği Güvenlik Merkezi tootrigger saldırı olası bir hizmet reddi tür neden olabilir.

İşte bu tür bir uyarı örneği:

![Giden DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Kaynak analizi
Güvenlik Merkezi kaynak analizi hello ile Merhaba tümleştirme gibi bir hizmet (PaaS) Hizmetleri olarak platformda odaklanır [Azure SQL veritabanı tehdit algılama](../sql-database/sql-database-threat-detection.md) özelliği. Bu alanlar hello analiz'ın sonuçlarından bağlı olarak, Güvenlik Merkezi kaynakla ilişkili bir uyarı tetikler.

### <a name="potential-sql-injection"></a>Olası SQL ekleme
SQL ekleme, burada kötü amaçlı kod ayrıştırma ve yürütme için SQL Server örneğini tooan daha sonra geçirilen dizeleri eklenen bir saldırı aracıdır. SQL Server sözdizimsel açıdan geçerli olan aldığı tüm sorguları yürüttüğü için SQL deyimleri oluşturan her türlü yordam, ekleme güvenlik açıklarına karşı gözden geçirilmelidir. SQL tehdit algılama, machine learning, davranış analizi ve Azure SQL veritabanlarınızın yerinde sürüyor olabilir anomali algılama toodetermine şüpheli olayları kullanır. Örneğin:

* Eski bir çalışan tarafından veritabanı erişimi denendi
* SQL ekleme saldırıları
* Olağan dışı erişim tooa üretim veritabanını evde bir kullanıcıdan

![Olası SQL Ekleme uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

Bu uyarı Hello bilgilerinde kullanılan tooidentify saldırıya hello kaynak, hello algılama zamanı ve hello saldırı hello durumunu olabilir. Ayrıca bir bağlantı toofurther araştırma adımları sağlar.

### <a name="vulnerability-toosql-injection"></a>Güvenlik Açığı tooSQL ekleme
Bu uyarı, veritabanında bir uygulama hatası algılandığında tetiklenir. Bu uyarı, olası güvenlik açığı tooSQL ekleme saldırıları gösteriyor olabilir.

![Olası SQL Ekleme uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Tanınmayan konumdan olağan dışı erişim
Tanınmayan bir IP adresi erişim olayından hello son nokta görülen değil hello sunucuda algılandığında bu uyarı tetiklenir.

![Olağan dışı erişim uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Bağlamsal bilgiler
Bir araştırma sırasında ek bağlam tooreach verdict hello tehdit hello doğası hakkında analist gerekir ve nasıl toomitigate onu.  Örneğin, bir ağ anomali algılandı, ancak anlama olmadan başka ne hello ağda veya şekilde hedeflenen toohello kaynakla gerçekleştiği her sabit toounderstand hangi eylemleri tootake sonraki olduğu. tooaid ile bir güvenlik olayı yapıları, ilgili olaylar ve hello Investigator yardımcı olabilecek bilgiler içerebilir. Merhaba kullanılabilirliği ek bilgi göre değişir üzerinde hello algılanan tehdit türünün hello ortamınızın yapılandırmasını ve tüm güvenlik olayları için kullanılamaz.

Ek bilgi varsa, hello güvenlik olayı hello uyarıların listesi aşağıda gösterilir. Burada aşağıdaki gibi bilgiler bulunabilir:

- Günlük temizleme olayları
- Bilinmeyen bir cihaza takılı olan PNP cihazı
- Eyleme dönüştürülemeyen uyarılar 

![Olağan dışı erişim uyarısı](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, Güvenlik Merkezi'nde güvenlik uyarılarını hello farklı türleri hakkında öğrendiniz. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik olayı işleme](security-center-incident.md)
* [Azure Güvenlik Merkezi algılama özellikleri](security-center-detection-capabilities.md)
* [Azure Güvenlik Merkezi planlama ve işlemler kılavuzu](security-center-planning-and-operations-guide.md)
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md): hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/): Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.
