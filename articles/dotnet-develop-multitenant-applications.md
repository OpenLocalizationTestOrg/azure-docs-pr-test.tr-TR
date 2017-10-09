---
title: "aaaMulti Kiracı Web uygulama düzeni | Microsoft Docs"
description: "Mimari genel bakış ve nasıl tooimplement çok kiracılı web uygulamasını Azure üzerinde açıklamak tasarım desenleri bulun."
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Azure'da çok müşterili uygulamalar
Çok kiracılı uygulama ayrı kullanıcılar ya da "kiracılar," tooview hello uygulama kendi olduğu gibi sorgulamanıza veren paylaşılan bir kaynaktır. Kendisini tooa çok müşterili uygulama uygundur tipik bir senaryo hello tüm hangi kullanıcıların uygulama toocustomize hello kullanıcı deneyimi istiyor ancak Aksi takdirde biridir hello aynı temel iş gereksinimleri. Office 365, Outlook.com ve visualstudio.com büyük çok müşterili uygulamalar örnekleridir.

Bir uygulama sağlayıcının açısından, çoklu müşteri mimarisi hello yararları çoğunlukla toooperational ilgili ve maliyet verimliliği. Uygulamanızın bir sürümünü birçok kiracılar/sistem birleştirilmesi izleme, performans ayarlama, yazılım bakımı ve veri yedekleri gibi yönetim görevleri müşterilerinizle, hello ihtiyaçlarını karşılayabilir.

Merhaba aşağıdaki hello en önemli hedefleri ve gereksinimleri bir sağlayıcının açısından listesini sağlar.

* **Sağlama**: Merhaba uygulaması için yeni kiracılar mümkün tooprovision olması gerekir.  Çok sayıda kiracılar, çok müşterili uygulamalar için genellikle gerekli tooautomate bu işlem tarafından olan Self Servis sağlama olanağı.
* **Bakım**: mümkün tooupgrade Merhaba uygulaması olması ve birden çok kiracıya kullanırken diğer bakım görevlerini gerçekleştirebilirsiniz.
* **İzleme**:, her zaman tooidentify mümkün toomonitor hello uygulamayı herhangi bir sorun ve tootroubleshoot olmalıdır bunları. Bu, her bir kiracı Merhaba uygulaması nasıl kullanarak izlemeyi içerir.

Düzgün uygulanan bir çok kiracılı uygulama hello aşağıdaki toousers avantaj sağlar.

* **Yalıtım**: hello etkinlikleri tek tek kiracıların diğer kiracılar tarafından Merhaba uygulaması hello kullanımını etkilemez. Kiracılar, diğer kişilerin verilere erişemez. Merhaba uygulaması özel kullanıma sahip oldukları gibi toohello Kiracı görünüyor.
* **Kullanılabilirlik**: tek tek kiracılar istediğiniz hello uygulama toobe sürekli kullanılabilir belki de bir SLA tanımlanan garanti ile. Yeniden hello etkinlikleri diğer kiracıların hello hello uygulamanın kullanılabilirliğini etkilemez.
* **Ölçeklenebilirlik**: Merhaba uygulaması toomeet hello isteğe bağlı bağımsız kiracıların ölçeklendirir. Hello varlığı ve diğer kiracıların Eylemler hello hello uygulamanın performansını etkilemez.
* **Maliyetleri**: maliyetleri çoklu kiracı kaynaklarının hello paylaşımı sağladığından ayrılmış, tek kiracılı uygulama çalıştıran daha düşük.
* **Özelleştirilebilirliğini**. Merhaba özelliği toocustomize hello uygulama ekleme veya özellik kaldırma, renklerini ve logolar, ekleme veya değiştirme bile kendi kod veya komut dosyası gibi çeşitli şekillerde tek bir kiracıya.

Kısacası, gerçekleştirmeniz gereken birçok konuları varken tooprovide yüksek düzeyde ölçeklenebilir bir hizmet hesabı da bir dizi hello hedefleri ve ortak toomany çok müşterili uygulamalar gereksinimleri vardır. Bazı belirli senaryolar ve tek tek hedefleri hello önemini ilgili olabilir ve her bir senaryo gereksinimleri farklılık gösterir. Merhaba çok müşterili uygulaması sağlayıcısı olarak da hedefleri ve gereksinimleri gibi hello kiracılar hedefleri ve gereksinimleri, Karlılık, faturalama, birden çok hizmet düzeyleri, sağlama, bakım izleme ve Otomasyon toplantı sahip olursunuz.

Çok kiracılı bir uygulamanın ek tasarım konuları hakkında daha fazla bilgi için bkz: [azure'da çok Kiracılı uygulama barındırma][Hosting a Multi-Tenant Application on Azure]. Çok kiracılı hizmet olarak yazılım (SaaS) veritabanı uygulamalarının ortak veri mimarisi düzenlerine ilişkin bilgi için bkz. [Azure SQL Database ile Çok Kiracılı SaaS Uygulamaları için Tasarım Düzenleri](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

Çok kiracılı bir sistem tasarlarken karşılaşılan anahtar sorunları tooaddress izin birçok özellik hello Azure sağlar.

**Yalıtım**

* Segment Web sitesi kiracılar tarafından ana bilgisayar üstbilgisi ile veya olmadan SSL iletişimi
* Web sitesi kiracılar sorgu parametreleri tarafından segmentlere
* Çalışan rollerini Web Hizmetleri
  * Çalışan rolleri. genellikle veri hello arka uç uygulamasının üzerinde işlem.
  * Merhaba ön uç uygulamaları için genellikle görür web rolleri.

**Depolama**

Veri Yönetimi hello gibi Azure SQL Database veya Azure Storage Hizmetleri gibi tablo, büyük miktarlarda yapılandırılmamış veri depolama için hizmetleri sağlayan hizmet ve büyük miktarda yapılandırılmamış metin hizmetleri toostore sağlayan Blob hizmeti hello veya ikili veri video, ses ve görüntü gibi.

* Çok kullanıcılı verileri uygun SQL veritabanında güvenlik altına alma başına-SQL Server oturumları Kiracı.
* Azure tabloları uygulama kaynakları bir kapsayıcı düzeyinde erişim ilkesini belirtme için kullanarak, tooissue yeni URL'SİNİN paylaşılan erişim imzaları ile korunan hello kaynakları için gerek kalmadan özelliği tooadjust izinleri hello.
* Uygulama kaynakları Azure sıralar Azure kuyrukları kiracılar adına işleme yaygın olarak kullanılan toodrive olsa da sağlama veya Yönetim için kullanılan toodistribute iş ayrıca gerekebilir.
* Hizmet veri yolu kuyrukları uygulama kaynakları bu iter iş tooa için paylaşılan bir hizmeti, her Kiracı gönderen yalnızca hello hizmetinden yalnızca hello alıcıları sırasında (ACS verilen talepler türetilmiş gibi) izinleri toopush toothat sıra sahip olduğu tek bir sıraya kullanabilirsiniz birden çok kiracılardan gelen hello sıra hello verilerden izin toopull sahip.

**Bağlantı ve güvenlik hizmetleri**

* Azure Service Bus, geliştirilmiş ölçek ve esneklik için kabaca bağlı şekilde tooexchange iletileri vermeden uygulamalar arasında bulunur bir Mesajlaşma altyapısı.

**Ağ Hizmetleri**

Azure kimlik doğrulamayı desteklemek ve yönetilebilirliğini barındırılan uygulamalar geliştirmek, birçok ağ hizmetleri sağlar. Bu hizmetler hello şunları içerir:

* Azure sanal ağ sağlar, sağlamak ve sanal özel ağları (VPN'ler) Azure'da yönetin yanı sıra bunları güvenli bir şekilde bağlantı şirket içi BT altyapısı.
* Sanal ağ trafik Yöneticisi sağlar, birden çok barındırılan Azure üzerinden gelen trafiğe Hizmetleri hello çalıştırdıkları olup olmadığını tooload Bakiye aynı veri merkezinde veya farklı veri merkezlerinde Merhaba dünya genelinde.
* Azure Active Directory (Azure AD) olduğu bulut uygulamalarınız için kimlik yönetimi ve erişim denetimi özelliklerinden sağlar modern, REST tabanlı bir hizmettir. Uygulama kaynakları Azure AD tooprovides kimlik doğrulaması ve kimlik doğrulama ve yetkilendirme toobe dışı oluşturmak hello özelliklerini verirken kullanıcılar toogain erişim tooyour web uygulamaları ve Hizmetleri yetkilendirmek kolay bir yol için Azure AD kullanarak, kod.
* Azure Service Bus güvenli Mesajlaşma sağlar ve veri akış özelliği için dağıtılmış ve karmaşık güvenlik duvarı ve güvenlik gerek kalmadan Azure arasındaki iletişimi gibi karma uygulamalar uygulamalar ve şirket içi uygulamalar ve hizmetler, barındırılan altyapıları. Service Bus geçişi için uygulama kaynaklarını toohello kullanarak (örneğin, şirket içi gibi hello sistem dışında barındırılan) uç noktaları toohello ait olabilir gösterilen hizmetlerini Kiracı veya sağlanan özellikle hello Kiracı (Hizmetleri olabilir hassas, Kiracı özgü verileri bunların arasında geçen nedeniyle).

**Kaynak sağlama**

Azure, çeşitli yollarla hello uygulama için sağlama yeni kiracılar sağlar. Çok sayıda kiracılar, çok müşterili uygulamalar için genellikle gerekli tooautomate bu işlem tarafından olan Self Servis sağlama olanağı.

* Çalışan rollerini tooprovision ve Kiracı kaynaklarını (örneğin, ne zaman yeni bir kiracı işaretlerini yukarı veya iptal eder) başına devre sağlama izin, ölçüm kullanın ve belirli bir zamanlama uyarınca ölçek yönetmek için veya yanıt toohello aşma anahtarının eşik ölçümleri toplama performans göstergeleri. Bu aynı rol güncelleştirmeleri ve yükseltmeleri toohello çözüm çıkışı kullanılan toopush de olabilir.
* Azure BLOB'ları kullanılan tooprovision işlem veya önceden başlatılmış depolama kaynaklarını yeni kiracılar için hizmet paketleri, VHD görüntüleri ve diğer kaynakları kapsayıcı düzeyinde erişim ilkeleri tooprotect hello işlem sağlarken olabilir.
* SQL veritabanı kaynakları için bir kiracı sağlama için Seçenekler şunlardır:
  
  * DDL komut dosyalarında veya derlemeleri içindeki kaynaklar olarak katıştırılmış
  * SQL Server 2008 R2 DAC program aracılığıyla dağıtılan paketler.
  * Bir ana başvuru veritabanından kopyalama
  * Veritabanını içeri aktarma ve dışarı aktarma tooprovision yeni veritabanlarını dosyadan kullanma.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
