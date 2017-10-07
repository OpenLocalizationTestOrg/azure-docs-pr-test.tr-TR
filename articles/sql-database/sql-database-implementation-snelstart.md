---
title: "aaaAzure SQL veritabanı Azure örnek olay incelemesi - Snelstart | Microsoft Docs"
description: "İş hizmetlerinin 1.000 yeni Azure SQL veritabanlarının ayda bir hızda nasıl SnelStart kullanan SQL veritabanı toorapidly genişletilmiş hakkında bilgi edinin"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Azure ile SnelStart hızlı bir şekilde iş hizmetlerinin 1.000 yeni Azure SQL veritabanlarının ayda bir hızda genişletilmiştir
![SnelStartLogo](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart hello Hollanda popüler finansal ve iş-yönetimi yazılımı küçük ve orta ölçekli işletmeler (SMB) sağlar. 55,000 müşterilerine 110 çalışanlar, bir BT personeli 35 dahil olmak üzere bir personeli tarafından sunulur. Azure üzerinde oluşturulmuş masaüstü yazılım tooa yazılım olarak-hizmet (SaaS) teklifi hareket ettirerek SnelStart en hello yapılan tanıdık ortamlarında C# kullanarak ve performans ve ölçeklenebilirlik hiçbiri üzerinden - tarafından en iyi duruma getirme Yönetimi otomatikleştirme yerleşik hizmetlerin veya Esnek havuzları kullanan altında sağlama işletmeler. Azure kullanarak sağlar müşterilerin şirket içi ve hello arasında taşıma SnelStart hello ortadan bulut.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>Neden SnelStart Hizmetleri hello Masaüstü toohello buluttan genişletilmiş
> "Azure ile çalışma biz yazılım daha hızlı teslim etmek, hızlı bir şekilde toocustomer taleplerini tepki taleplerini artırdığınızda çözümlerini ölçeklendirme anlamına gelir."
> 
> — Henry bırakıldı, Yazılım Mimarı
> 
> 

SnelStart çalışan başarılı yazılım iş yıllardır, geleneksel geliştirme modelini kullanarak: kod, paketi, sevk ve yineleyin. Zaman içinde daha hızlı değişiklik ayak hello büyüdü ve daha hızlı. Düzenlemeleri sık değiştirilen ve müşteriler daha kolay şekilde tooprocess finansal kayıtları gereken ve yukarı, hesap uzmanları ve kamu tookeep bu değişikliklerle işbirliği.

"Yazılım toocustomers sevkiyat pahalı ve sınırlama," tooHenry göre bırakıldı, Yazılım Mimarı. Ne sıklıkta biz yazılımı yayınlamak "üretim, paketleme ve nakliye maliyetleri sınırlı. Biz toopackage güncelleştirmeleri düzenli sevkiyat vardı, ancak, yaptığı sabit toomeet bizim müşterilerin ihtiyaçlarını değiştirme. Biz hiçbir zaman müşterilerimizin toohello son hello ürün sürümüne yükseltme gösterilmeyeceği. Bu nedenle, biz toosupport birden çok sürümü iş çok zor toodo iyi destek hello yapmadan vardı."

Edilmiş ekler, "biz şekilde istedik tooprogram ve sürüm güncelleştirmeleri bir hızlandırılmış hızını biz daha hızlı yenilik ve müşterilerimiz için yeni hizmetler oluşturmak için. Biz de şekilde tooautomate müşterilerimizin iş yönetimi gereksinimlerini daha sipariş toosimplify işler istedik."

Çözüm SnelStart için hello bir bulut tabanlı SaaS sağlayıcısı olma tarafından hizmetlerinin tooextend oluştu. Hello Azure SQL veritabanı platform vardır-olarak-hizmet altyapı (Iaas) çözümünü gerekir hello önemli BT yükünü yansıtılmasını olmadan alma SnelStart olunmasına yardımcı oldu.

Merhaba bulut modeli de SnelStart toofix hatalar sağlar ve yeni özellikleri hızlı bir şekilde, toodownload ve yükseltme yazılım ihtiyaç duyan müşteriler sağlayın. According tooBeen, "kullanarak Azure bulut hizmetleri sağlar bize tooquickly act üçüncü tarafların gereksinimlerini değiştirdikten sonra. Yeni bir sürüm toothousands müşterilerin tooship sahip yerine biz üçüncü taraflar tarafından gerekli bizim masaüstü uygulaması toonew biçimlerden gönderilen bilgiler uyarlayabilirsiniz."

## <a name="a-modern-company-with-traditional-roots"></a>Geleneksel kökleri modern şirketle
SnelStart hello genel bir müzik Gereci bölümleri üretici olarak hello şirket başlatıldığında too1964, dating humble kökleri ile modern, Çevik, yüksek teknoloji bir iştir. Merhaba SnelStart yazılım iş Hello merkezinde gerçekten hello kişisel bilgisayar hello artışı sırasında hello 1980 lerin, vuruş başlatıldı. kendi ellere içine önemlidir aldı hello şirket daha iyi alternatif toohello hesap yazılım hello anda gerekli. 1982 içinde hello şirket ne sonunda SnelStart hesap yazılım olur, hello foundation oluşturuldu. Merhaba başından hello yazılım basitliği ve hız için admired — çok hello şirket sonunda değiştirilen odak ve kendisi bir yazılım şirketine reinvented.

1995'te, ilk Windows muhasebe uygulama SnelStart yayımladı. Merhaba uygulaması, Microsoft Visual Basic 1.0 ve Microsoft Access veritabanlarında, yerleşik hello Müşteri temel toomore 5.000 kullanıcıları daha büyümesine olunmasına yardımcı oldu.

Bugün, SnelStart bir ana iş kolu (LOB) ve iş yönetimi uygulama Felemenkçe SMB'ler ve kendi kendine employed Girişimciler hedefleyen sağlayıcısıdır. Carlo Kuip, BT Mimarı diyor, "Amacımız tooprovide yüzde 100 Otomasyon iş Yönetimi Hizmetleri müşterilerimiz için aynıdır."

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Performans ve esnek havuzlar maliyetle en iyi duruma getirme
Esnek havuzların büyük ölçekli bir erken katılım SnelStart oluştu. Esnek havuzlar hello şirket sınırı maliyetlerini azaltmaya ve performans gereksinimlerini daha verimli bir şekilde yönetebilirsiniz. Göre tooBeen, "esnek havuzlar kullanarak, biz aşırı sağlama olmadan, müşterilerimizin hello ihtiyaçlarına göre performans en iyi duruma getirebilirsiniz. Biz yoğun yüküne göre tooprovision olsaydı, oldukça maliyetli olacaktır. Bunun yerine, seçeneği tooshare kaynakları hello arasında birden çok, düşük kullanım veritabanları verir toocreate iyi gerçekleştiren ve uygun maliyetli bir çözüm. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Azure SQL veritabanları yalıtım ve güvenlik için verileri containerize Yardım
Azure SQL veritabanı SnelStart tooeasily sağlar ve şeffaf bir şekilde müşterilerin şirket içi iş yönetimi veri tooAzure taşıyın. Hello Azure SQL veritabanı sağlayan yalıtımı, bir sınır kimlik doğrulama, yetkilendirme ve kolay yedekleme ve geri yükleme özellikleri için kullanışlı bir kapsayıcıdır. Veritabanları iş yönetimi için oldukça uygun kavramsal model sağlar. "Bu kapsayıcı sınırında öğeleri önemli tooa iş ve iyi korumalı, yalıtılmış veritabanı tutar bu saklanması hassas veriler içeriyor. according tooCarlo Kuip, BT Mimarı Biz hello veritabanı düzeyinde yetkilendirme yönetebilir ve hatta hello Yönetimi bu veritabanlarının genişleme çalışanlarını Veritabanı Yöneticileri (DBAs) gerek kalmadan otomatikleştirmek ve."

Azure SQL Data Warehouse aynı zamanda bir rol hello SnelStart güvenlik ve yönetim yazıdaki izinsiz giriş algılama, kullanıcı etkinlik günlüğü ve bağlantısı gibi telemetri verilerini toplamak hello şirket yardımcı olarak oynar.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Böylece geliştiriciler değeri teslim daha fazla zaman harcayabilir azure yükü kaldırır
Hello Azure platformu model, altyapı yükünü kaldırıldı ve C# yönetim kitaplıklarını kullanarak SnelStart tooautomate dağıtımları etkin. Kuip durumları gibi "bizim çok küçük bir ekibiniz aynı anda artan ölçeklenebilirlik, hızlı ve olağanüstü durum kurtarma sırasında geçerli işlem seçenekleri müşterilerimizin mümkün toogrow bulamadığımız. Merhaba shift tooservices geliştirme kaynakları yeni hizmetler ve özellikler, yalnızca var olan kodu tookeep yukarı yeni düzenlemeler veya vergi kodlarıyla güncelleştirme yerine toofocus serbest." Müşterinizle ekler, "Yönetim otomatikleştirme ve hello SaaS teklifi kullanarak daha fazla işlem personeli toomake büyük yatırımlar gerek kalmadan müşterilerimizin değer mümkün toodeliver duyuyoruz." Örneğin, Azure ve esnek havuzlar, SnelStart mümkün tooadd yeni özellikler, Banka ile daha sağlam müşteri verileri tümleştirme de dahil olmak üzere çeşitli yeni hizmetleri, küçük işletme arka plan kontrollerinden ve e-posta hizmetleri faturalama kullanmaktı.

> "Yalnızca hello 2016 ilk birkaç ay, biz 12.000'den yaklaşık 5500 toomore bizim Azure SQL veritabanı dağıtımlarından genişletilmiş ve biz aylık yaklaşık 1.000 veritabanları şu anda ekliyoruz."
> 
> — Henry bırakıldı, Yazılım Mimarı
> 
> 

Veritabanı Yönetimi, daha fazla hello esnek iş özelliğini kullanarak otomatik hale getirilmiştir. Kuip durumları gibi "yüksek oranda hello SQL DB [sunucu] örneğine veritabanı otomatik olarak bulmayı veriyoruz." Bu SnelStart tooexecute yönetim işlemlerini kendi dinamik olarak artan müşteri arasında ek yükü olmadan temel sağlar.

SnelStart de müşteri verilerini üçüncü taraf yazılım iş ortakları tarafından oluşturulan uygulamaları arasındaki bir aracı gibi davranan bir API geliştirme. Kuip durumları olarak "Bu API veri girişi faturaları ve diğer belgeler için ortadan gibi diğer satıcılar tooadd işlevselliği tooour yazılımları etkinleştirir." Müşteriler artık kendi küçük işletme hesap yazılımına toomanually türü faturalar sahip olmaz; Merhaba SnelStart yazılım hello gerekli bilgileri doğrudan değiştirecektir. Müşteriler böylece toojoin kendi iş yönetim görevleri hello endüstri dijital dönüşümünde gelen Gelişmekte olan bilgi hello ekosistemi ile.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Azure Hizmetleri için SnelStart SaaS etkinleştirmek nasıl
Azure kullanarak SnelStart müşterilerine ve daha sorunsuz bir şekilde hello bulutta kendi muhasebe hizmet verebilir. Örneğin, müşteriler ve muhasebe bilgileri Azure üzerinde barındırılan SnelStart'ın istemci API doğrudan erişerek paylaşabilirsiniz. Kuip durumları, "Bu yeniden kullanılabilir hizmetler kullanılabilir tooour müşteri kullanıma yönelik web uygulamaları ve tooallow erişim toobusiness yönetim müşteriler ve müşterilerimizin tarafından kullanılan toothird taraf yazılımlar için ortak altyapı ve işlevler sağlar. Ürün yapılandırma yetenekleri sağlayan, güvenlik duvarı kurallarını yönetme ve uzun süre çalışan işlemleri yedeklemeler gibi yönetme örnekler."

> Amacımız tooprovide yüzde 100 Otomasyon müşterilerimiz için iş Yönetimi Hizmetleri değil." 
> 
> — Carlo Kuip, BT Mimarı
> 
> 

Ayrıca, SnelStart web hizmetleri hem Müşteriler hem de Azure SQL Database esnek havuzlar muhasebe tooeasily erişim verileri sağlar. Veritabanı esneklik ve Azure Resource Manager ile birlikte bu SaaS modeli SnelStart her Azure dağıtım tamamlayan ölçeklenebilirlik özelliklerle sağlar. Merhaba uygulaması, tam olarak C# yönetim kitaplıklarını kullanarak otomatik hale getirilmiştir.

![SnelStart mimarisi](./media/sql-database-implementation-snelstart/figure1.png)

Şekil 1 '. Haziran 2016 itibariyle SnelStart, birden fazla 11.000 veritabanları ve 50'den fazla esnek havuzlar sahiptir.

## <a name="simplicity-from-hello-cloud"></a>Basitlik hello buluttan
Tooan Azure bulut tabanlı çözüm taşıma itibaren SnelStart yenilikçi özellikleri ve Hizmetleri sunarken yapabilir toosupport hızlı müşteri büyümesi kaldırıldı. TooBeen, göre "Azure ile biz yakın sürekli güncelleştirmeleri müşterilerimiz için bizim personelinin genişletmeden sunabilir. Ve diğer harika Azure özellikler biz tüm hello alın — ister ölçeklenebilirlik ve olağanüstü durum kurtarma — içinde paketlenmiş. "

> "Ne zaman gerçekte üzerinden Redmond bulamadığımız... Belirli bir sorun hakkında bana telefon bir geliştiriciden hello Hollanda edilene bir çağrı aldım. Biz mümkün tooget Microsoft toodeliver bir değişiklik 48 saat toosolve içinde üretim ortamlarında bizim sorunu olan. "
> 
> — Henry bırakıldı, Yazılım Mimarı
> 
> 

SnelStart de hello güçlü ortaklığı hello Microsoft Azure SQL DB ekibiyle geliştirdik appreciates. Kuip durumlar olarak "tartışmalara özelliklere sahip olduğumuz ve nasıl bir şeyin toouse teknolojisi takdir iki tarafta da."
Merhaba hemen SnelStart için kendi memnun Müşteri temel büyüyen tookeep hedefidir. Edilmiş olarak durumları "Merhaba teknik ve biz ISV sahip kaynak sınırlamaları yoktur kadar büyümesine hiçbir sınır toohow."

## <a name="more-information"></a>Daha fazla bilgi
* toolearn Azure esnek havuzları hakkında daha fazla bilgi görmek [esnek havuzlar](sql-database-elastic-pool.md).
* Web rolleri ve çalışan rolleri hakkında daha fazla toolearn bkz [çalışan rolleri](../fundamentals-introduction-to-azure.md#compute).    
* Azure SQL Data Warehouse hakkında daha fazla toolearn bakın [SQL veri ambarı](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn SnelStart, hakkında daha fazla bilgi görmek [SnelStart](http://www.snelstart.nl).

